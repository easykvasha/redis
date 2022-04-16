## redis
Information about redis db

# Формулировка задания.
1.	Сохранить большой JSON (~20МБ) в виде разных структур - строка, hset, zset, list;
2.	Протестировать скорость сохранения и чтения;
3.	Настроить редис кластер на 3х нодах с отказоустойчивостью, затюнить таймоуты.
4.	Предоставить отчет.

## Данные.
Я выбрал данные о перевозках пассажиров и багажа автомобильным и наземным электрическим транспортом. (data.json, размер порядка 30Мбайт, github не дает залить, могу отдельным файлом отправить)
Структура данных:
* "system_object_id":("STRING"),
* "CarrierName" ("STRING", Наименование юридического лица или индивидуального предпринимателя, осуществляющего перевозки пассажиров по маршруту"),
* "global_id" ("NUMBER"),
* "RouteNumber" ("STRING", "Номер маршрута"),
* "DirectRouteTrack" ("STRING", "Координаты прямого трека маршрута"),
* "ReverseTrackOfFollowing" ("STRING", "Трасса следования маршрута (обратное направление)"),
* "is_deleted" ("NUMBER"),
* "signature_date" ("STRING"),
* "ReverseRouteTrack" ("STRING", "Координаты обратного трека маршрута"),
* "TrackOfFollowing" ("STRING", "Трасса следования маршрута (прямое направление)"),
* "RouteName" ("STRING", "Наименование маршрута"),
* "ID" ("INTEGER", "Код"),
* "TypeOfTransport" ("DICTIONARY", "Вид транспорта").

# Выполнение.
1. Сохраним сначала в формате строки. Для это написал скрипт на python - [вставка строками](https://github.com/easykvasha/redis/blob/main/main.py)

Замеры времени показали следующий результат: ![Результат для строчек](https://github.com/easykvasha/redis/blob/main/string.png)

Также написан [код на чтение](https://github.com/easykvasha/redis/blob/main/load_string.py)

Замер времени на чтение для строки: ![Чтение строчек](https://github.com/easykvasha/redis/blob/main/string_load.png)

2. Теперь будет сохрание для сложной структуры (ключам были даны названия для простоты) был написан [следующий код](https://github.com/easykvasha/redis/blob/main/hset.py)

После замеров времени получили ![Результат для для других структур](https://github.com/easykvasha/redis/blob/main/hset.png)

Также написан [код на чтение](https://github.com/easykvasha/redis/blob/main/load_stucture.py)

Замер времени на чтение для структур: ![Чтение структур](https://github.com/easykvasha/redis/blob/main/hset_load.png)

===================
# Настройка redis кластера на 3-х нодах
