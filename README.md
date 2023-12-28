# Лабораторная работа №2. Kubernetes

## Цель работы

Поднять кластер Kubernetes локально, в нём развернуть свой сервис.

## Ход работы

Для выполнения работы был использован локальный кластер Minikube, который позволяет поднять локальный кластер Kubernetes. После установки Minikube, был запущен кластер с помощью команды `minikube start`:

<p align="center">
    <img src="./images/image-1.png">
</p>

Создание "витруального" хранилища образов для докера на порту 5000:

<p align="center">
    <img src="./images/image-2.png">
</p>

В качестве разворачиваемого сервиса было создано приложение выводящее в браузере: "Hello Docker world!". Для этого было создано 3 файла: Dockerfile, app.py и requirements.

Dockerfile:
<p align="center">
    <img src="./images/Dockerfile-image.png">
</p>

app.py:
<p align="center">
    <img src="./images/appPy-image.png">
</p>

requirements:
<p align="center">
    <img src="./images/requirements-image.png">
</p>

После создания всез необходимых файлов был собран докер-образ
<p align="center">
    <img src="./images/image-3.png">
</p>
Чтобы с помощью kubernetes можно было развернуть созданное приложение необходимо прописать манифесты (Deployment и Service) в формате yalm-файлов.

Deployment.yalm:
<p align="center">
    <img src="./images/deployment-image.png">
</p>

Описание Deployment'а:

- `replicas: 1` - количество реплик нашего приложения
- `selector` - селектор, по которому Kubernetes будет искать поды, которые нужно масштабировать
- `template` - шаблон пода, который будет создан при масштабировании
- `containers` - список контейнеров, которые будут запущены в поде
- `name` - имя контейнера
- `image` - образ, который будет запущен в контейнере. В данном случае, это образ нашего приложения. Ранее он был загружен в Docker Hub.
- `ports` - список портов, которые будут открыты в контейнере

Service.yalm
<p align="center">
    <img src="./images/service-image.png">
</p>

Описание Service'а:

- `type:` - тип сервиса.
- `selector` - селектор, по которому Kubernetes будет искать поды, которые нужно балансировать
- `ports` - список портов, которые будут открыты в сервисе
- `nodePort` - порт, который будет открыт на каждой ноде кластера
- `targetPort` - порт, на который будет перенаправлен трафик
- `port` - порт, который будет открыт в сервисе
- `protocol` - протокол, по которому будет работать сервис

После yalm-файлы были применены:
<p align="center">
    <img src="./images/image-4.png">
</p>

Сервис был запущен с помощью команды `minikube service my-first-image`
<p align="center">
    <img src="./images/image-5.png">
</p>

Результат:
<p align="center">
    <img src="./images/result-image.png">
</p>

## Вывод

В результате выполнения лабораторной работы был поднят кластер Kubernetes локально, в нём был развернут свой сервис.
