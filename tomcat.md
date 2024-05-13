### [Install Tomcat 9 on Ubuntu](https://linuxize.com/post/how-to-install-tomcat-9-on-ubuntu-20-04/)

1. Создаем пользователя, от имени которого будем запускать Tomcat.

`sudo useradd -m -U -d /opt/tomcat -s /bin/false tomcat`

2. Загружаем последнюю версию Tomcat 9.x (нам **не подойдет Tomcat версии 10, т.к. он использует пакет jakarta**)  
   URL на последнюю версию [копируем отсюда: /bin/apache-tomcat-VERSION.tar.gz](https://downloads.apache.org/tomcat/tomcat-9/). Для версии 9.0.68:

`wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.68/bin/apache-tomcat-9.0.68.tar.gz -P /tmp`

3. Распаковываем:

`sudo tar -xf /tmp/apache-tomcat-9.0.68.tar.gz -C /opt/tomcat/` (_Tab_ для автодополнения имени архива)  
`rm /tmp/apache-tomcat-9.0.68.tar.gz` - удалям архив

4. Для последующих обновлений создаем универсальную ссылку

`sudo ln -s /opt/tomcat/apache-tomcat-9.0.68 /opt/tomcat/latest`

5. Даем доступ юзеру `tomcat` к каталогу:

`sudo chown -R tomcat: /opt/tomcat`

6. Делаем скрипты `*.sh` исполняемыми:

`sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'`

#### [Создаем сервис для старта Tomcat](https://linuxize.com/post/how-to-install-tomcat-9-on-ubuntu-20-04/#creating-systemd-unit-file)

7. Создаем  _tomcat.service_:  

`sudo mcedit /etc/systemd/system/tomcat.service`

Копируем содержимое [_tomcat.service_](https://linuxize.com/post/how-to-install-tomcat-9-on-ubuntu-20-04/#creating-systemd-unit-file):  _Shift+Mouse Right Click, F2, F10_ в _mcedit_

**Не забываем поправить _JAVA_HOME_ на наш:** `echo ${JAVA_HOME}`

#### [Конфигурируем Tomcat](https://linuxize.com/post/how-to-install-tomcat-9-on-ubuntu-20-04/#configuring-tomcat-web-management-interface)

8. Добавляем внутри _tomcat-users_ права на администрирование:  
`<user username="tomcat" password="пароль_на_администрирование_tomcat" roles="tomcat,manager-gui,admin-gui"/>`

`sudo mcedit /opt/tomcat/latest/conf/tomcat-users.xml`  
`sudo cat /opt/tomcat/latest/conf/tomcat-users.xml`

9. Разрешаем администрирование Tomcat снаружи (для демо приложения допустимо, убедитесь что пароль у вас не _tomcat_)  
Комментируем или удаляем _Valve_ с разрешением только для _localhost_:  

`sudo mcedit /opt/tomcat/latest/webapps/manager/META-INF/context.xml`  
`sudo mcedit /opt/tomcat/latest/webapps/host-manager/META-INF/context.xml`

10. Рестартуем сервисы:

`sudo systemctl daemon-reload`

11. Запускаем Tomcat и проверяем статус:

`sudo systemctl enable --now tomcat`  
`sudo systemctl status tomcat`  
_Q_ для выхода

12. Если у вас открыт наружу порт 8080, уже можно посмотреть результат: [http://javaops-demo.ru:8080](http://javaops-demo.ru:8080)  
Иначе откройте его: 

`sudo ufw allow 8080/tcp`

#### Полезное
`sudo systemctl stop tomcat.service` - stop  
`sudo systemctl start tomcat.service` - start  
`sudo systemctl daemon-reload` - reload tomcat java opts