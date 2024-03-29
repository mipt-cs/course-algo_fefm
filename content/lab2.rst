Основы shell и Python3
######################

:date: 2021-09-10 09:00
:summary: Работа в интерпретаторе Python 3.
:status: published

.. default-role:: code
.. contents:: Содержание

Командный интерпретатор
=======================

Kомандный интерпретатор (или командная оболочка) – это программа, принимающая и выполняющая программы. Командный интерпретатор также поддерживает конструкции программирования, позволяя составлять сложные команды из более простых. Эти сложные команды, или сценарии можно сохранять в виде файлов, которые могут становиться новыми самостоятельными командами. В действительности многие команды в обычной Linux-системе являются сценариями.
Мы рассмотрим командный интерпретатор bash – это один из нескольких интерпретаторов, доступных в Linux.

Для ввода данных и вывода результатов интерпретаторы используют три стандартных потока ввода/вывода:

#. `stdin` – стандартный поток ввода (standard input stream), обеспечивающий ввод для команд.
#. `stdout` – стандартный поток вывода (standard output stream), обеспечивающий отображение результатов выполнения команд.
#. `stderr` – стандартный поток ошибок (standard error stream), обеспечивающий отображение ошибок, возникающих при выполнении команд.


При помощи потоков ввода обеспечивается ввод данных для команд (обычно с клавиатуры). Потоки вывода отображают текстовые символы, которые обычно выводятся на экран.

Команды в ОС Linux состоят из имени, опций и параметров. Некоторые команды не имеют ни опций, ни параметров, некоторые имеют и то, и другое, а некоторые – только опции или только параметры.


Команды
=======

echo
----

Команда echo выводит на экран свои аргументы, как показано в примере ниже

.. code-block:: bash

	[user@comp ~]$ echo Hello World
	Hello World
	[user@comp ~]$ echo Hello      World
	Hello World
	[user@comp ~]$ echo "Hello      World"
	Hello      World
	[user@comp ~]$ echo "Hello      World"  # comment here
	Hello      World
	[user@comp ~]$ echo "\"Hello  World\""  # comment here
	"Hello  World"
	[user@comp ~]$

Bash использует символы-разделители, такие как пробелы, символы табуляции и символы новой строки для разделения входной строки на маркеры, которые передаются на вход вашей команде, поэтому в третьей строке все пробелы были сокращены до одного. Чтобы избежать этого, необходимо заключить строку в кавычки – либо в двойные, либо в одинарные.

Другими словами, если строка заключена в кавычки, то все дополнительные символы-разделители сохраняются, и вся строка воспринимается как один маркер. Чтобы использовать кавычки внутри кавычек необходимо использовать символ \\» как показано в последнем примере.

Если строка содержит символ #, то все последующие символы вы этой строке игнорируются.


man
---

По ходу использования операционной системы Linux вам часто будет требоваться информация о том, что делает та или иная команда или системный вызов, какие у них параметры и опции, для чего предназначены некоторые системные файлы, каков их формат и т.д. Получить эту информацию можно при помощи утилиты `man`:

.. code-block:: bash

	man <имя>

где имя – это имя интересующей вас команды, утилиты, системного вызова, библиотечной функции или файла.

Например:

.. code-block:: bash

	man echo

чтобы выйти из man, нажмите клавишу «q».

Иногда имена команд интерпретатора и системных вызовов или какие-либо еще имена совпадают. Тогда чтобы найти интересующую вас информацию, необходимо задать утилите `man` категорию, к которой относится эта информация (номер раздела). Деление информации по категориям может слегка отличаться от одной версии UNIX к другой. В Linux, например, принято следующее разделение:

#. Исполняемые файлы или команды интерпретатора.
#. Системные вызовы.
#. Библиотечные функции.
#. Специальные файлы (обычно файлы устройств).
#. Формат системных файлов и принятые соглашения.
#. Игры (обычно отсутствуют).
#. Макропакеты и утилиты – такие как сам man.
#. Команды системного администратора.
#. Подпрограммы ядра (нестандартный раздел).


