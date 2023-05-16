<h2 align="center"> ----- Apache ----- </h2>

` su `

` dnf update `

` echo 'SELINUX=disabled' > /etc/sysconfig/selinux `

` reboot `
<hr>
После перезагрузки:

` su `

` dnf install httpd httpd-devel php81-release `

` dnf clean all  `

` dnf makecache `

` dnf update php*  `

` dnf install php php-common php-cli  `
<hr>

` systemctl enable --now httpd `

` cd /home/ваш-пользователь `

` mkdir www `

` cd www `

` mkdir название-сайта `

` cd название-сайта `

` nano index.php `

Внутри пишем:

``` 
<?php
   phpinfo();
?>
```

Сохраняем(Ctrl+O)

Выходим(Ctrl+X)

` chown -R ваш-пользователь:apache /home/ваш-пользователь/www `

` chmod 775 /home /home/ваш-пользователь /home/ваш-пользователь/www `

В /etc/httpd/conf/httpd.conf находим строку :

` DocumentRoot "/var/www/html"  `

И меняем на: 

` DocumentRoot "/home/ваш-пользователь/www/название-сайта" `

Меняем ` <Directory "/var/www"> ` на ` <Directory "/home/ваш-пользователь/www"> `

Меняем ` <Directory "/var/www/html"> ` на ` <Directory "/home/ваш-пользователь/www/название-сайта"> `

Сохраняем всё 

Перезапускаем Apache

` systemctl restart httpd `

Заходим по адресу: http://localhost

<h2 align="center"> ----- MySQL ----- </h2>

` su ` 

` dnf install mysql mariadb-server phpmyadmin `

` systemctl enable --now mariadb `

` mysql_secure_installation `
## После этого надо будет настроить 

- У вас потребует ввести пароль, нажмите Enter
- На вопрос "Switch to unix_socket authentication", напишите в консоль Y и нажмите Enter
- На вопрос "Change the root password", напишите в консоль Y и нажмите Enter
- Введите новый пароль
- Повторите пароль
- На вопрос "Remove anonymous users", напишите в консоль Y и нажмите Enter 
- "Disallow root login remotely?", отвечаем Y и жмем Enter
- "Remove test database and access to it?", отвечаем Y и жмем Enter
- "Reload privelege tables now?", отвечаем Y и жмем Enter

Переходим к файлу конфигурации phpmyadmin 

` nano /etc/httpd/conf.d/phpMyAdmin.conf `

Находим там строку ` <Directory /usr/share/phpMyAdmin/ `

Внутри меняем строку ` Require local ` на  ` Require all granted `

Сохраняем(` Ctrl+O `) и выходим(` Ctrl+X `)

Перезапускаем Apache 

` systemctl restart httpd `

phpmyadmin Доступен по адресу "http://localhost/phpmyadmin"

<h2 align="center"> ----- Python 3.11.3 ----- </h2>

1. Скачать на Python.org(Могут быть более новые версии)

   ` wget https://www.python.org/ftp/python/3.11.3/Python-3.11.3.tar.xz `
   
   ` dnf groupinstall 'Development Tools' `
   
   ` dnf install -y zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel zlib* libffi-devel readline-devel tk-devel gcc `
   
   ` dnf remove python3-pip `
2. Распаковать
   
   ` tar xf Python-3.11.3.tar.xz ` 

   ` cd Python-3.11.3 `
3. Подготовить компиляцию
   
   ` ./configure --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib" `
  
4. Забилдить
   
   ` make `
5. Установить
   
   ` make install `
   
6. ` python3.11 -V `

` dnf install python3-devel mysql-devel `
<h2 align="center"> ----- Postgresql 13 -----  </h2>

Установка для РЕД ОС 7.3 осуществляется командой:

` dnf install postgresql13-server pgadmin4 pgadmin4-qt `

Настройка postgresql:

` postgresql-13-setup initdb `

Запуск сервера PostgreSQL:

` systemctl enable --now postgresql-13 `

Настроим пароль:

1. ` su - postgres `
2.  ` psql `
3.  ` postgres `
4.  ` \password `
5.  Выход из оболочки ` \q `

Далее запускаем pgAdmin4 и добавляем сервер

1. Нажимаем кнопку ` win ` 
2. Переходим в Программирование->pgAdmin4
3. После запуска нажимаем "Reset Master Password" и вводим новый пароль
4. Подтверждаем и если потребуют ввести пароль вводим его
5. Далее нажимаем "Add New Server"
6. В поле Name пишем любое название
7. переходим на вкладку "Connection" и в поле "Host name/address" пишем localhost, и в поле "Password" вводим пароль котрый мы меняли в пункте 'Настроим пароль'
8. Нажимаем кнопку Save 
9. Всё, у вас появился сервер в pgAdmin4

<h2 align="center">-----Django-----</h2>

` dnf install python3-mod_wsgi `

Переходим в дерективу сайта и создаем виртуальное окружение 

` python3 -m venv .venv `

Активируем его 

` source .venv/bin/activate `

Устанавливаем все нужные модули

` pip3 install --upgrade pip django mod_wsgi mysqlclient `

Получаем путь к WSGI

` mod_wsgi_express module-config `

Копируем строку LoadModule...

Создаем django-проект

` django-admin startproject mysite . `

Изменяем файл wsgi.py

` cd mysite `
` nano wsgi.py `

Находим строку ` import os `, и добавляем ` import os,sys `

На следующей строке пишем:

` sys.path.append("/полный/до/папки/.venv") `

Сохраняем и выходим

Изменим файл конфигурации apache2

` cd /etc/httpd/conf `

` nano httpd.conf `

Удаляем строки 

` DocumentRoot... `

