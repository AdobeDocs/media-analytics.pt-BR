---
title: Migrar perfis para os novos campos de mídia de streaming
description: Saiba como migrar perfis para os novos campos de mídia de streaming
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
TQID: https://experienceleague.adobe.com/c1WHnEeZnI3PP6aO40pDHpJCi2Z0ERiNY8lCj4wyMiU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 0%

---

# Migrar perfis para os novos campos de streaming de mídia

Este documento descreve o processo de migração do serviço de filtragem de perfil que existe sobre os fluxos de coleta de dados do Adobe ativados para Adobe Analytics para dados de mídia de transmissão. A migração converte o serviço de filtragem de perfis de usar o tipo de dados de serviços de mídia de streaming da Adobe chamado &quot;Mídia&quot; para usar o novo tipo de dados correspondente chamado &quot;[Detalhes de Relatórios de Mídia](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.&quot;

## Migrar perfis

Para migrar a filtragem de perfil do tipo de dados antigo chamado &quot;Mídia&quot; para o novo tipo de dados chamado &quot;[Detalhes de Relatórios de Mídia](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, edite as regras de filtragem de perfil existentes:

1. Na Adobe Experience Platform, na seção [!UICONTROL **Fontes**], vá para a guia [!UICONTROL **Fluxos de Dados**].

1. Localize o fluxo de dados responsável pela importação de dados de mídia de transmissão do Adobe Analytics para o Adobe Experience Platform por meio da Coleção de dados da Adobe.

1. Selecione [!UICONTROL **Atualizar fluxo de dados**] para modificar a configuração da filtragem de perfil, substituindo cada regra personalizada que contenha um campo obsoleto pelo novo campo correspondente do novo objeto XDM.

1. Localize os filtros que contêm campos do objeto &quot;Mídia&quot; obsoleto.

1. Anexe esses filtros adicionando campos do novo objeto &quot;Detalhes de relatórios de mídia&quot;.

1. Use um operador OR entre os dois campos;

1. Valide se os perfis ainda estão funcionando como esperado.

Consulte o parâmetro [ID de Conteúdo](/help/reporting/dimensions/content.md) e o restante das variáveis de mídia de streaming documentadas em [Serviços de mídia de streaming](/help/media-overview.md) para mapear entre os campos antigos e os novos campos. O caminho de campo antigo pode ser encontrado na propriedade &quot;Caminho do campo XDM&quot;, enquanto o novo caminho de campo pode ser encontrado na propriedade &quot;Caminho do campo XDM do relatório&quot;.

## Exemplo

Para facilitar o cumprimento das diretrizes de migração, considere o exemplo de fluxo de dados a seguir que contém uma única regra de filtragem de perfil. Nesse caso, como há apenas uma única regra, é necessário aplicar as diretrizes de migração apenas uma vez.

1. Na Adobe Experience Platform, na seção [!UICONTROL **Fontes**], vá para a guia [!UICONTROL **Fluxos de Dados**].

1.Localize o fluxo de dados responsável pela importação de dados de mídia de transmissão do Adobe Analytics para o Adobe Experience Platform via Adobe Analytics.

1. Selecione **[!UICONTROL Atualizar fluxo de dados]** para inserir a interface de edição conforme mostrado na imagem abaixo.

   ![perfil de fluxo de dados do AEP](assets/aep-dataflow-profile.jpeg)

1. Selecione **[!UICONTROL Avançar]** para ir para a guia Filtragem.

   ![guia de filtro de fluxo de dados do AEP](assets/aep-dataflow-filtering-profile.jpeg)

1. Na guia **[!UICONTROL Filtragem]**, identifique as regras de filtragem que dependem dos campos `media.mediaTimed`.

   ![Regras de filtro de fluxo de dados do AEP](assets/dataflow-filtering-rules-profile.jpeg)


   Para cada filtro que usa o objeto media.mediaTimed, encontre seu correspondente no objeto `mediaReporting` usando as variáveis de mídia de streaming documentadas em [Serviços de mídia de streaming](/help/media-overview.md) para mapear entre os campos antigos e os novos campos. O caminho de campo antigo é encontrado na propriedade &quot;Caminho do campo XDM&quot;, enquanto o novo caminho de campo é encontrado na propriedade &quot;Caminho do campo XDM do relatório&quot;. Por exemplo, para [Inícios da mídia](/help/reporting/metrics/media-starts.md), o correspondente para `media.mediaTimed.impressions.value` é `xdm.mediaReporting.sessionDetails.isViewed`.

   ![Campos XDM novos e antigos](assets/xdm-fields-new-and-old.jpeg)

1. Arraste o campo `mediaReporting` relevante para a regra de filtragem e use o operador OR entre as duas regras. Adicione a mesma regra da existente ao usar o novo campo.

   ![Adicionar regras de filtro](assets/add-filter-rules.jpeg)

1. Selecione **[!UICONTROL Avançar]** para salvar as alterações.
