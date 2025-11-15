---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №11
subtitle: Управление загрузкой системы
author:
  - Амина Аджигалиева
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 26 октября 2025

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

Получить навыки работы с загрузчиком системы GRUB2: его настройкой, изменением параметров загрузки, устранением неполадок и восстановлением доступа к системе.

# Ход выполнения работы

## Модификация параметров GRUB2

![Редактирование файла /etc/default/grub](Screenshot_1.png){ #fig:001 width=80% }

## Генерация конфигурации загрузчика

![Генерация нового файла конфигурации GRUB](Screenshot_2.png){ #fig:002 width=80% }

## Проверка отображения меню загрузки

![Меню загрузки GRUB](Screenshot_3.png){ #fig:003 width=80% }

## Устранение неполадок загрузки

![Редактирование параметров загрузки для rescue.target](Screenshot_4.png){ #fig:004 width=80% }

## Режим восстановления

![Работа в режиме восстановления, просмотр загруженных модулей](Screenshot_5.png){ #fig:005 width=80% }

## Аварийный режим

![Редактирование параметров загрузки для emergency.target](Screenshot_6.png){ #fig:006 width=80% }

## Минимальная загрузочная среда

![Работа в аварийном режиме, список модулей](Screenshot_7.png){ #fig:007 width=80% }

## Сброс пароля root

![Добавление параметра rd.break в GRUB](Screenshot_8.png){ #fig:008 width=80% }

## Работа в initramfs

![Попытка сброса пароля root в initramfs](Screenshot_9.png){ #fig:009 width=80% }

## Повторная попытка сброса пароля root

![Редактирование параметров загрузки в GRUB](Screenshot_101.png){ #fig:010 width=80% }

## Повторная попытка сброса пароля root

![Успешный сброс пароля root](Screenshot_102.png){ #fig:011 width=80% }

# Итоги работы

## Вывод

В ходе лабораторной работы №11 были освоены принципы настройки и восстановления загрузчика GRUB2.  
Были изучены режимы восстановления (`rescue.target`), аварийной загрузки (`emergency.target`) и методы сброса пароля root.  
Полученные навыки позволяют администрировать процесс загрузки Linux и устранять неполадки при запуске системы.
