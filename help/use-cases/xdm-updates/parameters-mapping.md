---
title: Migrar públicos-alvo para o novo tipo de dados Adobe Analytics para mídia de streaming
description: Saiba como migrar públicos-alvo para o novo tipo de dados Adobe Analytics para mídia de streaming
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
source-git-commit: 61e5279e6d53b18955424e76d05d440b83dae07e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 44%

---

# Mapeamento de parâmetros do Media Analytics para Adobe Experience Platform e Customer Journey Analytics

Este documento fornece uma lista abrangente de todos os parâmetros do Media Analytics utilizados no Adobe Experience Platform e no Customer Journey Analytics. Ele tem como objetivo oferecer suporte à integração de dados importados do Adobe Analytics com a Platform por meio do [Conector Source do Analytics](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics) ou do [Conector Source do Analytics para Classificações](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/classifications), mapeando cada parâmetro para o caminho do campo XDM correspondente.

## Variáveis reservadas do Media Analytics

Para todas as variáveis reservadas do Media Analytics, os dados assimilados do Adobe Analytics na AEP até (e incluindo) maio de 2025 podem ser encontrados no &quot;Caminho do campo XDM atual&quot; apontado nas tabelas abaixo.

Como as equipes do Media Analytics e do ADC estão trabalhando atualmente para a migração completa para o &quot;Caminho do campo XDM do relatório&quot;, uma comunicação oficial será compartilhada assim que a migração for concluída e o &quot;Caminho do campo XDM do relatório&quot; estiver disponível para uso.

## Parâmetros de streaming de mídia

| Nome do campo | Caminho atual do campo XDM (obsoleto) | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Tipo de fluxo | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimensão | Tipo de fluxo |                                                                       |
| ID de conteúdo | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimensão | ID de conteúdo |                                                                       |
| Comprimento do conteúdo | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimensão | Comprimento do conteúdo |                                                                       |
| Tipo de conteúdo | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimensão | Tipo de conteúdo |                                                                       |
| ID da sessão de mídia | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimensão | ID da sessão de mídia |                                                                       |
| Nome do reprodutor de conteúdo | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimensão | Nome do reprodutor de conteúdo |                                                                       |
| Canal de conteúdo | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimensão | Canal de conteúdo |                                                                       |
| Segmento de conteúdo | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimensão | Segmento de conteúdo |                                                                       |
| Nome do conteúdo | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimensão | Nome do conteúdo |                                                                       |
| Caminho do vídeo | *Não usado no AEP/CJA* |                                                   |           |                   | propriedade específica do Adobe Analytics |
| Programa | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimensão | Programa |                                                                       |
| Temporada | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimensão | Temporada |                                                                       |
| Episódio | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimensão | Episódio |                                                                       |
| Gênero | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimensão | não suportado | Usar campo mediaReporting |
| Rede | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimensão | Rede |                                                                       |
| Mostrar tipo | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimensão | Mostrar tipo |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimensão | MVPD |                                                                       |
| Autorizado | Não suportado | mediaReporting.sessionDetails.authorized | Dimensão | Autorizado |                                                                       |
| Faixa de horário | Não suportado | mediaReporting.sessionDetails.dayPart | Dimensão | Faixa de horário |                                                                       |
| Tipo de feed de mídia | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimensão | Tipo de feed de mídia |                                                                       |
| Artista | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimensão | Artista |                                                                       |
| Álbum | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimensão | Álbum |                                                                       |
| Rótulo | Não suportado | mediaReporting.sessionDetails.label | Dimensão | Rótulo |                                                                       |
| Autor | Não suportado | mediaReporting.sessionDetails.author | Dimensão | Autor |                                                                       |
| Estação | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | Dimensão | Estação |                                                                       |
| Editor | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimensão | Editor |                                                                       |
| Inícios da mídia | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Métrica | Inícios da mídia |                                                                       |
| Início do conteúdo | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Métrica | Início do conteúdo |                                                                       |
| Conteúdo concluído | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Métrica | Conteúdo concluído |                                                                       |
| Tempo gasto no conteúdo | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Métrica | Tempo gasto no conteúdo |                                                                       |
| Tempo gasto com a mídia | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Métrica | Tempo gasto com a mídia |                                                                       |
| Tempo de reprodução exclusivo | Não suportado | mediaReporting.sessionDetails.uniqueTimePlayed | Métrica | Tempo de reprodução exclusivo |                                                                       |
| Marcador de progresso 10% | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Métrica | Marcador de progresso 10% |                                                                       |
| Marcador de progresso 25% | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Métrica | Marcador de progresso 25% |                                                                       |
| Marcador de progresso 50% | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Métrica | Marcador de progresso 50% |                                                                       |
| Marcador de progresso 75% | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Métrica | Marcador de progresso 75% |                                                                       |
| Marcador de progresso 95% | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Métrica | Marcador de progresso 95% |                                                                       |
| Público-alvo médio por minuto | Não suportado | mediaReporting.sessionDetails.averageMinuteAudience | Métrica | Público-alvo médio por minuto |                                                                  |
| Segundos desde a última chamada | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Métrica | Segundos desde a última chamada |                                                              |
| Fluxos afetados por interrupções | Não suportado | mediaReporting.sessionDetails.hasPauseImpactedStreams | Métrica | Fluxos afetados por interrupções | cobrimos mediaTimed calculando esse valor a partir de outros eventos |
| Eventos interrompidos | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Métrica | Eventos interrompidos |                                                                       |
| Duração total da pausa | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Métrica | Duração total da pausa |                                                                       |
| Continuação do conteúdo | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Métrica | Continuação do conteúdo |                                                                       |
| Visualizações do segmento de conteúdo | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Métrica | Visualizações do segmento de conteúdo |                                                                     |

