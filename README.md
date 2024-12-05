
# Ingress Controller Test Project

Este projeto tem como objetivo testar e demonstrar a configuração de um **Ingress Controller** no Kubernetes. O projeto executa três sistemas diferentes baseados em containers, e cada um acessível por meio de um Service. Abaixo estão os detalhes sobre como configurar e executar o projeto.

</br>

## Objetivo

O objetivo principal deste repositório é testar e demonstrar como configurar diferentes regras de **Ingress Controller** no Kubernetes para rotear tráfego para três sites simples. Cada site tem uma configuração básica, e as regras de **Ingress** foram configuradas para testar:

- **`ingress-simple-rule.yaml`**: Direcionando todo o tráfego para apenas um site (quando aplicado).
- **`ingress-path-rule.yaml`**: Direcionando o tráfego com base em paths (caminhos da URL).
- **`ingress-default-rule.yaml`**: Direciona para uma página default.
- **`ingress-host-rule.yaml`**: Direcionando o tráfego por meio de sub-domínios.


</br>

## Tecnologias Utilizadas

- **Docker**: Para criar containers dos três sites.
- **Kubernetes**: Para orquestrar os containers e aplicar regras de **Ingress Controller**.
- **Ingress Controller**: Para gerenciar o tráfego de rede dentro do cluster Kubernetes.


</br>

## Pré requisito
- Cluster Kubernetes;
- Acesso ao cluster;
- kubectl instalado;
- [Nginx Ingress Controller](https://kubernetes.github.io/ingress-nginx/deploy/) instalado no cluster;


<br>

## Exemplo de uso

1. Configurar acesso ao cluster EKS:
```
aws eks update-kubeconfig --name eks
```

2. Instalar o Nginx Ingress Controller:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/aws/deploy.yaml
```

3. Aplicar os Deployments e Services:
```
kubectl apply -f deployment.yaml -f services.yaml
```

4. Aplicar as regras de Ingress de Path, de Host e de página default:
```
kubectl apply -f ingress-path-rule.yaml -f ingress-host-rule.yaml -f ingress-default-rule.yaml
```
**Nota**: A regra `ingress-simple-rule.yaml` não será aplicada neste exemplo, pois direciona para apenas um único Service.

5. Configurar o DNS:

    5.1. Identificar Host ou IP do Load Balancer:
    
    5.1.1. Identificar o namespace do Nginx Ingress Controller:
    ```
    kubectl get namespace
    ```
    5.1.2. Obter o endereço host do Load Balancer:
    ```
    kubectl get svc -n ingress-nginx
    ```
    **Nota**: O host será identificado como EXTERNAL-IP, Ingress do tipo LoadBalancer.

    5.1.3. Utilizar o comando dig para obter o IP do Load Balancer:
    ```
    dig host.elb.us-east-1.amazonaws.com +short
    ```
    **Nota**: Dependendo da quantidade de Zonas de Disponibilidade, o host do Load Balancer pode retornar mais de um IP. Basta selecionar um.
    
    

    5.2. Configurar o DNS:
    
    **Nota**: Utilize apenas uma das configurações, por Host ou por IP, seguindo **tipo**, **subdomínio**, e **host** ou **IP**.
    
    5.2.1. Configurar no painel DNS por Host:
    ```dns
    CNAME www host.elb.us-east-1.amazonaws.com
    CNAME site1 host.elb.us-east-1.amazonaws.com
    CNAME site2 host.elb.us-east-1.amazonaws.com
    ```
    5.1.4. Configurar no painel DNS por IP:
    ```dns
    A @ 54.87.51.157
    A site1 54.87.51.157
    A site2 54.87.51.157
    ```
<br>

## Conclusão
Este projeto fornece um ambiente de teste para configurar e entender como o Ingress Controller funciona no Kubernetes direcionando o tráfego, permitindo a criação de regras flexíveis para gerenciar as requisições.