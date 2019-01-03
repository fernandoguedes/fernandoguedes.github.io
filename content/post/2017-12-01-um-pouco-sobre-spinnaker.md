---
categories:
- Integração Contínua
- Deploy Contínuo
date: 2017-12-01
feature-img: assets/2016-01-15/promises.jpg
published: true
status: publish
tags:
- Integração Contínua
- Deploy Contínuo
- spinnaker
- docker
- kubernetes
title: 'Um pouco sobre o Spinnaker - Abstraindo as complexidades da entrega contínua'
type: post
author: Luís Fernando Guedes
url: /2017/12/01/um-pouco-sobre-spinnaker/
---

Olá, vão fazer três meses que entrei na [Portal Telemedicina](http://portaltelemedicina.com.br/), e uma das minhas missões iniciais era tornar ágil o processo de entrega de software, basicamente fazer funcionar o fluxo de ponta a ponta - do desenvolvimento ao deploy - com o processo todo automatizado, sem a necessidade de trabalhos manuais para a entrega em diferentes ambientes.

Em janeiro desse ano (2017) a Portal participou de uma seleção mundial do programa [Launchpad Accelerator](http://portaltelemedicina.com.br/portal-telemedicina-acelerada-google/) e teve a oportunidade de contar com o expertise da Google, fez treinamentos, foi acelerada financeiramente e através de créditos em produtos e seviços, em meio a essa troca de experiências e conhecimento, o nosso CEO Rafael Figueroa, conheceu o [Spinnaker](https://spinnaker.io), compartilhou comigo e disse que poderia ser nosso forte aliado na automação de todo esse processo.

## História

O Spinnaker foi criado para satisfazer as necessidades internas de deploy e gerenciamento de infraestrutura da Netflix, e desde 2014 vinha sendo utilizado, efetuando mais de 3000 deploys/dia em 1000 microsserviços (!). Com a ferramenta em pleno funcionamento, em parceria com o Google a tornaram open-source em outubro de 2015, e desde então, vem ganhando o mundo.

## Composição

> Spinnaker is an open source, multi-cloud continuous delivery platform that helps you release software changes with high velocity and confidence.

A ferramenta é um conjunto de microsserviços e drivers que se integram a diferentes _cloud providers_ e oferece diferentes estratégias de deploy - do red/black (blue/green) ao canary - abstraindo a complexidade do controle e gerenciamento da infraestrutura necessária para que esse processo seja ágil e funcione da maneira correta.

### Microsserviços

O Spinnaker é composto por 10 microsserviços entre APIs, frontends, integrações e persistência de dados, abaixo cada uma e responsabilidades:

![Arquitetura do Spinnaker](/spinnaker/architeture.png)

- [Deck](https://github.com/spinnaker/deck): Interface web para gerenciamento e acompanhamento de todas as execuções background da ferramenta;
- [Gate](https://github.com/spinnaker/gate): Gateway de APIs, responsável pela distribuição de requests aos microsserviços;
- [Orca](https://github.com/spinnaker/orca): Controla todas as operações e pipelines;
- [Clouddriver](https://github.com/spinnaker/clouddriver): Orquestração de clusters e containers multi *cloud provider*;
- [Front50](https://github.com/spinnaker/front50): Persistência de dados utilizando Redis, garante histórico de operações, builds, pipelines, deploys, etc;
- [Rosco](https://github.com/spinnaker/rosco): Responsável por buildar imagens vindas de diferentes serviços (como [GCE Images](https://cloud.google.com/compute/docs/images), [AWS AMIs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html));
- [Igor](https://github.com/spinnaker/rosco): Fornece interface para triggers que podem ser integrados aos pipelines, possui integração com webhooks e algumas ferramentas como Jenkins e Travis;
- [Echo](https://github.com/spinnaker/rosco): Sistema de notificação;
- [Fiat](https://github.com/spinnaker/rosco): Faz o controle de acesso em um sistema baseado em RBAC - Role Based Access Control;
- [Halyard](https://github.com/spinnaker/halyard): Serviço que faz a configuração e gerenciamento do Spinnaker e seus microsserviços, permite instalar, atualizar e fazer rollbacks.

Uma vantagem dessa arquitetura, é que conseguimos acessar pequenas partes do todo, com isso, facilitando integrações externas a processos que não sigam o convencional, exemplo: executar um pipeline de deploy via comando de um bot do slack.

### Pipelines

O pipeline pode ser um processo, um conjunto de processos ou um conjunto de pipelines, para ilustrar melhor visualize a imagem abaixo:

![Pipelines](/spinnaker/pipelines.jpeg)

Para ativar um pipeline é necessário um trigger que pode ser um webhook ou um registry ([the Registry is a stateless, highly scalable server side application that stores and lets you distribute Docker images](https://docs.docker.com/registry/)).

- Bake & Deploy to Test: Consiste em preparar o que for necessário para enviar seu _app_ para o ambiente de teste;
- Validate Test: Pelo fato do Spinnaker também oferecer triggers que podem ser ativados manualmente, ao enviar algo para o ambiente de QA por exemplo, você pode determinar que apenas os testadores podem validar e manualmente  aprovar (podendo ser também acessado via API) o seu envio para um ambiente de homologação;
- Promote to Prod: Automatizado, sem estresse, faz o deploy utilizando clusters, instâncias, kubernetes e load balancers, de acordo com a estratégia configurada, como disse anteriormente possui diferentes estratégias que são gerenciadas pela própria ferramenta.

## Portal Telemedicina

Tivemos alguns desafios iniciais aqui na Portal, primeiramente precisávamos criar toda a estrutura básica de testes, checagem estática de código e formatação, depois adicionar isso aos pipelines do [Bitbucket](https://bitbucket.org) (plataforma que atualmente usamos aqui), "dockerizar" as aplicações, criar a infraestrutura do Spinnaker e seus microsserviços, e por fim, o principal, integrar e juntar as pontas. Acabamos utilizando webhooks (git) entre Bitbucket e Google Cloud Registry, e um "observador" de imagens entre Google Cloud Registry e Spinnaker, tudo isso sobre a orquestração do git flow - com algumas adaptações.

 Partimos praticamente do zero para entrega contínua em pouco mais de um mês com importância fundamental do Spinnaker, até agora os resultados foram satisfatórios, em momentos intensos de entrega, conseguimos realizar diversos deploys por dia sem downtime, diminuindo o tempo entre a entrega e o ciclo de feedback.
