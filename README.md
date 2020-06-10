# neoway-challenge

Os arquivos contidos neste repositório foram utilzados para criar o serviço encontrado em http://yawoen.joaoguilherme.me/. Os passos descritos a seguir, refletem os passos seguidos para definição da infraestrutura.

## Pré-requisitos 

* Google cloud SDK instalado e configurado (https://cloud.google.com/sdk)
* Projeto criado no Google Cloud

## Definição de projeto do GCP

```
gcloud config set project <project-id>
```

## Criação do cluster

```
gcloud container clusters create <cluster-name> --num-nodes=1
```

## Definição de credenciais do cluster localmente

```
gcloud container clusters get-credentials <cluster-name>
```

## Aplicação do namespace

```
kubectl apply -f yawoen-namespace.yaml
```

## Aplicação do deployment

```
kubectl apply -f yawoen-deployment.yaml
```

## Aplicação do serviço

```
kubectl apply -f yawoen-service.yaml
```

## Definição de regras de acesso

```
kubectl apply -f rules.yaml
```
## Aplicação de cronjobs (Horario de funcionamento do serviço)

```
kubectl apply -f up-cronjob.yaml
kubectl apply -f down-cronjob.yaml
```

# Monitoramento (http://grafana.yawoen.joaoguilherme.me/)

## Adiciona Prometheus + grafana 

Kubernetes Engine > Aplicativos > PRocurar po Prometheus+Grafana 

## Expor serviço do grafana

```
kubectl patch svc "${APP_INSTANCE_NAME}-grafana" \
  --namespace "${NAMESPACE}" \
  -p '{"spec": {"type": "LoadBalancer"}}'
```
