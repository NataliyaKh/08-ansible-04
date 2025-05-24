# Домашнее задание к занятию 5 «Тестирование roles». Наталия Ханова. 

## Подготовка к выполнению

1. Установите molecule и его драйвера: `pip3 install "molecule molecule_docker molecule_podman`.
2. Выполните `docker pull aragast/netology:latest` —  это образ с podman, tox и несколькими пайтонами (3.7 и 3.9) внутри.

## Основная часть

Ваша цель — настроить тестирование ваших ролей. 

Задача — сделать сценарии тестирования для vector. 

Ожидаемый результат — все сценарии успешно проходят тестирование ролей.

### Molecule

1. Запустите  `molecule test -s ubuntu_xenial` (или с любым другим сценарием, не имеет значения) внутри корневой директории clickhouse-role, посмотрите на вывод команды. Данная команда может отработать с ошибками или не отработать вовсе, это нормально. Наша цель - посмотреть как другие в реальном мире используют молекулу И из чего может состоять сценарий тестирования.
![xenial](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5-1-xenial.png)

2. Перейдите в каталог с ролью vector-role и создайте сценарий тестирования по умолчанию при помощи `molecule init scenario --driver-name docker`.
![scenario](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5-2-initsc.png)

3. Добавьте несколько разных дистрибутивов (oraclelinux:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.
![test1](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5-3-mtest1.png)

![test2](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5-3-mtest2.png)

[Лог molecule test](https://github.com/NataliyaKh/08-ansible-04/blob/main/molecule-test.log)

4. Добавьте несколько assert в verify.yml-файл для  проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска и др.). 
[verify.yml](https://github.com/NataliyaKh/vector/blob/main/molecule/default/verify.yml)

5. Запустите тестирование роли повторно и проверьте, что оно прошло успешно.
[Лог проверок](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-verifier.txt)

![check1](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5-4-check1.png)

![check2](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5-4-check2.png)

5. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

[commit2](https://github.com/NataliyaKh/vector/releases/tag/v0.2)

### Tox

1. Добавьте в директорию с vector-role файлы из [директории](docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash).
2. Запустите `docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash`, где path_to_repo — путь до корня репозитория с vector-role на вашей файловой системе.
3. Внутри контейнера выполните команду `tox`, посмотрите на вывод.

![tox1](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox3.png)

![tox2](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox4.png)

![tox3](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox5.png)

![tox4](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox6.png)

![tox5](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox7.png)

[Вывод](https://github.com/NataliyaKh/08-ansible-04/blob/main/tox_aragast.log)

5. Создайте облегчённый сценарий для `molecule` с драйвером `molecule_podman`. Проверьте его на исполнимость.

[scenario2](https://github.com/NataliyaKh/vector/tree/main/molecule/second)

6. Пропишите правильную команду в `tox.ini`, чтобы запускался облегчённый сценарий.

[tox.ini](https://github.com/NataliyaKh/vector/blob/main/tox.ini)

8. Запустите команду `tox`. Убедитесь, что всё отработало успешно.

![mytox1](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox8.png)

![mytox2](https://github.com/NataliyaKh/08-ansible-04/blob/main/ansible-5t3-tox9.png)

[Log](https://github.com/NataliyaKh/08-ansible-04/blob/main/tox3_log.txt)

9. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

[tag8](https://github.com/NataliyaKh/vector/releases/tag/v0.8)

После выполнения у вас должно получится два сценария molecule и один tox.ini файл в репозитории. Не забудьте указать в ответе теги решений Tox и Molecule заданий. В качестве решения пришлите ссылку на  ваш репозиторий и скриншоты этапов выполнения задания. 

## Необязательная часть

1. Проделайте схожие манипуляции для создания роли LightHouse.
2. Создайте сценарий внутри любой из своих ролей, который умеет поднимать весь стек при помощи всех ролей.
3. Убедитесь в работоспособности своего стека. Создайте отдельный verify.yml, который будет проверять работоспособность интеграции всех инструментов между ними.
4. Выложите свои roles в репозитории.

В качестве решения пришлите ссылки и скриншоты этапов выполнения задания.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.
