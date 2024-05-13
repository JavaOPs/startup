### [Добавление переменных окружения конфигурацию](https://devconnected.com/set-environment-variable-bash-how-to/)

Чтобы переменные окружения экспортировались при открытиии сессии, их нужно занести их в конфигурацию:  

`cd ~ && mcedit .bashrc`  

Добавляем `export` в конец файла (копируем и вставляем через `Shift+Right Mouse Click`)

Для `JAVA_HOME`:  
`export JAVA_HOME=...`   
`export PATH=$JAVA_HOME/bin:$PATH` - если устанавливали java не из Ubuntu репозитория  
_F2+F10_

Далее
`source .bashrc` или `. .bashrc` - обновляем окружение  
`java -version` - проверяем версию  
`echo $JAVA_HOME` - проверяем переменную окружения

### [Установка PostgreSQL, создание БД](postgres.md)
