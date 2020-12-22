---
title: Parâmetros de áudio e vídeo
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: ef237fd0d9e2bcebe011d819224d98d450830d07
workflow-type: tm+mt
source-wordcount: '6252'
ht-degree: 99%

---


# Parâmetros de áudio e vídeo {#audio-and-video-parameters}

>[!IMPORTANT]
>
>Em 7 de fevereiro de 2019, o Adobe Analytics para vídeo e áudio lançou uma mudança de nome de métrica. <i>Inicializações da mídia</i> agora será chamada <i>Inícios da mídia</i>. Essa mudança foi feita para refletir os padrões do setor em métricas e relatórios e para facilitar a identificação da métrica nos relatórios.

>[!NOTE]
>
>A partir de 13 de setembro de 2018, uma mudança foi feita nos rótulos de algumas dimensões, métricas e relatórios para permitir o rastreamento entre conteúdo das análises de áudio e vídeo. Os rótulos que mudaram incluem: *inicializações de vídeo* para *inicializações de mídia*, *duração do vídeo* para *duração do conteúdo* e *nome do vídeo* para *nome do conteúdo*. Os relatórios de vídeo nos Reports and Analytics foram atualizados para usar o nome “Mídia” no lugar de “Vídeo”. As mudanças nos rótulos não afetaram a coleção de dados nem os dados de histórico. Observe essas alterações caso você as esteja usando no Report Builder ou em qualquer outra extração automática de dados externa que possa ser afetada por essa alteração.

Esse tópico apresenta uma lista de dados de conteúdo de áudio e vídeo, incluindo valores de dados de contexto, que a Adobe coleta por meio de variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** Informações sobre valores e requisitos de implementação.
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de áudio e vídeo.
   * *Tipo* - Especifica o tipo da variável a ser definida, a string ou o número.
   * *Enviado com* - Indica quando os dados são enviados: *Início da mídia* é a chamada do Analytics enviada no início da mídia, *Início do anúncio* é a chamada do Analytics enviada no início do anúncio, e assim por diante; as chamadas de *Fechamento* são as chamadas compiladas do Analytics enviadas diretamente do servidor do heartbeat para o servidor da Analytics no final da sessão de mídia, ou no final do anúncio, do capítulo, etc. As chamadas de fechamento não estão disponíveis nas chamadas do pacote de rede.
   * *Versão mín. do SDK* - Indica qual versão do SDK você precisaria para acessar o parâmetro.
   * *Valor de exemplo* - Fornece exemplo de uso comum de variável.
* **Parâmetros de rede:** exibe os valores passados para os servidores do Adobe Analytics ou Heartbeat. Esta coluna mostra os nomes dos parâmetros que são vistos nas chamadas de rede geradas pelos SDKs do Adobe Media.
* **Relatórios:** informações sobre como visualizar e analisar os dados de áudio e vídeo.
   * *Disponível* - Indica se os dados estão disponíveis no relatórios por padrão (*Sim*) ou se exigem configuração personalizada (*Personalizado*).
   * *Variável reservada* - Indica se os dados são capturados como um evento, eVar, prop ou classificação em uma variável reservada.
   * *Expiração* - Indica se os dados expiram após cada hit ou após cada visita.
   * *Nome do relatório* - Nome do relatório do Adobe Analytics para a variável.
   * *Dados de contexto* - Nome dos dados de contexto do Adobe Analytics passados para o servidor de relatórios e usados nas regras de processamento.
   * *Feed de dados* - Nome da coluna para variável encontrada nos feeds de dados da sequência de cliques ou transmissão ao vivo.
   * *Audience Manager* - Nome da característica encontrada no Adobe Audience Manager.

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo descrita em Relatório/Variável reservada como &quot;classificação&quot;.\
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe os adicionará novamente.

## Principais dados de mídia de streaming {#core-audio-and-video-data}

