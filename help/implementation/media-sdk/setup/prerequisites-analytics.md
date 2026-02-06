---
title: Pré-requisitos para implementações somente do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar o complemento Adobe Analytics para mídia de streaming para implementações exclusivas do Adobe Analytics
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 43%

---

# Pré-requisitos para implementações somente do Adobe Analytics

Os pré-requisitos descritos nesta seção são específicos para implementar o complemento Adobe Analytics para mídia de streaming em implementações exclusivas do Adobe Analytics (quando não estiver usando o Edge).

1. **Concluir os pré-requisitos gerais**<br>
Se você implementar os serviços de mídia de transmissão para implementações somente do Adobe Analytics ou para implementações do Edge, verifique se atende aos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você tem uma implementação do Adobe Analytics**<br>
Ao implementar o complemento Adobe Analytics para mídia de streaming para uma implementação somente do Analytics, também é necessária uma implementação básica do Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) para obter mais informações.

1. **Obter o URL do servidor de rastreamento de mídia**<br>
Solicite o URL do servidor de rastreamento de mídia ao seu representante do Adobe Analytics. Esta é a URL `collection-api-server` do Mobile SDK, do JavaScript SDK e do servidor de rastreamento da API não coletora do Roku. Os nomes de domínio para a implementação da API são: `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o SDK de mídia atual ou implemente as extensões necessárias**<br>
Dependendo do caminho de implementação, [baixar o SDK atual](/help/getting-started/download-sdks.md) para plataformas da Web, móveis ou OTT. As extensões necessárias devem ser implementadas para habilitar o complemento Adobe Analytics para mídia de streaming.

1. **Ativar relatórios do Adobe Analytics**<br>
Para permitir o uso de relatórios no Analytics e visualizar os dados de conteúdo e anúncios coletados, é necessário ativar os relatórios no Analytics. Consulte [Ativação de relatórios de mídia](/help/reporting/media-reports-enable.md).
