---
## Front matter
title: "Отчёт по лабораторной работе №2"
subtitle: "Управление пользователями и группами"
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

Закрепить навыки администрирования в Linux, научиться создавать и настраивать учётные записи пользователей и групп, 
управлять правами доступа и параметрами паролей, а также освоить работу с системными файлами конфигурации.

# Ход выполнения работы

## Переключение учётных записей пользователей

Сначала я определила текущего пользователя с помощью команды `whoami`, а затем получила дополнительную информацию через команду `id`. 
После этого выполнила вход под суперпользователем `root`, используя команду `su`. Результаты представлены на скриншоте ниже.

![Определение текущего пользователя и вход под root](Screenshot_1.png){ #fig:001 width=80% }

Далее я открыла файл `/etc/sudoers` с помощью команды `visudo`, чтобы изучить настройки доступа пользователей.  
Скриншот показывает содержимое файла.

![Просмотр файла sudoers](Screenshot_2.png){ #fig:002 width=80% }

Затем я создала нового пользователя **alice**, добавила его в группу `wheel`, установила пароль и выполнила вход под его учётной записью.  
Позже был создан пользователь **bob**, которому также назначен пароль. Проверка их данных показана на скриншоте.

![Создание пользователей alice и bob](Screenshot_3.png){ #fig:003 width=80% }

## Создание учётных записей пользователей

Чтобы новые пользователи автоматически получали домашний каталог, я изменила параметры в файле `/etc/login.defs`, 
включив `CREATE_HOME yes` и отключив `USERGROUPS_ENAB no`.  

![Изменение файла login.defs](Screenshot_4.png){ #fig:004 width=80% }

Также я изменила содержимое каталога `/etc/skel`, добавив в него стандартные директории и настроив `.bashrc`, 
указав редактор по умолчанию.

![Изменение .bashrc в /etc/skel](Screenshot_5.png){ #fig:005 width=80% }

После этого был создан пользователь **carol**, которому я назначила пароль и изменила параметры действия пароля: 
минимальный срок — 30 дней, максимальный — 90 дней, предупреждение — за 3 дня.  

![Настройка параметров пароля carol](Screenshot_6.png){ #fig:006 width=80% }

## Работа с группами

Я создала группы `main` и `third`, затем добавила alice и bob в группу `main`, а carol в группу `third`.  
После этого проверила их принадлежность к группам при помощи команды `id`.

![Добавление пользователей в группы и проверка членства](Screenshot_7.png){ #fig:007 width=80% }

# Контрольные вопросы

1. **Как узнать UID и группы пользователя?**  
   С помощью команд: `id`, `groups`, `id -u`, `id -G`.

2. **UID пользователя root?**  
   UID суперпользователя всегда равен 0. Проверка: `id root`.

3. **Различие su и sudo?**  
   `su` полностью переключает на другого пользователя,  
   `sudo` — позволяет выполнять отдельные команды с правами администратора.

4. **Где задаются параметры sudo?**  
   В файле `/etc/sudoers`.

5. **Безопасное редактирование sudoers?**  
   Через `visudo`, который проверяет синтаксис файла.

6. **Какая группа используется для полного доступа через sudo?**  
   Группа `wheel`.

7. **Файлы для настройки новых пользователей:**  
   `/etc/login.defs`, `/etc/default/useradd`, `/etc/skel/`.

8. **Где хранится информация о группах?**  
   В `/etc/passwd` (основная), `/etc/group` (дополнительная).

9. **Команды для изменения свойств пароля:**  
   `passwd`, `chage`.

10. **Можно ли напрямую изменять файл /etc/group?**  
    Нежелательно. Рекомендуется использовать команды `groupadd`, `groupdel`, `usermod`.

# Заключение

В ходе выполнения лабораторной работы я освоила основные приёмы администрирования пользователей и групп в Linux. 
Я создала несколько учётных записей, изменила параметры паролей, настроила группы и отредактировала конфигурационные файлы.  
Эти действия позволили на практике закрепить знания о работе с файлами `/etc/passwd`, `/etc/shadow`, `/etc/group`, а также о настройке sudo. 
Полученный опыт имеет важное значение для управления многопользовательскими системами и обеспечения их безопасности.