{style="table-layout:auto"}

## Atualização dos parâmetros de estado do player

| Nome do campo | Caminho atual do campo XDM (obsoleto) | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Fluxos afetados pelos Estados do player | Não suportado | mediaReporting.states.isSet | Métrica | não suportado | usar campo mediaReporting |
| Contagens de estados do player | Não suportado | mediaReporting.states.count | Métrica | não suportado | usar campo mediaReporting |
| Duração total dos estados do player | Não suportado | mediaReporting.states.time | Métrica | não suportado | usar campo mediaReporting |
| Nome do estado do player | Não suportado | mediaReporting.states.name | Dimensão | não suportado | usar campo mediaReporting |

{style="table-layout:auto"}

## Parâmetros de capítulo

| Nome do campo | Caminho atual do campo XDM (obsoleto) | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Capítulo | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimensão | Capítulo |           |
| Início do capítulo | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Métrica | Início do capítulo |           |
| Capítulo concluído | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Métrica | Capítulo concluído |          |
| Tempo gasto com capítulo | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Métrica | Tempo gasto com capítulo |        |

{style="table-layout:auto"}

## Parâmetros de anúncio 

| Nome do campo | Caminho atual do campo XDM (obsoleto) | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| ID do anúncio | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimensão | ID do anúncio |           |
| Anúncio na posição do pod | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimensão | Anúncio na posição do pod |     |
| Duração do anúncio | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Métrica | Duração do anúncio |           |
| Nome do reprodutor do anúncio | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimensão | Nome do reprodutor do anúncio |           |
| ID do ad break | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimensão | ID do ad break |           |
| Nome do anúncio | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimensão | Nome do anúncio |           |
| Anunciante | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimensão | Anunciante |           |
| ID da campanha | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimensão | ID da campanha |           |
| Início do anúncio | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Métrica | Início do anúncio |           |
| Anúncio concluído | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Métrica | Anúncio concluído |           |
| Tempo gasto com anúncio | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Métrica | Tempo gasto com anúncio |           |

{style="table-layout:auto"}

## Parâmetros de qualidade

| Nome do campo | Caminho atual do campo XDM (obsoleto) | Caminho do campo XDM do relatório | Tipo de dados | Campos derivados | Notas |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Taxa média de bits | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Ambos | Taxa média de bits |           |
| Hora de início | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Ambos | Hora de início |           |
| Queda de quadros | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Ambos | Queda de quadros |           |
| Eventos de buffer | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Ambos | Eventos de buffer |           |
| Duração total do buffer | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Ambos | Duração total do buffer |     |
| Alterações da taxa de bits | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Ambos | Alterações da taxa de bits |         |
| Erros/Eventos de erro | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Ambos | Erros/Eventos de erro |  |
| IDs de erro do SDK do reprodutor | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimensão | não suportado | usar campo mediaReporting |
| IDs de erro externo | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimensão | não suportado | usar campo mediaReporting |
| Quedas antes do início | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Métrica | Quedas antes do início |     |
| Fluxos afetados pelo buffer | Não suportado | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Métrica | Fluxos afetados pelo buffer | calculado a partir de outros eventos |
| Fluxos afetados pela mudança na taxa de bits | Não suportado | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Métrica | Fluxos afetados pela mudança na taxa de bits | calculado a partir de outros eventos |
| Fluxos afetados por erros | Não suportado | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Métrica | Fluxos afetados por erros | calculado a partir de outros eventos |
| Fluxos afetados pela queda de quadros | Não suportado | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Métrica | Fluxos afetados pela queda de quadros | calculado a partir de outros eventos |

{style="table-layout:auto"}

## Classificações do Media Analytics

As classificações do Media Analytics são assimiladas na AEP por meio de um fluxo separado conhecido como ACDC. Cada grupo de classificação listado na tabela abaixo corresponde a um conjunto de dados exclusivo na AEP. No CJA, é necessário estabelecer uma conexão entre o conjunto de dados de eventos do Media Analytics e cada um dos conjuntos de dados de classificação.

