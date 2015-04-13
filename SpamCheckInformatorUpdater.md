## Как узнать, что скрипт обновился ##

Просто положите с cron такой однострочник:
```
wget -q -O - http://dl.dropbox.com/u/922069/Blog/spam-check | md5sum | sed 's/\-/\/path\/to\/spam-check/' | md5sum -c || echo 'SpamCheck updated!!!'
```

  * `\/path\/to\/spam-check` замените на путь, где у вас лежит скрипт
  * `echo 'SpamCheck updated!!!'` замените на нужную вам команду, например, отправка мыла.
  * Адрес "<a href='http://dl.dropbox.com/u/922069/Blog/spam-check'><a href='http://dl.dropbox.com/u/922069/Blog/spam-check'>http://dl.dropbox.com/u/922069/Blog/spam-check</a></a>" является постоянным. По этому линку всегда можно слить самую свежую версию (аля зеркало).

<br><br><br>

<h4>Пример получения уведомлений по джабберу</h4>
<pre><code>wget -q -O - http://dl.dropbox.com/u/922069/Blog/spam-check | md5sum | sed 's/\-/\/path\/to\/spam-check/' | md5sum -c || echo 'SpamCheck updated!!!' | sendxmpp admin@jabber.domain.ru<br>
</code></pre>
<h4>По мылу почти тоже самое</h4>
<pre><code>wget -q -O - http://dl.dropbox.com/u/922069/Blog/spam-check | md5sum | sed 's/\-/\/path\/to\/spam-check/' | md5sum -c || echo 'SpamCheck updated!!!' | ssmtp admin@domain.ru<br>
</code></pre>

<br><br><br>

<h5>Как настроить ssmtp и sendxmpp</h5>
<ul><li><a href='http://angel2s2.blogspot.com/2009/04/ssmtp.html'>ssmtp - минимальная настройка</a><br>
</li><li><a href='http://angel2s2.blogspot.com/2009/05/sendxmpp.html'>SendXMPP: Мониторим сервер с помощью Jabber</a><br>