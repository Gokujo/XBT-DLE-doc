# Установка дополнительных пакетов

## Инструкция с 0-web.ru
<tabs>
    <tab title="Ubuntu / Debian">
        <code-block lang="bash">apt-get install cmake g++ libboost-date-time-dev libboost-dev libboost-filesystem-dev libboost-program-options-dev libboost-regex-dev libboost-serialization-dev libmysqlclient15-dev make zlib1g-dev</code-block>
    </tab>
    <tab title="CentOS, Fedora Core, Red Hat">
        <code-block lang="bash">yum install boost-devel gcc-c++ mysql-devel</code-block>
        <b>Если ошибка - Processing Conflict mysql55 conflicts mysql</b>:
        <b>Решение</b>: Вместо mysql-devel установить mysql55-devel:
        <code-block lang="bash">yum install boost-devel gcc-c++ mysql55-devel subversion</code-block>
        <b>Если ошибка - Error Package mysql-devel-5.1.73-3.el6_5.x86_64 (updates) Requires mysql = 5.1.73-3.el6_5</b>
        <b>Решение</b>:
        <code-block lang="bash">cd /etc/yum.repos.d
wget http://rpms.famillecollet.com/enterprise/remi.repo
yum --enablerepo=remi install mysql-devel
        </code-block>
    </tab>
    <tab title="FreeBSD">
        Обновляем порты:
        <code-block lang="bash">
        portsnap fetch
        portsnap update
        </code-block>
        <b>Внимание!</b> На время установки рекомендую отключить apache и mysql:
        <code-block lang="bash">
        /usr/local/etc/rc.d/apache22 stop
        /usr/local/etc/rc.d/mysql-server stop
        </code-block>
        Далее:
        <code-block lang="bash">
        make -C /usr/ports/devel/subversion install clean
        make -C /usr/ports/devel/boost-jam install clean
        make -C /usr/ports/devel/boost-libs install clean
        make -C /usr/ports/lang/gcc48 install clean
        rehash
        </code-block>
    </tab>
</tabs>

## Инструкция из сети
<tabs>
    <tab title="Ubuntu / Debian">
        <code-block lang="bash">apt-get install cmake default-libmysqlclient-dev g++ git libboost-dev make zlib1g-dev</code-block>
    </tab>
    <tab title="CentOS, Fedora Core, Red Hat">
        <code-block lang="bash">dnf install boost-devel cmake gcc-c++ git make mysql-devel systemd-devel
</code-block>
    </tab>
</tabs>

Создать ярлык x64 (/usr/lib64) библиотек для x86 (/usr/lib)
```Bash
ln -s /usr/lib64/mysql/libmysqlclient.so /usr/lib/libmysqlclient.so
ln -s /usr/lib64/libsystemd.so.0 /usr/lib/libsystemd.so.0
```
