# Домашняя работа к занятию «Система мониторинга Zabbix» - Боровик А. А.

### Задание 1

Ответ:
1. Авторизация

![Авторизация](https://github.com/Lex-Chaos/zabbix-hw/blob/main/img/Authorization.png)

2. Команды
```
# Устанавливаю PostgreSQL
apt install postgresql

# Устанавливаю репозиторий Zabbix
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb

dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb

apt update

# Устанавливаю Zabbix-сервер и Web-интерфейс
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts

# Устанавливаю и запускаю сервер базы данных
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'

su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'

# Импортирую первычные скрипты
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# Редактирую файл zabbix_server.conf
sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf

# Запускаю сервера Zabbix и Apache
systemctl restart zabbix-server apache2

systemctl enable zabbix-server apache2

# Проверяю работу серверов
systemctl status zabbix-server

systemctl status apache2
```
---

### Задание 2

Ответ:

1. Хосты доступны

![Хосты доступны](https://github.com/Lex-Chaos/zabbix-hw/blob/main/img/02-Hosts_richble.png)

2. Логи агентов

![Лог агента 1](https://github.com/Lex-Chaos/zabbix-hw/blob/main/img/03-Log(agent1).png)

![Лог агента 2](https://github.com/Lex-Chaos/zabbix-hw/blob/main/img/04-Log(agent2).png)

3. Последние данные

![Последние данные](https://github.com/Lex-Chaos/zabbix-hw/blob/main/img/05-Latest_data.png)

4. Команды

```
# Устанавливаю репозиторий Zabbix
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb

dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb

apt update

# Устанавливаю Zabbix агент
apt install zabbix-agent

# Запускаю Zabbix агент
systemctl restart zabbix-agent

systemctl enable zabbix-agent

# Проверяю Zabbix агент
systemctl status zabbix-agent

# Правлю конфиг
sed -i 's/Server=127.0.0.1/Server=192.168.0.138'/g' /etc/zabbix/zabbix_agentd.conf
```
---

### Задание 3*

Ответ:
