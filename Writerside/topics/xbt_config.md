# Настройка XBT
## Конфигурация
Открываем файл конфигурации
<tabs>
    <tab title="Файл от 0-web">
        <code-block lang="plain text">~/xbt/xbt_tracker.conf</code-block>
    </tab>
    <tab title="Файл с исходника в сети">
        <code-block lang="plain text">~/xbt/tracker/xbt_tracker.conf</code-block>
    </tab>
</tabs>

Правим под себя конфигурацию:

**ВНИМАНИЕ!!!** XBTT должен работать с той же самой БД что и сайт!
(в случае отличия префикса таблиц от dle - заменить на свой)

```
mysql_host = localhost
mysql_user = ПОЛЬЗОВАТЕЛЬ_БД
mysql_password = ПАРОЛЬ_ДЛЯ_БД
mysql_database = ИМЯ_БД
mysql_table_prefix = dle_tracker_
```



## Скрипт запуска
<tabs>
    <tab title="Файл от 0-web">
        <code-block lang="plain text">wget http://0-web.ru/uploads/xbt/xbt_lin.txt -O /etc/init.d/xbt; chmod +x /etc/init.d/xbt</code-block>
    </tab>
    <tab title="Файл с исходника в сети">
        <code-block lang="bash">nano /etc/init.d/xbt</code-block>
        Туда прописываем:
        <code-block lang="bash"><![CDATA[#!/bin/sh

XBT_PATH="~/xbt/tracker"

start() {
    echo "Starting XBT Tracker"
    start-stop-daemon --start --quiet --exec $XBT_PATH/xbt_tracker -- --conf_file $XBT_PATH/xbt_tracker.conf
    echo $?
}

stop() {
    echo "Stopping XBT Tracker"
    start-stop-daemon --stop --quiet --pidfile /root/xbt/xbt_tracker.pid
    echo $?
}

case "$1" in
            start)
                start
;;
            stop)
                stop
;;
            *)
                echo "Usage: $0 {start|stop}"
                exit 1
esac

exit 1
]]>
        </code-block>
        <code-block lang="bash">chmod +x /etc/init.d/xbt
update-rc.d xbt defaults 99</code-block>
    </tab>
</tabs>

### Работа со скриптом
Команды для работы с xbt для линукс:

Стартовать xbt:
```Bash
/etc/init.d/xbt start
```

Остановить xbt:
```Bash
/etc/init.d/xbt stop
```

Перестартовать xbt:
```Bash
/etc/init.d/xbt restart
```

Для автоматического запуска хбт при перезагрузке сервера - добавить стоку: `/etc/init.d/xbt start` в `/etc/rc.local` или в crontab:
```Bash
@reboot         sleep 10 && /etc/init.d/xbt start >/dev/null 2>&1
```