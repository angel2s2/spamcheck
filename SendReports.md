Для автоматической проверки своих серверов можно использовать нижеприведенные команды, которые стоит добавить в Cron.

### Пример получения уведомлений по джабберу, только если хоть один из переданных скрипту ip найден хоть в одной DNSBL ###
##### полный вывод скрипта #####
```
_SP=$(/path/to/spam-check domain.ru 2>&1) || echo "$_SP" | sendxmpp admin@jabber.domain.ru
```

##### только DNSBL, в которых есть указанные ip #####
```
_SP=$(/path/to/spam-check domain.ru 2>&1 >/dev/null) || echo "$_SP" | sendxmpp admin@jabber.domain.ru
```

##### только уведомление #####
```
/path/to/spam-check -q domain.ru || echo 'My ip in DNSBL!!!' | sendxmpp admin@jabber.domain.ru
```


### Пример получения уведомлений по джабберу, не зависимо от результатов проверки ###
##### полный вывод скрипта #####
```
echo "$(/path/to/spam-check domain.ru 2>&1)" | sendxmpp admin@jabber.domain.ru
```

##### только DNSBL, в которых есть указанные ip #####
```
echo "$(/path/to/spam-check domain.ru 2>&1 >/dev/null)" | sendxmpp admin@jabber.domain.ru
```

##### только уведомление #####
```
/path/to/spam-check -q domain.ru ; echo 'spam-check finished!' |  sendxmpp admin@jabber.domain.ru
```

<br><br><br>

<h3>А как по мылу?</h3>
Чтобы отправить отчет по мылу, а не по джабберу, достаточно заменить "<b><i>sendxmpp admin@jabber.domain.ru</i></b>" на "<b>ssmtp admin@domain.ru</b>", например:<br>
<pre><code>_SP=$(/path/to/spam-check domain.ru 2&gt;&amp;1) || echo "$_SP" | ssmtp admin@domain.ru<br>
</code></pre>

<br><br><br>

<h4>Как настроить ssmtp и sendxmpp</h4>
<ul><li><a href='http://angel2s2.blogspot.com/2009/04/ssmtp.html'>ssmtp - минимальная настройка</a>
</li><li><a href='http://angel2s2.blogspot.com/2009/05/sendxmpp.html'>SendXMPP: Мониторим сервер с помощью Jabber</a><br></li></ul>

<br><br><br>

<h4>P.S.: На всякий случай, как вывести результат работы сприпта в файл:</h4>
<h5>полный вывод скрипта</h5>
<pre><code>/path/to/spam-check domain.ru &gt;/path/to/spam-check.log 2&gt;&amp;1<br>
</code></pre>

<h5>только DNSBL, в которых есть указанные ip</h5>
<pre><code>/path/to/spam-check domain.ru 2&gt;/path/to/spam-check.log &gt;/dev/null<br>
</code></pre>