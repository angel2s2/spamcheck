## Предисловие ##
Помимо стандартных случаев ведения логов, в данном тексте будут описаны настройки под различные демоны.

## Подробное описание параметров --log и --slog ##
_`--log [file]`_ <br />
Параметр _`--log`_ может использоваться как в сочетинии с именем файла, так и без. В первом случае будут произведены стандартые проверки на возможность записи, такие как существование каталога и права записи. При использовании параметра _`--log`_ без имени файла, будут проверены файлы _`/etc/*syslog*.conf`_ на присутствие незакоменитированных строк содежащих подстроку _`spamcheck`_ и в случае удачи логгирование будет происходить посредством утилиты _`logger`_. Если отсутствуют настройки лога для _`spamcheck`_, он будет вестись в файле по умолчанию _`./spamcheck.log`_.<br />
<br />
_`--slog`_<br />
Используя этот параметр, журнал логов будет записан с помощью утилиты _`logger`_. Параметр _`--log`_ и проверка настроек, присущая ему игнорируются.

## Настройка лога ##
> _Для начала определимся, что настройки будут производиться для ведения лога только в файле `/var/log/spamcheck.log`_<br />
> _Так же считаем, что изначально конфиги были стандартными._<br />

**metalog**

_Настройка текущего демона еще не производилась, вы можете помочь нам прислав настройку_

<br />

**rsyslog**

Для начала поправим вывод `*.info`:
```
#*.info;
mail.none;authpriv.none;cron.none                -/var/log/messages
if $syslogpriority-text == 'info' and \
	not ($syslogtag startswith "spamcheck:")	-/var/log/messages
```
И добавим файл лога
```
:syslogtag, startswith, "spamcheck:"			-/var/log/spamcheck.log
```

<br />

**syslog**

_Настройка текущего демона еще не производилась, вы можете помочь нам прислав настройку_

<br />

**syslog-ng**

Добавим в файл _`/etc/syslog-ng.conf`_ следующие строки:
```
destination d_spamcheck { file("/var/log/spamcheck.log"); };
filter f_spamcheck { program("spamcheck"); };
log { source(src); filter(f_spamcheck); destination(d_spamcheck); };
```
Изменяем фильтры:
```
filter f_user { facility(user) and not filter(f_spamcheck); };
filter f_messages { level(info..warn) and not facility(auth, authpriv, mail, news, cron) and not program(syslog-ng) and not filter(f_iptables) and not filter(f_spamcheck); };
filter f_everything { level(debug..emerg) and not facility(auth, authpriv) and not filter(f_spamcheck); };
filter f_info { level(info) and not filter(f_spamcheck); };
```