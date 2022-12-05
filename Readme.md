# Краткое описание.
Мини задачи направлены на анализ совершенных покупок с помощью Python. В каждом файле можно посмотреть заметки для пояснений.

Во всех задачах используются одинаковые данные. В uniq_id_cust - таблица с уникальными идентификаторами пользователей, orders - уникальные идентификаторы заказов (номер чека), items - товарные позиции, входящие в заказы.

![image](https://user-images.githubusercontent.com/100629361/205740628-b6d5a735-3bff-4e70-8241-951f62956fd9.png)

# Задачи проекта

## Найти колличество пользователей, совершивших покупку 1 раз.

По результатам выявили 93 099 пользователей, которые совершили (любую) покупку один раз. Если учитывать только успешные (оплаченные) заказы, то число пользователей равняется 91 816.

## Найти среднее число заказов, которые не доставляются по разным причниам. Дополнительно детализировать причины.

Все возможные причины нарушения доставки.

![Причины недоставки](https://user-images.githubusercontent.com/100629361/205737139-5ab0b25b-1022-48f8-816b-6068bcc1fe7a.PNG)

После разбивки значений по месяцам получили следующую картину по средним значениям:

Статус------Среднее_знач

0	approved------1.000000

1	canceled------26.77778

2	created-------1.666667

3	invoiced------15.79167

4	processing----17.20833

5	shipped-------50.94444

6	unavailable---32.20833

Деталицация по причинам.

![Детализация причин](https://user-images.githubusercontent.com/100629361/205738048-642bd5ed-606f-45c8-8e0c-5e61af888d8f.PNG)

Больше всего недоставленных заказов в ноябре (среднее значение за 3 года = 255).
Самая частая причина отсутствия доставки - shipped (Заказ отгружен, но не доставлен).

## По каждому товару определить, в какой день недели товар чаще всего покупается.

Для ответа на этот вопрос объединили таблицы с заказами и продуктами. В результирующую таблицу не включали данные по недоступным и неоплаченным заказам.

На выходе получили таблицу с данными о продажах каждого товара с детализацией по дням недели.

![image](https://user-images.githubusercontent.com/100629361/205740378-a457c175-258a-4c86-95e4-f775b5ed06e0.png)

## Определить среднее число покупок в неделю по каждому пользователю.

В данной задаче не использовали заказы со статусами: создан, выставлен счет (неоплачен), недоступен и отменен.

Значение покупок с разбивкой по месяцам - в таблице: right_orders, столбец orders_by_week

![image](https://user-images.githubusercontent.com/100629361/205741349-75509a1f-f8de-4187-ac1c-4b47f771c129.png)

Среднее значение покупок по каждому пользователю - в таблице: right_orders_weeks,стоблец count_by_week

![image](https://user-images.githubusercontent.com/100629361/205741405-614d3cd5-fa9e-40e4-9c06-4363241583b7.png)


## Провести когортный анализ пользователей. В период с января по декабрь выявить когорту с самым высоким retention на 3й месяц.

Для решения данной задачи выявили первый и последний месяц и на их основе отобрали заказчиков, которые совершали покупки в течении трех первых месяцев с момента их первой покупки.

![image](https://user-images.githubusercontent.com/100629361/205742112-f29e2a66-a221-45b5-aa7a-4152283c8013.png)

В результате, месяцем с наибольшим Retention оказался май.

## Построить RFM-сегментацию пользователей для качественной оценки аудитории. В кластеризации использовать следующие метрики: R - время от последней покупки пользователя до текущей даты, F - суммарное количество покупок у пользователя за всё время, M - сумма покупок за всё время. Для каждого RFM-сегмента построить границы метрик recency, frequency и monetary для интерпретации этих кластеров.

Рассматривали только 2017 год, так как он единственный является полным.

Для подсчета Frequency - посчитали колличество покупок по каждому покупателю

Для подсчета Monetary - сумму свех чеков каждого пользователя.

Для подсчета Recency - посчитали кол-во дней между текущим временем и последней покупкой пользователя.

Так как большинство пользователей делали покупку только 1 раз, то при использовании квантилей мы наблюдаем сильный перекос Frequency, поэтому можем сделать вывод, что данный показатель не будет особо репрезентативным.

По итогу получаем следующую таблицу:

![image](https://user-images.githubusercontent.com/100629361/205749251-8b1b0a98-8779-4d7d-bdd7-2c00568ca786.png)

Всего получили 49 сегментов. Информация о границах сегментации подробно расписана в файле (https://github.com/AlenaLes/Simple_analysis/blob/main/First_project_6.ipynb).
