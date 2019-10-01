---
seo-title: Parâmetros de áudio e vídeo
title: Parâmetros de áudio e vídeo
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 89870fcf20bdfa75a178ffc2124498b94cabe4a7

---


# Parâmetros de áudio e vídeo{#audio-and-video-parameters}

>[!IMPORTANT]
>
>On February 7th, 2019, Adobe Analytics for Video and Audio released a metric name change. <i>Inicializações da mídia</i> agora será chamada <i>Inícios da mídia</i>. This change was made to reflect industry standards in metrics and reporting, and to make the metric easily identifiable in reporting.

>[!NOTE]
>
>Beginning on September 13th, 2018 a change was made to the labels for some dimensions, metrics, and reports, to allow for cross-content tracking of video and audio analytics. Os rótulos que mudaram incluem: *inicializações de vídeo* para *inicializações de mídia*, *duração do vídeo* para *duração do conteúdo* e *nome do vídeo* para *nome do conteúdo*. Os relatórios de vídeo nos Reports and Analytics foram atualizados para usar o nome “Mídia” no lugar de “Vídeo”. As mudanças nos rótulos não afetaram a coleção de dados nem os dados de histórico. Anote essas alterações caso precise usá-las no Report Builder ou em qualquer outra extração de dados externa automatizada que possa ser afetada por essa alteração.

Este tópico apresenta uma lista de dados de conteúdo de áudio e vídeo, incluindo valores de dados de contexto, que a Adobe coleta por meio das variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de áudio e vídeo.
   * *Tipo* - Especifica o tipo de variável a ser definida: sequência de caracteres ou número.
   * *Sent With* - Indicates when the data is sent: *Media Start* is the analytics call sent on media start, *Ad Start* is the analytics call sent on ad start, and so on; the *Close* calls are the compiled analytics calls sent directly from the heartbeat server to the analytics server at the end of the media session, or the end of the ad, chapter, etc. As chamadas de fechamento não estão disponíveis nas chamadas de pacotes de rede.
   * *Versão mín. do SDK* - Indica a versão do SDK necessária para acessar o parâmetro.
   * *Exemplo de valor* - Fornece exemplo de uso comum da variável.
* **Parâmetros de rede:** exibe os valores enviados ao servidor do Adobe Analytics ou do Heartbeats. Essa coluna mostra os nomes dos parâmetros visualizados nas chamadas de rede geradas pelos SDKs do Adobe Media.
* **Relatórios:** informações sobre como visualizar e analisar os dados de áudio e vídeo.
   * *Disponível* - Indica se os dados estão disponíveis nos relatórios por padrão (*Sim*) ou exigem configuração personalizada (*Personalizado*)
   * *Variável reservada* - Indica se os dados são capturados como um evento, eVar, prop ou classificação em uma variável reservada.
   * *Expiração* - Indica se os dados expiram após cada ocorrência ou visita.
   * *Nome do relatório* - Nome do relatório do Adobe Analytics para a variável
   * *Dados de contexto* - Nome dos dados de contexto do Adobe Analytics transmitidos ao servidor de relatórios e usados nas regras de processamento.
   * *Feed de dados* - Nome da coluna para variáveis encontradas em feeds de dados de Sequência de cliques ou em tempo real
   * *Audience Manager* - Nome do recurso encontrado no Adobe Audience Manager

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo descrita em Relatório/Variável reservada como "classificação".\
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe adicionará os que estiverem faltando novamente.

## Dados principais de áudio e vídeo {#section_y55_y1m_n1b}