### Tipo de transmissão {#stream-type}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [mediaType](./audio-video-parameters.md#create-media-object) </li> <li> **Chave de API:**<br/> media.streamType </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 2.2<br/><br/>Disponível em [Visão geral da API Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li>  <li> **Exemplo de valor:**<br/> &quot;vídeo&quot; </li> <li> **Descrição:**<br/> Identifica o tipo de fluxo. Os valores válidos são “audio”, “video” e “all”.  <br/><br/>[Segmentos de relatório](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo de fluxo de mídia: Todos - <br/>Segmentar todos os dados de fluxo de mídia; Regra: O conteúdo (ID) existe <br/><br/>Tipo de fluxo de mídia: Áudio - <br/>Segmentar todos os dados de fluxo de áudio; Regra: Conteúdo (ID) existe E Tipo de fluxo de mídia = áudio <br/><br/>Tipo de fluxo de mídia: &quot;Vídeo&quot; - <br/>Segmentar todos os dados de fluxo de vídeo; Regra: Conteúdo (ID) existe E Tipo de fluxo de mídia != audio <br/><br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do Relatório:Tipo**<br/> de Fluxo </li> <li> **Dados de contexto:**<br/> (a.media.streamType) </li> <li> **Feed de dados:**<br/> videostreamtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

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
| <ul> <li> **Chave de SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/> media.id </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> &quot;4586695ABC&quot; </li> <li>**Descrição:**<br/> A ID do conteúdo, que pode ser usada para vincular a outras IDs do setor/CMS, é igual ao último valor de `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> On VISIT </li> <li> **Nome do relatório:**<br/> Content </li> <li> **Dados de contexto:**<br/> (a.media.name) </li> <li> **Feed de dados:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

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
| <ul> <li> **Chave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/> media.length </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> VOD: 128; Ao vivo: 86.400; Linear: 1.800. </li><li> **Descrição:**<br/> Comprimento/tempo de execução do clipe - Esse é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). Ele equivale ao último valor de `l:asset:length` de eventos do tipo Principal. <br/>Se `l:asset:length` não estiver definido, então o último valor de `l:asset:duration` será usado. <br/>Nos relatórios, a Duração do vídeo é a classificação e a Duração do vídeo (variável) é a eVAR.  <br/> **Importante:** esta propriedade é usada para calcular várias métricas, como as de acompanhamento de progresso e Público-alvo médio por minuto. Se isso não for definido ou não for maior que zero, essas métricas não estarão disponíveis.  Para Mídia em tempo real com duração desconhecida, o valor de 86400 é o padrão. <br/>Antes da versão 1.5.1, isso era `l:asset:duration`; depois da 1.5.1, passou a ser `l:asset:length.` <br/> **Data de lançamento: 13/09/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Heartbeats:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Duração do conteúdo (variável) </li> <li> **Dados de contexto:**<br/> (a.media.length) </li> <li> **Feed de dados:**<br/> videolength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **Chave de SDK:**<br/>  [comprimento](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/> media.length </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> VOD: 128; Ao vivo: 86.400; Linear: 1.800. </li> <li> **Descrição:**<br/> Comprimento/tempo de execução do clipe - Esse é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). Ele equivale ao último valor de `l:asset:length` de eventos do tipo Principal. Se `l:asset:length` não estiver definido, então o último valor de `l:asset:duration` será usado. Nos relatórios, a Duração do vídeo é a classificação e a Duração do vídeo (variável) é a eVAR.  <br/> **Importante:** esta propriedade é usada para calcular várias métricas, como as de acompanhamento de progresso e Público-alvo médio por minuto. Se isso não for definido ou não for maior que zero, essas métricas não estarão disponíveis.  Para Mídia em tempo real com duração desconhecida, o valor de 86400 é o padrão. Antes da versão 1.5.1, isso era `l:asset:duration`; depois da 1.5.1, passou a ser `l:asset:length.`<br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Pulsações:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Duração do vídeo </li> <li> **Dados de contexto:**<br/> (a.media.length) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **Chave de SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/> media.contentType </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres restrita </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> &quot;vod&quot; </li> <li> **Descrição:**<br/> Valores disponíveis por **Tipo de fluxo:** <br/> _Áudio:_ &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot;, &quot;radio&quot; <br/> _Vídeo:_ &quot;VoD&quot;, &quot;Ao vivo&quot;, &quot;Linear&quot;, &quot;UGC&quot;, &quot;DVoD&quot; <br/> Os clientes podem fornecer valores personalizados para esse parâmetro. Isso é igual a `s:stream:type.` Se isso não for definido, isso é igual a `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Heartbeats:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Tipo de conteúdo </li> <li> **Dados de contexto:**<br/> (a.contentType) </li> <li> **Feed de dados:**<br/> videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID da sessão de mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave de API:**<br/> obtida no back-end </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.8 </li> <li> **Valor de exemplo:**<br/> 1482236761294786918253 </li> <li> **Descrição:**<br/> Isso identifica uma instância de um fluxo de conteúdo exclusivo para uma reprodução individual.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **Heartbeat:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **Disponível:**<br/> usar regra de processamento </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.vsid) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Sinalizador de mídia baixada

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> `config.downloadedcontent` </li> <li> **Chave de API:**<br/> obtida no back-end </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** <br/>Inicie a extensão v1.1.0 do Android e iOS </li> <li> **Exemplo de valor:**<br/> true </li> <li> **Descrição:**<br/> Defina como true quando a ocorrência for gerada devido à reprodução de uma sessão de mídia de conteúdo baixada. Não apresente quando o conteúdo baixado não for reproduzido.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.downloaded) </li> <li> **Heartbeat:**<br/> (s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.downloaded) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### Nome do reprodutor de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/> media.playerName </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> &quot;Brightcove&quot; </li> <li> **Descrição:**<br/> Nome do reprodutor.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **Heartbeats:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Nome do reprodutor de conteúdo </li> <li> **Dados de contexto:**<br/> (a.media.playerName) </li> <li> **Feed de dados:**<br/> videoplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [marketing](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/> media.channel </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> &quot;Esportes&quot; </li> <li> **Descrição:**<br/> Estação/canais de distribuição ou onde o conteúdo é reproduzido. Qualquer valor da sequência de caracteres é aceito aqui.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **Heartbeats:**<br/> (s:sp:channel) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Canal de conteúdo </li> <li> **Dados de contexto:**<br/> (a.media.channel) </li> <li> **Feed de dados:**<br/> videochannel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> &quot;0-10&quot; </li> <li> **Descrição:**<br/> O intervalo que descreve a parte do conteúdo que foi exibida (em minutos). O segmento é calculado como os valores mín. e máx. do indicador de reprodução durante a sessão de reprodução.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Segmento do conteúdo </li> <li> **Dados de contexto:**<br/> (a.media.segment) </li> <li> **Feed de dados:**<br/> videosegment </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Nome do conteúdo (variável)

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/> media.name </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Descrição:**<br/> Esse é o nome &quot;amigável&quot; (legível) do conteúdo, igual ao último valor de `s:asset:name.`<br/>No relatório, Nome do vídeo é a classificação e Nome do conteúdo (variável) é a eVAR. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Heartbeats:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Nome do conteúdo (variável) </li> <li> **Dados de contexto:**<br/> (a.media.friendlyName) </li> <li> **Feed de dados:**<br/> videoname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

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
| <ul> <li> **Chave de SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/> media.name </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/> &quot;The Big Bang Theory&quot; </li> <li> **Descrição:**<br/> Esse é o nome &quot;amigável&quot; (legível) do conteúdo, igual ao último valor de `s:asset:name.` <br/>No relatório, Nome do vídeo é a classificação e Nome do conteúdo (variável) é a eVAR.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Pulsações:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Nome do vídeo </li> <li> **Dados de contexto:**<br/> (a.media.friendlyName) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Caminho do vídeo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início da mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> &quot;4586695ABC&quot; </li> <li> **Descrição:**<br/> Fornece a capacidade de rastrear o caminho de um visualizador em um site e/ou aplicativo, para ver o caminho que eles tomaram para exibir um vídeo específico. Qualquer combinação de número inteiro e/ou letra.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Pulsações:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> prop </li> <li> **Nome do relatório:**<br/> Caminho do vídeo </li> <li> **Dados de contexto:**<br/> (a.media.name) </li> <li> **Feed de dados:**<br/> videopath </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### Versão do SDK

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Chave de API:**<br/> media.sdkVersion </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> “2.62.0_release” </li> <li> **Descrição:**<br/> A versão do SDK usada pelo reprodutor. Isso pode ter qualquer valor personalizado que faça sentido para o reprodutor. <br/><br/>Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **Heartbeats:**<br/> (s:sp:sdk) </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado* </li> <li> **Dados de contexto:**<br/> (a.media.sdkVersion) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul><br/>* Usar regra de processamento personalizada |

