# Домашнее задание 1: Запуск приложений в K8S

**Созданы манифесты для** pod-heloww-world,pod-netology и service-netology. 

1. **screenshots/kubectl_get_pods_1.png** — вывод `microk8s kubectl get pods` (только hello-world)
2. **screenshots/curl_hello-world.png** — вывод `curl http://localhost:8080`
3. **screenshots/kubectl_get_pods_svc.png** — вывод `microk8s kubectl get pods && microk8s kubectl get svc`
4. **screenshots/curl_netology-svc.png** — вывод `curl http://localhost:8081`



# Домашнее задание 2: Запуск приложений в K8S

## Описание
В этом задании были развернуты:
1. **Deployment с nginx + multitool** (2 контейнера в одном Pod)
2. **Service** для доступа к приложению
3. **Test Pod** для проверки доступности
4. **Deployment с Init-контейнером** (ожидание запуска сервиса)

## Задание 1. Deployment с nginx + multitool

### Манифесты
- [deployment-web.yaml](deployment-web.yaml) — Deployment с nginx и multitool
- [service-web.yaml](service-web.yaml) — Service для доступа к приложению
- [test-pod.yaml](test-pod.yaml) — Pod для проверки доступности


# Домашнее задание 3: Сетевое взаимодействие в Kubernetes

## Задание 1: Настройка Service (ClusterIP и NodePort)

### Манифесты
- deployment-multi-container.yaml
- service-clusterip.yaml
- service-nodeport.yaml
- deployment-frontend.yaml
- deployment-backend.yaml
- service-frontend.yaml
- service-backend.yaml
- ingress.yaml

### Запуск
microk8s kubectl apply -f deployment-multi-container.yaml
microk8s kubectl apply -f service-clusterip.yaml
microk8s kubectl apply -f service-nodeport.yaml
microk8s kubectl apply -f deployment-frontend.yaml
microk8s kubectl apply -f deployment-backend.yaml
microk8s kubectl apply -f service-frontend.yaml
microk8s kubectl apply -f service-backend.yaml
microk8s kubectl apply -f ingress.yaml

Deployment с nginx + multitool запущен (3 реплики)

ClusterIP Service работает (доступ изнутри кластера)

NodePort Service работает (доступ снаружи)

Ingress настроен и работает (маршрутизация по путям)




# Домашнее задание 4: Хранение в K8S

## Задание 1: Volume (обмен данными между контейнерами)

### Манифест
- [containers-data-exchange.yaml](containers-data-exchange.yaml)

### Запуск
microk8s kubectl apply -f containers-data-exchange.yaml

## Задание 2: PV, PVC

### Манифест
pv-pvc.yaml

microk8s kubectl apply -f pv-pvc.yaml

Объяснение: PV перешёл в состояние Released. Это значит, что PVC был удалён, но данные на диске сохранились благодаря политике Retain.

Объяснение: Файл остался на диске, потому что политика Retain не удаляет данные автоматически. PV был удалён из Kubernetes, но физические данные сохранились.

## Задание 3: StorageClass

### Манифесты
sc.yaml
pv-for-sc.yaml


microk8s kubectl apply -f sc.yaml
microk8s kubectl apply -f pv-for-sc.yaml


# Домашнее задание: Настройка приложений и управление доступом в Kubernetes

## Задание 1: Работа с ConfigMaps

### Манифесты
- [configmap-web.yaml](configmap-web.yaml) — ConfigMap с веб-страницей
- [deployment.yaml](deployment.yaml) — Deployment с nginx + multitool
- [service-nodeport-web.yaml](service-nodeport-web.yaml) — Service типа NodePort

### Запуск
microk8s kubectl apply -f configmap-web.yaml
microk8s kubectl apply -f deployment.yaml
microk8s kubectl apply -f service-nodeport-web.yaml

Проверка

curl http://localhost:30081

Результат: страница из ConfigMap отображается

## Задание 2: Настройка HTTPS с Secrets
Генерация сертификата

openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout tls.key -out tls.crt -subj "/CN=myapp.example.com"

Создание Secret

microk8s kubectl create secret tls tls-secret --key tls.key --cert tls.crt

## Манифесты

    ingress-tls.yaml — Ingress с TLS

Проверка

microk8s kubectl get secrets tls-secret
microk8s kubectl get ingress tls-ingress

## Задание 3: Настройка RBAC
## Манифесты

    role-pod-reader.yaml — Role для просмотра подов

    rolebinding-developer.yaml — RoleBinding для пользователя developer

Включение RBAC

microk8s enable rbac

Проверка доступа

Успешный доступ (просмотр подов):

microk8s kubectl get pods --as=developer

Запрещённый доступ (создание подов):

microk8s kubectl run test-pod --image=nginx --as=developer

Error from server (Forbidden): pods is forbidden: User "developer" cannot create resource "pods" in API group "" in the namespace "default"