Если вы знаете раздел, к которому относится информация, то утилиту man можно вызвать в Linux с дополнительным параметром

.. code-block:: bash

	man <номер_раздела> <имя>

В других операционных системах этот вызов может выглядеть иначе. Для получения точной информации о разбиении на разделы, форме указания номера раздела и дополнительных возможностях утилиты man наберите команду

.. code-block:: bash

	man man


Директории. Команды pwd, ls, cd
-------------------------------

Каждая выполняемая программа «работает» в строго определённой директории файловой системы. Такая директория называется текущей директорией, можно представлять, что программа во время работы «находится» именно в этой директории, это её «рабочее место». В зависимости от текущей директория может меняться поведение программы: зачастую программа будет по умолчанию работать с файлами, расположенными именно в текущей директория — до них она «дотянется» в первую очередь. Текущая директория есть у любой программы, в том числе и у командной оболочки пользователя. Поскольку взаимодействие пользователя с системой обязательно опосредовано командной оболочкой, можно говорить о том, что пользователь «находится» в той директория, которая в данный момент является текущей директорией его командной оболочки.

Все команды, отдаваемые пользователем при помощи `bash`, наследуют текущую директорию `bash`, т. е. «работают» в той же директория. По этой причине пользователю важно знать текущую директория `bash`. Для этого служит утилита `pwd`:

.. code-block:: bash

	[user@comp ~]$ pwd
	/home/user
	[user@comp ~]$

Команда `pwd` возвращает полный путь текущей директории `bash`. В данном случае текущей является директория «/home/user».

Утилиты, которые мы рассмотрим далее, по умолчанию читают и создают файлы в текущей директории.

Для вывода содержимого текущей директории испольузется команда `ls`:

.. code-block:: bash

	[user@comp ~]$ ls
	Desktop    Music       Public     Documents  Downloads
	Pictures    Templates
	[user@comp ~]$

Если указать опцию `-a`, можно будет увидеть все файлы, включая скрытые (имена которых начинаются с точки).

.. code-block:: bash

	[user@comp ~]$ ls -a
	.                   ..                .bash_history
	.icons              .bash_logout      .selected_editor
	.bash_profile       .java             .ssh
	.bashrc             .lesshst          Desktop
	.mc                 Templates         Music
	Documents           Downloads         .nano
	.viminfo            Pictures          Public
	[user@comp ~]$


Первая ссылка указывает на текущую папку (.), вторая (..) указывает на папку уровнем выше. Это открывает еще более широкие возможности для навигации по каталогам.

После самой команды `ls` в качестве ее аргумента можно указать один или более файлов или директорий. Если указать имя файла, то команда `ls` выведет информацию только об этом файле. А если указать название директории, `ls` покажет все ее содержимое. Опция `-l` команды `ls` бывает очень полезной если вы хотите кроме имен файлов узнать более подробную информацию о них (права на файл, имя владельца, время последнего изменения файла и его размер).
В следующем примере показано применение опции `-l` для вывода информации о файлах хранящихся в директории `/usr`

.. code-block:: bash

	[user@comp ~]$ ls -l /usr
	total 276
	drwxr-xr-x   2 root root 131072 Sep  8 21:25 bin
	drwxr-xr-x   2 root root   4096 Sep  6  2016 games
	drwxr-xr-x  48 root root  20480 Sep  4 22:31 include
	drwxr-xr-x 222 root root  69632 Sep  4 23:35 lib
	drwxr-xr-x  10 root root   4096 Oct  7  2010 local
	drwxr-xr-x   3 root root   4096 Aug 19  2016 locale
	drwxr-xr-x   2 root root  12288 Sep  4 23:35 sbin
	drwxr-xr-x 427 root root  20480 Sep  4 23:35 share
	drwxrwsr-x   6 root src    4096 Sep  8 21:25 src
	[user@comp ~]$

