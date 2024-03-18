# DockerSwarm

Задача 1:
Создаем конфигурацию файла с контейнерами
root@Roman-Linux:/home/ari# nano docker-compose.yml

 ![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/fb70bef9-26df-4b70-a62e-4bf6a78f1b27)

Запускаем:
root@Roman-Linux:/home/ari# docker compose up -d


![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/ba095e20-7772-440d-a147-7a06ddad9f52)

Проверяем подняты ли контейнеры:
![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/a2abc0ad-28ea-4dac-ac35-faea1cdf4851)

команда ip a
 и к ней добавляем :6080
![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/1e42e93b-debe-4926-a405-b64708a6c493)

![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/4cb3e6b5-524c-49cb-bf6c-42bb052e79a6)

![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/09851bbb-f984-43fe-848b-0aefc0bb1d39)

![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/dc51f781-2516-4310-b10e-cf390c51038f)


После этого можем запустить удаление:
root@Roman-Linux:/home/ari# docker compose down

![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/1f930a2c-2c46-4f87-a0db-5ab4b04a3d5e)

root@Roman-Linux:/home/ari# docker compose down

[+] Running 3/3

 ✔ Container ari-adminer-1  Removed                                                                                              0.2s 

 ✔ Container ari-db-1       Removed                                                                                              0.4s 

 ✔ Network ari_default      Removed  


 Задача 2:
  Включаем режим
 root@Roman-Linux:/home/ari# docker swarm init

 ![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/491087dd-80a7-48c8-8a79-3aaa5bd2b9d5)

Проверяем список всех нод 
root@Roman-Linux:/home/ari# docker node ls

ID                            HOSTNAME      STATUS    AVAILABILITY   MANAGER STATUS   ENGINE VERSION

bqd4s6eq9aikziye62t571kyw *   Roman-Linux   Ready     Active         Leader           25.0.4

Создаем свою тестовую сеть:

root@Roman-Linux:/home/ari# docker network create --driver overlay test-networks --attachable

q0raz3odevunsn2ouyj3efcfs

Создаем 1 контейнер

root@Roman-Linux:/home/ari# docker service create --name mariadb_service --replicas 1 -e MYSQL_ROOT_PASSWORD=12345 -p 3306:3306 --network test-networks mariadb:10.10.2

np32s7tpgp17r8rgxjgcg2xgv

overall progress: 1 out of 1 tasks 

1/1: running   [==================================================>] 

verify: Service converged 
![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/e5343f88-381d-40c7-99b7-a6069246172d)

Делаем 4 контейнера:

![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/6286d4af-de9e-4a8c-9b3c-426f8edfcdec)

Задача 3:глобальный режим 
 Делаем глобальные настройки
 
 ari@Roman-Linux:~$ docker node update --label-add env=prod benr329swnllcuo54udptdpcr

benr329swnllcuo54udptdpcr

После прооверяем 

ari@Roman-Linux:~$ docker inspect benr329swnllcuo54udptdpcr

[

    {

        "ID": "benr329swnllcuo54udptdpcr",

        "Version": {

            "Index": 30

        },

        "CreatedAt": "2024-03-18T20:08:13.414937801Z",

        "UpdatedAt": "2024-03-18T20:12:00.813877599Z",

        "Spec": {

            "Labels": {

                "env": "prod"

            },

            "Role": "manager",

            "Availability": "active"

        },

        "Description": {

            "Hostname": "Roman-Linux",

            "Platform": {

                "Architecture": "x86_64",

                "OS": "linux"

            },

            "Resources": {

                "NanoCPUs": 4000000000,

                "MemoryBytes": 4096507904

            },

            "Engine": {

                "EngineVersion": "25.0.4",

                "Plugins": [

                    {

                        "Type": "Log",

                        "Name": "awslogs"

                    },

                    {

                        "Type": "Log",

                        "Name": "fluentd"

                    },

                    {

                        "Type": "Log",

                        "Name": "gcplogs"

                    },

                    {

                        "Type": "Log",

                        "Name": "gelf"

                    },

                    {

                        "Type": "Log",

                        "Name": "journald"

                    },

                    {

                        "Type": "Log",

                        "Name": "json-file"

                    },

                    {

                        "Type": "Log",

                        "Name": "local"

                    },

                    {

                        "Type": "Log",

                        "Name": "splunk"

                    },

                    {

                        "Type": "Log",

                        "Name": "syslog"

                    },

                    {

                        "Type": "Network",

                        "Name": "bridge"

                    },

                    {

                        "Type": "Network",

                        "Name": "host"

                    },

                    {

                        "Type": "Network",

                        "Name": "ipvlan"

                    },

                    {

                        "Type": "Network",

                        "Name": "macvlan"

                    },

                    {

                        "Type": "Network",

                        "Name": "null"

                    },

                    {

                        "Type": "Network",

                        "Name": "overlay"

                    },

                    {

                        "Type": "Volume",

                        "Name": "local"

                    }

                ]

            },

            "TLSInfo": {

                "TrustRoot": "-----BEGIN CERTIFICATE-----\nMIIBazCCARCgAwIBAgIUOeKt2D9KOlJoeAAyegr058uQmEIwCgYIKoZIzj0EAwIw\nEzERMA8GA1UEAxMIc3dhcm0tY2EwHhcNMjQwMzE4MjAwMzAwWhcNNDQwMzEzMjAw\nMzAwWjATMREwDwYDVQQDEwhzd2FybS1jYTBZMBMGByqGSM49AgEGCCqGSM49AwEH\nA0IABFPYl2P6Y0ZixietZ0aoksLa1GNuCwhGHm26fLk+9OcP9nPQ8Ac432dC5g7V\nHDEbh0R93bhkHGh/IuWkd5iWHg+jQjBAMA4GA1UdDwEB/wQEAwIBBjAPBgNVHRMB\nAf8EBTADAQH/MB0GA1UdDgQWBBS2lgUiw9NVix6XslEzAvTbwU0wlDAKBggqhkjO\nPQQDAgNJADBGAiEAt/4uq0kV1QDrs5seGyFg5CYgfqP2L6buXYYncyGwhmsCIQC8\nZb/4rC9aJCqmowXbg0MDKQiS5R+PVdnOBXEA42VcQw==\n-----END CERTIFICATE-----\n",

                "CertIssuerSubject": "MBMxETAPBgNVBAMTCHN3YXJtLWNh",

                "CertIssuerPublicKey": "MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEU9iXY/pjRmLGJ61nRqiSwtrUY24LCEYebbp8uT705w/2c9DwBzjfZ0LmDtUcMRuHRH3duGQcaH8i5aR3mJYeDw=="

            }

        },

        "Status": {

            "State": "ready",

            "Addr": "192.168.0.103"

        },

        "ManagerStatus": {

            "Leader": true,

            "Reachability": "reachable",

            "Addr": "192.168.0.103:2377"

        }

    }

]
![image](https://github.com/Jetrong/DockerSwarm/assets/136317824/2ef89b33-6496-4554-bc79-7befa7027ebe)



