---
## Front matter
title: "Отчёт по прохождению внешнего курса: Системный администратор Linux с нуля"
subtitle: "Часть 3"
author: "Аджигалиева Амина"

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
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучить основы системного администрирования и Linux

# Ход выполнения

## Основы сетевой конфигурации в Linux

Какой командой можно назначить IP-адрес вручную?
ip a add 192.168.122.2/24 dev eth0

![скрин задания](image/1.png){ #fig:001 width=70% }

Что делает директива auto eth0 в /etc/network/interfaces?
Верный ответ: Поднимает интерфейс автоматически при загрузке системы

![скрин задания](image/2.png){ #fig:002 width=70% }

Какая команда используется для удаления IP с интерфейса?
Верный ответ: ip a del 192.168.122.2/24 dev eth0

![скрин задания](image/3.png){ #fig:003 width=70% }

Что произойдет при перезагрузке, если IP-адрес был задан только через ip?
Верный ответ: IP-адрес исчезнет

![скрин задания](image/4.png){ #fig:004 width=70% }

Где задается шлюз по умолчанию в конфигурации интерфейса?
Верный ответ: В поле gateway в /etc/network/interfaces

![скрин задания](image/5.png){ #fig:005 width=70% }

![Результат теста](image/6.png){ #fig:006 width=70% }

## Базовая диагностика сети

Какая команда показывает открытые TCP-порты и процессы, которые их слушают?
Верный ответ: ss -tulnp

![скрин задания](image/7.png){ #fig:006 width=70% }

Какой флаг в ss включает отображение номеров портов и PID/имен процессов?
Верный ответ: -p

![скрин задания](image/8.png){ #fig:007 width=70% }

Что делает команда dig?
Верный ответ: Выполняет DNS-запрос и отображает IP-адреса

![скрин задания](image/9.png){ #fig:008 width=70% }

Какая команда может использоваться для проверки подключения к удаленному TCP-порту без передачи данных?
Верный ответ: nc -vz

![скрин задания](image/10.png){ #fig:009 width=70% }


![Результат теста](image/11.png){ #fig:011 width=70% }

## Настройка SSH-доступа и его защита

Какой порт использует SSH по умолчанию?
Верный ответ: 22

![скрин задания](image/12.png){ #fig:012 width=70% }

Где находится основной конфигурационный файл демона SSH-сервера?
Верный ответ: /etc/ssh/sshd_config

![скрин задания](image/13.png){ #fig:013 width=70% }

Какой командой можно временно остановить службу SSH (systemd)?
Верный ответ: systemctl stop ssh

![скрин задания](image/14.png){ #fig:014 width=70% }
 
Какой файл публичного ключа нужно добавить на сервер для авторизации по ключу?
Верный ответ: id_rsa.pub

![логи ssh](image/15.png){ #fig:015 width=70% }

Какой параметр в sshd_config отключает вход пользователя root по SSH?
Верный ответ: PermitRootLogin no

![скрин вопроса](image/16.png){ #fig:016 width=70% }


![Результат теста](image/17.png){ #fig:017 width=70% }

## Повышение безопасности сетевого взаимодействия

![скрин вопроса](image/18.png){ #fig:018 width=70% }


![скрин вопроса](image/19.png){ #fig:019 width=70% }


![скрин вопроса](image/20.png){ #fig:020 width=70% }


![скрин вопроса](image/21.png){ #fig:021 width=70% }


![скрин вопроса](image/22.png){ #fig:022 width=70% }


![Результат теста](image/23.png){ #fig:023 width=70% }

## Что такое пакеты и как они устроены

![скрин вопроса](image/24.png){ #fig:024 width=70% }


![скрин вопроса](image/25.png){ #fig:025 width=70% }


![скрин вопроса](image/26.png){ #fig:026 width=70% }


![Результат теста](image/27.png){ #fig:027 width=70% }

## Обновление системы и безопасность

![скрин вопроса](image/28.png){ #fig:028 width=70% }


![скрин вопроса](image/29.png){ #fig:029 width=70% }


![скрин вопроса](image/30.png){ #fig:030 width=70% }


![Результат теста](image/31.png){ #fig:031 width=70% }

## Работа с зависимостями и решение конфликтов

![скрин вопроса](image/32.png){ #fig:032 width=70% }


![скрин вопроса](image/33.png){ #fig:033 width=70% }


![скрин вопроса](image/34.png){ #fig:034 width=70% }


![Результат теста](image/35.png){ #fig:035 width=70% }

## Работа с локальными .deb-пакетами и сторонними источниками

![скрин вопроса](image/36.png){ #fig:036 width=70% }


![скрин вопроса](image/37.png){ #fig:037 width=70% }


![скрин вопроса](image/38.png){ #fig:038 width=70% }


![Результат теста](image/39.png){ #fig:039 width=70% }

## Знакомство с логами

![скрин вопроса](image/40.png){ #fig:040 width=70% }


![скрин вопроса](image/41.png){ #fig:041 width=70% }


![скрин вопроса](image/42.png){ #fig:042 width=70% }


![Результат теста](image/43.png){ #fig:043 width=70% }

## Система логирования в Linux

![скрин вопроса](image/44.png){ #fig:044 width=70% }


![скрин вопроса](image/45.png){ #fig:045 width=70% }


![скрин вопроса](image/46.png){ #fig:046 width=70% }


![Результат теста](image/47.png){ #fig:047 width=70% }

## Поиск и фильтрация логов под конкретные задачи

![скрин вопроса](image/48.png){ #fig:048 width=70% }


![скрин вопроса](image/49.png){ #fig:049 width=70% }


![скрин вопроса](image/50.png){ #fig:050 width=70% }


![Результат теста](image/51.png){ #fig:051 width=70% }

## Расследование инцидентов по логам

![скрин вопроса](image/52.png){ #fig:052 width=70% }


![скрин вопроса](image/53.png){ #fig:053 width=70% }


![скрин вопроса](image/54.png){ #fig:054 width=70% }


![Результат теста](image/55.png){ #fig:055 width=70% }

## Управление жизненным циклом логов и ротация

![скрин вопроса](image/56.png){ #fig:056 width=70% }


![скрин вопроса](image/57.png){ #fig:057 width=70% }


![скрин вопроса](image/58.png){ #fig:058 width=70% }


![Результат теста](image/59.png){ #fig:059 width=70% }

## Контейнеризация как подход

![скрин вопроса](image/60.png){ #fig:060 width=70% }


![скрин вопроса](image/61.png){ #fig:061 width=70% }


![скрин вопроса](image/62.png){ #fig:062 width=70% }


![скрин вопроса](image/63.png){ #fig:063 width=70% }


![скрин вопроса](image/64.png){ #fig:064 width=70% }


![Результат теста](image/65.png){ #fig:065 width=70% }

## Работа с контейнерами в Podman

![скрин вопроса](image/66.png){ #fig:066 width=70% }


![скрин вопроса](image/67.png){ #fig:067 width=70% }


![скрин вопроса](image/68.png){ #fig:068 width=70% }


![скрин вопроса](image/69.png){ #fig:069 width=70% }


![скрин вопроса](image/70.png){ #fig:070 width=70% }


![Результат теста](image/71.png){ #fig:071 width=70% }

## Управление ресурсами контейнеров

![скрин вопроса](image/72.png){ #fig:072 width=70% }


![скрин вопроса](image/73.png){ #fig:073 width=70% }


![скрин вопроса](image/74.png){ #fig:074 width=70% }


![скрин вопроса](image/75.png){ #fig:075 width=70% }


![скрин вопроса](image/76.png){ #fig:076 width=70% }


![Результат теста](image/77.png){ #fig:077 width=70% }

## Образы, реестры и базовая безопасность

![скрин вопроса](image/78.png){ #fig:078 width=70% }


![скрин вопроса](image/79.png){ #fig:079 width=70% }


![скрин вопроса](image/80.png){ #fig:080 width=70% }


![скрин вопроса](image/81.png){ #fig:081 width=70% }


![Результат теста](image/82.png){ #fig:082 width=70% }

# Заключение

Освоили основы администрирования по внешнему курсу Linux

