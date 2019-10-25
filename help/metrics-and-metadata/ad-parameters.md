---
seo-title: Parâmetros de anúncio
title: Parâmetros de anúncio
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Parâmetros de anúncio{#ad-parameters}

Este tópico apresenta uma lista de dados de anúncios de vídeo, incluindo valores de dados de contexto, que a Adobe coleta por meio das variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de vídeo.
   * *Tipo* - Especifica o tipo de variável a ser definida: sequência de caracteres ou número.
   * *Enviado com* - Indica quando os dados são enviados: O *Media Start* é a chamada do Analytics enviada no início da mídia, o *Ad Start* é a chamada do Analytics enviada no início do anúncio e assim por diante; as chamadas de *Fechamento* são as chamadas de análise compiladas enviadas diretamente do servidor de pulsação para o servidor de análise no final da sessão de mídia, ou no final do anúncio, capítulo etc. As chamadas de fechamento não estão disponíveis nas chamadas de pacotes de rede.
   * *Versão mín. do SDK* - Indica a versão do SDK necessária para acessar o parâmetro.
   * *Exemplo de valor* - Fornece exemplo de uso comum da variável.
* **Parâmetros de rede:** exibe os valores enviados ao servidor do Adobe Analytics ou do Heartbeats. Essa coluna mostra os nomes dos parâmetros visualizados nas chamadas de rede geradas pelos SDKs do Adobe Media.
* **Relatórios:** informações sobre como visualizar e analisar os dados de vídeo.
   * *Disponível* - Indica se os dados estão disponíveis nos relatórios por padrão (*Sim*) ou exigem configuração personalizada (*Personalizado*)
   * *Variável reservada* - Indica se os dados são capturados como um evento, eVar, prop ou classificação em uma variável reservada.
   * *Nome do relatório* - Nome do relatório do Adobe Analytics para a variável
   * *Dados de contexto* - Nome dos dados de contexto do Adobe Analytics transmitidos ao servidor de relatórios e usados nas regras de processamento.
   * *Feed de dados* - Nome da coluna para variáveis encontradas em feeds de dados de Sequência de cliques ou em tempo real
   * *Audience Manager* - Nome do recurso encontrado no Adobe Audience Manager

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo que esteja
>descrita em Relatório/variável reservada como "classificação".
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para mídia
>rastreamento. De tempos em tempos, a Adobe adiciona novas propriedades e, quando isso ocorre,
>os clientes devem reativar seus conjuntos de relatórios para obter acesso à nova mídia
>propriedades. Durante o processo de atualização, a Adobe determina se a variável
>as classificações são ativadas verificando os nomes das variáveis. Se algum de
>estiverem ausentes, a Adobe adicionará os que estiverem faltando novamente.

## Dados de vídeo do anúncio {#ad-video-data}

### ID do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.id </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any  </li> <li> ****<br/> Valor da amostra: "2125" </li><li> **Descrição:**<br/>ID do anúncio. (Qualquer combinação de número inteiro e/ou letra)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>name) </li> <li> ****<br/> Pulsação: (s:asset:ad_id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On VISIT </li> <li> **Nome do relatório:**<br/>Ad </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>name) </li> <li> **Feed de dados:**<br/>videoad </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Anúncio na posição do pod

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podPosition </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 1 </li><li> **Descrição:**<br/>A posição (índice) do anúncio dentro da quebra do anúncio pai. O primeiro anúncio tem índice 0, o segundo anúncio tem índice 1, etc.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podPosition) </li> <li> ****<br/> Pulsação: (s:asset:pod_position) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad In Pod Position </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>podPosition) </li> <li> **Feed de dados:**<br/>videoadinpod </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Duração do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.length </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> ****<br/> Valor da amostra: "15"  </li><li> **Descrição:**<br/>duração do anúncio de vídeo em segundos.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>length) </li> <li> ****<br/> Pulsação: (l:asset:ad_length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar e classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad Length e Ad Length (variável) </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>length) </li> <li> **Feed de dados:**<br/>videoadlength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nome do player do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.playerName </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: "Forma livre" </li><li> **Descrição:**<br/>O nome do player responsável pela renderização do anúncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>playerName) </li> <li> ****<br/> Pulsação: (s:sp:player_name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad Player Name </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>playerName) </li> <li> **Feed de dados:**<br/>videoadplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nome do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podFriendlyName </li> <li> ****<br/> Obrigatório: SDK:Sim; API: Não. </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: "pre-roll" </li><li> **Descrição:**<br/>o nome amigável da quebra de anúncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podFriendlyName) </li> <li> ****<br/> Pulsação: (s:asset:pod_name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Pod Name </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>podFriendlyName) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Índice de ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podPosition </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 1 </li><li> **Descrição:**<br/>O índice de quebra de anúncio dentro do conteúdo, começando em 1. Essa propriedade é usada **somente** pelo SDK do Media para gerar a ID do pod.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/>não </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>N/A </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posição do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podSecond </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 90 </li><li> **Descrição:**<br/>O deslocamento do intervalo do anúncio dentro do conteúdo, em segundos.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podSecond) </li> <li> ****<br/> Pulsação: (l:asset:pod_offset) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Pod Position </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>podSecond) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>pod) </li> <li> ****<br/> Pulsação: (s:asset:pod_id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Pod de anúncios </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>pod) </li> <li> **Feed de dados:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nome do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.name </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> ****<br/> Valor da amostra: "Ford F-150" </li><li> **Descrição: nome**<br/>amigável do anúncio.  Nos relatórios, o "Ad Name" é a classificação e o "Ad Name (variable)" é a eVar.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>friendlyName) </li> <li> ****<br/> Pulsação: (s:asset:ad_name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar e classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad Name e Ad Name (variable) </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>friendlyName) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Metadados de publicidade padrão {#standard-ad-metadata}

### Anunciante

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>ADVERTISER </li> <li> **Chave da API:**<br/>media.ad.advertiser </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>Empresa/Marca cujo produto aparece no anúncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>anunciante) </li> <li> ****<br/> Pulsação: (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i>Anunciante </i> </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>anunciante) </li> <li> **Feed de dados:**<br/>videoadvertiser </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID da campanha

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>CAMPAIGN_ID </li> <li> **Chave da API:**<br/>media.ad.campaignId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: Número inteiro ou nome (string).  </li><li> **Descrição:**<br/>ID da campanha de publicidade.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>campaign) </li> <li> ****<br/> Pulsação: (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i>ID da campanha </i> </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>campaign) </li> <li> **Feed de dados:**<br/>videocampaign </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### ID de criação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>CREATIVE_ID </li> <li> **Chave da API:**<br/>media.ad.creativeId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: Número inteiro ou nome (string).  </li><li> **Descrição:**<br/>ID do anúncio criativo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>criativo) </li> <li> ****<br/> Pulsação: (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i>ID de criação </i> </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>criativo) </li> <li> **Feed de dados:**<br/>adclassificationcreative </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID do site

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SITE_ID </li> <li> **Chave da API:**<br/>media.ad.siteId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>ID do site do anúncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>site) </li> <li> ****<br/> Pulsação: (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i> </i> </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>site) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL da arte

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>CREATIVE_URL </li> <li> **Chave da API:**<br/>media.ad.creativeURL </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>URL do anúncio criativo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>creativeURL) </li> <li> ****<br/> Pulsação: (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i> </i> </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>creativeURL) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### ID de posicionamento

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>PLACEMENT_ID </li> <li> **Chave da API:**<br/>media.ad.placementId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:ID de**<br/>posicionamento do anúncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>colocação) </li> <li> ****<br/> Pulsação: (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i> </i> </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>colocação) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Métricas de publicidade {#ad-metrics}

### Início do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Início do anúncio </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>Número de inicializações do anúncio de vídeo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>exibir) </li> <li> ****<br/> Pulsação:  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Ad Starts </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>exibir) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Anúncio completo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>número de conclusões do anúncio de vídeo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>concluído) </li> <li> ****<br/> Pulsação: (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Ad Completes </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>concluído) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Tempo gasto com anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 15 </li><li> **Descrição:**<br/>O tempo total, em segundos, gasto assistindo ao anúncio (isto é, o número de segundos reproduzidos).  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Tempo gasto com anuncio </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Dados de contexto: (a.media.ad.<br/>timePlayed) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## APIs relacionadas {#section_Related_APIs}

### createAdObject APIs:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject APIs:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### APIs MediaHeartbeatConfig:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* IOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

