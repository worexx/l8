# Лабораторная №8

## Задание 1 
##### Подготовка

1. Создайте папку 'chat'
2. В папкe 'chat' создайте папки 'tpl' и 'public'
3. В папке 'chat' создайте файл 'package.json' со следующим содержимым:

        {
            "name": "NodeChat",
            "version": "1.0.0",
            "description": "My first Node.js chat",
            "dependencies": {
                "socket.io": "latest",
                "express": "latest",
                "jade": "latest"
            },
            "author": "Ваше имя"
        }

4. В командной строке перейдите в директорию 'chat' и выполните команду 'npm install'
5. Дождитесь установки модулей и убедитесь, что в папке 'chat' появилась папка 'node_modules' с установленными модулями

## Задание 2
##### Создание HTML-шаблона JADE (jade-lang.com)

1. В текстовом редакторе создайте файл 'chat\tpl\page.jade'
2. В созданном файле напишите следующий текст:

        !!!
        html
        head
        title= "Node chat"
        body
        #content(style="width: 500px; height: 300px; margin: 0 0 20px 0; border: solid 1px #999; overflow-y: scroll;")
        form#form(action='', onsubmit='return false')
        input#field(style="width:350px;")
        input#send(type='submit', value='Послать')

3. Будьте аккуратны: используйте либо табуляцию, либо пробелы!!!
4. Сохраните файл 'page.jade'

## Задание 3
##### Создание сервера

1. В текстовом редакторе создайте файл 'chat\_index.js'
2. Подключите модуль 'express'
3. Создайте сервер (переменная 'app') на основе фреймворка 'express'
4. Произведите настройки сервера:
    - укажите, что файлы для представлений находятся в папке 'tpl'
    - укажите, что для представлений используется движок 'jade'
    - принициализируйте движок как: app.engine("jade", require("jade").__express);
    - укажите, что собираетесь использовать в качестве статической папки папку 'public'
5. Создайте для сервера обработчик метода 'get', который обрабатывает обращение к корню сервера
6. В обработчике осуществите рендеринг шаблона JADE используя метод 'render'
7. Подключите модуль 'socket.io' (переменная 'io') и поставьте его на прослушку порта '8080'
8. Создайте для сокета обработчик метода 'on', который обрабатывает событие 'connection'
9. Сохраните файл и запустите созданный сервер из командной строки.
10. Наберите в браузере 'http://localhost:8080' и убедитесь в корректной работе приложения

## Задание 4
##### Создание клиента

1. В текстовом редакторе создайте файл 'chat\public\chat.js'
2. В этом файле опишите событие 'window.onload', в котором:
    - создайте сокетное соединение к адресу 'http://localhost:8080'
    - создайте массив 'messages' для хранения сообщений приходящих с сервера
    - создайте для сокета обработчик метода 'on', который обрабатывает серверное сообщение 'message'
    - создайте обработчик события 'onclick' для html-элемента 'input' c 'id="submit"' (кнопка)
3. Обработчик кнопки должен: 
    - выбрать введённые пользователем данные из текстового поля
    - послать выбранные данные на сервер в сообщении под именем 'send'
4. Обработчик сокета должен:
    - принять сообщение сервера и сохранить его в массиве 'messages'
    - вывести содержимое массива 'messages' в html-элемент 'div'
5. Сохраните файл 'chat.js'

## Задание 5
##### Подключение скриптов в шаблоне страницы

1. Откройте в текстовом редакторе файл page.jade
2. После строки описывающей заголовок страницы допишите:

        script(src='/chat.js')
        script(src='/socket.io/socket.io.js')

3. Сохраните файл page.jade

## Задание 6
##### Обработка сообщений на сервере

1. Откройте в текстовом редакторе файл 'chat\_index.js'
2. В сокетном обработчике события 'connection' опишите следующий функционал:
    - послать клиенту сообщение 'message' с содержимым: { message: "Добро пожаловать в чат!" }
    - принять сообщение клиента 'send' и переслать его содержимое всем клиентам (сокетам) в виде сообщения 'message' с содержимым: { message: ТО-ЧТО-ПРИСЛАЛ-КЛИЕНТ }
3. Сохраните файл '_index.js'
4. Запустите сервер из консоли. 
5. Используя разные браузеры или разные вкладки браузера протестируйте чат
