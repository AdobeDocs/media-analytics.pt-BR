---
title: Visão geral da migração
description: Saiba como migrar das versões 1.x para 2.x do SDK de mídia.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 100%

---

# Visão geral da migração herdada do VHL 1.x para VHL 2.x {#migration-overview}

A migração do VHL 1.x para o VHL 2.x é simples, e a nova versão apresenta APIs simplificadas para inicialização, configuração e delegações de player.

Aqui estão as principais diferenças entre as versões 1.x e 2.x:

* **Plug-ins, representantes -** Você não precisa mais implementar plug-ins e representantes para o Analytics, o VideoPlayer e o Heartbeat.
* **Configuração -** Não é mais necessário representar as configurações para os plug-ins 1.x.

## Benefícios do 2.x {#benefits-of-two-x}

* Todos os métodos públicos estão consolidados na classe `MediaHeartbeat` para facilitar a implementação para os desenvolvedores.
* Todas as configurações estão agora consolidadas na classe `MediaHeartbeatConfig`.
* Não é mais necessário instanciar as configurações para os plug-ins do Analytics, VideoPlayer e Heartbeat. Você só precisa instanciar a classe `MediaHeartbeat` com instâncias `MediaHeartbeatDelegate` e `MediaHeartbeatConfig`. Essa é a única implementação necessária para inicializar o Media Analytics.

  Com a inicialização do `MediaHeartbeat`, é possível excluir com segurança toda a implementação do Analytics Plug-in, do VideoPlayer Plug-in e do Heartbeat Plug-in. Além disso, é necessário remover todas as implementações existentes para a inicialização do que utiliza uma matriz de plug-ins como entrada. Você pode ver comparações lado a lado das implementações 1.x e 2.x aqui: [Comparação de código do: 1.x para 2.x.](./code-comparison-1x-2x.md)

As novas APIs em 2.x estão descritas detalhadamente aqui: [Conversão de API 1.x para 2.x.](./1x-2x-api-change.md)
