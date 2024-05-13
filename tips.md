### [При падении по OOM - пространство подкачки](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04-ru)
### Опционально: [настройка sshd_config](sshd_config.md)

#### Установка `sshd` (если `ssh` не работает)

Для работы `ssh` на сервере должен быть запущен демон (процесс, работающий в фоновом режиме). На большинстве серверов он установлен «из коробки».

- `ps -aux | grep sshd` - проверка запушенного процесса  
- `sudo netstat -plant | grep :22` - кто слушает 22 порт  
- `telnet localhost 22` - проверка соединения  

Если же на сервере не установлен `sshd`, то его легко установить с помощью пакетного менеджера:

- `sudo apt-get update && sudo apt-get upgrade`  
- `sudo apt-get install openssh-server`  
- `sudo systemctl enable ssh --now` - (опция _--now_: запуск демона сразу)  

#### Настройка `firewall`

- `sudo ufw allow ssh` - открыть входящие соединения на порт 22 (или тот, который указан в конфиге) для пакетов TCP  
- `sudo ufw allow 1234/tcp` - нестандартный порт, например, 1234  
- `sudo ufw enable` или `sudo ufw reload` - активация изменений

#### [Смена `hostname`](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command)
