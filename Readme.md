**Созданы манифесты для** pod-heloww-world,pod-netology и service-netology. 

1. **screenshots/kubectl_get_pods_1.png** — вывод `microk8s kubectl get pods` (только hello-world)
2. **screenshots/curl_hello-world.png** — вывод `curl http://localhost:8080`
3. **screenshots/kubectl_get_pods_svc.png** — вывод `microk8s kubectl get pods && microk8s kubectl get svc`
4. **screenshots/curl_netology-svc.png** — вывод `curl http://localhost:8081`



# Домашнее задание: Запуск приложений в K8S

## Описание
В этом задании были развернуты:
1. **Deployment с nginx + multitool** (2 контейнера в одном Pod)
2. **Service** для доступа к приложению
3. **Test Pod** для проверки доступности
4. **Deployment с Init-контейнером** (ожидание запуска сервиса)

---

## Задание 1. Deployment с nginx + multitool

### Манифесты
- [deployment-web.yaml](deployment-web.yaml) — Deployment с nginx и multitool
- [service-web.yaml](service-web.yaml) — Service для доступа к приложению
- [test-pod.yaml](test-pod.yaml) — Pod для проверки доступности