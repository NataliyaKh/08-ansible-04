# Домашнее задание к занятию 3 «Использование Ansible». Наталия Ханова. 
## Подготовка к выполнению

1.    Подготовьте в Yandex Cloud три хоста: для clickhouse, для vector и для lighthouse.
2.    Репозиторий LightHouse находится [по ссылке](https://github.com/VKCOM/lighthouse).

## Основная часть

1.    Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.
2.    При создании tasks рекомендую использовать модули: get_url, template, yum, apt.
3.    Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.
4.    Подготовьте свой inventory-файл prod.yml.
5.    Запустите ansible-lint site.yml и исправьте ошибки, если они есть.
6.    Попробуйте запустить playbook на этом окружении с флагом --check.
7.    Запустите playbook на prod.yml окружении с флагом --diff. Убедитесь, что изменения на системе произведены.
8.    Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.
9.    Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.
10.   Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-03-yandex на фиксирующий коммит, в ответ предоставьте ссылку на него.

## Plays

1. Install Clickhouse: Установка Clickhouse

    Тег: `clickhouse`

    Загрузка дистрибутивов Clickhouse.
    Установка пакетов Clickhouse (clickhouse-common-static, clickhouse-client, clickhouse-server).
    Создание базы данных logs.
    Запуск сервиса Clickhouse.

    Переменные: 
    `clickhouse_version` - версия программы Clickhouse
    `clickhouse_packages` - имена пакетов Clickhouse

2. Install Vector: Установка Vector

    Тег: `vector`

    Загрузка дистрибутива Vector.
    Установка пакета Vector.
    Создание файла конфигурации Vector из шаблона.
    Запуск сервиса Vector.

    Переменные: 
    `vector_version` - версия программы Vector.

3. Install NGINX: Установка NGINX

    Тег: `lighthouse` 

    Установка и настройка NGINX для работы с LightHouse, настройка перезагрузки NGINX в случае изменения конфигурации.
    Запуск NGINX. 

4. Install Lighthouse: Установка LightHouse

    Тег: `lighthouse`     

    Установка зависимостей LightHouse.
    Клонирование репозитория LightHouse.
    Создание файла конфигурации LightHouse из шаблона.

    Переменные:
    `lighthouse_vcs` - адрес репозитория LightHouse
    `lighthouse_location` - папка назначения для локального репозитория LightHouse