### Versão do VHL

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **Descrição:**<br/> A versão do SDK do Media usada para a sessão de rastreamento. <br/><br/>Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **Heartbeats:**<br/> (s:sp:hb_version) </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.vhlVersion) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadados de mídia de fluxo padrão {#standard-audio-and-video-metadata}

### Programa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> SHOW </li> <li> **Chave da API:**<br/> media.show </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> &quot;Família Moderna&quot; &quot;A Última Dança&quot; &quot;Menina Nova&quot; </li> <li> **Descrição:**<br/> Nome do programa/série <br/>Nome do programa é necessário somente se o programa for parte de uma série.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Programa </li> <li> **Dados de contexto:**<br/> (a.media.show) </li> <li> **Feed de dados:**<br/> videoshow </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### Formato de transmissão

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> STREAM_FORMAT </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;Live&quot; </li> <li> **Descrição:**<br/> Formato do fluxo (Live, VOD, Linear).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.format) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Temporada

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> SEASON </li> <li> **Chave da API:**<br/> media.season </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/> &quot;2&quot; </li> <li> **Descrição:**<br/> O número da temporada do programa.  Séries da temporada são necessárias somente se o programa for parte de uma série.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.season) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Temporada </li> <li> **Dados de contexto:**<br/> (a.media.season) </li> <li> **Feed de dados:**<br/> videoseason </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.season) </li> </ul> |

