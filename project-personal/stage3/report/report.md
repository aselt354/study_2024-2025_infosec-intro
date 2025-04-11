---
## Front matter
title: "Индивидуальный проект. Этап 3"
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

Целью данного этапа индивидуального проекта является получение навыков работы с инструментом Hydra.

# Задание

- Реализовать эксплуатацию уязвимости с помощью брутфорса паролей.

# Теоретическое введение

Hydra (или THC-Hydra) — это мощный инструмент для проведения атак методом подбора паролей (brute-force) и словарных атак на различные протоколы и сервисы, такие как HTTP, FTP, SSH, RDP, MySQL и многие другие.  Он был разработан группой THC (The Hacker's Choice) и широко используется как в тестировании на проникновение (penetration testing), так и для обучения по вопросам информационной безопасности. Hydra может эффективно использоваться для взлома аутентификационных механизмов на сервисах, которые не применяют защиты от атак на основе подбора паролей (например, отсутствие ограничений по числу попыток входа или слабыми паролями).

Hydra использует метод перебора возможных комбинаций логинов и паролей, которые предоставляются в виде списка (например, с помощью словаря). Во время атаки она тестирует каждую пару "пользователь-пароль" с использованием различных протоколов и сервисов.

Основные характеристики Hydra:

- Многопоточность: Hydra позволяет запускать несколько потоков одновременно, что значительно увеличивает скорость подбора паролей.

- Поддержка множества протоколов: Можно атаковать как стандартные сервисы (SSH, FTP), так и веб-формы.

- Гибкость конфигурации: Hydra предоставляет множество опций для настройки атаки, таких как количество потоков, использование прокси-серверов, настройка параметров аутентификации и т. д.

Для использования Hydra необходимо установить ее на свою машину. Hydra поддерживает операционные системы Linux, Windows и macOS. После установки, инструмент запускается через командную строку и требует указания параметров для атаки.

Пример: 

hydra -l admin -P /path/to/rockyou.txt -s 80 localhost http-get-form "/path/to/login:username=^USER^&password=^PASS^&Login=Login"

- -l admin — логин, который будет использоваться в атаке (в данном случае "admin").

- -P /path/to/rockyou.txt — путь к файлу словаря паролей (например, популярный словарь rockyou.txt).

- -s 80 — порт, на котором работает целевой сервис (в данном случае HTTP — порт 80).

- localhost — целевой хост (в данном случае — локальный сервер).

- http-get-form — указание, что атака будет на веб-форму через метод GET.

- Путь к форме аутентификации и другие параметры конфигурации (например, типы полей формы) указываются в конце команды.

# Выполнение лабораторной работы

 Для начала нам нужен словарь для брута. Мы будем использовать словарь rockyou, который является сборником наиболее популярных и потенциальных паролей. В Kali Linux словарь находится в каталоге /usr/share/wordlists/ нам нужно его только разархивировать и переместить в домашнюю директорию. (рис. [-@fig:001]).

![Установка словаря с потенциальными паролями](image/1.png){#fig:001 width=70%}

Захожу на сайт DVWA, полученный в ходе выполнения предыдущего этапа проекта.Нам нужны будут данные о cookie для запроса hydra, из за этого включаем функцию cookie-editor. (рис. [-@fig:002]).

![Добавление функции cookie-editor](image/2.png){#fig:002 width=70%}

Теперь можем отправить запрос hydra, указывая имя пользователя, словарь с паролями, домашний host, данные о DVWA, параметры cookie, строка, которая присутствует на странице при неудачной аутентификации. В результате мы видим, что нам вывелся подходящий пароль. (рис. [-@fig:003]).

![Hydra-запрос](image/3.png){#fig:003 width=70%}

Далее перейдем в DVWA и введем логин и соответствующий пароль, который выдал нам Hydra. Мы видим, что пароль был успешно подобран. (рис. [-@fig:004]).

![Результат](image/4.png){#fig:004 width=70%}

# Выводы

В ходе выполнения третьего этапа индивидуального проекта я познакомилась с инструментом Hydra и получила практические навыки с ним.

