---
lang: ru-RU
title: Презентация по лабораторной работе №13
subtitle: Управление брандмауэром в Linux (firewalld)
author: Амина Аджигалиева
institute: Российский университет дружбы народов, Москва, Россия
date: 5 ноября 2025

slide_level: 2
theme: metropolis
aspectratio: 169
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель работы

## Цель

Изучить управление фильтрацией пакетов в Linux с использованием `firewalld`,  
освоить работу с режимами **runtime** и **permanent**, добавлением служб и портов  
через командную строку и графическую утилиту `firewall-config`.

# Ход выполнения работы

## Определение параметров брандмауэра

![Вывод зон и настроек](Screenshot_1.png){ width=80% }

## Анализ активной конфигурации

![Текущая конфигурация](Screenshot_2.png){ width=80% }

## Добавление службы VNC (runtime)

![Добавление vnc runtime](Screenshot_3.png){ width=80% }

## Добавление VNC в permanent конфигурацию

![Сохранение и применение настроек](Screenshot_5.png){ width=80% }

## Добавление пользовательского порта

![Добавление порта](Screenshot_7.png){ width=80% }

## Включение служб через графический интерфейс

![GUI: включение служб](Screenshot_8.png){ width=80% }

## Добавление UDP-порта 2022

![GUI: порт 2022/udp](Screenshot_9.png){ width=80% }

## Настройка доступа к службам telnet, imap, pop3, smtp

![Добавление telnet](Screenshot_11.png){ width=80% }

## Проверка итоговой конфигурации

![GUI: службы добавлены](Screenshot_12.png){ width=80% }


# Заключение

В ходе работы я:

- изучила управление брандмауэром `firewalld`;
- научилась добавлять и удалять службы и порты;
- разобралась в различии **runtime** и **permanent** настроек;
- освоила как работу через CLI, так и через GUI (`firewall-config`).

Полученные навыки помогут в администрировании серверов и обеспечении сетевой безопасности.