В первой колонке показана информация о правах доступа к каждому файлу в списке. Следующая колонка показывает количество ссылок на каждый элемент списка. Третья и четвертая колонки — владелец и группа файла соответственно. Пятая колонка — размер. Шестая — время последнего изменения файла ('last modified time' или mtime). Последняя колонка — имя файла или директории (Если это ссылка, то после знака «–>» стоит имя объекта на который она ссылается).


Иногда возникает потребность посмотреть информацию только о директориях, а не о всем их содержимом. С этой задачей поможет справиться опция `-d`, которая указывает команде выводить информацию только о директориях.

.. code-block:: bash

	[user@comp ~]$ ls -dl /usr
	drwxr-xr-x 11 root root 4096 Aug 19  2016 /usr

Действие опции `-R` противоположно действию `-d`. Она позволяет выводить информацию о файлах находящихся в директории рекурсивно. Сначала показывается содержимое директории верхнего уровня, потом по очереди содержимое всех поддиректорий и так далее. Вывод этой команды может быть достаточно объемным, поэтому мы не приводим ее пример, но вы можете попробовать сделать это самостоятельно, набрав в командной строке `ls -R` или `ls -Rl`.

Команда cd
----------

Для смены текущей директории командного интерпретатора можно воспользоваться командой `cd`. Для этого необходимо набрать команду в виде

.. code-block:: bash

	cd <имя директории>

где <имя директории> – полное или относительное имя директории, которую вы хотите сделать текущей. Команда `cd` без параметров сделает текущей директорией домашнюю директорию пользователя.

В операционной системе Linux может быть несколько видов путей к файлу:

#. Полный, абсолютный путь linux от корня файловой системы — начинается от корня «/» и описывает весь путь к файлу. Например: «/home/user/myfile»
#. Относительный путь linux — это путь к файлу относительно текущей папки. Например (для файла находящегося в родительской папке): «../myfile».
#. Путь относительно домашний папки текущего пользователя — путь в файловой системе, только не от корня, а от папки текущего пользователя. Чтобы задать путь подобным образом он должен начинаться с «~/». Например: «~/myfile».


Отделить путь к файлу от его имени можно с помощью команд `dirname` и `basename` соответственно:

.. code-block:: bash

	[user@comp ~]$ basename /home/user/somefile
	somefile
	[user@comp ~]$ basename somefile
	somefile
	[user@comp ~]$ dirname /home/user/somefile
	/home/somefile
	[user@comp ~]$ dirname ./somefile
	.
	[user@comp ~]$ dirname somefile
	.
	[user@comp ~]

Заметим, что для «somefile» и «./somefile» `dirname` выдаёт одинаковый результат: «.», что понятно: как было сказано выше, эти формы пути совершенно эквивалентны, а при автоматической обработке результатов dirname гораздо лучше получить «.», чем пустую строку.


Команда mkdir
-------------

Для создания новой поддиректории используется команда `mkdir`. В простейшем виде команда выглядит следующим образом:

.. code-block:: bash

	mkdir <имя_директории>

По умолчанию команда `mkdir` не может создать вложенной структуры директорий. Поэтому, если вам нужно создать несколько вложенных одна в другую директорий (my/super/dir), то вам придется три раза поочередно вызывать эту команду:

.. code-block:: bash

	[user@comp ~]$ mkdir my/super/dir
	mkdir: cannot create directory 'my/super/dir': No such file or directory
 	[user@comp ~]$ mkdir my
	[user@comp ~]$ mkdir my/super
	[user@comp ~]$ mkdir my/super/dir
	[user@comp ~]$

Упростить эту операцию можно добавив опцию 	`-p` к команде `mkdir`. Эта опция позволяет создавать вложенную структуру директорий:

.. code-block:: bash

	[user@comp ~]$ mkdir -p my/super/dir
	[user@comp ~]$

Команда cat
-----------

Команда `cat` может быт использована для просмотра содержимого небольшого текстового файла на экране. Если набрать ее в виде

.. code-block:: bash

	cat <имя файла>

то на экран будет выдано все его содержимое.

Не пытайтесь рассматривать на экране содержимое директорий – все равно не получится. Не пытайтесь просматривать содержимое неизвестных файлов, особенно если вы не знаете, текстовый он или бинарный. Вывод на экран бинарного файла может привести к непредсказуемому поведению терминала.