### Episódio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> EPISODE </li> <li> **Chave da API:**<br/> media.episode </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/> &quot;13&quot; </li> <li> **Descrição:**<br/> O número do episódio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Episódio </li> <li> **Dados de contexto:**<br/> (a.media.episode) </li> <li> **Feed de dados:**<br/> videoepisode </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### ID do ativo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> ASSET_ID </li> <li> **Chave da API:**<br/> media.assetId </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/> &quot;89745363&quot; </li> <li> **Descrição:**<br/> Esse é o identificador exclusivo de conteúdo do ativo de mídia, como o identificador de episódio da série de TV, o identificador de ativo do filme ou o identificador de evento em tempo real. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> ID de ativo </li> <li> **Dados de contexto:**<br/> (a.media.asset) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Gênero

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> GENRE </li> <li> **Chave da API:**<br/> media.genre </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;Drama&quot;, &quot;Comédia&quot; </li> <li> **Descrição:**<br/> Tipo ou agrupamento de conteúdo conforme definido pelo produtor do conteúdo. Os valores devem ser delimitados por vírgulas na implementação da variável. Nos relatórios, a eVar lista dividirá cada valor em um item de linha, com cada item de linha recebendo peso de métricas iguais.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar de lista </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Gênero </li> <li> **Dados de contexto:**<br/> (a.media.genre) </li> <li> **Feed de dados:**<br/> videogenre </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Data da primeira exibição

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> FIRST_AIR_DATE </li> <li> **Chave da API:**<br/> media.firstAirDate </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início da mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/> &quot;2016-01-25&quot; </li> <li> **Descrição:**<br/> A data quando o conteúdo foi exibido na televisão pela primeira vez. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Data da primeira exibição </li> <li> **Dados de contexto:**<br/> (a.media.airDate) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Primeira data digital

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> FIRST_DIGITAL_DATE </li> <li> **Chave da API:**<br/> media.firstDigitalDate </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/> &quot;2016-01-25&quot; </li> <li> **Descrição:**<br/> A data quando o conteúdo foi exibido em qualquer canal ou plataforma digital pela primeira vez. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Primeira data digital </li> <li> **Dados de contexto:**<br/> (a.media.digitalDate) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Classificação de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> RATING </li> <li> **Chave da API:**<br/> media.rating </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> TVY, TVG, TVPG, TVMA </li> <li> **Descrição:**<br/> A classificação conforme definida pelas Diretrizes de controle parental da TV.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Classificação de conteúdo </li> <li> **Dados de contexto:**<br/> (a.media.rating) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Originador

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> ORIGINATOR </li> <li> **Chave da API:**<br/> media.originator </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;Warner Brothers&quot;, &quot;Sony&quot;, &quot;Disney&quot; </li> <li> **Descrição:**<br/> O criador do conteúdo.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Originador </li> <li> **Dados de contexto:**<br/> (a.media.originator) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Rede

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> NETWORK </li> <li> **Chave da API:**<br/> media.network </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;Fox&quot;, &quot;Bravo&quot;, &quot;ESPN&quot; </li> <li> **Descrição:**<br/> O nome da rede/canal.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Rede </li> <li> **Dados de contexto:**<br/> (a.media.network) </li> <li> **Feed de dados:**<br/> videonetwork </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Mostrar tipo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> SHOW_TYPE </li> <li> **Chave da API:**<br/> media.showType </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;0&quot; = Episódio completo; &quot;1&quot; = Pré-visualização/Trailer; &quot;2&quot; = Clipe; &quot;3&quot; = Outros. </li> <li> **Descrição:**<br/> Tipo de conteúdo, expresso como um número inteiro entre 0 e 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Mostrar tipo </li> <li> **Dados de contexto:**<br/> (a.media.type) </li> <li> **Feed de dados:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> MVPD </li> <li> **Chave da API:**<br/> media.pass.mvpd </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;Comcast&quot;, &quot;DirecTV&quot;, &quot;Dish&quot; </li> <li> **Descrição:**<br/> O MVPD fornecido pela autenticação da Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> MVPD </li> <li> **Dados de contexto:**<br/> (a.media.pass.mvpd) </li> <li> **Feed de dados:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorizado

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> AUTHORIZED </li> <li> **Chave da API:**<br/> media.pass.auth </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/> &quot;TRUE&quot; </li> <li> **Descrição:**<br/> O usuário foi autorizado por meio da autenticação da Adobe.  <br/>**Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Pulsações:**<br/> (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Autorizado </li> <li> **Dados de contexto:**<br/> (a.media.pass.auth) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Faixa de horário

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> DAY_PART </li> <li> **Chave da API:**<br/> media.dayPart </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor de exemplo:**<br/>  </li> <li> **Descrição:**<br/> Uma propriedade que define a hora do dia em que o conteúdo foi transmitido ou reproduzido. Isso pode ter qualquer valor definido, de acordo com as necessidades dos clientes.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Parte do dia </li> <li> **Dados de contexto:**<br/> (a.media.dayPart) </li> <li> **Feed de dados:**<br/> videodaypart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo de feed de mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> FEED </li> <li> **Chave da API:**<br/> media.feed </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> &quot;East-HD&quot;, &quot;West-HD&quot;, &quot;East-SD&quot; </li> <li> **Descrição:**<br/> Tipo de feed.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Tipo de feed de mídia </li> <li> **Dados de contexto:**<br/> (a.media.feed) </li> <li> **Feed de dados:**<br/> videofeedtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> media.artist </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 1.5.7 <br/>Disponível em [Visão geral do Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemplo de valor:**<br/> &quot;The Beatles&quot; </li> <li> **Descrição:**<br/> Nome do artista.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artist) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do Relatório:**<br/> Artista</li> <li> **Dados de contexto:**<br/> (a.media.artist) </li> <li> **Feed de dados:**<br/> videoaudioartist </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artist) </li> </ul> |

