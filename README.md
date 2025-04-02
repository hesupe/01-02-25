![image](https://github.com/user-attachments/assets/224a3a2f-3c4c-4055-905a-78423f0c6203)


Установил линукс на oraclebox. поставил 4гб оперативной памяти и 4 процессора.

Установил гостевые дополнения

![image](https://github.com/user-attachments/assets/986e6ac4-0075-4f86-a5c5-328a47e05a11)

Первым шагом была установка Wget — инструмента, необходимого для загрузки файлов напрямую через терминал. Это удобно для быстрого получения данных без использования графического интерфейса.

`sudo yum install wget`

![image](https://github.com/user-attachments/assets/eacdf3a0-eb42-42f9-861a-cc57e12aea48)

Далее был установлен Curl — утилита для работы с различными сетевыми протоколами (HTTP, HTTPS, FTP и др.), что особенно полезно для тестирования API или загрузки данных.

`sudo yum install curl`

![image](https://github.com/user-attachments/assets/d353160c-2dd6-47c8-b5aa-3f0d35e819d7)

Для установки Docker потребовалось добавить его официальный репозиторий. Поскольку Oracle Linux основан на CentOS, был использован репозиторий для CentOS.

`sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

![image](https://github.com/user-attachments/assets/a655e55a-e196-4191-bb68-0e56e8ced114)

После этого была выполнена установка основных компонентов Docker: docker-ce, docker-ce-cli и containerd.io.

`sudo yum install docker-ce docker-ce-cli containerd.io`

![image](https://github.com/user-attachments/assets/a5b084eb-89b1-4f3e-9f81-5c40dd0bee5d)
![image](https://github.com/user-attachments/assets/1f8253e3-9d35-4d6c-9d44-d16ae3019d53)

Для автоматического запуска Docker при старте системы была выполнена команда:

`sudo systemctl enable docker --now`

![![image](https://github.com/user-attachments/assets/39762f9a-8450-4429-92e9-13d1a44ddd02)

Установка Docker Compose

Для управления несколькими контейнерами был установлен Docker Compose. Сначала была определена последняя версия через API GitHub:

`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

![image](https://github.com/user-attachments/assets/bd0dc96d-abd6-4b4c-93a7-80cc21e9bcc4)

Затем Docker Compose был загружен и установлен:

`sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

![image](https://github.com/user-attachments/assets/04c1088d-7bc4-4ffc-8935-fe1b09007aa5)

После установки были настроены права на выполнение файла Docker Compose и проверена его версия:

`sudo chmod +x /usr/bin/docker-compose docker-compose --version`

![image](https://github.com/user-attachments/assets/e9110c9f-7a03-44b8-8240-3ce2f6ce19c6)

Права на файл были проверены командой:

`ls -l /usr/bin/docker-compose`

![image](https://github.com/user-attachments/assets/f44de82c-44b2-4212-ae49-d1ec479267c8)

Файл получил права -rwxr-xr-x, что означает возможность чтения, записи и выполнения.

Для настройки системы мониторинга была установлена Grafana. Сначала был установлен Git, так как он отсутствовал в системе:

`git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/f133af13-e81f-4375-bffb-bb835e853038)

Затем был клонирован репозиторий и настроена структура каталогов:

`cd grafana_stack_for_docker`
`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`
`sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`
Для обеспечения корректных прав доступа владелец созданных папок был изменён на текущего пользователя:

`sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`
Был создан конфигурационный файл grafana.ini, если он отсутствовал:

`touch /mnt/common_volume/grafana/grafana-config/grafana.ini`
Файлы конфигурации были скопированы в соответствующую директорию:

`cp config/* /mnt/common_volume/swarm/grafana/config/`
Файл grafana.yaml был переименован в docker-compose.yaml для использования Docker Compose:

`mv grafana.yaml docker-compose.yaml`

Запуск контейнеров был выполнен в фоновом режиме:

`sudo docker compose up -d`


все команды
![image](https://github.com/user-attachments/assets/c8ec3bb5-9f1d-40fb-b83a-0664159d4461)

установка
![image](https://github.com/user-attachments/assets/c81fe24a-3111-4919-8c01-f730f99b2de6)

работа

![image](https://github.com/user-attachments/assets/85630126-0d5f-4a0d-a93d-3ba8774349ba)

Для остановки контейнеров использовалась команда:

`sudo docker compose stop`

![image](https://github.com/user-attachments/assets/38fc2417-9e2c-42b5-82c1-b945faf2161c)

Для полной очистки проекта, включая остановку и удаление контейнеров, сетей и других ресурсов, использовалась команда:

`sudo docker compose down`

![image](https://github.com/user-attachments/assets/f39435c1-5203-4b69-bdd6-f613118b300e)

Для проверки состояния контейнеров использовалась команда:


`sudo docker compose ps`

![image](https://github.com/user-attachments/assets/7d1c13c0-749a-4ad8-b11a-54e7f8fb7c93)


Клонирование репозитория Grafana

Для работы с проектом Grafana был клонирован репозиторий с GitHub:

`git clone https://github.com/ROMABLUNT/grafana_college.git`

![image](https://github.com/user-attachments/assets/10945b47-9bf3-4901-a412-ae40cc11c031)

pwd, показывает текущую директорию

![image](https://github.com/user-attachments/assets/87cccbea-0113-4fe1-b350-f7b13ec6b382)

Настройка Prometheus и Node Exporter
Были настроены конфигурационные файлы для Node Exporter и Prometheus, добавлены данные из репозитория разработчика.

`sudo vi docker-compose.yaml` Добавляю node exporter

![image](https://github.com/user-attachments/assets/9c680ae2-f77a-48ae-9675-5da2111d23bf)
![image](https://github.com/user-attachments/assets/d5e5e488-1efc-43a6-a448-7ba54f45be5b)

`sudo vi prometheus.yaml` добавляю  "exporter:9100"

![image](https://github.com/user-attachments/assets/bd289172-1ab0-43b7-bbe1-4fcb5e3eafe0)
![image](https://github.com/user-attachments/assets/d3fa7137-b72d-4ce9-bad7-7e4c52af8046)

В итоге по localhost:3000 попадаю на графану

![image](https://github.com/user-attachments/assets/c0b13726-fcf7-4c47-941f-f30ca0a5617b)


Создание Dashboard и визуализаций
![image](https://github.com/user-attachments/assets/4c16da06-2ed3-44db-9bb0-fe7b18c982a1)

![image](https://github.com/user-attachments/assets/6a24d4d4-6546-454a-9796-5d4df3359eed)

![image](https://github.com/user-attachments/assets/ddb8ff8a-2ebd-4e96-b1ed-995a2e18e188)

![image](https://github.com/user-attachments/assets/2bad764f-d863-4687-9518-addf217bd77a)

![image](https://github.com/user-attachments/assets/0c38c8fa-3857-486c-bdb6-dba5017605bb)

![image](https://github.com/user-attachments/assets/210fd384-8789-4160-8b85-d3e8b389f2f1)

![image](https://github.com/user-attachments/assets/7090a661-c282-4788-ada5-28d85461a842)

![image](https://github.com/user-attachments/assets/87d5d79d-63db-49d9-8e05-5841c873fac5)


Был создан Dashboard в Grafana, добавлены визуализации и настроен источник данных Prometheus. URL Prometheus был указан, аутентификация установлена (логин: admin, пароль: admin). После сохранения настроек была выполнена проверка работоспособности.


Результат работы был успешно отображён в интерфейсе Grafana.

![image](https://github.com/user-attachments/assets/75ff6834-3315-4e60-b88f-fea246d442e5)

VICTORIA METRICS

Заполняю новый коннекшн

![image](https://github.com/user-attachments/assets/b4e46c98-1ff4-490f-a31e-3958576f2967)

Ставлю код и параметр запроса 

![image](https://github.com/user-attachments/assets/5c79a32b-2edf-4594-872e-b5a59ba48fcd)

Ввожу в терминал две команды

![image](https://github.com/user-attachments/assets/4b8ccd08-fec0-483b-8aa8-2304663c56a5)

`echo -e "# TYPE OILCOINT_metric1 gauge\nOILCOINT_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus`  

`curl -G 'http://localhost:8428/api/v1/query' --data-urlencode 'query=OILCOINT_metric1'`

Всё окей

Результат в графане

![image](https://github.com/user-attachments/assets/21481a3f-fa64-4d46-ba26-da2359941329)

В виктории метрикс
![image](https://github.com/user-attachments/assets/acb1b950-9e71-4ef8-a934-e622a6f8fd3a)

