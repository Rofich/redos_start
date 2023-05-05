https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax <br>

https://stackoverflow.com/questions/8087184/installing-python-3-on-rhel <br>
https://habr.com/ru/articles/501414/ <br>
https://habr.com/ru/companies/nixys/articles/723082/ <br>

<h2 align="center"> ----- Python 3.11.3 ----- </h2>

1. Скачать на Python.org(Могут быть более новые версии)
   ` wget https://www.python.org/ftp/python/3.11.3/Python-3.11.3.tar.xz `
2. Распаковать
   ` tar xf Python-3.11.3 ` 
   ` cd Python-3.11.3 `
3. Подготовить компиляцию
   ` ./configure `
4. Строить
   ` make `
5. Установить
   ` make install `

<h2 align="center"> ----- Postgresql 13 -----  </h2>

Установка для РЕД ОС 7.3 осуществляется командой:

` dnf install postgresql13-server `

Настройка postgresql:

` postgresql-13-setup initdb `

Запуск сервера PostgreSQL:

` systemctl enable --now postgresql-13 `