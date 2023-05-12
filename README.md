<h2 align="center"> ----- Apache ----- </h2>

` su `

` dnf update `

` echo 'SELINUX=disabled' > /etc/sysconfig/selinux `

` reboot `
<hr>
После перезагрузки:

` su `

` dnf install httpd php81-release `

` dnf clean all  `

` dnf makecache `

` dnf update php*  `

` dnf install php php-cli php-common `
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

` dnf install mysql mariadb-server `

` systemctl enable --now mariadb `

` mysql_secure_installation `
## После этого надо будет настроить 

- У вас потребует ввести пароль, нажмите Enter
- На вопрос "Switch to unix_socket authentication", напишите в консоль Y и нажмите Enter
- На вопрос "Change the root password", напишите в консоль Y и нажмите Enter
- Введите новый пароль
- Повторите пароль
- На вопрос "Remove anonymous users", напишите в консоль Y и нажмите Enter 

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
   
   ` ./configure `
4. Забилдить
   
   ` make `
5. Установить
   
   ` make install `
   
6. ` python3.11 -V `

` dnf install python3-devel mysql-devel `
<h2 align="center"> ----- Postgresql 13 -----  </h2>

Установка для РЕД ОС 7.3 осуществляется командой:

` dnf install postgresql13-server `

Настройка postgresql:

` postgresql-13-setup initdb `

Запуск сервера PostgreSQL:

` systemctl enable --now postgresql-13 `
