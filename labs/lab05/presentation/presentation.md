---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №5
subtitle: Управление системными службами (systemd)
author:
  - Амина Аджигалиева
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 22 сентября 2025

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

# Цели и задачи работы

## Цель работы

Получить навыки управления системными службами операционной системы посредством systemd.

# Ход выполнения работы

## Управление сервисом vsftpd

![Проверка статуса и установка vsftpd](Screenshot_1.png){ #fig:001 width=80% }

## Управление сервисом vsftpd

![Запуск и проверка статуса vsftpd](Screenshot_2.png){ #fig:002 width=80% }

## Управление сервисом vsftpd

![Включение и отключение автозапуска](Screenshot_3.png){ #fig:003 width=80% }

## Управление сервисом vsftpd

![Проверка и добавление ссылки для vsftpd](Screenshot_4.png){ #fig:004 width=80% }

## Управление сервисом vsftpd

![Статус vsftpd после добавления в автозапуск](Screenshot_5.png){ #fig:005 width=80% }

## Управление сервисом vsftpd

![Вывод зависимостей vsftpd](Screenshot_6.png){ #fig:006 width=80% }

## Конфликты юнитов

![Проверка статуса сервисов](Screenshot_7.png){ #fig:007 width=80% }

## Конфликты юнитов

![Попытка запуска firewalld и iptables](Screenshot_8.png){ #fig:008 width=80% }

## Конфликты юнитов

![Просмотр настроек юнитов firewalld и iptables](Screenshot_9.png){ #fig:009 width=80% }

## Конфликты юнитов

![Маскирование службы iptables](Screenshot_10.png){ #fig:010 width=80% }

## Конфликты юнитов

![Попытка запуска и добавления iptables в автозагрузку](Screenshot_11.png){ #fig:011 width=80% }

## Изолируемые цели

![Список изолируемых целей](Screenshot_12.png){ #fig:012 width=80% }

## Изолируемые цели

![Переход в rescue.target](Screenshot_13.png){ #fig:013 width=80% }

## Цель по умолчанию

![Установка multi-user.target по умолчанию](Screenshot_14.png){ #fig:014 width=80% }

## Цель по умолчанию

![Установка graphical.target по умолчанию](Screenshot_15.png){ #fig:015 width=80% }

# Вывод

В ходе выполнения лабораторной работы я изучила основы управления сервисами и целями в системе **systemd**.  
Я установила и настроила службу **vsftpd**, рассмотрела конфликты между сервисами **firewalld** и **iptables**, освоила работу с изолируемыми целями и целями по умолчанию.  
Полученные знания позволяют уверенно управлять службами в Linux и повышать надёжность работы операционной системы.
