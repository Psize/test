Скриншот авторизации в админке 
![image](https://github.com/user-attachments/assets/d10c7e2f-e376-4a7f-8761-9ea09ccb57fe)

Список используемых команд 
Для установки Zabbix Server 
a. Установите репозиторий Zabbix
Документация с сайта  https://www.zabbix.com/ru/download?zabbix=7.2&os_distribution=alma_linux&os_version=9&components=server_frontend_agent&db=pgsql&ws=apache

Исключите пакеты Zabbix поставляемые в репозитории EPEL, если он у Вас установлен. Отредактируйте файл /etc/yum.repos.d/epel.repo и добавте следующую директиву.

[epel]
...
excludepkgs=zabbix*
Продолжите установку репозитория Zabbix.

# rpm -Uvh https://repo.zabbix.com/zabbix/7.2/release/alma/9/noarch/zabbix-release-latest-7.2.el9.noarch.rpm
# dnf clean all
b. Установите Zabbix сервер, веб-интерфейс и агент
# dnf install zabbix-server-pgsql zabbix-web-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-selinux-policy zabbix-agent
c. Создайте базу данных
Документация
Установите и запустите сервер базы данных.

Выполните следующие комманды на хосте, где будет распологаться база данных.

# sudo -u postgres createuser --pwprompt zabbix
# sudo -u postgres createdb -O zabbix zabbix
На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.

# zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
