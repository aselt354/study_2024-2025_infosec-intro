---
## Front matter
title: "Прохождения внешнего курса на тему Основы кибербезопасности. Часть 2"
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

# 3 Защита ПК/телефона

## 3.1 Шифрование диска

Вопрос/Ответ 1 (рис. [-@fig:001])

![Вопрос/Ответ 1](image/3.1.1.png){#fig:001 width=70%}

Пояснение ответа:
Шифровать можно(и нужно) отдельные сектора диска(включая загрузочный сектор), флэшки с конфиденциальными данными.

Вопрос/Ответ 2 (рис. [-@fig:002])

![Вопрос/Ответ 2](image/3.1.2.png){#fig:002 width=70%}

Пояснение ответа:
Метод шифрования:

- Для процедуры Encrypt/Decrypt используется симметрические шифрования (AES)

- Данные шифруются секторами 

- Шифрование ускоряется TMP криптопроцессом

- Шифровать можно и загрузочный сектор. При этом пользователь должен запомнить пароль для дешифрирование ключа.

Вопрос/Ответ 3 (рис. [-@fig:003])

![Вопрос/Ответ 3](image/3.1.3.png){#fig:003 width=70%}

Пояснение ответа:
Программы,с которыми можно зашифровать жесткий диск: VeraCrypt, BitLocker, LUKC, FileVault.


## 3.2 Пароли

Вопрос/Ответ 1 (рис. [-@fig:004])

![Вопрос/Ответ 1](image/3.2.1.png){#fig:004 width=70%}

Пояснение ответа:
Пароль считается стройким если в нем используются множество видов символов(буквы, цифры, знаки, буквы в большом регистре), чем больше видов, тем больше нужно переборов, чтобы его взломать.

Вопрос/Ответ 2 (рис. [-@fig:005])

![Вопрос/Ответ 2](image/3.2.2.png){#fig:005 width=70%}

Пояснение ответа:
Наиболее безопасным является хранение паролей именно в менеджерах паролей. 

Вопрос/Ответ 3 (рис. [-@fig:006])

![Вопрос/Ответ 3](image/3.2.3.png){#fig:006 width=70%}

Пояснение ответа:
Капча проверяет пользователя не является ли он программой перебора данных для взлома, обычно используются разные методы, такие как: нахождения правильной картинки или набора букв/цифр. Итак, капча защищает от автоматизированных атак, направленные на получение несанкционированного доступа.

Вопрос/Ответ 4 (рис. [-@fig:007])

![Вопрос/Ответ 4](image/3.2.4.png){#fig:007 width=70%}

Пояснение ответа:
Хеширование паролей используется для того, чтобы не хранить паролина сервере в открытом виде, это делается для безопасности.

Вопрос/Ответ 5 (рис. [-@fig:008])

![Вопрос/Ответ 5](image/3.2.5.png){#fig:008 width=70%}

Пояснение ответа:
Соль не поможет для улучшения стойкости паролей к атаке перебором, если злоумышленник получил доступ к серверу, так как соль добавляется во время хеширования, но это никак не меняет пароль пользователя и он остается прежним, что позволяет злоумышленнику добраться до цели.

Вопрос/Ответ 6 (рис. [-@fig:009])

![Вопрос/Ответ 6](image/3.2.6.png){#fig:009 width=70%}

Пояснение ответа:
Меры защиты от утечек данных перебором:

- Использовать длинные пароли с символами алфавита разного регистра, цифрами, спец. символами 

- Использовать менеджеры паролей для хранения 

- Регуляное изменение пароли к критическим сервисам 

- Использование разных паролей для разных сайтов, программ.

## 3.3 Фишинг 

Вопрос/Ответ 1 (рис. [-@fig:010])

![Вопрос/Ответ 1](image/3.3.1.png){#fig:010 width=70%}

Пояснение ответа:
В ссылке https://online.sberbank.wix.ru/CSAFront/index.do:

- Домен wix.ru - это беспратный хостинг, никак не связанный со Сбербанком.

- online.sberbank- это всего лишь поддомен хостинга wix.ru, а не настоящий сайт Сбербанка, настоящий- sberbank.ru или online.sberbank.ru

В ссылке https://passport.yandex.ucoz.ru/auth?origin=home_ desktop_ru:

- ucoz.ru- это также бесплатный конструктор сайтов 

- passport.yandex- поддомен ucoz.ru

Вопрос/Ответ 2 (рис. [-@fig:011])

![Вопрос/Ответ 2](image/3.3.2.png){#fig:011 width=70%}

Пояснение ответа:
Фишинговый имейл может прийти от знакомого адреса, это называется ip или имейл spoofing- подмена адреса отправителя.

## 3.4 Беспроводные сети WiFi

Вопрос/Ответ 1 (рис. [-@fig:012])

![Вопрос/Ответ 1](image/3.4.1.png){#fig:012 width=70%}

Пояснение ответа:
Email Спуфинг- это подмена адреса отправителя в имейлах.

Вопрос/Ответ 2 (рис. [-@fig:013])

![Вопрос/Ответ 2](image/3.4.2.png){#fig:013 width=70%}

Пояснение ответа:

Троян- вирус, проникающий в систему под видом легитимного ПО.

## 3.5 Безопасность мессенджеров

Вопрос/Ответ 1 (рис. [-@fig:014])

![Вопрос/Ответ 1](image/3.5.1.png){#fig:014 width=70%}

Пояснение ответа:
Ключ шифрования в протоколе мессенджеров Signal формируется при генерации первого сообщения стороной-отправителя.

Вопрос/Ответ 2 (рис. [-@fig:015])

![Вопрос/Ответ 2](image/3.5.2.png){#fig:015 width=70%}

Пояснение ответа:
Суть сквозного шифрования состоит в том, что сообщения передаются по узлам связи в зашифрованном виде.







