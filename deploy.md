### Деплой war на сервер

- Меняем в пропертях БД имя и пароль на те, что сконфигурены на PostgreSQL сервере

- Получаем _war_ для деплоя:  

#### BaseJava

Делаем _Build_ и проверяем настройки БД в _[PROJECT_DIR]/out/artifacts/basejava/basejava.war/WEB-INF/classes/resumes.properties_

В JDK 19 доступ по reflect к пакетам java запрещен, при деплое возможна ошибка:   
_reflect.InaccessibleObjectException: Unable to make field private final int java.time.LocalDate.year accessible: module java.base does not "opens java.time"_

`sudo su`  
`cp /opt/tomcat/latest/bin/catalina.sh /opt/tomcat/latest/bin/_catalina.sh` - сделаем копию на всякий случай  
`mcedit /opt/tomcat/latest/bin/catalina.sh`  

Находим _JDK_JAVA_OPTIONS=_ (F7, Shift+Right Click) и добавляем между ними:  
`JDK_JAVA_OPTIONS="JDK_JAVA_OPTIONS --add-opens=java.base/java.time=ALL-UNNAMED"`    
(можно скопировать соседнюю строчку: F3, Down, F5, Shift+F3 и отредактировать или отредактировать локально и скопировать на сервер с сохранением прав на запуск)

#### TopJava

Локально собираем WAR: `mvn -DskipTests=true package`

Создаем на сервере каталог, куда будет указывать _TOPJAVA_ROOT_ с правами для всех: `sudo mkdir -m 777 /opt/topjava`  
Копируем в _TOPJAVA_ROOT_ каталог _/config/messages_ с локализацией и проперти DB: _/config/db.properties_

Добавляем для Tomcat свои переменные окружения в скрипт _setenv.sh_: `sudo mcedit /opt/tomcat/latest/bin/setenv.sh`    
Записываем туда
```
export TOPJAVA_ROOT=/opt/topjava
export CATALINA_OPTS="$CATALINA_OPTS -Dspring.profiles.active=datajpa,vds"
```
И делаем его исполняемым: `sudo chmod +x /opt/tomcat/latest/bin/setenv.sh`  
Наше приложение будет запускаться с профилями `datajpa,vds`  

-----------------------

`sudo systemctl restart tomcat` - рестартуем Tomcat   
`sudo tail -f /opt/tomcat/latest/logs/catalina.out` - смотрим логи в процессе деплоя

Открываем в браузере Tomcat Manager: _http://[сервер_IP_или_домен]:8080/manager_ (пароль для него вы задавали при установки Tomcat в _tomcat-users.xml_)  

- В **"WAR file to deploy"** выбираем наш _war_ и деплоим его

Наконец, делаем перенаправление порта 80 на 8080, чтобы приложение было доступно по адресу _http://[сервер_IP_или_домен]_  
`sudo iptables -A PREROUTING -t nat -p tcp --dport 80 -j REDIRECT --to-ports 8080`

- Демо BaseJava: [http://javaops-demo.ru/basejava](http://javaops-demo.ru/basejava)   
- Демо TopJava: [http://javaops-demo.ru/topjava](http://javaops-demo.ru/topjava)
