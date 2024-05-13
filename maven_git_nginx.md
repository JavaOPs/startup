`sudo apt update`

### Установка Maven
`sudo apt install maven`  
`mvn -version`  

Для последней версии - скопировать путь к [Binary tar.gz archive](https://maven.apache.org/download.cgi)  
`wget https://dlcdn.apache.org/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz`   
`tar -xvf apache-maven-3.9.5-bin.tar.gz` - разархивируем (используйте Tab для автодополнения имени архива)  
`rm apache-maven-3.9.5-bin.tar.gz` - архив больше не нужен  
Переносим в каталог программ `/opt/apache-maven` (без версии)   
Добавляем переменные окружения [в конфигурацию](env.md):

```
export M2_HOME=/opt/apache-maven
export M2=$M2_HOME/bin
export PATH=$PATH:$M2
```

### Установка Git
`sudo apt install git`  
`git --version`

### [Установка Nginx](https://firstvds.ru/technology/lemp-install#nginx-install)
Веб-сервер [Nginx](https://ru.wikipedia.org/wiki/Nginx) очень удобен для задания правил маршрутизации (в том числе защиты от спама и атак), работа с куками, сжатия трафика, обработки статического контента и поддержки SSL(Https)

`sudo apt -y install nginx`  
Проверка:  `nginx -v`, `systemctl status nginx`, `ps -ax| grep nginx`

Если nginx запущен, по умолчанию отображается _/var/www/html/index.nginx-debian.html_ (можете поправить его содержание)  
(проследить путь можно через `sudo nginx -t`, `cat /etc/nginx/nginx.conf`, ` ll /etc/nginx/sites-enabled/*`)  

Проверяем из браузера: `http://server_ip_or_dns_name`  
Управление nginx: `sudo service nginx reload/stop/start`

## [Рефакторинг и деплой](https://javaops.ru/view/startup/deploy)

