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
![Снимок 12]<img width="1280" height="800" alt="12" src="https://github.com/user-attachments/assets/6ee9b1d5-043e-4f4f-9a58-3b106e525e29" />
![Снимок 13]<img width="1280" height="800" alt="13" src="https://github.com/user-attachments/assets/7b5d222f-dd78-44e1-b026-042eb4e2121b" />
![Снимок 14]<img width="1280" height="800" alt="14" src="https://github.com/user-attachments/assets/3008440c-0c02-4cf0-b60e-932140e45036" />
![Снимок 15]<img width="1280" height="722" alt="15" src="https://github.com/user-attachments/assets/39b2ab91-fa01-41c8-bcf0-74978c336b7f" />


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
swget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4%2Bdebian11_all.deb 
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
sudo apt install zabbix-agent -y
sudo systemctl restart zabbix-agent 
sudo systemctl enable zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf
sudo systemctl restart zabbix-agent
sed -i 's/Server=127.0.0.1/Server=192.168.0.138'/g' /etc/zabbix/zabbix_server.conf

```
![Снимок 21]<img width="1280" height="800" alt="21" src="https://github.com/user-attachments/assets/16eaa0d9-2fef-4f47-ad3d-ac9123db1468" />
![Снимок 22]<img width="1280" height="800" alt="22" src="https://github.com/user-attachments/assets/bf716b60-ecd9-43e3-91d1-70942e016679" />
![Снимок 23]<img width="1280" height="800" alt="23" src="https://github.com/user-attachments/assets/112ca692-f83e-4514-aaa1-dfb7a42958a0" />
![Снимок 24]<img width="1280" height="800" alt="24" src="https://github.com/user-attachments/assets/d851efaf-b58b-4986-a6f4-7d17145a04f6" />
![Снимок 25]<img width="1280" height="715" alt="25" src="https://github.com/user-attachments/assets/cf30feab-5dc1-405d-b8ea-c3a2534cea48" />
