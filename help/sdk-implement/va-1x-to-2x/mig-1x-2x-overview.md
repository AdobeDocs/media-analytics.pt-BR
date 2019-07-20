---
seo-title: Visão geral da migração
title: Visão geral da migração
uuid: d 84 f 55 bc-fa 90-45 c 1-b 97 d-cb 5 fe 58 e 80 c 0
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Visão geral da migração{#migration-overview}

A migração do VHL 1.x para o VHL 2.x é simples, sendo que a nova versão apresenta APIs simplificadas para inicialização, configuração e para representantes do reprodutor.

Aqui estão as principais diferenças entre as versões 1.x e 2.x:

* **Plug-ins, representantes -** Você não precisa mais implementar plug-ins e representantes para o Analytics, o VideoPlayer e o Heartbeat.
* **Configuração -** Não é mais necessário representar as configurações para os plug-ins 1.x.

## Benefits of 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* Não é mais necessário instanciar as configurações para os plug-plugins do Analytics, videoplayer e Heartbeat. You only need to instantiate the `MediaHeartbeat` class with `MediaHeartbeatDelegate` and `MediaHeartbeatConfig` instances. Essa é a única implementação necessária para inicializar o Media Analytics.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Além disso, é necessário remover todas as implementações existentes para a inicialização do que utiliza uma matriz de plug-ins como entrada. Você pode ver comparações lado a lado das implementações 1.x e 2.x aqui: [Comparação de código do: 1.x para 2.x.](./code-comparison-1x-2x.md)

As novas APIs em 2.x estão descritas detalhadamente aqui: [Conversão de API 1.x para 2.x.](./1x-2x-api-change.md)
