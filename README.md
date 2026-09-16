# Домашнее задание «Как работает сеть в K8s» — Лугинина Виктория

Кластер установлен через kubeadm, сетевой плагин Calico.
Приложения размещены в namespace `app`: frontend, backend, cache.
Образ: `wbitt/network-multitool`.

Доступ: frontend → backend → cache.
Остальные подключения запрещены.

## Манифесты

- [app.yaml](./app.yaml)
- [netpol.yaml](./netpol.yaml)

## Политики

- `default-deny` — запрет входящего трафика ко всем подам в namespace
- `allow-frontend-to-backend` — frontend может обращаться к backend
- `allow-backend-to-cache` — backend может обращаться к cache

## Проверка

Разрешено:
- frontend → backend
- backend → cache

Запрещено (curl exit code 28):
- frontend → cache
- backend → frontend
- cache → backend
- cache → frontend

![1.png](https://github.com/victorialugi/k8s_netpol/blob/main/1.png)
![2.png](https://github.com/victorialugi/k8s_netpol/blob/main/2.png)
