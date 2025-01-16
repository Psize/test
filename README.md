Скриншот авторизации в админке 
![image](https://github.com/user-attachments/assets/d10c7e2f-e376-4a7f-8761-9ea09ccb57fe)

Список используемых команд 
Для установки Zabbix Server 
a. Установите репозиторий Zabbix\
Документация с сайта  https://www.zabbix.com/ru/download?zabbix=7.2&os_distribution=alma_linux&os_version=9&components=server_frontend_agent&db=pgsql&ws=apache\


a. Установите репозиторий Zabbix
Документация
Исключите пакеты Zabbix поставляемые в репозитории EPEL, если он у Вас установлен. Отредактируйте файл /etc/yum.repos.d/epel.repo и добавте следующую директиву.

[epel]\
...\
excludepkgs=zabbix*\
Продолжите установку репозитория Zabbix.

 rpm -Uvh https://repo.zabbix.com/zabbix/7.2/release/alma/9/noarch/zabbix-release-latest-7.2.el9.noarch.rpm\
 
 dnf clean all\
b. Установите Zabbix сервер, веб-интерфейс и агент\
 dnf install zabbix-server-pgsql zabbix-web-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-selinux-policy zabbix-agent\
c. Создайте базу данных\
Документация\
Установите и запустите сервер базы данных.
Выполните следующие комманды на хосте, где будет распологаться база данных.

 sudo -u postgres createuser --pwprompt zabbix\
 sudo -u postgres createdb -O zabbix zabbix\
На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.

 zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix\


     Установка PostgreSQL:
   ```bash
   sudo apt update
   sudo apt install postgresql postgresql-contrib

    Создание базы данных и пользователя:

    sudo -u postgres createuser --pwprompt zabbix
    sudo -u postgres createdb -O zabbix zabbix

    Настройка репозитория Zabbix:

    wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-1+debian11_all.deb
    sudo dpkg -i zabbix-release_6.0-1+debian11_all.deb
    sudo apt update

    Установка Zabbix Server и веб-интерфейса:

    sudo apt install zabbix-server-pgsql zabbix-frontend-php zabbix-apache-conf

    Импортирование схемы базы данных Zabbix:

    sudo -u zabbix zcat /usr/share/doc/zabbix-server-pgsql/schema.sql.gz | psql -U zabbix -d zabbix
    sudo -u zabbix zcat /usr/share/doc/zabbix-server-pgsql/images.sql.gz | psql -U zabbix -d zabbix
    sudo -u zabbix zcat /usr/share/doc/zabbix-server-pgsql/data.sql.gz | psql -U zabbix -d zabbix

    Настройка Zabbix Server:

    sudo nano /etc/zabbix/zabbix_server.conf

    Установка необходимых PHP модулей:

    sudo apt install php php-pgsql libapache2-mod-php php-mbstring php-gd php-xml php-bcmath php-ldap

    Запуск Zabbix Server:

    sudo systemctl start zabbix-server
    sudo systemctl enable zabbix-server

