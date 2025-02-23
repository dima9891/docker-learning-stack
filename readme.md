# Docker сборка для запуска учебных проектов

Эта сборка предназначена для работы с учебными проектами на PHP. Она сделана максимально просто для того чтобы можно было изучить и понять каждый файл и доработать в соответствии со своими нуждами.

Как устроена сборка:
- сервис php обрабатывает php код который лежит в папке app/public этого проекта. Для примера туда уже помещен тестовый файл.
- сервис nginx делает запросы к php и отдает результат на 80 порту, то есть в браузере все будет открываться по адресу http://localhost/

## Как запустить

1. Обязательно установить на компьютер программу docker (https://www.docker.com/products/docker-desktop/). Если у вас linux, то лучше не ставить Docker Desktop, а поставить только командные утилиты - это будет гораздо полезнее для будущего изучения докера.

Убедиться что докер на компьютере есть и установлен можно например командой ``docker -v`` - она выведет верcию программы в консоль.

2. В папке проекта есть файл .env.example - нужно его скопировать и переименовать копию в .env
В этом файле хранятся переменные окружения, пока она только одна - название проекта, PROJECT_NAME. Можете оставить как есть или переименовать по своему вкусу (в названии не должно быть пробелов и символы только английского алфавита)

3. В консоли вводим команду (чтобы все сработало вы должны находиться в корневой папке проекта)

```
docker compose up -d
```

Докер должен скачать нужные образы, применить к ним нужные настройки и запустить сервисы. Если все прошло без ошибок - в браузере должна открыться страница index.php из папки app/public по адресу http://localhost/

Флаг -d в команда означает что после завершения команды вы не будете получать в командной строке вывод этих контейнеров (разные сообщения, логи и так далее). Если вы запустите без этого флага чтобы все остановить нажмите Ctrl-C

## Как подключиться к Xdebug

Если у вас VSCode, то он должен подхватить настройки из файла .vscode/launch.json
Все что требуется - открыть какой-то php файл из папки app/public на редактирование, затем перейти слева на вкладку Run and Debug в VSCode и наверху выбрать в выпадающем списке рядом с кнопкой - "Listen to Xdebug"

Запускаем дебаггер и он начнет слушать сервис php на порту 9003. Можно поставить в php-файле какую-то точку останова и перезагрузить страницу в браузере - выполнение кода должно на точке остановиться и VSCode отобразит всю отладочную информацию.

## Как запустить собственные php файлы?

Все файлы которые вы будете помещать в папку app/public будут доступны из браузера.
Допустим, вы можете создать в папке app/public папку lesson-1 и в ней test.php
Теперь этот файл откроется по адресу http://localhost/lesson-1/test.php

Вы можете помещать внутрь папки app/public любое количество своих учебынх проектов, открывать их по имени папки и имени файла. 

## Как остановить и пересобрать docker образы?

Если нужно все выключить и остановить сервисы

```
docker compose down
```

Если вы поменяли что-то в docker-compose файле или в файлах конфигурации или в Dockerfile можно пересобрать образы командой

```
docker compose up -d --build
```
