---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №7
subtitle: Управление журналами событий в системе
author:
  - Амина Аджигалиева
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 15 октября 2025

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

Получить навыки работы с журналами мониторинга различных событий в системе.

# Ход выполнения работы

## Анализ системных журналов

![Сообщения о сбоях VBoxClient и вход под root](Screenshot_1.png){ #fig:001 width=80% }

## Анализ системных журналов

![Системные сообщения и ошибки VBoxClient](Screenshot_2.png){ #fig:002 width=80% }

## Анализ системных журналов

![Просмотр журнала /var/log/secure](Screenshot_3.png){ #fig:003 width=80% }

## Настройка регистрации через rsyslog

![Установка и запуск Apache](Screenshot_4.png){ #fig:004 width=80% }

## Настройка регистрации через rsyslog

![Просмотр error_log Apache](Screenshot_5.png){ #fig:005 width=80% }

## Настройка регистрации через rsyslog

![Редактирование httpd.conf](Screenshot_6.png){ #fig:006 width=80% }

## Настройка регистрации через rsyslog

![Создание правила для ошибок Apache](Screenshot_7.png){ #fig:007 width=80% }

## Настройка регистрации через rsyslog

![Создание файла debug.conf](Screenshot_8.png){ #fig:008 width=80% }

## Настройка регистрации через rsyslog

![Проверка отладочного логирования](Screenshot_9.png){ #fig:009 width=80% }

## Использование journalctl

![Просмотр системного журнала](Screenshot_10.png){ #fig:010 width=80% }

## Использование journalctl

![Сообщения об ошибках и дампы процессов](Screenshot_11.png){ #fig:011 width=80% }

## Использование journalctl

![Повторные ошибки с трассировкой стека](Screenshot_12.png){ #fig:012 width=80% }

## Использование journalctl

![Отображение доступных фильтров](Screenshot_13.png){ #fig:013 width=80% }

## Использование journalctl

![Просмотр событий UID=0](Screenshot_14.png){ #fig:014 width=80% }

## Использование journalctl

![Вывод последних строк журнала](Screenshot_15.png){ #fig:015 width=80% }

## Использование journalctl

![Фильтрация по приоритету ошибок](Screenshot_16.png){ #fig:016 width=80% }

## Использование journalctl

![События со вчерашнего дня](Screenshot_17.png){ #fig:017 width=80% }

## Использование journalctl

![Ошибки со вчерашнего дня](Screenshot_18.png){ #fig:018 width=80% }

## Использование journalctl

![Подробный вывод журнала](Screenshot_19.png){ #fig:019 width=80% }

## Использование journalctl

![Просмотр журнала sshd](Screenshot_20.png){ #fig:020 width=80% }

## Постоянный журнал journald

![Создание постоянного журнала journald](Screenshot_21.png){ #fig:021 width=80% }

# Вывод

В ходе выполнения лабораторной работы я изучила принципы работы системных журналов Linux и научилась настраивать их хранение и просмотр.  
Я освоила использование `journalctl`, фильтрацию сообщений, настройку приоритетов, а также перенаправление логов веб-сервера Apache через rsyslog.  
Был настроен постоянный журнал journald, что обеспечивает сохранность данных после перезагрузки.  
Полученные знания и навыки важны для контроля, диагностики и администрирования Linux-систем.
