---
## Front matter
title: "Отчёт по лабораторной работе №5"
subtitle: "Управление системными службами"
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

Получить навыки управления системными службами операционной системы посредством systemd.

# Ход выполнения работы

## Управление сервисом Very Secure FTP (vsftpd)

Сначала я получила права суперпользователя с помощью команды `su`.  
Затем проверила статус службы **vsftpd** командой `systemctl status vsftpd`.  
Так как сервис ещё не был установлен, система выдала сообщение об ошибке.  
После этого я установила пакет `vsftpd` через `dnf -y install vsftpd`.  

![Проверка статуса и установка vsftpd](Screenshot_1.png){ #fig:001 width=80% }

Затем я запустила службу командой `systemctl start vsftpd` и повторно проверила её статус.  
На скриншоте видно, что сервис **active (running)**, но пока не включён в автозапуск.  

![Запуск и проверка статуса vsftpd](Screenshot_2.png){ #fig:002 width=80% }

Далее я добавила сервис в автозапуск командой `systemctl enable vsftpd` и проверила его состояние.  
После этого отключила автозапуск через `systemctl disable vsftpd`, снова убедившись, что статус изменился.  

![Включение и отключение автозапуска](Screenshot_3.png){ #fig:003 width=80% }

С помощью команды `ls /etc/systemd/system/multi-user.target.wants/` я посмотрела список символических ссылок, отвечающих за запуск сервисов.  
Вначале ссылка на `vsftpd.service` отсутствовала, но после повторного выполнения `systemctl enable vsftpd` она появилась.  

![Проверка и добавление ссылки для vsftpd](Screenshot_4.png){ #fig:004 width=80% }

Затем я снова выполнила команду `systemctl status vsftpd`, где убедилась, что сервис работает и теперь включён в автозапуск (`enabled`).  

![Статус vsftpd после добавления в автозапуск](Screenshot_5.png){ #fig:005 width=80% }

В завершение я просмотрела зависимости службы с помощью команд:  
- `systemctl list-dependencies vsftpd`  
- `systemctl list-dependencies --reverse vsftpd`  

На скриншоте видно дерево зависимостей для данного юнита.  

![Вывод зависимостей vsftpd](Screenshot_6.png){ #fig:006 width=80% }

## Конфликты юнитов: firewalld и iptables

Сначала я получила права администратора и установила пакет **iptables** командой:  
`dnf -y install iptables*`.  
Затем проверила состояние сервисов `firewalld` и `iptables` с помощью `systemctl status`.  
На скриншоте видно, что `firewalld` активен, а `iptables` не запущен.  

![Проверка статуса сервисов](Screenshot_7.png){ #fig:007 width=80% }

Далее я попробовала запустить обе службы:  
`systemctl start firewalld` и `systemctl start iptables`.  
В результате при активации одной службы вторая отключалась, что подтверждает наличие конфликта.  

![Попытка запуска firewalld и iptables](Screenshot_8.png){ #fig:008 width=80% }

Чтобы изучить настройки юнитов, я открыла файлы их конфигурации:  
- `cat /usr/lib/systemd/system/firewalld.service`  
- `cat /usr/lib/systemd/system/iptables.service`  

В настройках **firewalld** явно указано, что он конфликтует с `iptables.service` и рядом других.  
В файле юнита **iptables** конфликтующих служб не перечислено.  

![Просмотр настроек юнитов firewalld и iptables](Screenshot_9.png){ #fig:009 width=80% }

Затем я вручную остановила службу iptables (`systemctl stop iptables`) и запустила `firewalld`.  
После этого выполнила команду `systemctl mask iptables`, чтобы заблокировать возможность его случайного запуска.  
В результате был создан символический линк на `/dev/null`.  

![Маскирование службы iptables](Screenshot_10.png){ #fig:010 width=80% }

После этого я проверила запуск iptables (`systemctl start iptables`) и добавление его в автозагрузку (`systemctl enable iptables`).  
Оба действия завершились ошибкой: система сообщила, что юнит **замаскирован** и поэтому не может быть активирован.  

![Попытка запуска и добавления iptables в автозагрузку](Screenshot_11.png){ #fig:011 width=80% }

## Изолируемые цели

Сначала я получила права администратора и перешла в каталог `/usr/lib/systemd/system`.  
С помощью команды `grep Isolate *.target` я просмотрела список всех целей, которые можно изолировать.  
На скриншоте видно, что такие цели содержат параметр `AllowIsolate=yes`.  

![Список изолируемых целей](Screenshot_12.png){ #fig:012 width=80% }

Затем я переключила систему в режим восстановления командой:  
`systemctl isolate rescue.target`.  
После ввода пароля root система перешла в **rescue mode**.  

Далее я выполнила перезапуск ОС с помощью команды:  
`systemctl isolate reboot.target`.  

![Перезагрузка через reboot.target](Screenshot_13.png){ #fig:013 width=80% }

## Цель по умолчанию

Сначала я проверила текущую цель по умолчанию с помощью команды:  
`systemctl get-default`.  
Результат показал, что используется **graphical.target**.  

Затем я изменила цель по умолчанию на текстовый режим:  
`systemctl set-default multi-user.target`.  
В результате при следующей загрузке система стартует в консольном режиме.  

![Установка multi-user.target по умолчанию](Screenshot_14.png){ #fig:014 width=80% }

После проверки я снова установила графический режим по умолчанию:  
`systemctl set-default graphical.target`.  
Теперь система будет загружаться в графическом интерфейсе.  

![Установка graphical.target по умолчанию](Screenshot_15.png){ #fig:015 width=80% }

# Контрольные вопросы

1. **Что такое юнит (unit)? Приведите примеры.**  
   Юнит — это объект управления в системе systemd, описывающий службу, цель, устройство или другой ресурс.  
   Примеры: `sshd.service`, `network.target`, `firewalld.service`, `multi-user.target`.

2. **Какая команда позволяет вам убедиться, что цель больше не входит в список автоматического запуска при загрузке системы?**  
   Для этого используется команда:  
   `systemctl disable <unit>`  
   После отключения можно проверить командой:  
   `systemctl status <unit>`  
   или просмотрев содержимое каталога `/etc/systemd/system/multi-user.target.wants/`.

3. **Какую команду вы должны использовать для отображения всех сервисных юнитов, которые в настоящее время загружены?**  
   `systemctl list-units --type=service`

4. **Как создать потребность (wants) в сервисе?**  
   Используется команда:  
   `systemctl enable <unit>`  
   Она создаёт символическую ссылку в каталогах `*.wants/`.

5. **Как переключить текущее состояние на цель восстановления (rescue target)?**  
   С помощью команды:  
   `systemctl isolate rescue.target`

6. **Поясните причину получения сообщения о том, что цель не может быть изолирована.**  
   Такая ошибка возникает, если в юнит-файле отсутствует параметр `AllowIsolate=yes`.  
   Только цели с этим параметром можно изолировать.

7. **Вы хотите отключить службу systemd, но, прежде чем сделать это, вы хотите узнать, какие другие юниты зависят от этой службы. Какую команду вы бы использовали?**  
   `systemctl list-dependencies --reverse <unit>`


# Заключение

В ходе выполнения лабораторной работы я изучила основы управления сервисами и целями в системе **systemd**.  
Я установила и настроила службу **vsftpd**, добавила её в автозагрузку и проверила работу с зависимостями.  
Также я рассмотрела пример конфликта сервисов **firewalld** и **iptables**, выявила причины их несовместимости и применила маскирование для предотвращения запуска конфликтующего юнита.  
Отдельное внимание было уделено изолируемым целям и смене целей по умолчанию, что позволило закрепить навыки переключения между графическим и текстовым режимами загрузки системы.  

Полученные знания и практические навыки позволяют уверенно управлять службами в Linux, контролировать их взаимодействие, а также повышать надёжность и безопасность работы операционной системы.  
