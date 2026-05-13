---
title: Visão geral da migração
description: Saiba como migrar das versões 1.x para 2.x do SDK de mídia.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 82%

---

# Visão geral da migração herdada do VHL 1.x para VHL 2.x {#migration-overview}

A migração do VHL 1.x para o VHL 2.x é simples, e a nova versão apresenta APIs simplificadas para inicialização, configuração e delegações de player.

Estas são as principais diferenças entre 1.x e 2.x:

* **Plug-ins, Representantes -** Não é mais necessário implementar plug-ins e delegados para o Analytics, VideoPlayer e Heartbeat.
* **Configuração -** Não é mais necessário instanciar as configurações dos plug-ins 1.x.

## Benefícios do 2.x {#benefits-of-two-x}

* Todos os métodos públicos estão consolidados na classe `MediaHeartbeat` para facilitar a implementação para os desenvolvedores.
* Todas as configurações estão agora consolidadas na classe `MediaHeartbeatConfig`.
* Não é mais necessário instanciar as configurações para os plug-ins do Analytics, VideoPlayer e Heartbeat. Você só precisa instanciar a classe `MediaHeartbeat` com instâncias `MediaHeartbeatDelegate` e `MediaHeartbeatConfig`. Essa é a única implementação necessária para inicializar o Media Analytics.

  Com a inicialização do `MediaHeartbeat`, é possível excluir com segurança toda a implementação do Analytics Plug-in, do VideoPlayer Plug-in e do Heartbeat Plug-in. Além disso, é necessário remover todas as implementações existentes para a inicialização do que utiliza uma matriz de plug-ins como entrada. Você pode ver comparações lado a lado das implementações 1.x e 2.x aqui: [Comparação de código do: 1.x para 2.x.](./code-comparison-1x-2x.md)

As novas APIs em 2.x estão descritas detalhadamente aqui: [Conversão de API 1.x para 2.x.](./1x-2x-api-change.md)
