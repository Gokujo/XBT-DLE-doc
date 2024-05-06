# Установка XBTT
## Оф. инструкция автора
**Файлы утеряны!** Если у вас сохртанились эти исходники, то просим сообщить нам через [форму контакта](https://skripters.biz/forum/misc/contact)

Создаём нужные каталоги:
```Bash
mkdir -p /home/xbt/xbt-source; cd /home/xbt/xbt-source/
```

Скачиваем исходники:
```Bash
wget http://0-web.ru/uploads/xbt/xbt_2466.zip; unzip -o xbt_2466.zip
chmod 777 Tracker/make.sh
wget http://0-web.ru/uploads/xbt/xbtt-source_2466.zip; unzip -o -d Tracker xbtt-source_2466.zip
cd Tracker; ./make.sh
```

Создаём конфигурационный файл:
```Bash
cp xbt_tracker.conf.default /home/xbt/xbt_tracker.conf; cp xbt_tracker /home/xbt/
```


### Если ошибка - cc1plus ошибка некорректный ключ "-std=c++11"
Необходима версия gcc 4.6 или больше, но её нет в репозиториях, по этому собираем более старую версию XBT
```Bash
rm -r /home/xbt/xbt-source; mkdir -p /home/xbt/xbt-source; cd /home/xbt/xbt-source
wget http://0-web.ru/uploads/xbt/xbt_2396.zip; unzip -o xbt_2396.zip; chmod 777 Tracker/make.sh
wget http://0-web.ru/uploads/xbt/xbtt-source_2396.zip; unzip -o -d Tracker xbtt-source_2396.zip
cd Tracker; ./make.sh
```

### Если ошибка - cc1plus error unrecognized command line option "-std=c++0x"
```Bash
yum update
yum remove gcc*
yum install gcc44*
ln -s /usr/bin/gcc44 /usr/bin/gcc
ln -s /usr/bin/g++44 /usr/bin/g++
```

### Если ошибка - ../misc/xcc_z.cpp 5 18 error zlib.h Нет такого файла или каталога
```Bash
yum install zlib-devel
```

### Если ошибка - /usr/bin/ld cannot find -lssl
```Bash
yum install openssl-devel
```

### Если ошибка - ‘template class std::auto_ptr’ is deprecated -Wdeprecated-declarations
Найти файл server.cpp и в нём найти `std::auto_ptr`

Заменить на `std::unique_ptr`


Найти `m_connections.push_back(connection);`

Заменить на `m_connections.push_back(connection.release());`

### Дле FreeBSD
Файлы:
- `Tracker/tracker_input.cpp`
- `misc/xbt/data_ref.h`
- `misc/bvalue.cpp`

Найти все `atoll`

Заменить на `atoi`

Файл: `Tracker/connection.cpp`

Добавить в самое начало:
```C++
#include <sys/uio.h>
#include <sys/types.h>
#include <sys/socket.h>
```

Файл: `Tracker/server.cpp`

Добавить в самое начало:
```C++
#include <sys/types.h>
#include <sys/socket.h>
```

Файл: `Tracker/make.sh`

Первую строку:
```C++
g++ $@ -DEPOLL -DNDEBUG -I ../misc -I . -O3 -o xbt_tracker -std=c++0x \
```

Заменить на:
```C++
g++48 $@ -DNDEBUG -O3 -I ../misc -I . -o xbt_tracker -I /usr/local/include -std=c++0x \
```

Следующее сообщение не является ошибкой, его игнорируем:
```
In file included from connection.cpp:5:0:
stdafx.h:3:0: warning: "FD_SETSIZE" redefined [enabled by default]
#define FD_SETSIZE 1024
^
In file included from /usr/local/lib/gcc48/gcc/x86_64-portbld-freebsd9.0/4.8.1/include-fixed/sys/types.h:287:0,
from connection.cpp:2:
/usr/include/sys/select.h:59:0: note: this is the location of the previous definition
#define FD_SETSIZE 1024U
^
In file included from server.cpp:4:0:
stdafx.h:3:0: warning: "FD_SETSIZE" redefined [enabled by default]
#define FD_SETSIZE 1024
^
In file included from /usr/local/lib/gcc48/gcc/x86_64-portbld-freebsd9.0/4.8.1/include-fixed/sys/types.h:287:0,
from server.cpp:1:
/usr/include/sys/select.h:59:0: note: this is the location of the previous definition
#define FD_SETSIZE 1024U
^
```

### В случае ошибок
Нужно убедится что стоит последняя версия boost и обновить её:

обновляется она предельно просто, идём на офф сайт: http://sourceforge.net/projects/boost/files/boost/

и качаем последнюю версию под линукс (Unix line)
```Bash
wget http://downloads.sourceforge.net/project/boost/boost/1.55.0/boost_1_55_0.zip
```

распаковываем из скачанного архива папку boost в: (может отличаться на разных дистрибутивах) с заменой существующей папки
- или /usr/local/include/
- или /usr/include/

## Инструкция с интернета
Переходим в домашний каталог
```Bash
cd ~
```

Создаём клон исходных файлов и компилируем файлы
```Bash
mkdir -p /home/xbt/xbt-source; cd /home/xbt
git clone https://github.com/OlafvdSpek/xbt
mv ~/xbt/xbt ~/xbt/xbt-source
rm -r ~/xbt/xbt
```

Запускаем компиляцию
```Bash
cd ~/xbt/xbt-source/Tracker
cmake .
make
```
Либо

```Bash
chmod 777 ~/xbt/xbt-source/Tracker/make.sh
cd ~/xbt/xbt-source/Tracker
./make.sh
```

После компиляции нужно определиться из какой папки должен будет запускаться трекер. В этом примере будет использоваться папка **~/xbt/tracker**
```Bash
cp xbt_tracker ~/xbt/tracker/
cp xbt_tracker.conf.default ~/xbt/tracker/
cp xbt_tracker.sql ~/xbt/tracker/
cd ~/xbt/tracker/
mv xbt_tracker.conf.default xbt_tracker.conf
```
