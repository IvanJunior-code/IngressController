
# Ingress Controller Test Project

Este projeto tem como objetivo testar e demonstrar a configuração de um **Ingress Controller** no Kubernetes. O projeto inclui três sites simples, cada um representando diferentes páginas (site default, site1 e site2), com suas respectivas configurações e containers Docker. Abaixo estão os detalhes sobre como configurar e executar o projeto.

</br>

## Objetivo

O objetivo principal deste repositório é testar e demonstrar como configurar diferentes regras de **Ingress Controller** no Kubernetes para rotear tráfego para os três sites simples. Cada site tem uma configuração básica, e as regras de **Ingress** foram configuradas para testar:

- **Ingress simples**: Direcionando todo o tráfego para apenas um site.
- **Ingress com host**: Direcionando o tráfego por meio de sub-domínios.
- **Ingress com path**: Direcionando o tráfego com base em paths (caminhos da URL).
- **Ingress padrão**: Direciona para uma página default.

</br>

## Tecnologias Utilizadas

- **Docker**: Para criar containers dos três sites.
- **Kubernetes**: Para orquestrar os containers e aplicar regras de **Ingress Controller**.
- **Ingress Controller**: Para gerenciar o tráfego de rede dentro do cluster Kubernetes.
- **Flask (Python)**: Para criar os sites simples (site default, site1 e site2).
- **Python**: Linguagem utilizada para desenvolver a aplicação web com Flask.
- **HTML**: Linguagem de marcação utilizada para estruturar as páginas dos sites.
- **CSS**: Estilos aplicados para definir a aparência dos sites.
</br>
