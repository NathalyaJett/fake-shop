# 🛍️ Fake Shop - Desafio CI/CD com Kubernetes e GitHub Actions

Este repositório é parte do desafio prático do curso de DevOps Cloud, focado em automatizar o processo de entrega contínua de uma aplicação e-commerce utilizando **Docker**, **Kubernetes**, **DigitalOcean** e **GitHub Actions**.

---

## ✅ Objetivo do Desafio

O objetivo é eliminar o gargalo no processo de deploy da aplicação Fake Shop. Antes, o deploy levava até dois dias, era manual e pouco confiável. Com a automação, toda atualização feita no repositório agora é entregue automaticamente em um ambiente Kubernetes provisionado na **DigitalOcean**.

---

## ⚙️ O que foi implementado

- Cluster Kubernetes criado na DigitalOcean com 2 nós.
- Manifestos Kubernetes criados:
  - `deployment.yaml` (para o app)
  - `postgres-deployment.yaml` (para o banco)
  - `services.yaml` (para exposição)
- Pipeline CI/CD com GitHub Actions:
  - Build da imagem Docker
  - Push para o Docker Hub
  - Deploy automático no Kubernetes com `kubectl`

---
## 🚀 Como funciona a automação

### Evento disparador

A pipeline é executada a cada push na branch `main`.

### Etapas do GitHub Actions

1. **Checkout do código**
2. **Login no Docker Hub**
3. **Build da imagem Docker**
4. **Push para o Docker Hub**
5. **Configuração do acesso ao cluster (via `KUBE_CONFIG_DATA`)**
6. **Deploy no Kubernetes com `kubectl apply -f k8s/`**

---

## 🧪 Como testar / rodar o deploy

1. Faça um `git push` para a branch `main`
2. Acesse a aba `Actions` no GitHub
3. Acompanhe a execução da pipeline `Build and Deploy Fake Shop`
4. Aguarde o sucesso e acesse o IP do LoadBalancer da DigitalOcean

---

## 🔐 Secrets usados no GitHub

As credenciais estão armazenadas como **secrets** no GitHub:

| Nome               | Descrição                             |
|--------------------|----------------------------------------|
| `DOCKERHUB_USERNAME` | Usuário do Docker Hub |
| `DOCKERHUB_TOKEN`    | Token de acesso ao Docker Hub |
| `KUBE_CONFIG_DATA`   | Config base64 do kubeconfig exportado |

---

## 🐳 Docker Hub

A imagem é publicada automaticamente em:
docker.io/<seu-usuário>/fake-shop:latest (Criada e publicada anteriormente no dockerhub)

## 🧠 Lições aprendidas e erros resolvidos

- 📌 **Erro no kubeconfig**: o `KUBE_CONFIG_DATA` estava apontando para um cluster antigo, corrigido ao exportar novamente da DigitalOcean.
- 🐞 **Erro no path do Dockerfile**: corrigido o local correto do `Dockerfile` para o build funcionar.
- ✅ Aprendizado sobre o fluxo de build no GitHub Actions e como utilizar `kubectl` com contexto remoto.

---

## ✅ Conclusão

Com essa automação, a entrega da aplicação agora leva **menos de 1 minuto** após o push no repositório. Isso elimina completamente a dor de cabeça das entregas manuais!

---
