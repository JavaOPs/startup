### [Install OpenJDK on Ubuntu](https://www.linuxcapable.com/how-to-install-openjdk-18-on-ubuntu-22-04-lts/)

Проверьте текущую JDK:  `java -version`. Если нет - устанавливаем последнюю версию:

`sudo apt update && sudo apt upgrade -y` - обновляем пакеты Ubuntu  
`apt-cache search openjdk` - ищем все доступные `openjdk` в дефолтном Ubuntu репозитории  
`sudo apt-get install openjdk-17-jdk -y` - находим последнюю версию и установливаем ее

Если вам хочется версию JDK, которой нет в стандартном Ubuntu репозитории - найдите ее на [jdk.java.net](https://jdk.java.net/) и скопируйте ссылку для скачивания. Например:

`cd ~`  
`wget https://download.java.net/java/GA/jdk19.0.1/afdd2e245b014143b62ccb916125e3ce/10/GPL/openjdk-19.0.1_linux-x64_bin.tar.gz`  
`tar -xvf openjdk-19.0.1_linux-x64_bin.tar.gz` - разархивируем (используйте _Tab_ для автодополнения имени архива)  
`rm openjdk-19.0.1_linux-x64_bin.tar.gz` - архив больше не нужен  
`sudo mv jdk-19* /opt/jdk-19` - переносим в каталог программ `/opt/jdk-19` (без младших цифр версии)
`export JAVA_HOME=/opt/jdk-19` - объявляем переменные окружения  
`export PATH=$PATH:$JAVA_HOME/bin`  
`java -version` - проверяем версию  

Чтобы переменные окружения сохранились в следующих сессиях, нужно занести их в конфигурацию, например в `~/.bashrc`

`cd ~ && mcedit .bashrc`  
Добавляем `export` в конец файла (копируем и вставляем через `Shift+Right Mouse Click`)

`export JAVA_HOME=/opt/jdk-19`  
`export PATH=$PATH:$JAVA_HOME/bin`  
_F2+F10_

Далее
`source .bashrc` или `. .bashrc` - обновляем окружение  
`java -version` - проверяем версию

[Set Environment Variable in Bash](https://devconnected.com/set-environment-variable-bash-how-to/)