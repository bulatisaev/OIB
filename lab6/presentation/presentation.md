---
## Front matter
lang: ru-RU
title: Лабораторная Работа №6. Мандатное разграничение прав в Linux
subtitle: Основы информационной безопасности
author:
  - Барсегян В.Л.
institute:
  - Российский университет дружбы народов им. Патриса Лумумбы, Москва, Россия

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'

## Fonts
mainfont: Arial
romanfont: Arial
sansfont: Arial
monofont: Arial
---


## Докладчик


  * Барсегян Вардан Левонович
  * НПИбд-01-22
  * Российский университет дружбы народов
  * [1132222005@pfur.ru]
  * <https://github.com/VARdamn/oib>
  
# Вводная часть

## Цели и задачи

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux. Проверить работу SELinx на практике совместно с веб-сервером Apache.

# Выполнение лабораторной работы

## Убеждаюсь, что SELinux работает в режиме enforcing политики targeted с помощью команд *getenforce* и *sestatus*. Запускаю веб-сервер командой *service httpd start* и проверяю его статус командой *service httpd status* 

![Запуск и проверка веб-сервера](image/1.png){ #fig:001 width=60% }

## Определяю контекст безопасности веб-сервера с помощью команды *ps auxZ | grep httpd* 

![Контекст безопасности веб-сервера](image/2.png){ #fig:002 width=60% }

## Просматриваю текущее состояние переключателей SELinux для Apache с помощью команды *sestatus -b | grep httpd* 

![Состояние переключателей SELinux](image/3.png){ #fig:003 width=60% }

## Смотрю статистику по политике с помощью команды *seinfo* 

![Статистика по политике](image/4.png){ #fig:004 width=60% }

## Определяю тип файлов и поддиректорий, находящихся в директории /var/www, с помощью команды *ls -lZ /var/www*. Аналогично для директории /var/www/html 

![Определение типа файлов и папок](image/5.png){ #fig:005 width=60% }

## Создаю файл /var/www/html/test.html и записываю следующий html-код 

![test.html](image/6.png){ #fig:006 width=60% }

## Проверяю контекст созданного файла командой *ps auxZ | grep test.html* 

![Контекст файла](image/7.png){ #fig:007 width=60% }

## Проверяю в браузере, что файл успешно отображается 

![Проверка в браузере](image/8.png){ #fig:008 width=60% }

## Изучаю справку man по командам httpd и selinux, также проверяю контекст файла командой *ls -Z /var/www/html/test.html* 

![Изучение man, проверка контекста](image/9.png){ #fig:009 width=60% }

## Изменяю контекст файла test.html командой *chcon -t samba_share_t /var/www/html/test.html*. После, проверяю его и открываю веб-страницу - нет доступа 

![Изменение контекста](image/10.png){ #fig:010 width=60% }

## Просматриваю системный лог-файл командой *tail /var/log/messages* 

![Системный лог-файл](image/11.png){ #fig:011 width=60% }

## В файле /etc/httpd/conf/httpd.conf меняю порт на 81 

![Смена порта](image/12.png){ #fig:012 width=60% }

## Перезагружаю веб-сервер - получен сбой 

![Сбой веб-сервера](image/13.png){ #fig:013 width=60% }

## Анализирую лог-файлы командами *tail -nl /var/log/messages* и *cat /var/log/http/error_log* 

![Проверка лог-файлов](image/14.png){ #fig:014 width=60% }

## Также проверяю лог-файл */var/log/http/access_log* 

![Проверка лог-файлов](image/15.png){ #fig:015 width=60% }

## Также проверяю лог-файл */var/log/audit/audit.log*. 

![Проверка лог-файлов](image/16.png){ #fig:016 width=60% }

## Выполняю команду *semanage port -a -t http_port_t -р tcp 81* и проверяю список портов командой *semanage port -l | grep http_port_t* - порт 81 появился в списке 

![Добавление порта 81 в список](image/17.png){ #fig:017 width=60% }

## Возвращаю контекст httpd_sys_cоntent__t к файлу /var/www/html/ test.html, введя *chcon -t httpd_sys_content_t /var/www/html/test.html*. Перезапускаю веб-сервер командой *sudo service httpd restart* 

![Возвращение контекста и перезапуск веб-сервера](image/18.png){ #fig:018 width=60% }

## Возвращаю порт 80 в конфигурационном файле 

![Смена порта на 80](image/19.png){ #fig:019 width=60% }

## Удаляю привязку http_port_t к 81 порту командой  *semanage port -d -t http_port_t -p tcp 81* и удаляю файл test.html командой *rm /var/www/html/test.html* 

![Удаление привязки к 81 порту и удаление html-файла](image/20.png){ #fig:020 width=60% }

# Вывод

Я развил навыки администрирования ОС Linux, познакомился с технологией SELinux, поработал с веб-сервером Apache
