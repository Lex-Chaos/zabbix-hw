# Домашняя работа к занятию «Система мониторинга Zabbix» - Боровик А. А.

### Задание 1

Ответ:
1. Авторизация
![Авторизация](https://github.com/Lex-Chaos/zabbix-hw/blob/main/img/Authorization.png)

2.
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

---

### Задание 3

Ответ:

### Задание 4*

Ответ:
