---
## Front matter
title: "Шаблон отчёта по лабораторной работе"
subtitle: "Простейший вариант"
author: "Дмитрий Сергеевич Кулябов"

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

## Цель работы

Цель доклада – рассмотреть методы обнаружения и защиты от DDoS-атак, их виды и эффективные меры защиты, включая брандмауэры, WAF и Anti-DDoS-сервисы.

## Определение Dos-атака

Атака типа "отказ в обслуживании" (DoS) — это злонамеренная попытка перегрузить сервер, сеть или службу, делая их недоступными для законных пользователей. Злоумышленники используют уязвимости, исказные пакеты или ботнеты, чтобы исчерпать ресурсы системы. 

## Случаи Dos-атак

- В 2000-х первая крупная атака отключила Yahoo! на час, показав уязвимость даже надежных систем. 
- В 2016 году ботнет Mirai вывел из строя Twitter и Netflix, использовав IoT-устройства. 
- В 2018 году GitHub столкнулся с рекордной атакой 1,35 Тбит/с. 

## Типы Dos-атак

- Атаки на основе объема – перегружают сеть избыточным трафиком (UDP Flood, ICMP Flood, Ping of Death, Smurf). 
- Протокольные атаки – используют уязвимости сетевых протоколов (SYN Flood, Signal of Death), создавая полуоткрытые соединения или сбои в работе сервера.
- Атаки на прикладном уровне – нацелены на веб-приложения (HTTP Flood, Slowloris, R.U.D.Y., Fork bomb), истощая их ресурсы.

## Типы Dos-атак

- DDoS-атаки – используют ботнеты и усиление трафика (DNS Amplification, ботнет-атаки) для массовой перегрузки систем.
- Исчерпание ресурсов – многократные запросы (авторизация, загрузка тяжёлых файлов, запросы к БД) перегружают сервер.
- Отражающие атаки – используют сторонние серверы для перенаправления трафика на жертву (DNS/NTP Reflection)

## Атаки на основе объема 

![Пинг-флут/ICMP-флут](image/1.png)

## Протокольные атаки

![SYN-флут](image/2.png)

## Атаки на прикладном уровне

![HTTP -флут](image/3.png)

## В чем различие Dos-атаки и DDos-атаки

- Источник атаки: DoS — атака с одного устройства, DDoS — с множества зараженных устройств.
- Обнаружение: DoS-атаку легче выявить и заблокировать, DDoS-атака маскирует источник.
- Скорость и масштаб: DDoS быстрее и мощнее, создавая огромный объем трафика.
- Способ выполнения: DoS использует один скрипт, DDoS координирует ботнет через сервер управления (C&C).
- Сложность отслеживания: Источник DoS-атаки можно определить, DDoS-атака затрудняет выявление инициатора.

## Методы обнаружения DoS/Ddos-атак

- Мониторинг сетевого трафика – анализ входящего/исходящего трафика, выявление аномалий (Wireshark, NetFlow).
- Мониторинг нагрузки на серверы – отслеживание скачков загрузки CPU, RAM, дисковой системы (Zabbix, Nagios).
- Анализ логов и поведения – выявление подозрительных IP, аномалий в соединениях (SIEM-системы).
- Сигнатурный и поведенческий анализ – сравнение с базой атак или выявление нетипичного поведения.
- Системы предотвращения атак (IPS, файрволы) – фильтрация подозрительного трафика, ограничение соединений.

## Мониторинг сетевого трафика NetFlow

![NetFlow](image/5.png)

## Средства защиты от DoS-атак

- Использование глубокую проверку пакетов (DPI) для анализа пакетов 
- Использование CDN (Content Delivery Network)
- Внедрение брандмауэры веб-приложений (WAFs) 
- Использование системы обнаружения вторжений (IDS) и предотвращения вторжений (IPS), firewall 
- Специализированные анти-DDoS сервисы
- Использовать шифрование Secure Sockets Layer (SSL) 
- Интегрирование алгоритмы машинного обучения и искусственный интеллект (ИИ)

## Выводы

Защита от DDoS-атак требует комплексного подхода: брандмауэры, фильтрация трафика, WAF, Anti-DDoS-сервисы и мониторинг сети. Объемные атаки блокируются фильтрацией и Anti-DDoS-сервисами, протокольные — защитой от SYN-флудов и аномальных пакетов, прикладные — WAF и обновлением SSL/TLS. Для распределенных атак применяются облачные решения, а отражающие предотвращаются настройкой серверов и анализом трафика. Важно сочетать разные методы и постоянно совершенствовать защиту.

## Список литературы

- https://moluch.ru/archive/497/109243/

- https://www.paloaltonetworks.com/cyberpedia/what-is-a-denial-of-service-attack-dos

- https://infobezlikbez.ru/ataki/dos-ataka/metody-zashchity-ot-dos-atak

- https://www.cloudflare.com/learning/ddos/glossary/denial-of-service/
