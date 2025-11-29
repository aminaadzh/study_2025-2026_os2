---
## Front matter
title: "Отчёт по лабораторной работе №13"
subtitle: "Фильтр пакетов"
author: "Амина Аджигалиева"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true
toc-depth: 2
lof: true
lot: true
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
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Цель работы

Получить навыки настройки пакетного фильтра в Linux.

# Ход выполнения работы

## Управление брандмауэром с помощью firewall-cmd

Сначала были получены административные привилегии с использованием команды `su -`.  
После перехода под пользователя root была определена зона брандмауэра по умолчанию:

`firewall-cmd --get-default-zone`

Значением оказалась зона **public**. Далее был выведен список доступных зон:

`firewall-cmd --get-zones`

Затем просмотрен перечень поддерживаемых служб, которые могут быть добавлены к правилам брандмауэра:

`firewall-cmd --get-services`

![Отображение зон, служб и текущей конфигурации](Screenshot_1.png){ #fig:001 width=80% }

Чтобы определить, какие службы разрешены в текущей зоне, была выполнена команда:

`firewall-cmd --list-services`

Далее были сопоставлены результаты вывода между:

`firewall-cmd --list-all`  
и  
`firewall-cmd --list-all --zone=public`

Обе команды вывели одинаковую информацию, что подтвердило использование зоны **public** по умолчанию.

![Отображение текущей конфигурации](Screenshot_2.png){ #fig:002 width=80% }

### Добавление службы VNC

Служба VNC была добавлена в конфигурацию временного времени выполнения:

`firewall-cmd --add-service=vnc-server`

После добавления была проверена активная конфигурация:

`firewall-cmd --list-all`

Сервис появился в списке разрешённых.

![Добавление vnc-server во временную конфигурацию](Screenshot_3.png){ #fig:003 width=80% }

Затем была перезапущена служба firewalld:

`systemctl restart firewalld`

После повторного выполнения команды для просмотра конфигурации выяснилось, что служба VNC исчезла:

`firewall-cmd --list-all`

Причина: изменение было внесено только во **временную конфигурацию (runtime)**. После перезапуска службы runtime-настройки сбрасываются.

![Отображение текущей конфигурации](Screenshot_4.png){ #fig:004 width=80% }

### Добавление VNC в постоянную конфигурацию

Для сохранения изменений на диске была выполнена команда:

`firewall-cmd --add-service=vnc-server --permanent`

Проверка конфигурации показала, что VNC ещё не отображается, так как permanent-изменения не загружаются автоматически в runtime:

`firewall-cmd --list-all`

Чтобы применить сохранённые изменения, был выполнен перезапуск конфигурации:

`firewall-cmd --reload`

После повторного просмотра активной конфигурации:

`firewall-cmd --list-all`

Служба VNC появилась в списке разрешённых.

![Добавление vnc-server в постоянную конфигурацию](Screenshot_5.png){ #fig:005 width=80% }

![применение настроек](Screenshot_6.png){ #fig:006 width=80% }

### Добавление пользовательского порта в конфигурацию брандмауэра

Был добавлен пользовательский порт **2022/TCP** в постоянную конфигурацию межсетевого экрана:

`firewall-cmd --add-port=2022/tcp --permanent`

После добавления конфигурация была перезагружена:

`firewall-cmd --reload`

Затем выполнена проверка активной конфигурации:

`firewall-cmd --list-all`

В выводе появился новый открытый порт **2022/tcp**, что подтверждает успешное добавление.

![Добавление порта 2022/tcp и проверка конфигурации](Screenshot_7.png){ #fig:007 width=80% }

## Управление брандмауэром с помощью firewall-config

Для работы с графической утилитой настройки брандмауэра был запущен интерфейс:

`firewall-config`

После запуска система запросила пароль пользователя, имеющего права управления службой.  
В выпадающем меню **Configuration** был выбран режим **Permanent**, чтобы все внесённые изменения сохранялись в постоянной конфигурации.

Далее была выбрана зона **public**. На вкладке **Services** были отмечены службы **http**, **https** и **ftp**, что разрешило доступ к ним.

![Включение служб http, https и ftp](Screenshot_8.png){ #fig:008 width=80% }

Затем на вкладке **Ports** был добавлен пользовательский порт:  
порт **2022**, протокол **udp**.

![Добавление порта 2022/udp](Screenshot_9.png){ #fig:009 width=80% }

После закрытия утилиты была выполнена проверка текущей конфигурации:

`firewall-cmd --list-all`

На этом этапе изменения не отобразились, так как режим Permanent сохраняет настройки на диске, но не активирует их в конфигурации времени выполнения.

Для применения настроек была загружена конфигурация:

`firewall-cmd --reload`

Затем вывод команды:

`firewall-cmd --list-all`

показал, что открытые порты и разрешённые службы успешно добавлены.

![Применение изменений после перезагрузки](Screenshot_10.png){ #fig:010 width=80% }

## Самостоятельная работа

Необходимо создать конфигурацию брандмауэра, которая разрешает доступ к службам **telnet**, **imap**, **pop3** и **smtp**.

**Служба telnet** была добавлена через командную строку как постоянный параметр:

`firewall-cmd --add-service=telnet --permanent`

Затем были применены изменения:

`firewall-cmd --reload`

После перезагрузки служба появилась в списке разрешённых.

![Добавление telnet через CLI](Screenshot_11.png){ #fig:011 width=80% }

Оставшиеся службы (**imap**, **pop3**, **smtp**) были добавлены через графическую утилиту **firewall-config**.  
В режиме Permanent, на вкладке **Services**, были включены соответствующие службы.

![Разрешение imap, pop3, smtp через GUI](Screenshot_12.png){ #fig:012 width=80% }

Итоговая проверка:

`firewall-cmd --list-all`

показала, что **telnet**, **imap**, **pop3** и **smtp** добавлены и находятся в конфигурации активной зоны.  
Настройки являются постоянными и будут применяться после перезагрузки системы.

# Контрольные вопросы

1. **Какая служба должна быть запущена перед началом работы с firewall-config?**  
   Требуется запущенная служба `firewalld`. Без неё утилита не сможет управлять конфигурацией брандмауэра.

2. **Команда для добавления UDP-порта 2355 в зону по умолчанию?**  
   `firewall-cmd --add-port=2355/udp --permanent`

3. **Команда для отображения всей конфигурации брандмауэра во всех зонах?**  
   `firewall-cmd --list-all-zones`

4. **Команда для удаления службы vnc-server из текущей конфигурации?**  
   `firewall-cmd --remove-service=vnc-server`

5. **Команда для активации конфигурации, добавленной с опцией --permanent?**  
   `firewall-cmd --reload`

6. **Параметр для проверки, что конфигурация активна в текущей зоне?**  
   `firewall-cmd --list-all`

7. **Команда для добавления интерфейса eno1 в зону public?**  
   `firewall-cmd --zone=public --add-interface=eno1 --permanent`

8. **Если зона не указана при добавлении интерфейса, куда он будет добавлен?**  
   В зону, установленную по умолчанию (`firewall-cmd --get-default-zone`).

# Заключение

В ходе выполнения лабораторной работы я разобралась с управлением межсетевым экраном в Linux с помощью утилит `firewall-cmd` и `firewall-config`.  
Я изучила принципы работы с зонами, службами и портами, научилась добавлять и удалять сервисы и порты как во временную конфигурацию, так и в постоянную.  
Используя графический интерфейс и командную строку, я настроила доступ к различным службам, добавила пользовательский порт и убедилась, что изменения сохраняются после перезапуска.  