Если даже ваш файл и текстовый, но большой, то все равно вы увидите только его последнюю страницу. Большой текстовый файл удобнее рассматривать с помощью утилиты `more`:

.. code-block:: bash

	more <текстовый файл>

Если мы в качестве параметров для команды `cat` зададим не одно имя, а имена нескольких файлов

.. code-block:: bash

	cat файл1 файл2 ... файлN

то система выдаст на экран их содержимое в указанном порядке.


Перенаправление ввода-вывода
----------------------------

Вывод команды cat можно перенаправить с экрана терминала в какой-нибудь файл, воспользовавшись символом перенаправления выходного потока данных – знаком "больше" – ">". Команда

.. code-block:: bash

	cat файл1 файл2 ... файлN > <файл результата>

запишет содержимое всех файлов, чьи имена стоят перед знаком ">", воедино в «файл результата» – конкатенирует их. Прием перенаправления выходных данных со стандартного потока вывода (экрана) в файл является стандартным для всех команд, выполняемых командным интерпретатором. Вы можете получить файл, содержащий список всех файлов текущей директории, если выполните команду ls -a с перенаправлением выходных данных

.. code-block:: bash

	ls -a > <новый файл>

Если имена входных файлов для команды `cat` не заданы, то она будет использовать в качестве входных данных информацию, которая вводится с клавиатуры, до тех пор, пока вы не наберете признак окончания ввода – комбинацию клавиш <CTRL> и <d>.

Таким образом, команда

.. code-block:: bash

	cat > <новый файл>

позволяет создать новый текстовый файл с именем «новый файл» и содержимым, которое пользователь введет с клавиатуры. У команды `cat` существует множество различных опций. Посмотреть ее полное описание можно в UNIX Manual.

Заметим, что наряду с перенаправлением выходных данных существует способ перенаправить входные данные. Если во время выполнения некоторой команды требуется ввести данные с клавиатуры, можно положить их заранее в файл, а затем перенаправить стандартный ввод этой команды с помощью знака "меньше" – "<" и следующего за ним имени файла с входными данными.

Перенаправление с помощью ">" перезаписывает соержимое файла заново. Если нужно дописать в конец, то следует воспользоваться ">>".

Например:

.. code-block:: bash

	[user@comp ~]$ ls -a > list.txt
	[user@comp ~]$ ls -a >> list.txt
	[user@comp ~]$

файл `list.txt` будет содержать результат работы обеих запусков команды `ls`.

Введение в Python3
==================

Данный курс будет посвящен изучению программирования с использованием языка **Python**. Python — это современный язык
программирования, работающий на всех распространённых операционных системах.

В настоящее время существует две версии языка Python: более старая и стремительно теряющая популярность версия 2 и
современная версия 3. Мы будем использовать версию 3 данного языка. Именно её необходимо установить дома, скачав данную
версию с сайта `www.python.org`_.

.. _www.python.org: http://www.python.org

Запустить интерпретатор python можно из командной строки:

.. code-block:: bash

   python3

Будьте внимательны: команда `python` запустит интерпретатор версии 2, с которым мы работать не будем. В системе
Windows можно использовать пункт меню «Python (command line)».

Интерактивный режим
-------------------

Откройте командную строку и напишите команду python3.

Вы увидите примерно следующее приглашение командной строки:

.. code-block:: pycon

   Python 3.1.2 (r312:79147, Jun 12 2010, 15:29:06)
   [GCC 4.4.3 20100316 (ALT Linux 4.4.3-alt2)] on linux2
   Type "help", "copyright", "credits" or "license" for more information.
   >>>

Вводите команды и наслаждайтесь результатом. А что можно вводить? Несколько примеров:

.. code-block:: pycon

   >>> 2 + 2
   4
   >>> 2 ** 100
   1267650600228229401496703205376
   >>> 'Hello' + 'World'
   'HelloWorld'
   >>> 'ABC' * 10
   'ABCABCABCABCABCABCABCABCABCABC'

