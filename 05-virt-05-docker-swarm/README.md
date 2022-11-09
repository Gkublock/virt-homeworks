# Домашнее задание к занятию "5. Оркестрация кластером Docker контейнеров на примере Docker Swarm"

## Как сдавать задания

Обязательными к выполнению являются задачи без указания звездочки. Их выполнение необходимо для получения зачета и диплома о профессиональной переподготовке.

Задачи со звездочкой (*) являются дополнительными задачами и/или задачами повышенной сложности. Они не являются обязательными к выполнению, но помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---


## Важно!

Перед отправкой работы на проверку удаляйте неиспользуемые ресурсы.
Это важно для того, чтоб предупредить неконтролируемый расход средств, полученных в результате использования промокода.

Подробные рекомендации [здесь](https://github.com/netology-code/virt-homeworks/blob/virt-11/r/README.md)

---

## Задача 1

Дайте письменые ответы на следующие вопросы:

- В чём отличие режимов работы сервисов в Docker Swarm кластере: replication и global?
global означает, что сервис будет запущен ровно в одном экземпляре на всех возможных нодах. А replicated означает, что n-ое кол-во контейнеров для данного сервиса будет запущено на всех доступных нодах.
- Какой алгоритм выбора лидера используется в Docker Swarm кластере?
RAFT - ноды делают запрос на лидерство: первый ответивший им становится. Далее они опрашивают друг друга на предмет доступнгости лидера и если лидер перестает отвечать, назначается новый
- Что такое Overlay Network?
Дословно, сеть, построенная поверх другой. Позволяет общаться контейнерам в рамках кластера между собой, даже если они на разных нодах. Маршрутизацией занимается docker engine

## Задача 2

Создать ваш первый Docker Swarm кластер в Яндекс.Облаке

Для получения зачета, вам необходимо предоставить скриншот из терминала (консоли), с выводом команды:
```
docker node ls
```
[root@node01 ~]# docker node ls
ID                            HOSTNAME             STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION
9tt9cwtuan42iq9jy173afjlu *   node01.netology.yc   Ready     Active         Leader           20.10.21
z5y3u4v9m6cwtp3nqy7h7fv2f     node02.netology.yc   Ready     Active         Reachable        20.10.21
slkjp7ppc38z0cr4o8f1iy1s4     node03.netology.yc   Ready     Active         Reachable        20.10.21
ezea1f6dcadm9brcz46j22cdj     node04.netology.yc   Ready     Active                          20.10.21
dmg2sxic9vsy8grh3bshao516     node05.netology.yc   Ready     Active                          20.10.21
rpaebxbhbt5p8f266f3c9u7ii     node06.netology.yc   Ready     Active                          20.10.21

## Задача 3

Создать ваш первый, готовый к боевой эксплуатации кластер мониторинга, состоящий из стека микросервисов.

Для получения зачета, вам необходимо предоставить скриншот из терминала (консоли), с выводом команды:
```
docker service ls
```
[root@node01 ~]# docker service ls
ID             NAME                          MODE         REPLICAS   IMAGE                                          PORTS
yrf8509wi9f6   monitoring_alertmanager       replicated   1/1        stefanprodan/swarmprom-alertmanager:v0.14.0    
nfx0cz6hu8dm   monitoring_caddy              replicated   1/1        stefanprodan/caddy:latest                      *:3000->3000/tcp, *:9090->9090/tcp, *:9093-9094->9093-9094/tcp
elsapfljd1y7   monitoring_cadvisor           global       6/6        google/cadvisor:latest                         
o8s357gcqlzj   monitoring_dockerd-exporter   global       6/6        stefanprodan/caddy:latest                      
vq7elz41wsxj   monitoring_grafana            replicated   1/1        stefanprodan/swarmprom-grafana:5.3.4           
zewawzqwmr0c   monitoring_node-exporter      global       5/6        stefanprodan/swarmprom-node-exporter:v0.16.0   
d3wnjj0er8ep   monitoring_prometheus         replicated   0/1        stefanprodan/swarmprom-prometheus:v2.5.0       
0m8w8awopm69   monitoring_unsee              replicated   1/1        cloudflare/unsee:v0.8.0     
## Задача 4 (*)

Выполнить на лидере Docker Swarm кластера команду (указанную ниже) и дать письменное описание её функционала, что она делает и зачем она нужна:
```
# см.документацию: https://docs.docker.com/engine/swarm/swarm_manager_locking/
docker swarm update --autolock=true
```

