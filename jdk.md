### [Install OpenJDK on Ubuntu](https://www.linuxcapable.com/how-to-install-openjdk-18-on-ubuntu-22-04-lts/)

Проверьте текущую JDK:  `java -version`. Если нет - устанавливаем последнюю версию:

`apt-cache search openjdk` - ищем все доступные `openjdk` в дефолтном Ubuntu репозитории  
`apt-get update` - обновляем пакеты  
`sudo apt-get install openjdk-19-jdk -y` - находим последнюю версию и установливаем ее
`export JAVA_HOME=/usr/bin/java`  (путь из дд `which java` без `/bin/java`)   
`readlink -f $(which java)` - [папка с JDK](https://stackoverflow.com/a/23427862/548473)

Если вам хочется версию JDK, которой нет в стандартном Ubuntu репозитории - найдите ее на [jdk.java.net](https://jdk.java.net/) и скопируйте ссылку для скачивания. Например: `cd ~`  
`wget https://download.java.net/java/GA/jdk21.0.1/415e3f918a1f4062a0074a2794853d0d/12/GPL/openjdk-21.0.1_linux-x64_bin.tar.gz`  
      
`tar -xvf openjdk-21.0.1_linux-x64_bin.tar.gz` - разархивируем (используйте _Tab_ для автодополнения имени архива)  
`rm openjdk-21.0.1_linux-x64_bin.tar.gz` - архив больше не нужен  
`sudo mv jdk-21* /opt/jdk-21` - переносим в каталог программ `/opt/jdk-21` (без младших цифр версии)    
`export JAVA_HOME=/opt/jdk-21` - объявляем переменные окружения  

`export PATH=$PATH:$JAVA_HOME/bin`  
`java -version` - проверяем версию  

### [Добавляем переменные окружения в конфигурацию](env.md)
#### Полезное
`update-java-alternatives --list` - List all java versions  
`sudo update-alternatives --config java` - Set java version as default 