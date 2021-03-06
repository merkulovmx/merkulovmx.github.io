---
layout: post
title: Как подключиться к станции Avaya.
date: Tue Sep 5 12:12:41 2017 +0200
author: merkulov
tags:
- avaya 
- telephony
comments: true
---
### Как подключиться к станции Avaya

Avaya - это телефонная станция. (рассматриваем Definity, начинаю также как и со станцией Nortel Meridian)

Для удаленного подключения к ней, необходимо знать IP-адрес станции. 

Чтобы подключиться будем использовать программу [Avaya Site Administration](https://yadi.sk/d/cAzxZm0r3McHxb)

Скачаем архив. Установим. Обновим. Запускаем ASA. 

1. Нажимаем New Voice System. Мануал для повышения знаний [Avaya manual](https://yadi.sk/i/xBx0kNpO3McHfE)
2. Вводим название сессии и прочее, что попросят. 
Предположим, что к станции есть удаленный доступ и будем использовать удаленное подключение по IP)
3. Всяко всё введенное можно изменить затем в System -> Properties
  - Логин, Пароль, повтор пароля (рис. 1)
  
  ![an image alt text](http://merkulovmx.github.io/images/5image1.jpg "рис. 1")
  
  - IP-адрес и порт (рис. 2)
  
  ![an image alt text](http://merkulovmx.github.io/images/5image2.jpg "рис. 2")
  
*Подключение создано.*

Для запуска подключения, нажимаем Start GEDI. 

*Этот режим имеет пользовательский интерфейс, но также существует режим консоли (вызывается Ctrl+E).*
*Например, в консоли можно проводить трассировку.*

Видим дружелюбное окно программы  (рис. 3)
1. Командная строка - в ней и вводятся все команды.
2. Вкладка Tree показывает дерево подключений, а также команды, которые можно вызывать.
3. Список комманд.
4. Отключиться от станции.
![an image alt text](http://merkulovmx.github.io/images/5image3.jpg "рис. 3")
*Следует помнить, что до завершения работы со станцией лучше сохранить изменения.*
*Иначе скачек напряжения или экстренный перезапуск станции уничтожит все изменения.*

1. Сохранить изменения на станции
{% highlight javascript %}
save translation
{% endhighlight %}{: .highlight-left }

#### Проверить привязан ли местный номер к городскому
### 1. Вывести таблицу городской к местному 
*Иногда в столбце пусто - если нет привязки к местному.*
*В зависимости от логики может и на группу местных номеров вести.* 
### Вывести таблицу городских номеров списком
{% highlight javascript %}
list ars digit-conversion (рис. 4)
{% endhighlight %}{: .highlight-left }

![an image alt text](http://merkulovmx.github.io/images/5image4.jpg "рис. 4")

1404526 - гор. номер
8060 - местный

### 2. Изменить настройки номера
{% highlight javascript %}
change station 8060 (рис. 5)
{% endhighlight %}{: .highlight-left }

1. Модель тел. аппарата. В данном случае аналог.
2. Порт. Где 5 - это ряд, 11 - номер порта
3. Имя пользователя тел. аппарата
4. Coverage Path - группы переадресации. В данном случае номер входит в две группы
5. COR, COS - ограничение для номера, например разрешен выход в город.

![an image alt text](http://merkulovmx.github.io/images/5image5.jpg "рис. 5")

*__Мысль в слух.__ "Круговорот телефонных станций в природе"* 
