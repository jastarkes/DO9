## 1. Получение метрик и логов

Для начала копируем swarm файл из проекта DevOps 7.
Добавляем в него сервисы мониторинга Prometheus, Loki, node_exporter, blackbox_exporter, cAdvisor, Grafana.

![alt text](src/screens/1.png "str")

Создаем структуру папок мониторинга и yml файлы.

![alt text](src/screens/2.png "str1")
![alt text](src/screens/3.png "str2")

Добавляем в pom-файл каждого сервиса зависимости micrometer и actuator, а в файлы app.properties добавляем метрики с эндпоинтами.

![alt text](src/screens/4.png "str3")

Собираем образы через докер-композ и запускаем.

![alt text](src/screens/5.png "str4")

Добавленные с помощью Micrometer метрики выводим в Prometheus.

![alt text](src/screens/6.png "str5")

В app.prop каждого сервиса добавляем настройки логирования.

![alt text](src/screens/7.png "str6")

В Grafana добавлены логи приложения с помощью Loki.
Далее начинаем создавать Docker Swarm стэк.

![alt text](src/screens/8.png "str7")

Разворачиваем стэк мониторинга и проверяем статус стэка и сервисов.

![alt text](src/screens/9.png "str8")

Видим, что в prometheus подключены сервисы мониторнига.

![alt text](src/screens/10.png "str9")

Метрики получаются корректно.

## 2. Визуализация

![alt text](src/screens/11.png "str10")

Добавил все нужные метрики. Пришлось объединить оба композ файла в одну сеть для корректной интеграции метрик.

## 3. Отслеживание критических событий

Для начала добавляем AlertManager в docker-compose.swarm.yml, создаем файл конфигурации и правила алертов.

![alt text](src/screens/12.png "str11")

Сайт alertmanager работает и видит конфиг.

![alt text](src/screens/13.png "str12")

Prometheus на связи.

![alt text](src/screens/14.png "str13")

Оповещения в тг-бот.