### Tipo de fluxo {#stream-type}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chave de API:**<br/>media.streamType </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 2.2 <br/><br/>Available in [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Exemplo de valor:** <br/>"vídeo" </li> <li> **Description:**<br/> Identifies the stream type. Os valores válidos são “audio”, “video” e “all”.  <br/><br/>[Reporting Segments](/help/metrics-and-metadata/segments.md): <br/><br/>Media Stream Type: All - <br/>Segment all media stream data; Rule: Content (ID) exists <br/><br/>Media Stream Type: Audio - <br/>Segment all audio stream data; Rule: Content (ID) exists AND Media Stream Type = audio <br/><br/>Media Stream Type: "Video" - <br/>Segment all video stream data; Rule: Content (ID) exists AND Media Stream Type != audio <br/><br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.streamType) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On VISIT </li> <li> **Nome do relatório:**<br/>Content </li> <li> ****<br/> Dados de contexto: (a.media.streamType) </li> <li> **Feed de dados:** <br/>videostreamtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.id </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"4586695ABC" </li> <li>**Description:**<br/> Content ID of the content, which can be used to tie back to other industry / CMS IDs, equal to the last value of `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On VISIT </li> <li> **Nome do relatório:**<br/>Content </li> <li> ****<br/> Context Data: (a.media.name) </li> <li> **Feed de dados:**<br/>video </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duração de conteúdo (variável)

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.length </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: VOD: 128; Ao vivo: 86400; Linear: 1800. </li><li> **Description:**<br/> Clip Length/Runtime - This is the maximum length (or duration) of the content being consumed (in seconds). It equals the last value of `l:asset:length` from events of type Main. <br/>If  is not set, then the last value of  is used. `l:asset:length``l:asset:duration` <br/>Nos relatórios, a Duração do vídeo é a classificação e a Duração do vídeo (variável) é a eVAR.  <br/> **Importante:** esta propriedade é usada para calcular várias métricas, como as de acompanhamento de progresso e Público-alvo médio por minuto. Se isso não for definido ou não for maior que zero, essas métricas não estarão disponíveis.  Para Mídia em tempo real com duração desconhecida, o valor de 86400 é o padrão. <br/>Antes da versão 1.5.1, isso era `l:asset:duration`; depois de 1.5.1, é `l:asset:length.`<br/> **Data de lançamento: 13/09/18** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Pulsações: (l:asset:length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Duração do conteúdo (variável) </li> <li> ****<br/> Dados de contexto: (a.media.length) </li> <li> **Feed de dados:**<br/>videolength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duração do vídeo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.length </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: VOD: 128; Ao vivo: 86400; Linear: 1800. </li> <li> ****<br/> Descrição: Duração do clipe/Tempo de execução - é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. Nos relatórios, a Duração do vídeo é a classificação e a Duração do vídeo (variável) é a eVAR.  <br/> **Importante:** esta propriedade é usada para calcular várias métricas, como as de acompanhamento de progresso e Público-alvo médio por minuto. Se isso não for definido ou não for maior que zero, essas métricas não estarão disponíveis.  Para Mídia em tempo real com duração desconhecida, o valor de 86400 é o padrão. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Pulsações: (l:asset:length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Duração do vídeo </li> <li> ****<br/> Dados de contexto: (a.media.length) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.contentType </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres restrita </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"vod" </li> <li> ****<br/> Descrição: Valores disponíveis por tipo **de** fluxo: <br/> _Áudio:_ "song", "podcast", "audiobook", "radio" <br/> __ Vídeo: "VoD", "Ao vivo", "Linear", "UGC", "DVoD" <br/> Os clientes podem fornecer valores personalizados para esse parâmetro. Isso é igual a `s:stream:type.` Se isso não for definido, isso é igual a `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.contentType) </li> <li> ****<br/> Pulsações: (s:stream:type) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Tipo de conteúdo </li> <li> ****<br/> Dados de contexto: (a.contentType) </li> <li> **Feed de dados:**<br/>videocontenttype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID da sessão de mídia

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/>obtida no back-end </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.8 </li> <li> ****<br/> Valor da amostra: 1482236761294786918253 </li> <li> **Description:**<br/> This identifies an instance of a content stream unique to an individual playback.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.vsid) </li> <li> **Heartbeat:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Context Data:**<br/> (a.media.vsid) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Nome do player de conteúdo

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/>media.playerName </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: "Brightcove" </li> <li> ****<br/> Descrição: Nome do player.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> **Heartbeats:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Nome do reprodutor de conteúdo </li> <li> **Context Data:**<br/> (a.media.playerName) </li> <li> **Feed de dados:**<br/>videoplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/>media.channel </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"Esportes" </li> <li> ****<br/> Descrição: Estação/Canais de distribuição ou onde o conteúdo é reproduzido. Qualquer valor da sequência de caracteres é aceito aqui.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.channel) </li> <li> ****<br/> Heartbeats: (s:sp:channel) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Canal de conteúdo </li> <li> ****<br/> Dados de contexto: (a.media.channel) </li> <li> **Feed de dados:**<br/>videochannel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Sample value: "0-10" </li> <li> ****<br/> Descrição: O intervalo que descreve a parte do conteúdo que foi visualizada (em minutos). O segmento é calculado como os valores mín. e máx. do indicador de reprodução durante a sessão de reprodução.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Segmento do conteúdo </li> <li> ****<br/> Dados de contexto: (a.media.segment) </li> <li> **Feed de dados:**<br/>videosegment </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Nome do conteúdo (variável)

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.name </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/>"The Big Bang Theory" </li> <li> **Description:This is the "friendly" (human-readable) name of the content, equal to the last value of In reporting, Video Name is the classification, and Content Name (variable) is the eVAR.**<br/>`s:asset:name.`<br/><br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeats: (s:asset:name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Nome do conteúdo (variável) </li> <li> ****<br/> Dados de contexto: (a.media.friendlyName) </li> <li> **Feed de dados:**<br/>videoname </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nome do vídeo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/>media.name </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/>"The Big Bang Theory" </li> <li> ****<br/> Descrição: Esse é o nome "amigável" (legível por humanos) do conteúdo, igual ao último valor de `s:asset:name.` <br/>No relatório, Nome do vídeo é a classificação e Nome do conteúdo (variável) é a eVAR.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Pulsações: (s:asset:name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Nome do vídeo </li> <li> ****<br/> Dados de contexto: (a.media.friendlyName) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Caminho do vídeo

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Início da mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"4586695ABC" </li> <li> ****<br/> Descrição: Fornece a capacidade de rastrear o caminho de um visualizador em um site e/ou aplicativo, para ver o caminho que eles tomaram para exibir um vídeo específico. Qualquer combinação de número inteiro e/ou letra.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>prop </li> <li> **Nome do relatório:**<br/>Caminho do vídeo </li> <li> ****<br/> Context Data: (a.media.name) </li> <li> **Feed de dados:**<br/>videopath </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

### Versão do SDK

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Chave de API:**<br/>media.sdkVersion </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"2.62.0_release" </li> <li> **Description:**<br/> The SDK version used by the player. Isso pode ter qualquer valor personalizado que faça sentido para o reprodutor. <br/><br/>Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>sdkVersion) </li> <li> ****<br/> Pulsações: (s:sp:sdk) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.sdkVersion) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versão do VHL

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> Descrição: A versão do SDK de mídia usada para a sessão de rastreamento. <br/><br/>Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>vhlVersion) </li> <li> ****<br/> Pulsações: (s:sp:hb_version) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> ****<br/> Dados de contexto: (a.media.vhlVersion) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadados padrão de áudio e vídeo {#section_pfc_hbm_n1b}

### Programa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SHOW </li> <li> **Chave da API:**<br/>media.show </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "Família Moderna" "Lista Negra" "Menina Nova" </li> <li> ****<br/> Descrição: Nome do <br/>programa/série O nome do programa é obrigatório somente se o show fizer parte de uma série.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.show) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Programa </li> <li> ****<br/> Dados de contexto: (a.media.show) </li> <li> **Feed de dados:**<br/>videoshow </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.show) </li> </ul> |

### Formato de transmissão

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>STREAM_FORMAT </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Live" </li> <li> **Description:**<br/> Format of the stream (Live, VOD, Linear).  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.format) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Context Data:**<br/> (a.media.format) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.format) </li> </ul> |

### Temporada

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SEASON </li> <li> **Chave da API:**<br/>media.season </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "2" </li> <li> **Description:**<br/> The season number the show belongs to.  Season Series is required only if the show is part of a series.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.season) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Temporada </li> <li> **Context Data:**<br/> (a.media.season) </li> <li> **Feed de dados:**<br/>videoseason </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.season) </li> </ul> |

### Episódio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>EPISODE </li> <li> **Chave da API:**<br/>media.episode </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "13" </li> <li> ****<br/> Descrição: O número do episódio.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.episode) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Episódio </li> <li> ****<br/> Dados de contexto: (a.media.episode) </li> <li> **Feed de dados:**<br/>videoepisode </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.episode) </li> </ul> |

### ID do ativo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>ASSET_ID </li> <li> **Chave da API:**<br/>media.assetId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "89745363" </li> <li> ****<br/> Descrição: Esse é o identificador exclusivo para o conteúdo do ativo de mídia, como o identificador do episódio da série TV, o identificador do ativo de filme ou o identificador do evento ao vivo. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.asset) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> ID de ativo </li> <li> ****<br/> Dados de contexto: (a.media.asset) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Gênero

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>GENRE </li> <li> **Chave da API:**<br/>media.genre </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "Drama", "Comédia" </li> <li> ****<br/> Descrição: Tipo ou agrupamento de conteúdo, conforme definido pelo produtor de conteúdo. Os valores devem ser separados por vírgulas na implementação da variável. Nos relatórios, a eVar da lista dividirá cada valor em um item da linha, com cada item recebendo o peso igual de métricas.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.genre) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar de lista </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Gênero </li> <li> ****<br/> Dados de contexto: (a.media.genre) </li> <li> **Feed de dados:**<br/>videogenre </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Data da primeira exibição

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>FIRST_AIR_DATE </li> <li> **Chave da API:**<br/>media.firstAirDate </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Início da mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "2016-01-25" </li> <li> ****<br/> Descrição: A data em que o conteúdo foi exibido pela primeira vez na televisão. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.airDate) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Data da primeira exibição </li> <li> **Context Data:**<br/> (a.media.airDate) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Primeira data digital

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>FIRST_DIGITAL_DATE </li> <li> **Chave da API:**<br/>media.firstDigitalDate </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "2016-01-25" </li> <li> **Description:**<br/> The date when the content first aired on any digital channel or platform. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.digitalDate) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> Primeira data digital </li> <li> ****<br/> Dados de contexto: (a.media.digitalDate) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Classificação de conteúdo

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>RATING </li> <li> **Chave da API:**<br/>media.rating </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>TVY, TVG, TVPG, TVMA </li> <li> **Description:**<br/> Rating as defined by TV Parental Guidelines.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.rating) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> Classificação de conteúdo </li> <li> ****<br/> Dados de contexto: (a.media.rating) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Originador

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>ORIGINATOR </li> <li> **Chave da API:**<br/>media.originator </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> ****<br/> Descrição: Criador do conteúdo.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.originator) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.originator)<br/> </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> Originador </li> <li> ****<br/> Dados de contexto: (a.media.originator) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Rede

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>NETWORK </li> <li> **Chave da API:**<br/>media.network </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Fox", "Bravo", "ESPN" </li> <li> ****<br/> Descrição: O nome da rede/canal.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.network) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Rede </li> <li> ****<br/> Dados de contexto: (a.media.network) </li> <li> **Feed de dados:**<br/>videonetwork </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.network) </li> </ul> |

### Mostrar tipo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SHOW_TYPE </li> <li> **Chave da API:**<br/>media.showType </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> ****<br/> Valor da amostra: "0" = episódio completo; "1" = Pré-visualização/reboque; "2" = Clipe; "3" = Outros. </li> <li> ****<br/> Descrição: Tipo de conteúdo, expresso como um número inteiro entre 0 e 3.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.type) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Mostrar tipo </li> <li> ****<br/> Dados de contexto: (a.media.type) </li> <li> **Feed de dados:**<br/>videoshowtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>MVPD </li> <li> **Chave da API:**<br/>media.pass.mvpd </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Comcast", "DirecTV", "Dish" </li> <li> **Description:**<br/> MVPD provided via Adobe authentication.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.mvpd) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.pass.)<br/>mvpd) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>MVPD </li> <li> **Context Data:**<br/> (a.media.pass.mvpd) </li> <li> **Feed de dados:**<br/>videomvpd </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorizado

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>AUTHORIZED </li> <li> **Chave da API:**<br/>media.pass.auth </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Sample value:**<br/> "TRUE" </li> <li> ****<br/> Descrição: O usuário foi autorizado por meio da autenticação da Adobe.  <br/>**Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.auth) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.pass.)<br/>auth) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Autorizado </li> <li> **Context Data:**<br/> (a.media.pass.auth) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Faixa de horário

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>DAY_PART </li> <li> **Chave da API:**<br/>media.dayPart </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> </li> <li> ****<br/> Descrição: Uma propriedade que define a hora do dia em que o conteúdo foi transmitido ou reproduzido. Isso pode ter qualquer valor definido, de acordo com as necessidades dos clientes.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.dayPart) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Parte do dia </li> <li> ****<br/> Dados de contexto: (a.media.dayPart) </li> <li> **Feed de dados:**<br/>videodaypart </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo de feed de mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>FEED </li> <li> **Chave da API:**<br/>media.feed </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"East-HD", "West-HD", "East-SD" </li> <li> ****<br/> Descrição: Tipo de feed.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.feed) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Tipo de feed de mídia </li> <li> ****<br/> Dados de contexto: (a.media.feed) </li> <li> **Feed de dados:**<br/>videofeedtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.artist </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Disponível na Visão geral [da coleção de](/help/media-collection-api/mc-api-overview.md) mídia ou [Baixar SDKs - Versões 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"The Beatles" </li> <li> ****<br/> Descrição: Nome do artista.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.artist) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.artist) </li> <li> **Feed de dados:** <br/>videoaudioartist </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Álbum

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.album </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Disponível na Visão geral [da coleção de](/help/media-collection-api/mc-api-overview.md) mídia ou [Baixar SDKs - Versões 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:**<br/>"Revolver" </li> <li> ****<br/> Description: Name of the album.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.album) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.album) </li> <li> **Feed de dados:** <br/>videoaudioalbum </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.album) </li> </ul> |

### Rótulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.label </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Disponível na Visão geral [da coleção de](/help/media-collection-api/mc-api-overview.md) mídia ou [Baixar SDKs - Versões 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:**<br/>"Revolver" </li> <li> ****<br/> Descrição: Nome do rótulo do registro.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.label) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Context Data:**<br/> (a.media.label) </li> <li> **Feed de dados:** <br/>videoaudiolabel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.author </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Disponível na Visão geral [da coleção de](/help/media-collection-api/mc-api-overview.md) mídia ou [Baixar SDKs - Versões 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"John Kennedy Toole" </li> <li> **Description:**<br/> Name of the author (of an audiobook).  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.author) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.author) </li> <li> **Feed de dados:** <br/>videoaudioauthor </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.author) </li> </ul> |

### Estação

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.station </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Disponível na Visão geral [da coleção de](/help/media-collection-api/mc-api-overview.md) mídia ou [Baixar SDKs - Versões 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"NPR" </li> <li> **Description:**<br/> Name / ID of the radio station.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.station) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.station) </li> <li> **Feed de dados:**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.station) </li> </ul> |

### Editor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.publisher </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Disponível na Visão geral [da coleção de](/help/media-collection-api/mc-api-overview.md) mídia ou [Baixar SDKs - Versões 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"Random Bauhaus" </li> <li> ****<br/> Descrição: Nome do editor de conteúdo de áudio.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.publisher) </li> <li> ****<br/> Pulsações: (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.publisher) </li> <li> **Feed de dados:**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Métricas de áudio e vídeo {#section_3D5F9C555274428AA6030D07596177E9}

### Inícios da mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set</li> <li> **Chave da API:**<br/>N/A</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> ****<br/> Enviado com: Início da mídia</li> <li> **Versão mín. do SDK:** Any</li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: Carregar evento para a mídia. (Isso ocorre quando o visualizador clica no botão _Reproduzir_). Isso fará a contagem mesmo se houver anúncios antes da exibição, buffering, erros, etc.  <br/>**Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.view) </li> <li> ****<br/> Pulsações: (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> ****<br/> Nome do relatório: Início da mídia </li> <li> ****<br/> Dados de contexto: (a.media.view) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.view) </li> </ul> |

### Início do conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Description:**<br/> First frame of media is consumed. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Starts </li> <li> **Context Data:**<br/> (a.media.play) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.play) </li> </ul> |

### Conteúdo concluído {#content-complete}

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: Um fluxo que foi observado até a conclusão. Isto não significa necessariamente que o utilizador tenha assistido ou escutado todo o fluxo; eles poderiam ter pulado na frente. This only means that the user reached the end of the stream, 100%. <br/>Consulte também Fim [da](quality-parameters.md#session-end) sessão <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Conclusões de conteúdo </li> <li> ****<br/> Dados de contexto: (a.media.complete) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tempo gasto no conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 105 </li> <li> ****<br/> Descrição: Resume a duração do evento (em segundos) para todos os eventos do tipo REPRODUZIR no conteúdo principal.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Time Spent </li> <li> ****<br/> Dados de contexto: (a.media.timePlayed) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tempo gasto com a mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 120 </li> <li> ****<br/> Descrição: Resume a duração do evento (em segundos) para todos os eventos do tipo PLAY, tanto principal quanto de conteúdo do anúncio.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> Tempo gasto com a mídia </li> <li> ****<br/> Dados de contexto: (a.media.totalTimePlayed) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tempo de reprodução exclusivo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 94 </li> <li> ****<br/> Descrição: O valor, em segundos, dos segmentos exclusivos do conteúdo reproduzido durante uma sessão. Exclui o tempo de reprodução em cenários de retorno, nos quais o visualizador assiste a um mesmo segmento de conteúdo várias vezes.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Context Data:**<br/> (a.media.uniqueTimePlayed) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Marcador de progresso de 10 %

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: O indicador de reprodução passa o marcador de 10% do conteúdo com base na duração. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>10% Progress Marker </li> <li> **Context Data:**<br/> (a.media.progress10) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcador de progresso de 25 %

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: O indicador de reprodução passa o marcador de 25% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>25% Progress Marker </li> <li> ****<br/> Dados de contexto: (a.media.progress25) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcador de progresso de 50 %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: O indicador de reprodução passa o marcador de 50% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>50% Progress Marker </li> <li> ****<br/> Dados de contexto: (a.media.progress50) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcador de progresso de setenta e cinco %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> **N/A** </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: O indicador de reprodução passa pelo marcador de 75% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>75% Progress Marker </li> <li> ****<br/> Dados de contexto: (a.media.progress75) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcador de progresso de 95 %

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Description:**<br/> Playhead passes the 95% marker of content based on content length. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>95% Progress Marker </li> <li> **Context Data:**<br/> (a.media.progress95) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Público-alvo médio por minuto

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>maior que ou igual a 1 </li> <li> **Description:**<br/> Average Minute Audience metric is computed as Total Content Time Spent, for one specific media item, divided by its length for all of its playback sessions: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Average Minute Audience </li> <li> ****<br/> Dados de contexto: (a.media.averageMinuteAudience) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Dados federados

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> ****<br/> Tipo:booleano </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra:true  </li> <li> ****<br/> Descrição: Definido como verdadeiro quando a ocorrência é federada (ou seja, recebida pelo cliente como parte de um compartilhamento de dados federado, em vez de sua própria implementação). </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>N/A </li> <li> ****<br/> Dados de contexto: (a.media.federated) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Fluxos estimados

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Sample value:**<br/> 1 - For a 19 minutes playback; <br/>2 - For a 31 minutes playback; <br/>3 - For a 78 minutes playback. </li> <li> ****<br/> Descrição: O número estimado de fluxos de áudio ou vídeo por cada conteúdo individual. Esse valor é aumentado para cada 30 minutos de reprodução (conteúdo + anúncios). Os clientes devem criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios. <br/><br/>Um fluxo é contado a cada 30 minutos, com base no `ms_s` (ou totalTimePlayed = Tempo total do vídeo), semelhante a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> ****<br/> Dados de contexto: (a.media.estimatedStreams) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### Fluxos afetados por interrupções

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: Esse valor é verdadeiro ou falso. É verdadeiro se uma ou mais pausas ocorreram durante a reprodução de um único item de mídia.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Paused Impacted Stream </li> <li> **Context Data:**<br/> (a.media.pause) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Eventos interrompidos

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> ****<br/> Valor da amostra: 2 </li> <li> **Description:**<br/> This metric is computed as a count of pause periods that occurred during a playback session.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Pause Events </li> <li> **Context Data:**<br/> (a.media.pauseCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Duração total da pausa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> ****<br/> Valor da amostra: 190 </li> <li> ****<br/> Descrição: Resume a duração (em segundos) de todos os eventos do tipo PAUSE. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Total Pause Duration </li> <li> ****<br/> Dados de contexto: (a.media.pauseTime) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Continuação do conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> **media.resume** </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> ****<br/> Descrição: Um Resumo é contado para cada reprodução que é retomada após mais de 30 minutos de buffer, pausa ou período de parada OU se esse valor for definido pelo player no trackPlay de VideoInfo. <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> Pulsações: (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Resumes </li> <li> ****<br/> Dados de contexto: (a.media.resume) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Visualizações do segmento de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Description:**<br/> The number of views of the main content. Uma Visualização do segmento de conteúdo é contabilizada quando há ao menos um quadro exibido.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Segment Views </li> <li> **Context Data:**<br/> (a.media.segmentView) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### Contagem de anúncios

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Sent with: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 2 </li> <li> ****<br/> Descrição: O número de anúncios iniciados durante a sessão de mídia.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> ****<br/> Dados de contexto: (a.media.adCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Contagem de capítulo

|   Implementação   | Network Parameters | Relatórios |
| --- | --- | --- |
| <ul> <li> ****<br/> Chave do SDK: N/A </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 2 </li> <li> ****<br/> Descrição: O número de capítulos iniciados durante a sessão de mídia.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> ****<br/> Dados de contexto: (a.media.chapterCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |

## APIs relacionadas {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* IOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