Первая команда вычисляет сумму двух чисел, вторая команда вычисляет 2 в степени 100, третья команда выполняет операцию
**конкатенации** ("склеивания") для строк, а четвертая команда печатает строку `'ABC'`, повторенную 10 раз.

Хотите закончить работу с питоном? Введите команду `exit()` (именно так, со скобочками, так как это — **функция**)
или нажмите ``Ctrl+D``.

Программируемый режим
---------------------

В предыдущей главе мы использовали Python для простых разовых вычислений, используя интерактивный режим.
Теперь создадим программу и выполним её целиком.

.. code-block:: python

   a = 179
   b = 197
   c = (a ** 2 + b ** 2) ** 0.5
   print (c)

Здесь мы используем  **переменные** — объекты, в которых можно сохранять различные (числовые, строковые и прочие)
значения. В первой строке переменной `a` присваивается значение `179`, затем переменной `b` присваивается значение
`971`, затем переменной `c` присваивается значение арифметического выражения, равного длине гипотенузы. После этого
значение переменной `c` выводится на экран.

Упражнение №1: первая программа
-------------------------------

Откройте произвольный текстовый редактор, например, `gedit`. Скопируйте туда текст программы, написанной выше.
Сохраните текст в файле с именем `hypot.py`.

Запустите *терминал*, перейдите в каталог, где лежит файл `hypot.py` и выполните эту программу:

.. code-block:: bash

   python3 hypot.py

Интерпретатор языка Python вместо интерактивного режима выполнит последовательность команд из файла.


При этом значения вычисленных выражений не выводятся на экран (в
отличие от интерактивного режима), поэтому для того, чтобы вывести результат работы программы, то есть значение
переменной `c`, нужна функция `print()`.

Базовый синтаксис языка Python 3
================================


Типы данных
-----------

Итак, мы видим, что Python умеет работать как минимум с двумя видами данных — числами и строками. Числа записываются
последовательностью цифр, также перед числом может стоять знак минус, а строки записываются в одинарных кавычках. `2`
и `'2'` — это разные объекты, первый объект — число, а второй — строка. Операция ``+`` для целых чисел и для строк
работает по-разному: для чисел это сложение, а для строк — конкатенация.

Кроме целых чисел есть и другой класс чисел: действительные (вещественные числа), представляемые в виде десятичных
дробей. Они записываются с использованием десятичной точки, например, `2.0`.

Определить тип объекта можно при помощи функции `type`:

.. code-block:: pycon

   >>> type(2)
   <class 'int'>
   >>> type('2')
   <class 'str'>
   >>> type(2.0)
   <class 'float'>

Обратите внимание: `type` является функцией, аргументы функции указываются в скобках после ее имени.

Операции с числами
------------------

Вот список основных операций для чисел:

- `A+B` — сумма;
- `A-B` — разность;
- `A*B` — произведение;
- `A/B` — частное;
- `A**B` — возведение в степень.

Полезно помнить, что квадратный корень из числа ``x`` — это `x**0.5`, а корень степени ``n`` — это `x**(1/n)`.

Есть также унарный вариант операции ``-``, то есть это операция с одним аргументом. Она возвращает число, противоположное
данному. Например: `-A`.

В выражении может встречаться много операций подряд. Как в этом случае определяется порядок действий? Например, чему
будет равно `1+2*3**1+1`? В данном случае ответ будет 8, так как сначала выполняется возведение в степень, затем —
умножение, затем —  сложение.

Более общие правила определения приоритетов операций такие:

#. Выполняются возведения в степень  **справа налево**, то есть `3**3**3` это 3²⁷.
#. Выполняются унарные минусы (отрицания).
#. Выполняются умножения и деления слева направо. Операции умножения и деления имеют одинаковый приоритет.
#. Выполняются сложения и вычитания слева направо. Операции сложения и вычитания имеют одинаковый приоритет.

Операции над строками
---------------------

- `A+B` — конкатенация;
- `A*n` — повторение ``n`` раз, значение ``n`` должно быть целого типа.




