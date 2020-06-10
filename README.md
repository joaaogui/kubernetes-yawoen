# neoway-challenge

# Cria projeto no google cloud

# Instala cli

# Seta projeto

gcloud config set project project-id

# Cria cluster

gcloud container clusters create yawoen-cluster --num-nodes=1

# get-credentials

gcloud container clusters get-credentials cluster-name

# Define namespace

kubectl apply -f .\yawoen-namespace.yaml

# Define deployment

kubectl apply -f .\yawoen-deployment.yaml

# Define serviço

kubectl apply -f .\yawoen-service.yaml

# Define regras de acesso

kubectl apply -f .\rules.yaml

# Aplica cronjobs

kubectl apply -f .\up-cronjob.yaml

# Monitoramento

## Adiciona Prometheus + grafana 

Kubernetes Engine > Aplicativos > PRocurar po Prometheus+Grafana 

## Expor grafana

### Substituir as variáveis de ambiente pelas variaveis definidas

kubectl patch svc "${APP_INSTANCE_NAME}-grafana" \
  --namespace "${NAMESPACE}" \
  -p '{"spec": {"type": "LoadBalancer"}}'
