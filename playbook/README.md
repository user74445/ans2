#### Подготовка к выполнению

Подготовьте хосты в соотвтествии с группами из предподготовленного playbook.

```
version: '3'
services:
  elastic:
    image: pycontribs/ubuntu
    container_name: elastic
    restart: unless-stopped
    entrypoint: "sleep infinity"

  kibana:
    image: pycontribs/ubuntu
    container_name: kibana
    restart: unless-stopped
    entrypoint: "sleep infinity"

```
#### Основная часть



inventory файл prod.yml
```
---
  local:
    hosts:
      localhost:
        ansible_connection: local
  elasticsearch:
    hosts:
      elastic:
        ansible_connection: docker
  kibana:
    hosts:
      kibana:
        ansible_connection: docker
  logstash:
    hosts:
      logstash:
        ansible_connection: docker

```


#### GROUP VARS

java_oracle_jdk_package -  пакет установки Java  
java_jdk_version - используемая версия Java  

elastic_home - переменная домашнего каталога для Elasticsearch  
kibana_home - переменная для домашнего каталога для Kibana  
elastic_version - версия Elasticsearch  
kibana_version - версия Kibana  

#### Описание Play

Поднимаются локальные докер контейнеры и в них устанавливаются Java, ElasticSearch, Kibana. Для  Kibana указываются пути до ElasticSearch в конфигурационных файлах.
Для шагов загрузки пакетов установлены теги never. При первом запуске необходимо запустить плейбук с флагом --tags all  

#### Установка Java

Установлены тэги java для дальнейшего использования и отладки  

- установка переменных (facts)
- загрузка установочного пакета
- создание рабочего каталога
- распаковка пакета
- создание по шаблону переменных окружений (templates)

#### Установка Elastic

установлены тэги elastic для дальнейшего использования и отладки  

- загрузка установочного пакета
- создание рабочего каталога
- распаковка в рабочий каталог из пакета
- создание по шаблону переменных окружений (templates)

#### Установка Kibana

установлены тэги kibana для дальнейшего использования и отладки  

- загрузка установочного пакета
- создание рабочего каталога
- распаковка в рабочий каталог из пакета
- создание по шаблону переменных окружений (templates)

#### Установка Logstash

установлены тэги Logstash для дальнейшего использования и отладки  

- загрузка установочного пакета
- создание рабочего каталога
- распаковка в рабочий каталог из пакета
- создание по шаблону переменных окружений (templates)
