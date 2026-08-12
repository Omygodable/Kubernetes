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
```bash
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