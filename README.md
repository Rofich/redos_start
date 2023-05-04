https://stackoverflow.com/questions/8087184/installing-python-3-on-rhel
https://habr.com/ru/articles/501414/
https://habr.com/ru/companies/nixys/articles/723082/

<h2 align="center"> ----- Postgresql 13 -----  </h2>

Установка для РЕД ОС 7.3 осуществляется командой:

` dnf install postgresql13-server `

Настройка postgresql:

` postgresql-13-setup initdb `

Запуск сервера PostgreSQL:

` systemctl enable --now postgresql-13 `

##
