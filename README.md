 Домашнее задание к занятию "`Очереди RabbitMQ`" - `Алексей Сидоров`
---

### Задание 1. Установка RabbitMQ

Используя Vagrant или VirtualBox, создайте виртуальную машину и установите RabbitMQ. Добавьте management plug-in и зайдите в веб-интерфейс.

`Cкриншот веб-интерфейса RabbitMQ:`

![img1](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img1.png)


---

### Задание 2. Отправка и получение сообщений

Используя приложенные скрипты, проведите тестовую отправку и получение сообщения. Для отправки сообщений необходимо запустить скрипт producer.py.

Для работы скриптов вам необходимо установить Python версии 3 и библиотеку Pika. Также в скриптах нужно указать IP-адрес машины, на которой запущен RabbitMQ, заменив localhost на нужный IP.
Зайдите в веб-интерфейс, найдите очередь под названием hello и сделайте скриншот. После чего запустите второй скрипт consumer.py и сделайте скриншот результата выполнения скрипта.

`Cкриншоты с результатом выполнения:`

![img2](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img2.png)

![img3](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img3.png)

---

### Задание 3. Подготовка HA кластера

Используя Vagrant или VirtualBox, создайте вторую виртуальную машину и установите RabbitMQ. Добавьте в файл hosts название и IP-адрес каждой машины, чтобы машины могли видеть друг друга по имени.
После этого ваши машины могут пинговаться по имени.
Затем объедините две машины в кластер и создайте политику ha-all на все очереди.
Также приложите вывод команды с двух нод:

```
$ rabbitmqctl cluster_status
```
Для закрепления материала снова запустите скрипт producer.py и приложите скриншот выполнения команды на каждой из нод:
```
$ rabbitmqadmin get queue='hello'
```
После чего попробуйте отключить одну из нод, желательно ту, к которой подключались из скрипта, затем поправьте параметры подключения в скрипте consumer.py на вторую ноду и запустите его.

`Cкриншот из веб-интерфейса RabbitMQ:`

![img5](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img5.png)

![img6](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img6.png)

`Cкриншот результата работы второго скрипта:`

![img7](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img7.png)

---

### Задание 4*. Ansible playbook.

Напишите плейбук, который будет производить установку RabbitMQ на любое количество нод и объединять их в кластер. При этом будет автоматически создавать политику ha-all.

`Ссылка на playbook:`

[playbook](https://github.com/PhartomX/netology_rabbitMQ/blob/main/playbook.yml)


---