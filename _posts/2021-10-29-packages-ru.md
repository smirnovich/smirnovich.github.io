---
layout: post
title: О конструкции package на VHDL
subtitle: И как с её помощью все сломать
tags: [fpga,VHDL, package]
lang: ru
published: false
comments: true
---

{: .box-note}
**Note:** Предполагается, что Вы уже знаете основы VHDL и можете создавать комбинационную и последовательностною логику.

## Что такое Package

Помимо тестбенч-файлов и файлов описания синтезируемого дизайна VHDL позволяет создавать своего рода библиотечные файлы, которые называются **package**.
In addition to testbench-files and regular synthesis-files VHDL provides library-files called **packages**. The package is a useful file to collect some universal data so it would not increase the size of the design files and can be easily shared from developer to developer. This kind of file is described by VHDL LRM and must be supported by all vendors. From now on, I've checked it with:

* Quartus 18.0
* Modelsim 10.5
* Vivado/Vsim 2019.2
* All edaplayground.com instruments

## Synthax
The ``ieee`` library  also consist of packages:  ``numeric_std``, ``std_logic_1164`` are also packages.

The basic structure of the package is shown below:

```vhdl
--my_pkg.vhd:

package my_pkg is
    constant WIDTH: integer := 32;
end package my_pkg;

package body my_pkg is
    constant LENGTH: integer := 64;
end package body my_pkg;
```
Since the default name of the library in a project is work, we can add this package in our code like:

```vhdl
--my_example1.vhd:
library work;
use work.my_pkg.all;

entity my_example1 is
   port(
       data_in : in bits(WIDTH-1 downto 0)
   );
end entity;
```

A package can store different types of items: types, constants, functions, components etc. According to the VHDL LRM, a package declaration defines the visible contents of a package, while the body provides hidden details. That mean, that this code would have an error:

```vhdl
--my_example2.vhd:
library work;
use work.my_pkg.all;

entity my_example2 is
   port(
       data_in : in bits(LENGTH-1 downto 0)
   );
end entity;
```
Example from Aldec on EDA playground:


{: .box-error}
**Error:** ``COMP96 ERROR COMP96_0078: "Unknown identifier "LENGTH".``

As you can see the data from the body cannot be seen outside the package, while data from the package itself is available.

## Signal in a package


{: .box-warning}
**Warning:** This is not recommended style, I'm just showing the potential risk.


The most interesting thing in a package is the availability to instantiate the signal in a package:
```vhdl
library ieee;
use ieee.std_logic_1164.all;

package my_pkg is
    signal flag: std_logic;
end package my_pkg;
<...>
```
Since it is in a ``package`` part, not in a ``body``, it is available for any block, which uses this package. It allows to invisibly connect different blocks so no one would find out. Amazing! (An example is available here: <https://www.edaplayground.com/x/6Utw>)


So I've created a simple design and decided to check it with an edaplayground (An example is available here: <https://www.edaplayground.com/x/6Utw>) and it works! With different simulation programs, it works well, 

![Screenshot RTL Quartus](/assets/pkg_images/rtl_quartus0.png)
![Screenshot RTL Quartus](/assets/pkg_images/rtl_quartus1.png)

As you can see it looks weird and makes some kind of ports for each block.

 But, unfortunately, some instruments forbid this manipulation: <https://support.xilinx.com/s/article/65848?language=en_US>
