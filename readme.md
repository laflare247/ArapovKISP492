# Arapov

![image](https://github.com/laflare247/ArapovKISP492/blob/dfb23fda759c58f99ef4cd2813b9ef6c0e2545ce/photo_2025-02-01_20-09-24.jpg)

Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Иметь образ Linux
Выделить 2+ ядер.
Выделать 4096+ МБ оперативы.
При установки операционной системы, нужно будет выбрать английский язык.

Далее переходим к установке docker с использованием grafana, вводим следующий набор команд:

1. `sudo yum install wget`

• устанавливает утилиту wget на вашу систему
![image](https://raw.githubusercontent.com/laflare247/ArapovKISP492/fb767828df460776215537d4a184da6ca2063211/5233554041613708500.jpg)


2. `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

• Скачиваем файл репозитория
![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708511.jpg)

3. `sudo yum install docker-ce docker-ce-cli containerd.io`

• Устанавливаем docker
![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708515.jpg)

4. `sudo systemctl enable docker --now`

• Запускаем его и разрешаем автозапуск

5. `sudo yum install curl`

• Для этого сначала убедимся в наличие пакета curl

6. `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

• Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней
версии Docker Compose
![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708520.jpg)

7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`                        

• Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708524.jpg)

8. `sudo chmod +x /usr/bin/docker-compose`

• Предоставление прав на выполнение файла docker-compose.

9. `docker-compose --version`

• Проверка установленной версии Docker Compose.

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708526.jpg)

• Можно скачать git прямо из командной строки прописав Y

10. `git clone https://github.com/skl256/grafana_stack_for_docker.git`

• выдаст ошибку и предложит скачать git, согласиться и продолжить
![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708529.jpg)

11. `cd grafana_stack_for_docker`
    
• переход в папку

12.`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

13. `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`

• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

14. `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе

15.` touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

16. `cp config/* /mnt/common_volume/swarm/grafana/config/`

• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

17. `mv grafana.yaml docker-compose.yaml `

• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls

18.` sudo docker compose up -d`

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.
![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708535.jpg)

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708536.jpg)

19.` sudo vi docker-compose.yaml`

•команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя, что позволяет вам редактировать его содержимое.

• Нас перекинет в текстовый редактор

• Что-бы что-то изменить в тесковом редакторе нажмите insert на клавиатуре

• Что бы сохранить что-то в этом документе нажимаем Esc пишем :wq! В этом текставом редакторе мы должны поставить node-exporter после services

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708537.jpg)  

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708538.jpg)

20. `sudo vi prometheus.yaml `

• команда открывает файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя.

• /mnt/common_volume/swarm/grafana/config/prometheus.yaml - исправить targets: на exporter:9100,

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708541.jpg)
![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708542.jpg)

## Grafana

* переходим на сайт `localhost:3000`
    * User & Password GRAFANA: `admin`
    * Код графаны: `3000`
    * Код прометеуса: `http://prometheus:9090`
* в меню выбираем вкладку Dashboards и создаем Dashboard
    * ждем кнопку +Add visualization, а после "Configure a new data source"
    * выбираем Prometheus
    * Connection
    * `http://prometheus:9090`
* Authentication
    * Basic authentication
        * User: `admin`
        * Password: `admin`
        * Нажимаем на Save & test и должно показывать зелёную галочку
* в меню выбираем вкладку Dashboards и создаем Dashboard
    * ждем кнопку "Import dashboard"
    * Find and import dashboards for common applications at grafana.com/dashboards: 1860 //ждем кнопку Load
    * Select Prometheus ждем кнопку "Import"

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708544.jpg)

## VictoriaMetrics

Для начала изменим docker-compose.yaml

1. `cd grafana_stack_for_docker`

• команда cd grafana_stack_for_docker изменяет текущий рабочий каталог на каталог grafana_stack_for_docker.

2. `sudo vi docker-compose.yaml`

• команда sudo открывает файл docker-compose.yaml в редакторе vi с правами суперпользователя.

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708545.jpg)

В самом текстовом редакторе после prometheus вставляем

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708548.jpg)

Захом в connection
там где мы писали http//:prometheus:9090 пишем http:victoriametrics:9090 И заменяем имя из "Prometheus-2" в "Vika"
нажимаем на dashboards add visualition выбираем "Vika"
снизу меняем на "code"
Переходим в терминал и пишем

3. `echo -e "# TYPE OILCOINT_metric1 gauge\nOILCOINT_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus  `

• команда отправляет бинарные данные (например, метрики в формате Prometheus) на локальный сервер, который слушает на порту 8428.

4. `curl -G 'http://localhost:8428/api/v1/query' --data-urlencode 'query=OILCOINT_metric1'`

• команда делает запрос к API для получения данных по метрике OILCOINT_metric1

• команда выводит текст, который может быть использован для определения метрики в формате, совместимом с Prometheus

• команда выводит информацию о типе и значении этой метрики в формате, который может быть использован системой мониторинга Prometheus.

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708568.jpg)

Значение 0 меняем на любое другое

Копируем переменную OILCOINT_metric1 и вставляем в query

Нажимаем run

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708571.jpg)

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708572.jpg)

Копируем переменную OILCOINT_metric1 и вставляем в code

![image](https://github.com/laflare247/ArapovKISP492/blob/b32d2d494d0fc8c5c9dd471d40726e61b3dcc27e/5233554041613708576.jpg)
