---
## Front matter
title: "Лабораторная работа №11"
subtitle: "Отчет"
author: "Устинова Виктория Вадимовна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
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
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получить навыки работы с загрузчиком системы GRUB2.

# Задание

1. Продемонстрируйте навыки по изменению параметров GRUB и записи изменений
в файл конфигурации (см. раздел 11.4.1).
2. Продемонстрируйте навыки устранения неполадок при работе с GRUB (см. раз-
дел 11.4.2).
3. Продемонстрируйте навыки работы с GRUB без использования root (см. раздел 11.4.3).

# Выполнение лабораторной работы

В файле /etc/default/grub установите параметр отображения меню загрузки в те-
чение 10 секунд (рис. [-@fig:001]).

![Заходим в файл через редактор nano и меняем 5 на 10](image/1.jpg){#fig:001 width=70%}

Запишите изменения в GRUB2(рис. [-@fig:002]).

![Изменения записаны, и при входе 5 секунд изменилось на 10](image/2.jpg){#fig:002 width=70%}

Прокрутите вниз до строки, начинающейся с linux ($root)/vmlinuz-. Эта строка загружает ядро системы. В конце этой строки введите(рис. [-@fig:003]).

![Убираем rhgb и quit и пишем systemd.unit=rescue.target и нажимаем ctrl x](image/3.jpg){#fig:003 width=70%}

Посмотрите список всех файлов модулей, которые загружены в настоящее время(рис. [-@fig:004]).

![72 модуля загружены](image/4.jpg){#fig:004 width=70%}

Посмотрите задействованные переменные среды оболочки:(рис. [-@fig:005]).

![Cмотрим вывод](image/5.jpg){#fig:005 width=70%}

Как только отобразится меню GRUB, ещё раз нажмите e на строке с текущей версией ядра, чтобы войти в режим редактора. В конце строки, загружающей ядро, введите(рис. [-@fig:006]).

![Убираем rhgb и quit и пишем команду, после этого снова смотрим systemctl list-units и там уже 53 и перезапускаем](image/6.jpg){#fig:006 width=70%}

В конце строки, загружающей ядро, введите
rd.break(рис. [-@fig:007]).

![Убираем rhgb и quit и пишем команду ](image/7.jpg){#fig:007 width=70%}

Чтобы получить доступ к системному образу для чтения и записи, сделайте содержимое каталога /sysimage новым корневым каталогом, теперь вы можете ввести команду задания пароля(рис. [-@fig:008]).

![Мы выполняем команды и меняем пароль](image/8.jpg){#fig:008 width=70%}

Вы должны убедиться, что тип контекста установлен правильно, Теперь вы можете вручную установить правильный тип контекста для /etc/shadow. Для этого введите chcon -t shadow_t /etc/shadow(рис. [-@fig:009]).

![Мы выполняем команды, перезагружаем систему и проверяем смену пароля](image/9.jpg){#fig:009 width=70%}

# Выводы

Мы успешно получили навыки работы с загрузчиком системы GRUB2.

# Ответы на контрольные вопросы

1. Файл для общих изменений: /etc/default /grub — в нём задают GRUB_TIMEOUT, GRUB_DEFAULT, GRUB_CMDLINE_LINUX и т.п. 
2. Итоговый конфигурационный файл GRUB2: /boot /grub/grub.cfg (в некоторых дистрибутивах /boot/grub 2/grub. cfg, на UEFI — может быть в EFI‑разделе); его генерируют скрипты из /etc /grub.d/, редактировать вручную не рекомендуется. 
3. Команда для применения изменений: после правки выполнить sudo grub-mkc onfig -o /boo t/grub/grub .cfg (в Debian/Ubun tu можно использовать sudo up date-grub).
