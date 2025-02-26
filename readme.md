# Лабораторная работа №3. Первый контейнер

## Студент

**Славов Константин, группа I2302**  
**Дата выполнения: _26.02.2025_**

## Цель работы

Данная лабораторная работа знакомит нас с работой в Docker, основами контейнеризации и подготовливает рабочее место для выполнения последующих лабораторных работ.

## Задание

1. Установить Docker Desktop и проверить его работоспособность.

![image](https://i.imgur.com/Sxinbv4.jpeg)

Если Docker установлен корректно, то в `cmd` после написания команды `docker --version` должна появиться версия данного ПО.

2. Создать репозиторий `containers02` и склонировать его себе на компьютер.

    ![image](https://i.imgur.com/9g6UgYN.jpeg)

3. В папке `containers02` создать файл `Dockerfile` со следующим содержимым:

```Dockerfile
FROM debian:latest
COPY ./site/ /var/www/html/
CMD ["sh", "-c", "echo hello from $HOSTNAME"]
```

![image](https://i.imgur.com/vWSEgzA.jpeg)

4. В той же папке проекта создать папку `site`. В новой папке создать файл `index.html` с произвольным содержимым.

![image](https://i.imgur.com/lsx9C1e.jpeg)

5. Собрать образ с помощью команды:

   ```sh
   docker build -t containers02 .
   ```

![image](https://i.imgur.com/9I8QuCk.jpeg)

Образ на моем компьютере создавался чуть менее 90 секунд.

6. Запустить контейнер с помощью команды:

   ```sh
   docker run --name containers02 containers02
   ```

![image](https://i.imgur.com/3o95fUK.jpeg)

После ввода данной команды, на выходе мы получаем просто строку `hello from` + первые 12 символа идентификатора контейнера.

7. Удалить контейнер и запустить снова в интерактивном режиме:

   ```sh
   docker rm containers02
   docker run -ti --name containers02 containers02 bash
   ```

8. Внутри контейнера выполнить:

   ```sh
   cd /var/www/html/
   ls -l
   ```

![image](https://i.imgur.com/SfJbVzQ.jpeg)

В результате ввода этих команд, на экран выводится список всех файлов, которые были скопированы в контейнер с подробной информацией, включая файл `index.html`.

9. Закрыть окно контейнера с помощью команды `exit`.

![image](https://i.imgur.com/NUmuHJc.jpeg)

## Выводы

В ходе выполнения лабораторной работы была развернута и сконфигурирована среда Docker Desktop. Создан и собран Docker-образ, в который были включены подготовленные файлы сайта. После развертывания контейнера проверена корректность переноса данных в `/var/www/html/`, а также успешное выполнение встроенных команд.

В процессе работы получены практические навыки по созданию Docker-образов, управлению контейнерами и работе в интерактивном режиме. Освоенные методы будут полезны при последующем использовании контейнеризации в учебных и реальных проектах.

## Используемые источники

- [Официальная документация Docker](https://docs.docker.com/)
- [Основы работы с контейнерами](https://opensource.com/resources/what-are-linux-containers)
- [Учебное руководство по Docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)
- [Руководство по написанию Dockerfile](https://docs.docker.com/engine/reference/builder/)
- [Лучшие практики создания Docker-образов](https://docs.docker.com/develop/dev-best-practices/)