Ветвление
---------

Ветвление (или условная инструкция) в Python имеет следующий синтаксис:

.. code-block:: python

   if Условие:
       Блок_инструкций_1
   else:
       Блок_инструкций_2

`Блок_инструкций_1` будет выполнен, если `Условие` истинно.  Если `Условие` ложно, будет выполнен `Блок_инструкций_2`.

В условной инструкции может отсутствовать слово `else` и последующий блок. Такая инструкция называется неполным
ветвлением.  Например, если дано число `x` и мы хотим заменить его на абсолютную величину `x`, то это можно сделать
следующим образом:

.. code-block:: python

   if x < 0:
       x = -x
   print(x)

В этом примере переменной `x` будет присвоено значение `-x`, но только в том случае, когда `x<0`. А вот инструкция
`print(x)` будет выполнена всегда, независимо от проверяемого условия.

Для выделения блока инструкций, относящихся к инструкции `if` или `else`, в  языке Python используются отступы. Все
инструкции, которые относятся к одному блоку, должны иметь равную величину отступа, то есть одинаковое число пробелов в
начале строки. Рекомендуется использовать *отступ в 4 пробела*.


Вложенные условные инструкции
-----------------------------

Внутри условных инструкций можно использовать любые инструкции языка Python, в том числе и условную инструкцию. Вложенное ветвление — после одной развилки в ходе исполнения программы появляется другая развилка. При этом вложенные блоки имеют больший размер отступа (например, 8 пробелов).

Примере программы, которая по данным ненулевым
числам x и y определяет, в какой из четвертей координатной плоскости находится точка (x,y):

.. code-block:: python

   x = int(input())
   y = int(input())
   if x > 0:
       if y > 0:               # x>0, y>0
           print("Первая четверть")
       else:                   # x>0, y<0
           print("Четвертая четверть")
   else:
       if y > 0:               # x<0, y>0
           print("Вторая четверть")
       else:                   # x<0, y<0
           print("Третья четверть")

В этом примере мы использовали *комментарии* – текст, который интерпретатор игнорирует.  Комментариями в Pythonе
является символ `#` и весь текст после этого символа до конца строки.
Желательно писать код так, чтобы комментарии были излишними, однако допускается писать их там, где возникают "призраки"
(утверждения или теоремы, которые использованы при написании кода, но не следуют из самого кода).
Однако код выше является **плохим примером документации**: комментарии врут, поскольку автором не учтены точки на осях.


Операторы сравнения
-------------------

Как правило, в качестве проверяемого условия используется результат вычисления одного из следующих операторов сравнения:

+----------+---------------------------------------------------------------------------------+
| Оператор | Значение                                                                        |
+==========+=================================================================================+
| `<`      | Меньше — условие верно, если первый операнд меньше второго.                     |
+----------+---------------------------------------------------------------------------------+
| `>`      | Больше — условие верно, если первый операнд больше второго.                     |
+----------+---------------------------------------------------------------------------------+
| `<=`     | Меньше или равно — условие верно, если первый операнд меньше или равен второму. |
+----------+---------------------------------------------------------------------------------+
| `>=`     | Больше или равно — условие верно, если первый операнд больше или равен второму. |
+----------+---------------------------------------------------------------------------------+
| `==`     | Равенство. Условие верно, если два операнда равны.                              |
+----------+---------------------------------------------------------------------------------+

Например, условие `(x * x < 1000)` означает «значение `x * x` меньше 1000», а условие `(2 * x != y)` означает «удвоенное
значение переменной `x` не равно значению переменной `y`».


Операторы сравнения в можно объединять в цепочки, например, `a == b == c` или `1 <= x <= 10`.

Тип данных bool
---------------

Операторы сравнения возвращают значения специального логического типа `bool`. Значения логического типа могут принимать
одно из двух значений: `True` (истина) или `False` (ложь). Если преобразовать логическое `True` к типу `int`, то
получится 1, а преобразование `False` даст 0. При обратном преобразовании число 0 преобразуется в `False`, а любое
ненулевое число в `True`. При преобразовании `str` в `bool` пустая строка преобразовывается в `False`, а любая непустая
строка в `True`.


