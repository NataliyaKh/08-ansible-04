# Домашнее задание к занятию 4 «Работа с roles». Наталия Ханова.

## Подготовка к выполнению

1. * Необязательно. Познакомьтесь с [LightHouse](https://youtu.be/ymlrNlaHzIY?t=929).
2. Создайте два пустых публичных репозитория в любом своём проекте: vector-role и lighthouse-role.
3. Добавьте публичную часть своего ключа к своему профилю на GitHub.

## Основная часть

Ваша цель — разбить ваш playbook на отдельные roles. 

Задача — сделать roles для ClickHouse, Vector и LightHouse и написать playbook для использования этих ролей. 

Ожидаемый результат — существуют три ваших репозитория: два с roles и один с playbook.

**Что нужно сделать**

1. Создайте в старой версии playbook файл `requirements.yml` и заполните его содержимым:

   ```yaml
   ---
     - src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
       scm: git
       version: "1.13"
       name: clickhouse 
   ```

![requirements](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-4-1-req.png)`

2. При помощи `ansible-galaxy` скачайте себе эту роль.

![install-role](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-4-2-install-role.png)`

3. Создайте новый каталог с ролью при помощи `ansible-galaxy role init vector-role`.

![init-role](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-4-3-init-role.png)

4. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 
5. Перенести нужные шаблоны конфигов в `templates`.
6. Опишите в `README.md` обе роли и их параметры. Пример качественной документации ansible role [по ссылке](https://github.com/cloudalchemy/ansible-prometheus).
7. Повторите шаги 3–6 для LightHouse. Помните, что одна роль должна настраивать один продукт.
8. Выложите все roles в репозитории. Проставьте теги, используя семантическую нумерацию. Добавьте roles в `requirements.yml` в playbook.
9. Переработайте playbook на использование roles. Не забудьте про зависимости LightHouse и возможности совмещения `roles` с `tasks`.
10. Выложите playbook в репозиторий.
11. В ответе дайте ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

[vector-role](https://github.com/NataliyaKh/ansible-roles_vector)

[lighthouse-role](https://github.com/NataliyaKh/ansible-roles_lighthouse)

[playbook](https://github.com/NataliyaKh/08-ansible-04/tree/main/playbook)

**Важно**: Роль clickhouse, ссылка на которую приводится в задании, не срабатывает, плейбук падает по таймауту со следующей ошибкой:
```
fatal: [clickhouse-01]: FAILED! => {"changed": false, "cmd": ["clickhouse-client", "-q", "create database logs;"], "delta": "0:00:00.050589", "end": "2025-05-07 01:10:49.932984", "failed_when_result": true, "msg": "non-zero return code", "rc": 210, "start": "2025-05-07 01:10:49.882395", "stderr": "Code: 210. DB::NetException: Connection refused (localhost:9000). (NETWORK_ERROR)", "stderr_lines": ["Code: 210. DB::NetException: Connection refused (localhost:9000). (NETWORK_ERROR)"], "stdout": "", "stdout_lines": []}
```

В итоге я использовала другую роль со сходным функционалом, найденную в Github. Именно на неё в настоящее время приводится ссылка в [requirements.yml](https://github.com/NataliyaKh/08-ansible-04/blob/main/playbook/requirements.yml).

Результат применения плейбука с ролями:
![it-works](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-4-roles-done.png)
