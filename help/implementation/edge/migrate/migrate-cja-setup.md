---
title: Migrar públicos-alvo para o novo tipo de dados Adobe Analytics para mídia de streaming
description: Saiba como migrar públicos-alvo para o novo tipo de dados Adobe Analytics para mídia de streaming
feature: Streaming Media
role: User, Admin, Developer
exl-id: 67e67a4b-bd61-4247-93b7-261bd348d29b
TQID: https://experienceleague.adobe.com/Y-Y-xWKm-zOzaQm8kMbgGx8r6BTNLl-Q5AltlF5v7aA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
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
source-wordcount: 759
ht-degree: 1%

---

# Migrar o Customer Journey Analytics para usar os novos campos de mídia de transmissão

Este documento descreve como uma configuração do Customer Journey Analytics que usa o tipo de dados de serviços de mídia de transmissão Adobe chamado &quot;Mídia&quot; deve ser atualizada para usar o novo tipo de dados correspondente chamado &quot;[Detalhes de Relatórios de Mídia](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;.&quot;

## Migrar Customer Journey Analytics

Para migrar uma configuração do Customer Journey Analytics do tipo de dados antigo chamado &quot;Mídia&quot; para o novo tipo de dados chamado &quot;[Detalhes do relatório de mídia](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)&quot;, atualize as seguintes configurações que estão usando o tipo de dados antigo:

* Visualizações de dados

* Campos derivados

### Migrar visualizações de dados

Para migrar as visualizações de dados para o novo tipo de dados:

1. Localize todas as visualizações de dados usando o tipo de dados obsoleto &quot;Mídia&quot;. Todos estes são campos cujo caminho começa com `media.mediaTimed`.

1. Realize uma das seguintes ações:

   * Nessas visualizações de dados, insira os campos do novo tipo de dados &quot;Detalhes de relatórios de mídia&quot;.

   * Crie um campo derivado que use o novo tipo de dados &quot;Detalhes de relatórios de mídia&quot; se estiver definido, ou que retorne ao tipo de dados &quot;Mídia&quot; antigo se o tipo de dados &quot;Detalhes de relatórios de mídia&quot; não estiver definido.

### Migrar campos derivados

Para migrar campos derivados para o novo tipo de dados:

1. Localize todos os campos derivados usando o tipo de dados obsoleto &quot;Mídia&quot;. Todos esses são campos derivados que contêm campos para os quais o caminho começa com `media.mediaTimed`.

1. Substitua todos os campos antigos no campo derivado pelo novo campo correspondente de &quot;Detalhes de relatórios de mídia&quot;.

Consulte o parâmetro [ID de Conteúdo](/help/reporting/dimensions/content.md) e o restante das variáveis de mídia de streaming documentadas em [Serviços de mídia de streaming](/help/media-overview.md) para mapear entre os campos antigos e os novos campos. O caminho de campo antigo é encontrado na propriedade &quot;Caminho do campo XDM&quot;, enquanto o novo caminho de campo é encontrado na propriedade &quot;Caminho do campo XDM do relatório&quot;.

![Caminhos antigos e novos do campo XDM](../../assets/field-paths-updated.jpeg)

## Exemplo

Para facilitar o cumprimento das diretrizes de migração, considere o exemplo a seguir que contém uma visualização de dados com campos do tipo de dados obsoleto antigo &quot;Mídia&quot;. Nessa visualização de dados, é necessário adicionar os novos campos correspondentes.

### Atualizar a visualização de dados

Você pode usar qualquer uma das seguintes opções para atualizar a visualização de dados:

#### Opção 1

1. Localize uma métrica ou uma dimensão que esteja usando o campo antigo do tipo de dados obsoleto.

   ![Caminho de campo antigo na exibição de dados](../../assets/old-field-data-view.jpeg)

1. Verifique o novo campo correspondente no artigo [Chapter offset](/help/reporting/dimensions/chapter-offset.md).

1. Localize o novo campo correspondente na visualização de dados.

   ![Novo caminho de campo na exibição de dados](../../assets/new-field-data-view.jpeg)

1. Arraste o novo campo para a métrica ou dimensão.

1. Repita esse processo para todas as métricas e dimensões que usam campos do tipo de dados obsoleto &quot;Mídia&quot;.

#### Opção 2

Essa opção cria um campo derivado que seleciona o valor do campo antigo ou o valor do novo campo com base no qual existe para um evento específico. Esse campo derivado substitui o tipo de dados antigo &quot;Mídia&quot; em qualquer projeto em que estiver sendo usado.

Se você quiser criar um campo derivado para o &quot;Nome do capítulo&quot; que usa o novo tipo de dados &quot;Detalhes de relatórios de mídia&quot;, se estiver definido, ou que retorna ao tipo de dados &quot;Mídia&quot; antigo, se o tipo de dados &quot;Detalhes de relatórios de mídia&quot; não estiver definido:

1. Arraste uma cláusula &quot;Case When&quot; para os campos derivados.

   ![Personalizar o novo campo para criar uma visualização de dados](../../assets/create-derived-field2.jpeg)

1. Preencha a cláusula **[!UICONTROL If]** usando o valor do **Caminho do Campo XDM do Relatório**, conforme mostrado na página [Nome do capítulo](/help/reporting/dimensions/chapter-name.md).

   ![Nome do capítulo](../../assets/chapter-name.jpeg)

   ![Nome do capítulo](../../assets/chapter-name2.jpeg)

   ![Condição de campo derivada](../../assets/derived-field-condition.jpeg)

   ![Nome do capítulo de campo derivado](../../assets/derived-field-chapter-name.jpeg)

1. Preencha o valor de fallback usando o campo antigo do tipo de dados obsoleto &quot;Mídia&quot;.

   ![Valor de fallback](../../assets/fallback-value.jpeg)

   ![Valor de fallback](../../assets/fallback-value2.jpeg)

   Essa é a definição final do campo derivado.

   ![Campo derivado concluído](../../assets/derived-field-complete.jpeg)

1. Para atualizar os campos derivados, localize um campo derivado que esteja usando os campos obsoletos antigos (caminho que começa com `media.mediaTimed`).

   ![campo derivado](../../assets/old-derived-field.jpeg)

1. Passe o mouse sobre o campo derivado que você deseja atualizar e selecione o ícone **[!UICONTROL Editar]**.

1. Localize todos os campos do tipo de dados antigo (caminho que começa com `media.mediaTimed`) e substitua-os pelo novo campo correspondente.

   ![Localizar campo com tipo de dados antigo](../../assets/locate-fields-with-old-datatype.jpeg)

1. Verifique o novo campo correspondente no artigo [Nome do conteúdo](/help/reporting/dimensions/content-name.md).

1. Substitua o campo antigo pelo novo campo.

   ![Novo campo](../../assets/derived-field-new.jpeg)

1. Repita esse processo para todos os campos derivados usando campos do tipo de dados obsoleto antigo &quot;Mídia&quot;.

   A migração da configuração do CJA foi concluída.
