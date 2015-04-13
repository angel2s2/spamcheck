# SpamCheck
##### скрипт для проверки IP-адресов по спам базам ##
---

```
spam-check [-q] [-l] [-d dnsbl | -f filename | -i] [-s dns_server] [-t] \
	   [--] [ip or domain-name ...]

   -q		- Ничего не выводить
   -l		- Показать список DNSBL-серверов
   -d		- Проверить по указанному DNSBL
   -f		- Взять список DNSBL-серверов из файла (по одному на строчку)
   -i		- Сграбить список DNSBL с сайта http://myiptest.com/
   -s		- Указать DNS-сервер, через который будет идти проверка 
		  (по умолчанию OpenDNS - 208.67.222.222)
   -t		- Считать Time Out''ы ошибкой
   --		- Считается, что дальше идут только ip и/или доменные имена
   [ip or domain-name ...]	- ip и/или доменные имена, которые нужно проверить
   --vesrion, --help, --usage	- без комментариев
```


***Automatically exported from http://code.google.com/p/spamcheck***
