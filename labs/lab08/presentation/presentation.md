---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №8
subtitle: Планировщики событий
author:
  - Амина Аджигалиева
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 13 октября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель работы

Получение навыков работы с планировщиками событий **cron** и **at** в операционной системе Linux.

# Ход выполнения работы

## Проверка состояния службы crond

![Проверка состояния службы crond](Screenshot_1.png){ #fig:001 width=80% }

## Создание задания в crontab

![Создание нового задания в crontab](Screenshot_2.png){ #fig:002 width=80% }

## Проверка выполнения задания через журнал

![Проверка выполнения задания через журнал /var/log/messages](Screenshot_3.png){ #fig:003 width=80% }

## Изменение расписания cron

![Изменение расписания выполнения задачи](Screenshot_4.png){ #fig:004 width=80% }

## Создание сценария eachhour

![Создание и редактирование скрипта eachhour](Screenshot_5.png){ #fig:005 width=80% }

## Настройка задания в /etc/cron.d

![Создание задания в каталоге /etc/cron.d](Screenshot_6.png){ #fig:006 width=80% }

## Планирование заданий с помощью at

![Планирование и выполнение одноразового задания с помощью at](Screenshot_7.png){ #fig:007 width=80% }

# Заключение

В ходе выполнения лабораторной работы я изучила работу планировщиков **cron** и **at**, научилась создавать и изменять расписания выполнения заданий, использовать системные каталоги для периодических сценариев и проверять результаты через журналы событий.  
Полученные навыки позволяют автоматизировать обслуживание и мониторинг серверов Linux, обеспечивая стабильную работу системы.
