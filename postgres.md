### [Установка PostgreSQL](https://ruvds.com/ru/helpcenter/postgresql-pgadmin-ubuntu/)

Перед установкой проверьте свою локаль: `locale`
Если не **"ru_RU.UTF-8"** - [поменяйте](https://askubuntu.com/a/872467/1357134): `sudo dpkg-reconfigure locales`

#### Установка / проверка
`sudo apt update`  
`sudo apt install postgresql` - установка  
`sudo systemctl is-active postgresql` - проверка: active  
`sudo systemctl is-enabled postgresql` - проверка: enabled  
`sudo systemctl status postgresql` - статус  
`sudo pg_isready` - _/var/run/postgresql:5432_ - готов к коннекту  

#### Создаем БД

`sudo su - postgres` - переключаемся на юзера postgres  
`psql` - запускаем SQL консоль;  
`\list` or `\l` - [посмотреть все БД](https://dba.stackexchange.com/questions/1285/264545)/ Убеждаемся, что Collate и Ctype - "ru_RU.UTF-8"  
`CREATE DATABASE YOUR_DB;` - создаем БД (_YOUR_DB_ для basejava: _resumes_, для topjava: _topjava_)  
Далее копируем в консоль sql команды для создания и заполнения таблиц.
`\q` - выход из консоли.

Или создаем базу скриптами: копируем sql скрипты на сервер чз `scp` или _WinSCP/ Total Commander_ и там запускаем их [любым способом](https://stackoverflow.com/questions/9736085/run-a-postgresql-sql-file-using-command-line-arguments)
Например: `psql YOUR_DB < /home/[your_login]/init_db.sql`

Опционально - создаем в `psql` нового пользователя:   

`CREATE USER "user" WITH password 'password';`  
`\du`  - [посмотреть всех юзеров](https://ubiq.co/database-blog/how-to-list-all-users-in-postgresql/)  
`GRANT ALL PRIVILEGES ON DATABASE YOUR_DB TO "user";`  
`\c YOUR_DB` - [переключиться на БД](https://stackoverflow.com/questions/3949876/how-to-switch-databases-in-psql)   
`\c` - посмотреть текущий коннект, `\z` - посмотреть все таблицы БД     
`GRANT ALL ON ALL TABLES IN SCHEMA public TO "user";` - [PostgreSQL GRANT](https://www.postgresqltutorial.com/postgresql-administration/postgresql-grant/)
`GRANT ALL ON ALL SEQUENCES IN SCHEMA public TO "user";`  
`\q`

Проверяем права:

`psql -h localhost -U user -d resumes`   
`SELECT * FROM resume;`  

Задаем пароль для пользователя _postgres_:

`\password postgres` - [change postgres user password](https://stackoverflow.com/a/12721020/548473)

