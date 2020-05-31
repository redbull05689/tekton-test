az login

az group create --location EastUS --name tekton

az aks create --resource-group tekton --name myAKSCluster --node-count 2

az aks get-credentials --name myAKSCluster --resource-group tekton

<!-- kubectl apply -f https://storage.googleapis.com/tekton-releases/latest/release.yaml -->
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml

### Репа приложения
https://gitlab.com/nmeisenzahl/tekton-demo

kaniko context - это папка внутри пода Каникол , в которой собирается образ(Ну наверное)


### Создадим секрет для возможности заливать докер образы в реджистри

--docker-server=hub.docker.com

kubectl create secret docker-registry tekton-demo  \
        --docker-username=redbull05689 --docker-password=dBQLrjBAU7UQcu6A \
        --docker-email=redbull05689@gmail.com

### install dashboard
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/previous/v0.5.3/tekton-dashboard-release.yaml

### Пробросить порт на тектон дашборд
 kubectl port-forward service/tekton-dashboard 9097:9097 -n tekton-pipelines