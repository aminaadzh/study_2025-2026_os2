---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №15
subtitle: Управление логическими томами
author:
  - Амина Аджигалиева
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 23 ноября 2025

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

## Основная цель

Получить практические навыки работы с LVM:
- создание физических томов;
- формирование групп томов;
- создание и расширение логических томов;
- изменение размеров файловых систем;
- постоянное монтирование томов.

# Создание физического тома

## Разметка диска /dev/sdb

![Разметка диска /dev/sdb](Screenshot_1.png){width=80%}

## Создание PV

![Создание PV и проверка pvs](Screenshot_2.png){width=80%}

# Создание VG и LV

## Создание группы томов vgdata

![Создание VG и LV](Screenshot_3.png){width=80%}

## Создание файловой системы

![Создание FS и запись в fstab](Screenshot_4.png){width=80%}

## Монтирование

![Проверка монтирования](Screenshot_5.png){width=80%}

# Расширение группы томов

## Добавление /dev/sdb2

![Создание второго раздела](Screenshot_6.png){width=80%}

## Расширение VG и LV

![Расширение VG/LV и проверка](Screenshot_7.png){width=80%}

## lvextend и расширение FS

![Расширение LV и ext4](Screenshot_8.png){width=80%}

## lvreduce и проверка

![Уменьшение LV и проверка размеров](Screenshot_9.png){width=80%}

# Самостоятельная работа

## Создание LV lvgroup

![Разметка /dev/sdc](Screenshot_10.png){width=80%}

## Создание PV, VG и LV

![Создание PV/VG/LV](Screenshot_11.png){width=80%}

## Форматирование XFS

![Форматирование XFS](Screenshot_12.png){width=80%}

## Запись в fstab

![fstab](Screenshot_13.png){width=80%}

## Проверка монтирования

![mount после загрузки](Screenshot_14.png){width=80%}

## Добавление /dev/sdc2

![Создание /dev/sdc2](Screenshot_15.png){width=80%}

## Увеличение LV и XFS-grow

![Расширение LV/XFS](Screenshot_16.png){width=80%}

## Проверка

![Проверка размеров](Screenshot_17.png){width=80%}

# Заключение

В ходе выполнения работы я освоила основные операции LVM:
- создание физических томов, VG и LV;
- изменение размеров логических томов;
- управление файловыми системами ext4 и XFS;
- автоматическое монтирование через fstab.