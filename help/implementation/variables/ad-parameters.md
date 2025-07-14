---
title: Parâmetros de anúncio
description: Saiba mais sobre parâmetros de anúncios, incluindo a implementação, rede e variáveis de relatório para dados de vídeo de anúncio.
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 89%

---

# Parâmetros de anúncio {#ad-parameters}

Este tópico apresenta uma lista de dados de anúncios de vídeo, incluindo valores de dados de contexto, que a Adobe coleta por meio das variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação.
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de vídeo.
   * *Tipo* - Especifica o tipo da variável a ser definida, a string ou o número.
   * *Enviado com* - Indica quando os dados são enviados: *Início da mídia* é a chamada do Analytics enviada no início da mídia, *Início do anúncio* é a chamada do Analytics enviada no início do anúncio, e assim por diante; as chamadas de *Fechamento* são as chamadas compiladas do Analytics enviadas diretamente do servidor do heartbeat para o servidor da Analytics no final da sessão de mídia, ou no final do anúncio, do capítulo, etc. As chamadas de fechamento não estão disponíveis nas chamadas do pacote de rede.
   * *Versão mín. do SDK* - Indica qual versão do SDK você precisaria para acessar o parâmetro.
   * *Valor de exemplo* - Fornece exemplo de uso comum de variável.
* **Parâmetros de rede:** exibe os valores passados para os servidores do Adobe Analytics ou Heartbeat. Esta coluna mostra os nomes dos parâmetros que são vistos nas chamadas de rede geradas pelos SDKs do Adobe Media.
* **Relatórios:** informações sobre como visualizar e analisar os dados do vídeo.
   * *Disponível* - Indica se os dados estão disponíveis no relatórios por padrão (*Sim*) ou se exigem configuração personalizada (*Personalizado*)
   * *Variável reservada* - Indica se os dados são capturados como um evento, eVar, prop ou classificação em uma variável reservada.
   * *Nome do relatório* - Nome do relatório do Adobe Analytics para a variável
   * *Dados de contexto* - Nome dos dados de contexto do Adobe Analytics passados para o servidor de relatórios e usados nas regras de processamento.
   * *Feed de dados* - Nome da coluna para variável encontrada nos feeds de dados da sequência de cliques ou transmissão ao vivo.
   * *Audience Manager* - Nome da característica encontrada no Adobe Audience Manager

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo que esteja
>>descrita em Relatório/variável reservada como “classificação”.
>>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento
>>de mídia. De tempos em tempos, a Adobe adiciona novas propriedades e, quando isso ocorre,
>>os clientes devem reativar seus conjuntos de relatórios para obter acesso a novas propriedades
>>de mídia. Durante o processo de atualização, a Adobe determina se as
>>classificações são ativadas verificando os nomes das variáveis. Se alguma delas
>>estiver ausente, a Adobe adicionará novamente as que estiverem faltando.

## Dados de vídeo do anúncio {#ad-video-data}

### ID do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.id </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any  </li> <li> **Valor de exemplo:**<br/> “2125” </li><li> **Descrição:**<br/> ID do anúncio. (Qualquer combinação de número inteiro e/ou letra)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Heartbeat:**<br/> (<code>s:asset:ad_id</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> On VISIT </li> <li> **Nome do relatório:**<br/> Ad </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>name) </li> <li> **Feed de dados:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference._id </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.name </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



### Anúncio na posição do pod

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.podPosition </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 1 </li><li> **Descrição:**<br/> A posição (índice) do anúncio dentro do ad break principal. O primeiro anúncio tem índice 0, o segundo anúncio tem índice 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_position</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Ad In Pod Position </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Feed de dados:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.index </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.podPosition </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.podPosition </li> </ul> |



### Duração do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.length </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Valor de exemplo:**<br/> “15”  </li><li> **Descrição:**<br/> Comprimento do anúncio de vídeo em segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Heartbeat:**<br/> (<code>l:asset:ad_length</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar e classification </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Ad Length e Ad Length (variável) </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>length) </li> <li> **Feed de dados:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.<br/>_xmpDM.duration </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.length </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### Nome do reprodutor do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.playerName </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> “Freewheel” </li><li> **Descrição:**<br/> O nome do reprodutor responsável pela renderização do anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (<code>s:sp:player_name</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Ad Player Name </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Feed de dados:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.playerName </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### Nome do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.podFriendlyName </li> <li> **Obrigatório:**<br/> SDK: Sim; API: Não. </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> “antes da exibição” </li><li> **Descrição:**<br/> O nome amigável do Ad Break.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_name</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Pod Name </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.<br/>adBreak._dc.title </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### Índice de ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave de API:**<br/> media.ad.podIndex </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 1 </li><li> **Descrição:**<br/> O índice do ad break dentro do conteúdo que começa em 1. Essa propriedade é usada **somente** pelo SDK do Media para gerar a ID do pod.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/> Não </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> N/D </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.index </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### Posição do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.podSecond </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 90 </li><li> **Descrição:**<br/> O deslocamento do ad break no conteúdo, em segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat:**<br/> (<code>l:asset:pod_offset</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Pod Position </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.adBreak.<br/>offset </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingPodDetails.<br/>offset </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingPodDetails.<br/>offset </li> </ul> |



