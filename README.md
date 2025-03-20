![image](https://github.com/user-attachments/assets/7227bcea-9c7e-40b0-a766-a47f1fdc95f2)![image](https://github.com/user-attachments/assets/8a9873b7-872a-4e24-848d-c4e3a9b49ec1)


Установил линукс на oraclebox. поставил 4гб оперативной памяти и 4 процессора.

Установил гостевые дополнения

![image](https://github.com/user-attachments/assets/986e6ac4-0075-4f86-a5c5-328a47e05a11)

wget

![image](https://github.com/user-attachments/assets/eacdf3a0-eb42-42f9-861a-cc57e12aea48)

curl

![image](https://github.com/user-attachments/assets/d353160c-2dd6-47c8-b5aa-3f0d35e819d7)

sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

![image](https://github.com/user-attachments/assets/a655e55a-e196-4191-bb68-0e56e8ced114)

sudo yum install docker-ce docker-ce-cli containerd.io

![image](https://github.com/user-attachments/assets/a5b084eb-89b1-4f3e-9f81-5c40dd0bee5d)
![image](https://github.com/user-attachments/assets/1f8253e3-9d35-4d6c-9d44-d16ae3019d53)

sudo systemctl enable docker --now

![![image](https://github.com/user-attachments/assets/39762f9a-8450-4429-92e9-13d1a44ddd02)

COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)

![image](https://github.com/user-attachments/assets/bd0dc96d-abd6-4b4c-93a7-80cc21e9bcc4)

sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose

![image](https://github.com/user-attachments/assets/04c1088d-7bc4-4ffc-8935-fe1b09007aa5)

sudo chmod +x /usr/bin/docker-compose docker-compose --version

![image](https://github.com/user-attachments/assets/e9110c9f-7a03-44b8-8240-3ce2f6ce19c6)

ls -l /usr/bin/docker-compose

![image](https://github.com/user-attachments/assets/f44de82c-44b2-4212-ae49-d1ec479267c8)

git clone https://github.com/skl256/grafana_stack_for_docker.git

![image](https://github.com/user-attachments/assets/f133af13-e81f-4375-bffb-bb835e853038)


все команды
![image](https://github.com/user-attachments/assets/c8ec3bb5-9f1d-40fb-b83a-0664159d4461)

установка
![image](https://github.com/user-attachments/assets/c81fe24a-3111-4919-8c01-f730f99b2de6)

работа

![image](https://github.com/user-attachments/assets/85630126-0d5f-4a0d-a93d-3ba8774349ba)

sudo docker compose stop

![image](https://github.com/user-attachments/assets/38fc2417-9e2c-42b5-82c1-b945faf2161c)

sudo docker compose down

![image](https://github.com/user-attachments/assets/f39435c1-5203-4b69-bdd6-f613118b300e)

