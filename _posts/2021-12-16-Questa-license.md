---
layout: post
title: QuestaSim IntelFPGA license obtaining (translation in progress)
tags: [FPGA, Questa, IntelFPGA]
lang: en
comments: true
---

From the 21.1 Quartus version ModelSim was changed on a [QuestaSim](https://fpgasoftware.intel.com/21.1/?edition=standard) as a default simulation instrument. In particular, QuestaSim Starter edition with altera/IntelFPGA libraries on-board. Despite the fact that this software is actually free, you still need to get a free license for it and correctly "install" it on your PC.

## License Obtaining

{: .box-note}
**Note:** It is assumed that you already have an IntelFPGA account, because you cannot download QuestaSim without it.

To create a license file you should use your account on [IntelFPGA Self-Licensing Center](https://www.intel.com/content/www/us/en/my-intel/fpga-sslc-sign-in.html). After log in choose "Sign up for Evaluation or Free Licenses".

![Self-Licesing website](/assets/questa-images/image1.png)

This page shows the list of avaliable products for your type of account, in particular, **Questa*-Intel® FPGA Starter Edition**. Для того, чтобы начать создание лицензии необходимо выбрать строку c Questa и в столбце "Number of Seats" указать количество мест, которое будет обеспечиваться будущей лицензией. 

![Self-Licesing-website](/assets/questa-images/image2.png)

После чего прочесть пользовательское соглашение и отметить галочку о его прочтении. По желанию можно поставить галочку если не хотите чтобы Intel с Вами связался по вопросу сбора обратной связи. И теперь кликаем кнопку Get License.

В появившемся поле необходимо указать информацию о машине, на которой будет лежать лицензия. 

![Generate lic](/assets/questa-images/image3.png)

Если Вы ранее никогда не генерировали лицензии, то необходимо нажать +New computer и заполнить информацию. Так, если Вы планируете использовать только на своем ПК, необходимо указать имя ПК, его вид, тип лицензии и ID ПК, под которым подразумевается его MAC.

![Create computer](/assets/questa-images/image4.png)

Указав всю информацию необходимо нажать Generate License, после чего через некоторое время Вам на почту пришлю файл с расширением ``*.dat``.

## Установка лицензии

{: .box-note}
**Note:** Информация описана пока что только для пользователей Windows, постараюсь вскоре дополнить для Linux (вообще вроде как для Linux порядок такой же как и для Modelsim). 

В письме будет довольно подробная информация о вариантах установки лицензии со ссылками на актуальные документы по типу [Quartus Prime Software Installation and Licensing Manual (.pdf)](https://www.intel.com/content/dam/www/programmable/us/en/pdfs/literature/manual/quartus_install.pdf). Что делал я:

* Переместил dat-файл в папку с ПО (D:/IntelFPGA)
* В переменных среды (Панель управления -> Система -> Дополнительные параметры системы -> Переменные среды) создал/изменил переменные ``LM_LICENSE_FILE`` и ``MGLS_LICENSE_FILE``, указав в них абсолютный путь до лицензии включая её имя.

После этого запустил Questa в формате GUI и все сработало! 
Надеюсь Вам помогла эта инструкция, если нет, то здесь работают комментарии, либо можно написать мне в Телеграмм  [@suggestmenews_bot](t.me/suggestmenews_bot)