### ID do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (<code>s:asset:pod_id</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Pod de anúncios </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>pod) </li> <li> **Feed de dados:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetViewDetails.adBreak._id </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingPodDetails.<br/>ID </li> </ul> |



### Nome do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/> media.ad.name </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/> “Ford F-150” </li><li> **Descrição:**<br/> Nome amigável do anúncio.  Nos relatórios, o “Ad Name” é a classificação e o “Ad Name (variable)” é a eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (<code>s:asset:ad_name</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar e classification </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Ad Name e Ad Name (variable) </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Feed de dados:**<br/> videoadname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference._dc.title </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.friendlyName </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.friendlyName </li> </ul> |



## Metadados de publicidade padrão {#standard-ad-metadata}

### Anunciante

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> ADVERTISER </li> <li> **Chave da API:**<br/> media.ad.advertiser </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/> Empresa/marca cujo produto está em destaque no anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Heartbeat:**<br/> (<code>s:meta:</code><br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> <i>Anunciante </i> </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Feed de dados:**<br/> videoadadvertiser </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.advertiser </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.advertiser </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.advertiser </li> </ul> |



### ID da campanha

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> CAMPAIGN_ID </li> <li> **Chave da API:**<br/> media.ad.campaignId </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> Número inteiro ou nome (sequência de caracteres).  </li><li> **Descrição:**<br/> A ID da campanha publicitária.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Heartbeat:**<br/> (<code>s:meta:</code><br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> <i>ID da campanha </i> </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Feed de dados:**<br/> videoadcampaign </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.campaign </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### ID de criação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> CREATIVE_ID </li> <li> **Chave da API:**<br/> media.ad.creativeId </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> Número inteiro ou nome (sequência de caracteres).  </li><li> **Descrição:**<br/> A ID da campanha criativa.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **Heartbeat:**<br/> (<code>s:meta:</code><br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> <i>ID de criação </i> </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>creative) </li> <li> **Feed de dados:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.creativeID </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### ID do site

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> SITE_ID </li> <li> **Chave da API:**<br/> media.ad.siteId </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/> A ID do site do anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Heartbeat:**<br/> (<code>s:meta:</code><br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>site) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.siteID </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### URL da arte

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> CREATIVE_URL </li> <li> **Chave da API:**<br/> media.ad.creativeURL </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/> URL da campanha criativa.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> (<code>s:meta:&lt;c/ode><br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.creativeURL </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### ID de posicionamento

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> PLACEMENT_ID </li> <li> **Chave da API:**<br/> media.ad.placementId </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/> A ID de posicionamento do anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placement) </li> <li> **Heartbeat:**<br/> (<code>s:meta:</code><br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>placement) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.adAssetReference.placementID </li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## Métricas de publicidade {#ad-metrics}

### Início do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início do anúncio </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li><li> **Descrição:**<br/> Número de anúncios de vídeo iniciados.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>view) </li> <li> **Heartbeat:**<br/> (<code>s:event:type=start</code>)<br/> (<code>s:asset:type=ad<code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Ad Starts </li> <li> **Feed de dados:**<br/> videoadstart </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.impressions.value > 0 => &quot;TRUE&quot; </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### Anúncio concluído

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li><li> **Descrição:**<br/> Número de conclusões de anúncios de vídeo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (<code>s:event:type=complete</code>)<br/> (<code>s:asset:type=ad</code>)  </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Ad Completes </li> <li> **Feed de dados:**<br/> videoadcomplete </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.completes.value > 0 => &quot;TRUE&quot; </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### Tempo gasto com anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 15 </li><li> **Descrição:**<br/> A quantidade total de tempo, em segundos, gasta assistindo ao anúncio (ou seja, o número de segundos reproduzidos).  O valor será exibido no formato de hora (<code>HH:MM:SS</code>) no Analysis Workspace e no Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Tempo gasto com anuncio </li> <li> **Feed de dados:**<br/> videoadtime </li> <li> **Dados de contexto:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/> advertising.timePlayed.value </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.advertisingDetails.<br/>timePlayed </li> </ul> |



## APIs relacionadas {#section_Related_APIs}

### createAdObject APIs:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject APIs:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig APIs:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