### Álbum

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> media.album </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 1.5.7 <br/>Disponível em [Visão geral do Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemplo de valor:**<br/> &quot;Revolver&quot; </li> <li> **Descrição:**<br/> Nome do álbum.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do Relatório:**<br/> Álbum </li> <li> **Dados de contexto:**<br/> (a.media.album) </li> <li> **Feed de dados:**<br/> videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### Rótulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> media.label </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 1.5.7 <br/>Disponível em [Visão geral do Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemplo de valor:**<br/> &quot;Revolver&quot; </li> <li> **Descrição:**<br/> Nome do rótulo do registro.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> </li> Rótulo<li> **Dados de contexto:**<br/> (a.media.label) </li> <li> **Feed de dados:**<br/> videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> media.author </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 1.5.7 <br/>Disponível em [Visão geral do Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemplo de valor:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **Descrição:**<br/> Nome do autor (de um audiobook).  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.author) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do Relatório:**<br/> Autor </li> <li> **Dados de contexto:**<br/> (a.media.author) </li> <li> **Feed de dados:**<br/> videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.author) </li> </ul> |

### Estação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> media.station </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 1.5.7 <br/>Disponível em [Visão geral do Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemplo de valor:**<br/> &quot;NPR&quot; </li> <li> **Descrição:**<br/> Nome/ID da estação de rádio.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do Relatório:**<br/> Estação </li> <li> **Dados de contexto:**<br/> (a.media.station) </li> <li> **Feed de dados:**<br/> videoaudiostation </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Editor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/> media.publisher </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Fechamento de mídia </li> <li> **Versão mín. Versão do SDK:** 1.5.7 <br/>Disponível em [Visão geral do Media Collection](/help/media-collection-api/mc-api-overview.md) ou [Baixar SDKs - Versões 2.2.](/help/sdk-implement/download-sdks.md)  </li> <li> **Exemplo de valor:**<br/> &quot;Random Bauhaus&quot; </li> <li> **Descrição:**<br/> Nome do publicador do conteúdo de áudio.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **Heartbeats:**<br/> (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Personalizado* </li> <li> **Dados de contexto:**<br/> (a.media.publisher) </li> <li> **Feed de dados:**<br/> videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.publisher) </li>  </ul><br/> * Usar regra de processamento personalizada |

## Métricas de mídia de transmissão {#audio-and-video-metrics}

### Inícios da mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente</li> <li> **Chave da API:**<br/> N/D</li> <li> **Tipo:**<br/> sequência de caracteres</li> <li> **Enviado com:**<br/> Início da mídia</li> <li> **Versão mín. do SDK:** Any</li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> Evento de carregamento da mídia. (Isso ocorre quando o visualizador clica no botão _Reproduzir_).  Isso fará a contagem mesmo se houver anúncios antes da exibição, buffering, erros, etc.  <br/>**Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> início de mídia </li> <li> **Dados de contexto:**<br/> (a.media.view) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### Início do conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O Primeiro quadro da mídia é consumido. Se o usuário ignorar o anúncio, o buffering etc., não haverá o evento de &quot;Início de conteúdo&quot;.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Content Starts </li> <li> **Dados de contexto:**<br/> (a.media.play) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### Conteúdo concluído {#content-complete}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> Um fluxo que foi observado até a conclusão. Isto não significa necessariamente que o utilizador tenha assistido a ou escutado todo o fluxo; eles poderiam ter avançado a reprodução. Isso somente significa que o usuário atingiu o fim do fluxo, 100%. <br/>Consulte também [Fim da sessão](quality-parameters.md#session-end) <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Conclusões de conteúdo </li> <li> **Dados de contexto:**<br/> (a.media.complete) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tempo gasto no conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 105 </li> <li> **Descrição:**<br/> Soma a duração do evento (em segundos) para todos os eventos do tipo PLAY no conteúdo principal.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Content Time Spent </li> <li> **Dados de contexto:**<br/> (a.media.timePlayed) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tempo gasto com a mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 120 </li> <li> **Descrição:**<br/> Soma a duração do evento (em segundos) para todos os eventos do tipo PLAY, no conteúdo principal e de publicidade.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Tempo gasto com a mídia </li> <li> **Dados de contexto:**<br/> (a.media.totalTimePlayed) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tempo de reprodução exclusivo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 94 </li> <li> **Descrição:**<br/> O valor, em segundos, dos segmentos exclusivos de conteúdo reproduzidos durante a sessão. Exclui o tempo de reprodução em cenários de retorno, nos quais o visualizador assiste a um mesmo segmento de conteúdo várias vezes.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.    <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.uniqueTimePlayed) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### Marcador de progresso de 10 %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 10% do conteúdo com base na duração. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.     <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> 10% Progress Marker </li> <li> **Dados de contexto:**<br/> (a.media.progress10) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcador de progresso de 25%

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 25% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.     <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> 25% Progress Marker </li> <li> **Dados de contexto:**<br/> (a.media.progress25) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcador de progresso de 50%

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 50% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.     <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> 50% Progress Marker </li> <li> **Dados de contexto:**<br/> (a.media.progress50) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcador de progresso de 75%

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave de API:**<br/> **N/D** </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 75% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.     <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> 75% Progress Marker </li> <li> **Dados de contexto:**<br/> (a.media.progress75) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcador de progresso de 95%

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 95% do conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.     <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> 95% Progress Marker </li> <li> **Dados de contexto:**<br/> (a.media.progress95) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Público-alvo médio por minuto

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> maior que ou igual a 1 </li> <li> **Descrição:**<br/> A métrica de Público médio por minuto é calculada como o Tempo total gasto com conteúdo para um item de mídia específico dividido pela sua duração para todas as sessões de reprodução: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Average Minute Audience </li> <li> **Dados de contexto:**<br/> (a.media.averageMinuteAudience) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Segundos desde a última chamada

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 600</li> <li> **Descrição:**<br/> os segundos desde a última métrica da chamada são 0 se o fluxo foi fechado com um evento completo ou com um evento final e, em geral, 600 se foi fechado devido ao tempo limite. Essa métrica não tem uma variável de solução e regras de processamento automático, portanto, é necessário criar uma regra de processamento personalizada para salvá-la.</li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> N/D </li> <li> **Dados de contexto:**<br/> (a.media.secondsSinceLastCall) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.secondsSinceLastCall) </li> </ul> |