### Conectar conjuntos de dados na Customer Journey Analytics

Para configurar a conexão no Customer Journey Analytics:

- Navegue até a guia **Conexões** e selecione **Criar nova conexão**.
- Na interface das Conexões, escolha **Adicionar conjuntos de dados** e localize o conjunto de dados de eventos do Media Analytics (usado para importar dados de mídia pelo ADC), juntamente com os quatro conjuntos de dados de classificação relevantes.

### Detalhes de configuração

Para cada conjunto de dados de pesquisa (conjunto de dados de classificação), configure da seguinte maneira:

- **conjunto de dados de vídeo**:
   - Chave: `_sandbox.key`
   - Chave correspondente: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Tipo de fonte de dados: `Web Data`

- **conjunto de dados de videoad**:
   - Chave: `_sandbox.key`
   - Chave correspondente: `Ad ID (advertising.adAssetReference._id)`
   - Tipo de fonte de dados: `Web Data`

- **conjunto de dados videoadpod**:
   - Chave: `_sandbox.key`
   - Chave correspondente: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Tipo de fonte de dados: `Web Data`

- **conjunto de dados videochapter**:
   - Chave: `_sandbox.key`
   - Chave correspondente: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Tipo de fonte de dados: `Web Data`

### Considerações sobre relatórios

Ao trabalhar com os conjuntos de dados de classificação durante os relatórios, faça referência aos caminhos de campo específicos da classificação (`ACDC XDM Path`) em vez dos campos XDM padrão do Media Analytics.

## Tabela de classificações

| Nome da classificação (grupo) | Nome do campo | Caminho XDM da ACDC |
|------------|----------|-------------|
| vídeo | Chave/ID do ativo | `<_sandbox>.key` |
| vídeo | Duração do vídeo | `<_sandbox>.video_length` |
| vídeo | Nome do vídeo | `<_sandbox>.video_name` |
| vídeo | ID do ativo | `<_sandbox>.asset_id` |
| vídeo | Data da primeira exibição | `<_sandbox>.first_air_date` |
| vídeo | Primeira data digital | `<_sandbox>.first_digital_date` |
| vídeo | Classificação de conteúdo | `<_sandbox>.content_rating` |
| vídeo | Originador | `<_sandbox>.originator` |
| videoad | Chave/ID do anúncio | `<_sandbox>.key` |
| videoad | Duração do anúncio | `<_sandbox>.ad_length` |
| videoad | Nome do anúncio | `<_sandbox>.ad_name` |
| videoad | ID de criação | `<_sandbox>.creative_id` |
| videoadpod | ID da chave/pod de anúncio | `<_sandbox>.key` |
| videoadpod | Posição do pod | `<_sandbox>.pod_position` |
| videoadpod | Nome do pod | `<_sandbox>.pod_name` |
| videochapter | Chave / Capítulo | `<_sandbox>.key` |
| videochapter | Extensão do capítulo | `<_sandbox>.chapter_length` |
| videochapter | Deslocamento do capítulo | `<_sandbox>.chapter_offset` |
| videochapter | Posição do capítulo | `<_sandbox>.chapter_position` |
| videochapter | Nome do capítulo | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Variáveis personalizadas do Media Analytics

No Adobe Analytics, as variáveis personalizadas são atribuídas a eventos ou eVars diferentes, dependendo das regras de implementação definidas em cada conjunto de relatórios. Como resultado, quando essas variáveis personalizadas são importadas para o Adobe Experience Platform (AEP), elas são mapeadas para caminhos XDM diferentes.

- Os eventos são armazenados no caminho:

  `_experience.analytics.event<x>to<y>.event<number>.value`

- As eVars são armazenadas no caminho:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

Em ambos os casos, o `<number>` corresponde ao evento específico ou ao número do eVar usado na configuração original do conjunto de relatórios do Adobe Analytics.

### Variáveis personalizadas

| Nome do campo | Caminho XDM | Tipo de dados |
|-------------|-------------|-----------|
| Sinalizador de mídia baixada | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Versão do SDK | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| Versão do VHL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| Formato de transmissão | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| Data da primeira exibição | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| Primeira data digital | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| Dados federados | `_experience.analytics.customDimensions.eVars.eVar<number>` e `_experience.analytics.event<x>to<y>.event<number>.value` | Ambos |
| Fluxos estimados | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Contagem de anúncios | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Contagem de capítulo | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| ID de criação | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| ID do site | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| URL da arte | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| ID de posicionamento | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensão |
| Quadros por segundo | `_experience.analytics.customDimensions.eVars.eVar<number>` e `_experience.analytics.event<x>to<y>.event<number>.value` | Ambos |
| IDs de erro do SDK do Media | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Fluxos afetados por bloqueios | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Eventos de paralisação | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |
| Duração total da paralisação | `_experience.analytics.event<x>to<y>.event<number>.value` | Métrica |

{style="table-layout:auto"}
