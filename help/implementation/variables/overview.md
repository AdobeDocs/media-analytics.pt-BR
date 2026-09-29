---
title: Visão geral das variáveis de mídia de transmissão
description: Saiba como as variáveis de mídia de transmissão são organizadas e como elas são mapeadas no Adobe Analytics e no Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%
---

# Visão geral das variáveis de mídia de transmissão

As variáveis são os dados que o player de mídia fornece sobre um fluxo, como nome do conteúdo, tipo de fluxo, nome do anúncio e qualidade de reprodução. A maioria das variáveis é definida no início da sessão e transportada até o fechamento da sessão pelo back-end de mídia, que as usa para preencher as dimensões e métricas usadas nos relatórios. Cada página de variável documenta como definir essa variável em cada método de implementação compatível.

## Como as variáveis são enviadas para o Adobe

Uma única variável carrega o mesmo valor para cada aplicativo ou serviço do Adobe, mas o formato desse valor depende do local para onde você o envia. A tabela a seguir lista cada aplicativo ou serviço e o formato variável que ele espera. A tabela de propriedades em cada página de variável mostra o valor exato a ser usado em cada formato.

| Formato dos dados | Descrição |
| --- | --- |
| Variável de dados de contexto | O formato enviado para o Adobe Analytics, nomeado com um prefixo `a.media` (como `a.media.name`). |
| Campo de coleção XDM | O formato enviado para o Customer Journey Analytics, expresso como um caminho de campo XDM (como `xdm.mediaCollection.sessionDetails.name`). |
| Característica do Audience Manager | O formato encaminhado ao Audience Manager, prefixado com `c_contextdata` (como `c_contextdata.a.media.name`). |

>[!MORELIKETHIS]
>
>* [Visão geral dos eventos](/help/implementation/events/overview.md): os eventos do player que contêm variáveis
>* [Visão geral das dimensões](/help/reporting/dimensions/overview.md): as dimensões de relatório que as variáveis preenchem
>* [Visão geral das métricas](/help/reporting/metrics/overview.md): as métricas de relatório que as variáveis preenchem
