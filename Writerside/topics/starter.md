# Установка XBT для модуля Tracker for DLE

<!--Writerside adds this topic when you create a new documentation project.
You can use it as a sandbox to play with Writerside features, and remove it from the TOC when you don't need it anymore.-->

## Подключение к серверу

Подключаться к серверу надо по SSH, например, через putty.
Скачать putty: [PuTTY Download Page](https://www.putty.org/)

_Skripters.biz рекомендует [BitVise](https://www.bitvise.com/ssh-client-download)_

## Как узнать какая ОС установлена?

Выполняем команду:

```Bash
uname -a
```

Получаем примерно такой вывод:

```Bash
$ uname -a
Linux user 2.6.38-10-generic-pae #46-Ubuntu SMP Tue Jun 28 16:54:49 UTC 2011 i686 i686 i386 GNU/Linux
```

Тут можно узнать что это убунта 32 бита
Более точно версию ОС можно узнать:

```Bash
cat /etc/issue
```

Получаем:

```Bash
$ cat /etc/issue
Ubuntu 11.04 \n \l
```

Вот тут уже более понятно что это версия убунты 11.04
