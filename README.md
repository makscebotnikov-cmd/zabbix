# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Чеботников М.Б.`

## Задание 1

Установите Zabbix Server с веб-интерфейсом.  
Процесс выполнения  
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.  
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.  
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.  
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.  
Требования к результаты  
Прикрепите в файл README.md скриншот авторизации в админке.  
Приложите в файл README.md текст использованных команд в GitHub.  
## Решение 1

```
sudo apt install postgresql
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bdebian11_all.deb 
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
sudo apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts nano -y
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
sudo zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf
sudo systemctl restart zabbix-server apache2
sudo systemctl enable zabbix-server apache2
sed -i 's/# DBPassword=/DBPassword=****/g' /etc/zabbix/zabbix_server.conf<img width="1280" height="800" alt="11" src="https://github.com/user-attachments/assets/26c36e44-13b1-4e82-947a-b0be1f126797" />

```
![Снимок 11]<img width="1280" height="800" alt="11" src="https://github.com/user-attachments/assets/7347b057-f682-43a7-9f17-74ef82966a63" />



## Задание 2  
Установите Zabbix Agent на два хоста.  
Процесс выполнения  
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.  
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.  
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.  
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.  
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.  
Требования к результаты  
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу  
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером  
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.  
Приложите в файл README.md текст использованных команд в GitHub  

## Решение 2

```
sudo -s
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
apt update
apt install zabbix-agent
systemctl restart zabbix-agent
systemctl enable zabbix-agent

```


![Снимок 211](https://github.com/user-attachments/assets/6892d059-7316-4b90-baf9-fb82adb8add5)

![Снимок 210](https://github.com/user-attachments/assets/7c6d7801-d789-447f-8f1b-0a4c394b5225)

![Снимок 212](https://github.com/user-attachments/assets/1b801554-fe8d-43d5-9338-13bf4b6f1c52)
