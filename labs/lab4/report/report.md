---
## Front matter
title: "Лабораторная работа №4"
subtitle: "Основы информационной безопасности"
author: "Тойчубекова Асель Нурлановна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Целью данной лабораторной работы является получение практических навыков работы в консоли с расширенными атрибутами файлов. 


# Задание

Выполнить все пункты в порядке выполнения лабораторной работы.

# Теоретическое введение

В операционных системах на основе Linux и Unix расширенные атрибуты (extended attributes, xattr) представляют собой механизм, который позволяет добавлять метаданные к файлам и каталогам. Они дополняют стандартные права доступа (чтение, запись, исполнение), предоставляя дополнительные уровни защиты и управления файлами. Расширенные атрибуты полезны для обеспечения безопасности, защиты от случайного удаления или изменения, а также для системных и прикладных задач.

Одним из наиболее известных примеров использования расширенных атрибутов является флаг immutable (i), который делает файл неизменяемым: его нельзя модифицировать, удалить или переименовать, даже если у пользователя есть права на запись. Другой важный атрибут — append-only (a), который разрешает только добавление данных в файл, но запрещает их удаление или перезапись. Эти атрибуты полезны, например, в журналах системных логов или критически важных конфигурационных файлах.

Работа с расширенными атрибутами осуществляется с помощью команд lsattr (для просмотра атрибутов) и chattr (для их изменения). Например, команда chattr +i file делает файл неизменяемым, а chattr -i file снимает это ограничение (требуются root-права). Благодаря этим возможностям расширенные атрибуты широко применяются в системном администрировании, обеспечивая дополнительную защиту файлов от нежелательных изменений.

# Выполнение лабораторной работы

От имени пользователя guest определим расширенные атрибуты файла
/home/guest/dir1/file1 командой lsattr /home/guest/dir1/file1. Далее установим на file1 права, разрешающие чтение и запись для владельца файла. Затем попробуем установить на файл расширенный атрибут a. Мы видим, что нам отказано от выполнении операции. (рис. [-@fig:001]).

![Установка прав доступа к файлу file1](image/1.png){#fig:001 width=70%}

Попробуем установить расширенный атрибут a на файл /home/guest/dir1/file1 от имени суперпользователя. Затем правильность установки атрибута командой lsattr. Мы видим, что все было успешно установлено.(рис. [-@fig:002]).

![Установка расширенного атрибута а на file1](image/3.png){#fig:002 width=70%}

Выполним запись в файл file1 слова «test» командой echo "test" >> /home/guest/dir1/file1. Затем проверим, выполнив чтение файла, командой cat /home/guest/dir1/file1. Мы видим, что слово test было успешно записано в файл. Далее попробуем стереть имеющуюся в нем информацию и перезаписать ее командой echo "abcd" > /home/guest/dirl/file1. Мы видим, что нам было отказано в доступе, так как атрибут i позволяет только добавлять информацию, а не изменять ее. Также если мы попытается переименовать файл нам будет отказано в доступе. (рис. [-@fig:003]).

![Проверка разрешенных действий с атрибутом а](image/4.png){#fig:003 width=70%}

Попробуем с помощью команды chmod 000 file1 установить на файл file1 права, например, запрещающие чтение и запись для владельца файла. Мы видим, что нам отказано в доступе. (рис. [-@fig:004]).

![Попытка сменить права доступа к file1](image/5.png){#fig:004 width=70%}

Снимем расширенный атрибут a с файла /home/guest/dirl/file1 от имени суперпользователя командой chattr -a /home/guest/dir1/file1. Теперь попробуем сново переписать информацию в file1 и командой cat видим, что все успешно перезаписалось. Также при попытке перезаписать файл у нас все получилось. (рис. [-@fig:005]).

![Проверка действий без атрибута а](image/6.png){#fig:005 width=70%}

Повторим наши действия по шагам, заменив атрибут «a» атрибутом «i». (рис. [-@fig:006]).

![Изменение атрибута файла на i](image/7.png){#fig:006 width=70%}

Попробуем записать текст в файл. Мы видим, что нам отказано в доступе. С помощью команды cat мы видим, что информация не перезаписана. Попробуем перезаписать информацию в файле. Мы видим, что нам также отказано в доступе. Затем если мы попробуем удалить или переименовать файл нам также отказано в доступе. Изменить права доступа у нас также не получается. (рис. [-@fig:007]).

![Проверка разрешенных действий с атрибутом i](image/8.png){#fig:007 width=70%}

# Выводы

В ходе выполнение лабораторной работы №4 я получила практические навыки работы в консоли с расширенными атрибутами файлов.

# Список литературы

- https://esystem.rudn.ru/pluginfile.php/2580982/mod_resource/content/3/004-lab_discret_extattr.pdf
