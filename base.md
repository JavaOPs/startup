### [APT (advanced packaging tool)](#apt)
### [Создание пользователя](#user)
### [Редактирование файлов](#editor)
### [Копирование между серверами](#copy)

---

<h2><a id="apt" >APT (advanced packaging tool)</a></h2>

- [Менеджер пакетов APT](https://firstvds.ru/technology/menedzher-paketov-apt)
- [Apt Update и Upgrade](https://itisgood.ru/2021/02/25/komandy-apt-update-i-upgrade-v-chem-raznica/)

`sudo apt update` - обновление индекса пакетов или списков пакетов  
`sudo apt upgrade -y` - обновляем пакеты Ubuntu на новые версии
`sudo boot` - перегрузить при необходимости

<h2><a id="user">Создание пользователя</a></h2>

[Работать из под `root` небезопасно](https://www.google.com/search?q=Lunux+почему+не+рекомендуется|нельзя+root): создадим нового пользователя с домашним каталогом и дадим ему права на команды администрирования (включим в группу `sudo`):

`useradd -m -s /bin/bash -G sudo your_user`    
`pinky -l your_user`  - информация о пользователе

`passwd your_user` - задать ему пароль  
`su - your_user` - залогиниться от его имени  
`cd ~` - перейти в домашний каталог  
`pwd` - посмотреть текущий каталог  
`sudo -l` - проверить свои права на выполнение команд от имени `root`  
`exit` - вернуться в `root`  

Далее при коннекте к серверу заходите уже не как `root`, а вновь созданный пользователь

[Управление пользователями](https://firstvds.ru/technology/linux-user-management)

<h2><a id="editor">Редактирование файлов</a></h2>

По умолчанию на Linux используется крайне неудобный для новичков редактор `Vim` (один из [самых популярных вопросов](https://stackoverflow.com/questions/11828270/how-do-i-exit-vim) - как из него выйти).
Я обычно редактирую файлы на локальном компьютере и копирую на сервер. Для редактирования на сервере установите редактор от Midnight Commander `mcedit`:

`sudo apt install -y mcedit`  
   
`mc` - файловый менеджер  
`sudo mcdeit имя_файла` - sudo нужно только для системных файлов  
Внизу него есть help по клавишам, выход - F10.

Если неверно отрисовываются линии, [нужно выбрать нужную локаль](https://askubuntu.com/a/872467/1357134)

<h2><a name="copy">Копирование между серверами</a></h2>

Для Windows:
- [WinSCP](https://winscp.net/eng/download.php) 
- [Total Commander](https://www.ghisler.com/) + плагин [Secure FTP](https://www.ghisler.ch/wiki/index.php/Secure_FTP_plugin). Если доступ закрыт, поставьте [VPN](https://github.com/JavaOPs/topjava/wiki/VPN)

Для Linux удобно использовать [утилиту _scp_](https://firstvds.ru/technology/basic-linux-commands) 

---------------
- [Гайды по Linux](https://firstvds.ru/technology#gaydy_po_linux)
- [Первые шаги в командной строке](https://firstvds.ru/technology/basic-linux-commands)

### [Установка JDK](jdk.md)
