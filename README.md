# storeit — infrastructure


## Kubernetes

Кластер Kubernetes развернут в VK Cloud.


## Установка

### Подготовка окружения 

1. Засетапить кластер Kubernetes в любом понравившемся облаке. Можно даже на голом железе с помощью k3s.
1. Попадаем в кластер, проверяем `kubectl get nodes`

### Установка argocd

1. Устанавливаем argocd из helm-чарта.

```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm install argocd argo/argo-cd --namespace argocd --create-namespace
```

1. Устанавливаем App-of-Apps

```bash
kubectl apply -f argocd/applications.yaml
kubectl port-forward svc/argocd-server -n argocd 8080:443
argocd admin initial-password -n argocd
```

1. Проверяем установку
`127.0.0.1:8080`

### TODO

- [ ] move cert-manager to argocd from vk cloud