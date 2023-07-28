---
title: Pré-requisitos para implementações exclusivas do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar mídia de transmissão com implementações somente do Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# Pré-requisitos para implementações exclusivas do Adobe Analytics

Os pré-requisitos descritos nesta seção são específicos para implementar mídia de transmissão com implementações exclusivas do Adobe Analytics (quando não estiver usando o Edge).

1. **Conclua os pré-requisitos gerais**<br>
Se você implementar a Mídia de transmissão somente para implementações do Adobe Analytics ou para implementações do Edge, certifique-se de atender aos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você tem uma implementação do Adobe Analytics**<br>
Ao implementar a Mídia de transmissão com uma implementação somente do Analytics, também é necessária uma implementação básica do Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) para obter mais informações.

1. **Obter o URL do servidor de rastreamento de mídia**<br>
Solicite o URL do servidor de rastreamento de mídia ao seu representante do Adobe Analytics. Este é o `collection-api-server` URL do SDK móvel, do SDK do JavaScript e do servidor de rastreamento da API não coletora do Roku. Os nomes de domínio para a implementação da API são: `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o SDK de mídia atual ou implemente as extensões necessárias**<br>
Dependendo do caminho de implementação, [baixar o SDK atual](/help/getting-started/download-sdks.md) para plataformas da Web, móveis ou OTT. As extensões necessárias devem ser implementadas para ativar os caminhos de extensões do Adobe Analytics para mídia de streaming.

1. **Ativar relatórios do Adobe Analytics**<br>
Para permitir o uso de relatórios no Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário ativar os relatórios no Analytics. Consulte [Ativação de relatórios de mídia](/help/reporting/media-reports-enable.md).