### Dados federados

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> true  </li> <li> **Descrição:**<br/> Definido como verdadeiro quando a ocorrência é federada (ou seja, recebida pelo cliente como parte de um compartilhamento de dados federado, em vez de sua própria implementação). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> N/D </li> <li> **Dados de contexto:**<br/> (a.media.federated) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Fluxos estimados

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> 1 - Para uma reprodução de 19 minutos; <br/>2 - Para uma reprodução de 31 minutos; <br/>3 - Para uma reprodução de 78 minutos. </li> <li> **Descrição:**<br/> O número estimado de fluxos de áudio ou vídeo por conteúdo individual. Esse valor é aumentado para cada 30 minutos de reprodução (conteúdo + anúncios). Os clientes devem criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios. <br/><br/>Um fluxo é contado a cada 30 minutos, com base no `ms_s` (ou totalTimePlayed = Tempo total de vídeo), semelhante a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.estimatedStreams) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### Fluxos afetados por interrupções

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> O valor é verdadeiro ou falso. É verdadeiro se uma ou mais pausas ocorreram durante a reprodução de um único item de mídia.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Paused Impacted Stream </li> <li> **Dados de contexto:**<br/> (a.media.pause) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Eventos interrompidos

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Valor de exemplo:**<br/> 2 </li> <li> **Descrição:**<br/> Essa métrica é calculada como uma contagem de períodos de interrupção que ocorreram durante uma sessão de reprodução.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Pulsações:**<br/> (s:evento:<br/>type=pause) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Pause Events </li> <li> **Dados de contexto:**<br/> (a.media.pauseCount) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Duração total da pausa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Valor de exemplo:**<br/> 190 </li> <li> **Descrição:**<br/> Soma a duração (em segundos) de todos os eventos do tipo PAUSA. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Total Pause Duration </li> <li> **Dados de contexto:**<br/> (a.media.pauseTime) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Continuação do conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave de API:**<br/> **media.resume** </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> Uma retomada é contabilizada a cada reprodução que continua após mais de 30 minutos de buffer, interrupção ou período de paralisação, OU se o valor for definido pelo reprodutor no objeto VideoInfo antes de trackPlay. <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=resume) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Content Resumes </li> <li> **Dados de contexto:**<br/> (a.media.resume) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.resume) </li> </ul> |

