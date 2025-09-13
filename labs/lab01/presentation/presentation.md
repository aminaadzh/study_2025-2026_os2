---
## Front matter
lang: ru-RU
title: Отчёт по лабораторной работе №1
subtitle: Установка и проверка Rocky Linux в VirtualBox
author:
  - Амина Аджигалиева
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 5 сентября 2025

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

Установить и настроить **Rocky Linux 10.0** в VirtualBox, проверить работу системы и базовых команд Linux.

# Ход выполнения

## Конфигурация виртуальной машины

* Имя: *aradzhigalieva*
* Память: **4 ГБ**, CPU: **4 ядра**
* Диск: **40 ГБ**, Видео: **128 МБ**

![Конфигурация ВМ](image/Screenshot_1.png){ #fig:001 width=70% }

## Запуск установщика (GRUB)

![Выбор Install Rocky Linux](image/Screenshot_2.png){ #fig:002 width=70% }

## Выбор языка

![Language selection](image/Screenshot_3.png){ #fig:003 width=70% }

## Выбор окружения

* **Server with GUI**
* Дополнительно: **Development Tools**

![Software Selection](image/Screenshot_4.png){ #fig:004 width=70% }

## Настройка диска

![Installation Destination](image/Screenshot_5.png){ #fig:005 width=70% }

## KDUMP

![KDUMP отключен](image/Screenshot_6.png){ #fig:006 width=70% }

## Настройка сети

![Network & Hostname](image/Screenshot_7.png){ #fig:007 width=70% }

## Root-учётная запись

![Root Account](image/Screenshot_8.png){ #fig:008 width=70% }

## Создание пользователя

![User Creation](image/Screenshot_9.png){ #fig:009 width=70% }

## Завершение установки

![Installation Complete](image/Screenshot_12.png){ #fig:010 width=70% }

## Установка Guest Additions

![Guest Additions](image/Screenshot_14.png){ #fig:011 width=70% }

# Проверка системы

## Информация о ядре

![Kernel version, CPU & Memory](image/Screenshot_15.png){ #fig:012 width=70% }

## Гипервизор

![Hypervisor](image/Screenshot_16.png){ #fig:013 width=70% }

## Смонтированные файловые системы

![Mount](image/Screenshot_17.png){ #fig:014 width=70% }

# Итоги

## Вывод

* Установка Rocky Linux прошла успешно.
* Настроены сеть, пользователи и локализация.
* Установлены Guest Additions для интеграции с VirtualBox.
* Проверены: ядро, процессор, память, гипервизор и файловые системы.
