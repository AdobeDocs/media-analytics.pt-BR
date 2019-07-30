---
seo-title: Parâmetros de anúncio
title: Parâmetros de anúncio
uuid: 92 cd 7 f 97-bb 5 a -4 de 6-8946-453 d 30271 d 0 f
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Parâmetros de anúncio{#ad-parameters}

Este tópico apresenta uma lista de dados de anúncios de vídeo, incluindo valores de dados de contexto, que a Adobe coleta por meio das variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de vídeo.
   * *Tipo* - Especifica o tipo de variável a ser definida: sequência de caracteres ou número.
   * *Enviado com* - Indica quando os dados são enviados: *O Media Start* é a chamada de análise enviada no início da mídia, *Ad Start* é a chamada de análise enviada no início do anúncio e assim por diante; *as* Chamadas Fechar são chamadas de análise compiladas enviadas diretamente do servidor de pulsação para o servidor do Analytics no final da sessão de mídia, ou o fim do anúncio, capítulo etc. As chamadas de fechar não estão disponíveis em chamadas de pacotes de rede.
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
>Não altere os nomes de classificação de variáveis listadas abaixo que sejam
>descrito em Relatório/Variável reservada como "classificação".
>As classificações de mídia são definidas quando um conjunto de relatórios está habilitado para mídia
>rastreamento. A Adobe adiciona novas propriedades ocasionalmente, quando isso ocorre,
>os clientes devem reativar seus conjuntos de relatórios para obter acesso à nova mídia
>propriedades. Durante o processo de atualização, a Adobe determina se a variável
>as classificações são ativadas verificando os nomes das variáveis. Se qualquer um de
>estiverem ausentes, a Adobe adicionará as ausentes novamente.

## Dados de vídeo do anúncio {#section_hq3_nbv_51b}

### ID do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.id </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any  </li> <li> **Valor da amostra:**<br/> " 2125 " </li><li> **Descrição:**<br/>ID do anúncio. (Qualquer combinação de número inteiro e/ou letra)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>name) </li> <li> **Heartbeat:**<br/> (s: ativo: ad_ id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On VISIT </li> <li> **Nome do relatório:**<br/>Ad </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>name) </li> <li> **Feed de dados:**<br/>videoad </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.name) </li> </ul> |



### Anúncio na posição do pod

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podPosition </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 1 </li><li> **Descrição:**<br/>A posição (índice) do anúncio no intervalo comercial pai. O primeiro anúncio tem índice 0, o segundo anúncio tem índice 1, etc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Podposition) </li> <li> **Heartbeat:**<br/> (s: ativo: pod_ position) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad In Pod Position </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>Podposition) </li> <li> **Feed de dados:**<br/>videoadinpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Duração do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.length </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Valor da amostra:**<br/> " 15 "  </li><li> **Descrição:**<br/>Duração do anúncio de vídeo em segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>length) </li> <li> **Heartbeat:**<br/> (l: ativo: ad_ length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar e classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad Length e Ad Length (variável) </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>length) </li> <li> **Feed de dados:**<br/>videoadlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nome do player do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.playerName </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> " Roda livre " </li><li> **Descrição:**<br/>O nome do player responsável pela renderização do anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad Player Name </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>playerName) </li> <li> **Feed de dados:**<br/>videoadplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nome do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podFriendlyName </li> <li> **Obrigatório:**<br/> SDK: Sim; API: Não. </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> " pre-roll " </li><li> **Descrição:**<br/>O nome amigável do anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Podfriendlyname) </li> <li> **Heartbeat:**<br/> (s: ativo: pod_ name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Pod Name </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>Podfriendlyname) </li> <li> **Feed de dados:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Índice de ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podPosition </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 1 </li><li> **Descrição:**<br/>O índice da quebra do anúncio no conteúdo que começa em 1. Essa propriedade é usada **somente** pelo SDK do Media para gerar a ID do pod.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/>não </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>N/A </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posição do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.podSecond </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 90 </li><li> **Descrição:**<br/>O deslocamento da quebra do anúncio dentro do conteúdo, em segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Podsecond) </li> <li> **Heartbeat:**<br/> (l: ativo: pod_ offset) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Pod Position </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>Podsecond) </li> <li> **Feed de dados:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID do ad break

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> c 4 a 577424 c 84067899 b 807 c 76722 d 495_ 1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (s: ativo: pod_ id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Pod de anúncios </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>pod) </li> <li> **Feed de dados:**<br/>videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nome do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chave da API:**<br/>media.ad.name </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Valor da amostra:**<br/> " Ford F -150 " </li><li> **Descrição:**<br/>Nome amigável do anúncio. Nos relatórios, o "Ad Name" é a classificação e o "Ad Name (variable)" é a eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Friendlyname) </li> <li> **Heartbeat:**<br/> (s: ativo: ad_ name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar e classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Ad Name e Ad Name (variable) </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>Friendlyname) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Metadados de publicidade padrão {#section_EFB805867916411E84DE1BA5A183D86A}

### Anunciante

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>ADVERTISER </li> <li> **Chave da API:**<br/>media.ad.advertiser </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>Empresa/Marca cujo produto é destacado no anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>advertiser) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ad vertiser) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i>Anunciante </i> </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>advertiser) </li> <li> **Feed de dados:**<br/>videoadvertiser </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID da campanha

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>CAMPAIGN_ID </li> <li> **Chave da API:**<br/>media.ad.campaignId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> Número inteiro ou nome (string).  </li><li> **Descrição:**<br/>ID da campanha publicitária.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>campaign) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ca mpaign) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i>ID da campanha </i> </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>campaign) </li> <li> **Feed de dados:**<br/>videocampaign </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### ID de criação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>CREATIVE_ID </li> <li> **Chave da API:**<br/>media.ad.creativeId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> Número inteiro ou nome (string).  </li><li> **Descrição:**<br/>ID da publicidade anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>creative) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr eative) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i>ID de criação </i> </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>creative) </li> <li> **Feed de dados:**<br/>adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID do site

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SITE_ID </li> <li> **Chave da API:**<br/>media.ad.siteId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>ID do site de publicidade.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>site) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.si te) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i> </i> </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>site) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL da arte

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>CREATIVE_URL </li> <li> **Chave da API:**<br/>media.ad.creativeURL </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>URL da publicidade anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Creativeurl) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr Eativeurl) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i> </i> </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>Creativeurl) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### ID de posicionamento

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>PLACEMENT_ID </li> <li> **Chave da API:**<br/>media.ad.placementId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Start, Ad Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>ID de posicionamento do anúncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>placement) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.pl acement) </li> </ul> | <ul> <li> **Disponível:**<br/> <i>Usar regra de processamento personalizada </i> </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> <i> </i> </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>placement) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Métricas de publicidade {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Início do anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Início do anúncio </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>Número de inicializações do anúncio de vídeo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>exibir) </li> <li> **Heartbeat:**<br/> (s: evento: type = start)<br/> (s: ativo: type = ad) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Ad Starts </li> <li> **Feed de dados:**<br/>videoadstart </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>exibir) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.view) </li> </ul> |



### Anúncio completo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>Número de conclusões de vídeos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>concluído) </li> <li> **Heartbeat:**<br/> (s: evento: type = complete)<br/> (s: ativo: type = ad)  </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Ad Completes </li> <li> **Feed de dados:**<br/>videoadcomplete </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>concluído) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Tempo gasto com anúncio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/>Ad Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 15 </li><li> **Descrição:**<br/>O tempo total, em segundos, gasto com o anúncio (ou seja, o número de segundos reproduzidos). O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. ad.<br/>Timeplayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Tempo gasto com anuncio </li> <li> **Feed de dados:**<br/>videoadtime </li> <li> **Dados de contexto:**<br/> (a. media. ad.<br/>Timeplayed) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### Apis createadobject:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### Apis do createadbreakobject:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### Apis mediaheartbeatconfig:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* IOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