### Visualizações do segmento de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE </li> <li> **Descrição:**<br/> A quantidade de visualizações do conteúdo principal. Uma Visualização do segmento de conteúdo é contabilizada quando há ao menos um quadro exibido.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Content Segment Views </li> <li> **Dados de contexto:**<br/> (a.media.segmentView) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |


### Contagem de anúncios

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave do SDK:**<br/> N/D </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 2 </li> <li> **Descrição:**<br/> O número de anúncios iniciados durante a sessão de mídia.    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.adCount) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Contagem de capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave do SDK:**<br/> N/D </li> <li> **Chave da API:**<br/> N/D </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 2 </li> <li> **Descrição:**<br/> O número de capítulos iniciados durante a sessão de mídia.    <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/> N/D </li> <li> **Nome do relatório:**<br/> Personalizado </li> <li> **Dados de contexto:**<br/> (a.media.chapterCount) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |


## Parâmetros da Lei de Privacidade do Consumidor da Califórnia (CCPA) {#ccpa-params}

### Reencaminhamento pelo lado do servidor para Recusar

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave do SDK:**<br/> N/D </li> <li> **Chave da API:**<br/> analytics.optOutServerSideForwarding </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado com:**<br/> Início da mídia </li> <li> **Versão mín. Versão do SDK:** N/A </li> <li> **Exemplo de valor:**<br/> true </li> <li>**Descrição:**<br/> Define como true quando o usuário final optar por não receber os dados compartilhados entre o Adobe Analytics e outras soluções da Experience Cloud (por exemplo, o Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **Heartbeats:**<br/> (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> On VISIT </li> <li> **Nome do relatório:**<br/> N/D </li> <li> **Dados de contexto:**<br/> N/D </li> <li> **Feed de dados:**<br/> video </li> <li> **Audience Manager:**<br/> N/D </li> </ul> |

### Compartilhamento de recusa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave do SDK:**<br/> N/D </li> <li> **Chave da API:**<br/> analytics.optOutShare </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> booleano </li> <li> **Enviado com:**<br/> Início da mídia </li> <li> **Versão mín. Versão do SDK:** N/A </li> <li> **Exemplo de valor:**<br/> true </li> <li>**Descrição:**<br/> Definido como verdadeiro quando o usuário final optou por não ter seus dados federados (por exemplo, para outros clientes do Adobe Analytics). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **Heartbeats:**<br/> (s:meta:cm.oos) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> On VISIT </li> <li> **Nome do relatório:**<br/> N/D </li> <li> **Dados de contexto:**<br/> N/D </li> <li> **Feed de dados:**<br/> video </li> <li> **Audience Manager:**<br/> N/D </li> </ul> |

## APIs relacionadas {#section_Related_APIs}

### APIs createMediaObject {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### APIs MediaHeartbeatConfig {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)
