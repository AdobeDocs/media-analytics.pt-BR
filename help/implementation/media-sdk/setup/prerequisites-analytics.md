---
title: Pré-requisitos para implementações somente do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar o complemento Coleção de mídia de transmissão com implementações somente do Adobe Analytics
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 43%

---

# Pré-requisitos para implementações somente do Adobe Analytics

Os pré-requisitos descritos nesta seção são específicos para implementar o complemento de coleção de mídia de transmissão com implementações exclusivas do Adobe (quando não estiver usando o Edge).

1. **Conclua os pré-requisitos gerais**<br>
Se você implementar o Complemento de coleção de mídia de transmissão para implementações somente do Adobe Analytics ou para implementações do Edge, certifique-se de atender aos requisitos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você tem uma implementação do Adobe Analytics**<br>
Ao implementar o complemento Coleção de mídia de transmissão com uma implementação somente do Analytics, também é necessária uma implementação básica do Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) para obter mais informações.

1. **Obter o URL do servidor de rastreamento de mídia**<br>
Solicite o URL do servidor de rastreamento de mídia ao seu representante do Adobe Analytics. Este é o `collection-api-server` URL do SDK móvel, do SDK do JavaScript e do servidor de rastreamento da API não coletora do Roku. Os nomes de domínio para a implementação da API são: `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o SDK de mídia atual ou implemente as extensões necessárias**<br>
Dependendo do caminho de implementação, [baixar o SDK atual](/help/getting-started/download-sdks.md) para plataformas da Web, móveis ou OTT. As extensões necessárias devem ser implementadas para habilitar os caminhos de extensões do complemento Streaming Media Collection.

1. **Ativar relatórios do Adobe Analytics**<br>
Para permitir o uso de relatórios no Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário ativar os relatórios no Analytics. Consulte [Ativação de relatórios de mídia](/help/reporting/media-reports-enable.md).
