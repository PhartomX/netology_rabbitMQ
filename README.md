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

![img4](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img4.png)

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

![img7](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img7.png)

`Вывод статуса кластера первой ноды:`

```
Cluster status of node rabbit@rabbitmq_one ...
Basics

Cluster name: rabbit@rabbitmq_one
Total CPU cores available cluster-wide: 4

Disk Nodes

rabbit@rabbitmq_one
rabbit@rabbitmq_two

Running Nodes

rabbit@rabbitmq_one
rabbit@rabbitmq_two

Versions

rabbit@rabbitmq_one: RabbitMQ 3.13.7 on Erlang 26.2.5.16
rabbit@rabbitmq_two: RabbitMQ 3.13.7 on Erlang 26.2.5.16

CPU Cores

Node: rabbit@rabbitmq_one, available CPU cores: 2
Node: rabbit@rabbitmq_two, available CPU cores: 2

Maintenance status

Node: rabbit@rabbitmq_one, status: not under maintenance
Node: rabbit@rabbitmq_two, status: not under maintenance

Alarms

(none)

Network Partitions

(none)

Listeners

Node: rabbit@rabbitmq_one, interface: [::], port: 15672, protocol: http, purpose: HTTP API
Node: rabbit@rabbitmq_one, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP
Node: rabbit@rabbitmq_one, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication
Node: rabbit@rabbitmq_one, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0
Node: rabbit@rabbitmq_two, interface: [::], port: 15672, protocol: http, purpose: HTTP API
Node: rabbit@rabbitmq_two, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP
Node: rabbit@rabbitmq_two, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication
Node: rabbit@rabbitmq_two, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0

Feature flags

Flag: classic_mirrored_queue_version, state: enabled
Flag: classic_queue_type_delivery_support, state: enabled
Flag: detailed_queues_endpoint, state: enabled
Flag: direct_exchange_routing_v2, state: enabled
Flag: drop_unroutable_metric, state: enabled
Flag: empty_basic_get_metric, state: enabled
Flag: feature_flags_v2, state: enabled
Flag: implicit_default_bindings, state: enabled
Flag: khepri_db, state: disabled
Flag: listener_records_in_ets, state: enabled
Flag: maintenance_mode_status, state: enabled
Flag: message_containers, state: enabled
Flag: message_containers_deaths_v2, state: enabled
Flag: quorum_queue, state: enabled
Flag: quorum_queue_non_voters, state: enabled
Flag: restart_streams, state: enabled
Flag: stream_filtering, state: enabled
Flag: stream_queue, state: enabled
Flag: stream_sac_coordinator_unblock_group, state: enabled
Flag: stream_single_active_consumer, state: enabled
Flag: stream_update_config_command, state: enabled
Flag: tracking_records_in_ets, state: enabled
Flag: user_limits, state: enabled
Flag: virtual_host_metadata, state: enabled
```

`Вывод статуса кластера второй ноды:`

```
Cluster status of node rabbit@rabbitmq_two ...
Basics

Cluster name: rabbit@rabbitmq_two
Total CPU cores available cluster-wide: 4

Disk Nodes

rabbit@rabbitmq_one
rabbit@rabbitmq_two

Running Nodes

rabbit@rabbitmq_one
rabbit@rabbitmq_two

Versions

rabbit@rabbitmq_two: RabbitMQ 3.13.7 on Erlang 26.2.5.16
rabbit@rabbitmq_one: RabbitMQ 3.13.7 on Erlang 26.2.5.16

CPU Cores

Node: rabbit@rabbitmq_two, available CPU cores: 2
Node: rabbit@rabbitmq_one, available CPU cores: 2

Maintenance status

Node: rabbit@rabbitmq_two, status: not under maintenance
Node: rabbit@rabbitmq_one, status: not under maintenance

Alarms

(none)

Network Partitions

(none)

Listeners

Node: rabbit@rabbitmq_two, interface: [::], port: 15672, protocol: http, purpose: HTTP API
Node: rabbit@rabbitmq_two, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP
Node: rabbit@rabbitmq_two, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication
Node: rabbit@rabbitmq_two, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0
Node: rabbit@rabbitmq_one, interface: [::], port: 15672, protocol: http, purpose: HTTP API
Node: rabbit@rabbitmq_one, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP
Node: rabbit@rabbitmq_one, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication
Node: rabbit@rabbitmq_one, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0

Feature flags

Flag: classic_mirrored_queue_version, state: enabled
Flag: classic_queue_type_delivery_support, state: enabled
Flag: detailed_queues_endpoint, state: enabled
Flag: direct_exchange_routing_v2, state: enabled
Flag: drop_unroutable_metric, state: enabled
Flag: empty_basic_get_metric, state: enabled
Flag: feature_flags_v2, state: enabled
Flag: implicit_default_bindings, state: enabled
Flag: khepri_db, state: disabled
Flag: listener_records_in_ets, state: enabled
Flag: maintenance_mode_status, state: enabled
Flag: message_containers, state: enabled
Flag: message_containers_deaths_v2, state: enabled
Flag: quorum_queue, state: enabled
Flag: quorum_queue_non_voters, state: enabled
Flag: restart_streams, state: enabled
Flag: stream_filtering, state: enabled
Flag: stream_queue, state: enabled
Flag: stream_sac_coordinator_unblock_group, state: enabled
Flag: stream_single_active_consumer, state: enabled
Flag: stream_update_config_command, state: enabled
Flag: tracking_records_in_ets, state: enabled
Flag: user_limits, state: enabled
Flag: virtual_host_metadata, state: enabled
```

`Вывод результата команды "rabbitmqadmin get queue='hello'" на нодах:`

![img8](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img8.png)
![img9](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img9.png)

`Проверка работоспособности кластера.`

`Запускаем скрипт для отправки сообщений:`

![img10](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img10.png)

`Останавливаем ноду, к которой подключались из скрипта:`

![img11](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img11.png)

`Правим параметры подключения в consumer.py и запускам скрипт:`

![img12](https://github.com/PhartomX/netology_rabbitMQ/blob/main/img/img12.png)

---

### Задание 4*. Ansible playbook.

Напишите плейбук, который будет производить установку RabbitMQ на любое количество нод и объединять их в кластер. При этом будет автоматически создавать политику ha-all.

`Ссылка на playbook:`

[playbook](https://github.com/PhartomX/netology_rabbitMQ/blob/main/playbook.yml)


---