Каскадные условные инструкции
-----------------------------


Пример программы, определяющий четверть координатной плоскости, можно переписать, используя «каскадную»
последовательность инструкцией `if... elif... else`:

.. code-block:: python

   x = int(input())
   y = int(input())
   if x > 0 and y > 0:
       print("Первая четверть")
   elif x < 0 and y > 0:
       print("Вторая четверть")
   elif x < 0 and y < 0:
       print("Третья четверть")
   elif x > 0 and y < 0:
       print("Четвертая четверть")
   else:
       print("Точка находится на осях или в центре координат.")

В такой конструкции условия `if`, ..., `elif` проверяются по очереди, выполняется блок, соответствующий первому из
истинных условий. Если все проверяемые условия ложны, то выполняется блок `else`, если он присутствует.
Обратите внимание, что таким образом мы чётче видим условия наступления случаев (нет "призраков"), а также
отлавливаем ситуацию, когда точка не находится ни в одной из четвертей.

Цикл while
----------

Цикл `while` («пока») позволяет выполнить одну и ту же последовательность действий, пока проверяемое условие истинно.
Условие записывается до тела цикла и проверяется до выполнения тела цикла. Как правило, цикл `while` используется, когда
невозможно определить точное значение количества проходов исполнения цикла.

Синтаксис цикла `while` в простейшем случае выглядит так:

.. code-block:: python

   while Условие:
       Блок_инструкций

При выполнении цикла `while` сначала проверяется условие. Если оно ложно, то  выполнение цикла прекращается и управление
передается на следующую инструкцию после тела цикла `while`. Если условие истинно, то выполняется инструкция, после чего
условие проверяется снова и снова выполняется инструкция. Так продолжается до тех пор, пока условие будет истинно. Как
только условие станет ложно, работа цикла завершится и управление передастся следующей инструкции после цикла.

Например, следующий фрагмент программы напечатает на экран всех целые числа, не превосходящие n:

.. code-block:: python

   a = 1
   while a <= n:
       print(a)
       a += 1

Общая схема цикла `while` в данном случае для перебора всех подходящих значений такая:

.. code-block:: python

   a = начальное_значение
   while а_является_подходящим_числом:
       обработать_a
       перейти_к_следующему_a

Выведем все степени двойки, не превосходящие числа n:

.. code-block:: python

   a = 1
   while a <= n:
       print(a)
       a *= 2

Цикл for
--------

Цикл `for` может быть использован как более краткая альтернатива циклу `while`.

Для последовательного перебора целых чисел из диапазона `[0; n)` можно использовать цикл `for`:

.. code-block:: python

   for i in range(10):
      print(i)

Этот код по выполняемым действиям полностью соответствуют циклу `while`:

.. code-block:: python

   i = 0
   while i < 10:
     print(i)
     i += 1

Можно задавать начальные и конечные значения для переменной цикла, а также шаг:

.. code-block:: python

   for i in range(20, 10, -2):
     print(i)

Аналогичный цикл `while`

.. code-block:: python

   i = 20
   while i > 10:
     print(i)
     i -= 2


Контест №1
==========

Программированию учатся на практике, поэтому в курсе каждую неделю будет *контест*.
Контест - это набор задач с системой автоматической проверки решения на тестовых наборах данных.
`Вход в контест`_, для входа используйте свои логины с распределительного контеста.

.. _`Вход в контест`: http://judge2.vdi.mipt.ru/cgi-bin/new-client?contest_id=94201

Если вы не регистрировались на распределительный контест, зарегистрируйтесь по этой ссылке_.

.. _ссылке: http://judge2.vdi.mipt.ru/cgi-bin/new-register?contest_id=94201

**Не забудьте указать ваши реальные ФИО для таблицы результатов.**

Попробуйте сдать решение первой задачи:

.. code-block:: python

   x, y = input().split()
   x = int(x)
   y = int(y)
   print(x + y)

