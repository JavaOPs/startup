### Деплой war на сервер

- Меняем в пропертях БД имя и пароль на те, что сконфигурены на PostgreSQL сервере

- Получаем _war_ для деплоя:  
  -  Для BaseJava делаем _Build_ и проверяем настройки БД в _[PROJECT_DIR]/out/artifacts/basejava/basejava.war/WEB-INF/classes/resumes.properties_  
  -  Для TopJava делаем `mvn -DskipTests=true package` и проверяем _[PROJECT_DIR]/target/topjava.war/WEB-INF/classes/db/postgres.properties_

- Открываем Tomcat Manager: _http://[сервер_IP_или_домен]:8080/manager_ (пароль для него вы задавали при установки Tomcat):  
`sudo cat /opt/tomcat/latest/conf/tomcat-users.xml`

- В **"WAR file to deploy"** выбираем наш _war_ и деплоим

В JDK 19 доступ по reflect к пакетам java запрещен, при деплое возможна ошибка:   
_reflect.InaccessibleObjectException: Unable to make field private final int java.time.LocalDate.year accessible: module java.base does not "opens java.time"_

`sudo su`  
`cp /opt/tomcat/latest/bin/catalina.sh /opt/tomcat/latest/bin/_catalina.sh` - сделаем копию на всякий случай  
`mcedit /opt/tomcat/latest/bin/catalina.sh`  

Находим _JDK_JAVA_OPTIONS=_ (F7, Shift+Right Click) и добавить между ними:  
`JDK_JAVA_OPTIONS="JDK_JAVA_OPTIONS --add-opens=java.base/java.lang=ALL-UNNAMED"`    
(можно скопировать соседнюю строчку: F3, Down, F5, F3 и отредактировать или отредактировать локально и скопировать на сервер с сохранением прав на запуск)  
Перезапускаем Tomcat: `sudo systemctl restart tomcat`

Наконец, делаем перенаправление порта 80 на 8080, чтобы прложение было доступно по http://[сервер_IP_или_домен]  
`sudo iptables -A PREROUTING -t nat -p tcp --dport 80 -j REDIRECT --to-ports 8080`