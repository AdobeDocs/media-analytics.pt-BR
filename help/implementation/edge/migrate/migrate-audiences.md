---
title: Migrar públicos-alvo para o novo tipo de dados Adobe Analytics para mídia de streaming
description: Saiba como migrar públicos-alvo para o novo tipo de dados Adobe Analytics para mídia de streaming
feature: Streaming Media
role: User, Admin, Developer
exl-id: 5664bf56-b228-430a-944c-faaab55fa108
TQID: https://experienceleague.adobe.com/TqsfcR2JgxVjDNx3-CBBa9n6pwvuGk9JgQ--DvWeHg0
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
source-git-commit: 92e1a77339d29b0ef7ec8adc76817b2ac61ee900
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 1%

---

# Migrar públicos-alvo para os novos campos de mídia de transmissão

Este documento descreve como um público-alvo que usa campos do tipo de dados de serviços de mídia de transmissão da Adobe chamado &quot;Mídia&quot; deve ser migrado para usar o novo tipo de dados correspondente chamado &quot;[Detalhes de relatórios de mídia](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.&quot;

## Migrar um público-alvo

Para migrar um público do tipo de dados antigo chamado &quot;Mídia&quot; para o novo tipo de dados chamado &quot;[Detalhes de relatórios de mídia](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, edite o público e, em cada regra, substitua o campo antigo do tipo de dados obsoleto pelo novo campo correspondente do novo tipo de dados:

1. Localize regras que contenham campos do tipo de dados &quot;Mídia&quot; obsoleto. Todos os campos começam com o caminho `media.mediaTimed`.

1. Duplique essas regras usando campos do novo tipo de dados &quot;[Detalhes de Relatórios de Mídia](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.

1. Mantenha ambas as regras em vigor até validar que os públicos-alvo estão funcionando como esperado.

1. Remova as regras que contêm campos do tipo de dados obsoleto &quot;Mídia&quot;.

1. Verifique se os públicos-alvo ainda estão funcionando como esperado.

Consulte o parâmetro [ID de Conteúdo](/help/reporting/dimensions/content.md) e o restante das variáveis de mídia de streaming documentadas em [Serviços de mídia de streaming](/help/media-overview.md) para mapear entre os campos antigos e os novos campos. O caminho de campo antigo é encontrado na propriedade &quot;Caminho do campo XDM&quot;, enquanto o novo caminho de campo é encontrado na propriedade &quot;Caminho do campo XDM do relatório&quot;.

![Caminhos antigos e novos do campo XDM](../../assets/field-paths-updated.jpeg)

## Exemplo

Para facilitar o cumprimento das diretrizes de migração, considere o exemplo a seguir, que contém um público-alvo com uma única regra. Como o público-alvo tem uma única regra, é necessário aplicar as diretrizes de migração apenas uma vez.

1. Selecione o botão **[!UICONTROL Editar público-alvo]** no canto superior direito.

1. Localize as regras configuradas para o público-alvo.

   ![Editar público-alvo](../../assets/audience-edit.jpeg)

   ![Editar público-alvo](../../assets/audience-edit2.jpeg)

1. Selecione a regra para abrir sua configuração.

   ![Editar público-alvo](../../assets/audience-edit3.jpeg)

1. (Opcional) Para exibir o caminho do campo usado na regra, selecione o botão de informações próximo ao nome do campo.

   ![Editar público-alvo](../../assets/audience-edit4.jpeg)

1. Identifique o nome do campo (neste caso, &quot;Inícios da mídia&quot;).

   ![Editar público-alvo](../../assets/audience-edit5.jpeg)

1. Consulte as variáveis de mídia de streaming documentadas em [Serviços de mídia de streaming](/help/media-overview.md) para mapear entre os campos antigos. O caminho de campo antigo pode ser encontrado na propriedade &quot;Caminho do campo XDM&quot;, enquanto o novo caminho de campo pode ser encontrado na propriedade &quot;Caminho do campo XDM do relatório&quot;. Por exemplo, para o parâmetro [Inícios da mídia](/help/reporting/metrics/media-starts.md), o correspondente para `media.mediaTimed.impressions.value` é `xdm.mediaReporting.sessionDetails.isViewed`.

   ![Caminho XDM atualizado](../../assets/updated-xdm-path.jpeg)

1. Adicione a mesma regra da existente usando o novo campo.

   ![Adicionar regra](../../assets/add-rule.jpeg)

   ![Adicionar regra](../../assets/add-rule2.jpeg)

   ![Adicionar regra](../../assets/add-rule3.jpeg)

1. Selecione **[!UICONTROL Salvar]** para salvar a audiência. Você pode manter essa configuração pelo tempo necessário para validar se o público-alvo ainda está funcionando como esperado.

1. Após a conclusão da validação, remova o campo antigo e selecione **[!UICONTROL Salvar]** para salvar o público-alvo.

   ![Adicionar regra](../../assets/add-rule4.jpeg)

1. Valide o público-alvo novamente.

   O processo de migração de público-alvo foi concluído.
