---
seo-title: Parâmetros de áudio e vídeo
title: Parâmetros de áudio e vídeo
uuid: fdacfb 8 b-db 3 e -46 fb-b 9 ad-c 3 a 749555 b 2 a
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Parâmetros de áudio e vídeo{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Em 7 de fevereiro de 2019, o Adobe Analytics para vídeo e áudio lançou uma alteração de nome de métrica. <i>Inicializações da mídia</i> agora será chamada <i>Inícios da mídia</i>. Essa alteração foi feita para refletir os padrões do setor nas métricas e relatórios, além de tornar a métrica facilmente identificável no relatório.

>[!NOTE]
>
>A partir de 13 de setembro de 23 18, foi feita uma alteração nos rótulos para algumas dimensões, métricas e relatórios, para permitir o rastreamento de conteúdo cruzado de análises de vídeo e áudio. Os rótulos que mudaram incluem: *inicializações de vídeo* para *inicializações de mídia*, *duração do vídeo* para *duração do conteúdo* e *nome do vídeo* para *nome do conteúdo*. Os relatórios de vídeo nos Reports and Analytics foram atualizados para usar o nome “Mídia” no lugar de “Vídeo”. As mudanças nos rótulos não afetaram a coleção de dados nem os dados de histórico. Anote essas alterações caso precise usá-las no Report Builder ou em qualquer outra extração de dados externa automatizada que possa ser afetada por essa alteração.

Este tópico apresenta uma lista de dados de conteúdo de áudio e vídeo, incluindo valores de dados de contexto, que a Adobe coleta por meio das variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de áudio e vídeo.
   * *Tipo* - Especifica o tipo de variável a ser definida: sequência de caracteres ou número.
   * *Enviado com* - Indica quando os dados são enviados: *O Media Start* é a chamada de análise enviada no início da mídia, *Ad Start* é a chamada de análise enviada no início do anúncio e assim por diante; *as* Chamadas Fechar são chamadas de análise compiladas enviadas diretamente do servidor de pulsação para o servidor do Analytics no final da sessão de mídia, ou o fim do anúncio, capítulo etc. As chamadas de fechar não estão disponíveis em chamadas de pacotes de rede.
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
>Não altere os nomes de classificação das variáveis listadas abaixo que estão descritas em Relatório/Variável reservada como "classificação".\
>As classificações de mídia são definidas quando um conjunto de relatórios é habilitado para rastreamento de mídia. De vez em quando, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver ausente, a Adobe adicionará as ausentes novamente.

## Dados principais de áudio e vídeo {#section_y55_y1m_n1b}

### Tipo de fluxo {#stream-type}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chave de API:**<br/>media.streamType </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 2.2 <br/><br/>Available in [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Exemplo de valor:** <br/>"vídeo" </li> <li> **Descrição:**<br/> Identifica o tipo de fluxo. Os valores válidos são “audio”, “video” e “all”.  <br/><br/>[Relatórios de relatórios](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo de transmissão de mídia: Todos - <br/>Segmentar todos os dados de fluxo de mídia; Regra: O conteúdo (ID) existe <br/><br/>no Tipo de fluxo de mídia: Áudio - <br/>segmenta todos os dados de fluxo de áudio; Regra: Conteúdo (ID) existe e Media Stream Type = audio <br/><br/>Media Stream Type: " Vídeo " - <br/>segmente todos os dados de fluxo de vídeo; Regra: Conteúdo (ID) existe e Tipo de fluxo de mídia!= audio <br/><br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. streamtype) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. streamtype) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On VISIT </li> <li> **Nome do relatório:**<br/>Content </li> <li> **Dados de contexto:**<br/> (a. media. streamtype) </li> <li> **Feed de dados:** <br/>videostreamtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.id </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"4586695ABC" </li> <li>**Descrição:**<br/> A ID do conteúdo do conteúdo, que pode ser usada para vincular de volta a outras IDs do setor/CMS, igual ao último valor de `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Pulsações:**<br/> (s: ativo: video_ id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On VISIT </li> <li> **Nome do relatório:**<br/>Content </li> <li> **Dados de contexto:**<br/> (a. media. name) </li> <li> **Feed de dados:**<br/>video </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duração de conteúdo (variável)

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.length </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VOD: ; 28; Live: ; 6400; Linear: . 800. </li><li> **Descrição:**<br/> Duração do clipe/Tempo de execução - esse é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). It equals the last value of `l:asset:length` from events of type Main. <br/>Se `l:asset:length` não estiver definido, o último valor será `l:asset:duration` usado. <br/>Nos relatórios, a Duração do vídeo é a classificação e a Duração do vídeo (variável) é a eVAR.  <br/> **Importante:** esta propriedade é usada para calcular várias métricas, como as de acompanhamento de progresso e Público-alvo médio por minuto. Se isso não for definido ou não for maior que zero, essas métricas não estarão disponíveis.  Para Mídia em tempo real com duração desconhecida, o valor de 86400 é o padrão. <br/>Pre versão 1.5.1, isso era `l:asset:duration`; depois de 1.5.1, isso é `l:asset:length.`<br/> **Data de lançamento: 13/09/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Pulsações:**<br/> (l: ativo: length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Duração do conteúdo (variável) </li> <li> **Dados de contexto:**<br/> (a. media. length) </li> <li> **Feed de dados:**<br/>videolength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Duração do vídeo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.length </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VOD: ; 28; Live: ; 6400; Linear: . 800. </li> <li> **Descrição:**<br/> Duração do clipe/Tempo de execução - esse é o comprimento máximo (ou duração) do conteúdo que está sendo consumido (em segundos). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. Nos relatórios, a Duração do vídeo é a classificação e a Duração do vídeo (variável) é a eVAR.  <br/> **Importante:** esta propriedade é usada para calcular várias métricas, como as de acompanhamento de progresso e Público-alvo médio por minuto. Se isso não for definido ou não for maior que zero, essas métricas não estarão disponíveis.  Para Mídia em tempo real com duração desconhecida, o valor de 86400 é o padrão. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Pulsações:**<br/> (l: ativo: length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Duração do vídeo </li> <li> **Dados de contexto:**<br/> (a. media. length) </li> <li> **Feed de dados:** <br/>videoclassificationlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.contentType </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres restrita </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"vod" </li> <li> **Descrição:**<br/> Valores disponíveis por **Tipo de fluxo**: <br/> _Áudio:_ "song", "podcast", "audiobook", "radio" <br/> _Vídeo:_ " Vod "," Live "," Linear "," UGC "," dvod " <br/> Clientes podem fornecer valores personalizados para esse parâmetro. This equals `s:stream:type.` If that is unset, this equals `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. contenttype) </li> <li> **Pulsações:**<br/> (s: fluxo: type) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Tipo de conteúdo </li> <li> **Dados de contexto:**<br/> (a. contenttype) </li> <li> **Feed de dados:**<br/>videocontenttype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID da sessão de mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/>obtida no back-end </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.8 </li> <li> **Valor da amostra:**<br/> 1482236761294786918253 </li> <li> **Descrição:**<br/> Isso identifica uma instância de um fluxo de conteúdo exclusivo para uma reprodução individual.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. vsid) </li> <li> **Heartbeat:**<br/> (s: evento: sid) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Dados de contexto:**<br/> (a. media. vsid) </li> <li> **Feed de dados:**<br/>vsid </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vsid) </li> </ul> |

### Nome do player de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/>media.playerName </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> " Brightcove " </li> <li> **Descrição:**<br/> Nome do player.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>playerName) </li> <li> **Pulsações:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Nome do reprodutor de conteúdo </li> <li> **Dados de contexto:**<br/> (a. media. playername) </li> <li> **Feed de dados:**<br/>videoplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.playerName) </li> </ul> |

### Canal de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/>media.channel </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"Esportes" </li> <li> **Descrição:**<br/> Estação de distribuição/Canais ou onde o conteúdo é reproduzido. Qualquer valor da sequência de caracteres é aceito aqui.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. channel) </li> <li> **Pulsações:**<br/> (s: sp: channel) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Canal de conteúdo </li> <li> **Dados de contexto:**<br/> (a. media. channel) </li> <li> **Feed de dados:**<br/>videochannel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> " 0-10 " </li> <li> **Descrição:**<br/> O intervalo que descreve a parte do conteúdo exibido (em minutos). O segmento é calculado como os valores mín. e máx. do indicador de reprodução durante a sessão de reprodução.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Segmento do conteúdo </li> <li> **Dados de contexto:**<br/> (a. media. segment) </li> <li> **Feed de dados:**<br/>videosegment </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segment) </li> </ul> |

### Nome do conteúdo (variável)

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Chave da API:**<br/>media.name </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/>"The Big Bang Theory" </li> <li> **Descrição:**<br/>Esse é o nome «amigável» (legível por humanos) do conteúdo, igual ao último valor de `s:asset:name.`<br/>relatórios em relatórios, Nome do vídeo é a classificação e Nome do conteúdo (variável) é a evar. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Pulsações:**<br/> (s: ativo: name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Nome do conteúdo (variável) </li> <li> **Dados de contexto:**<br/> (a. media. friendlyname) </li> <li> **Feed de dados:**<br/>videoname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nome do vídeo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Chave da API:**<br/>media.name </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.1 </li> <li> **Exemplo de valor:**<br/>"The Big Bang Theory" </li> <li> **Descrição:**<br/> Esse é o nome «amigável» (legível por humanos) do conteúdo, igual ao último valor de `s:asset:name.`<br/>relatórios em relatórios, Nome do vídeo é a classificação e Nome do conteúdo (variável) é a evar. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Pulsações:**<br/> (s: ativo: name) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Nome do vídeo </li> <li> **Dados de contexto:**<br/> (a. media. friendlyname) </li> <li> **Feed de dados:** <br/>videoclassificationname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Caminho do vídeo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início da mídia </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>"4586695ABC" </li> <li> **Descrição:**<br/> Fornece a capacidade de rastrear o caminho de um visualizador em um site e/ou aplicativo, para ver o caminho que eles levaram para visualizar um vídeo específico. Qualquer combinação de número inteiro e/ou letra.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Pulsações:**<br/> (s: ativo: video_ id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>prop </li> <li> **Nome do relatório:**<br/>Caminho do vídeo </li> <li> **Dados de contexto:**<br/> (a. media. name) </li> <li> **Feed de dados:**<br/>videopath </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

### Versão do SDK

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Chave de API:**<br/>media.sdkVersion </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"2.62.0_release" </li> <li> **Descrição:**<br/> A versão do SDK usada pelo player. Isso pode ter qualquer valor personalizado que faça sentido para o reprodutor. <br/><br/>Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Sdkversion) </li> <li> **Pulsações:**<br/> (s: sp: sdk) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. sdkversion) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versão do VHL

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **Descrição:**<br/> A versão do SDK do Heartbeat usada para a sessão de monitoramento. <br/><br/>Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  <br/><br/>[Mediaheartbeat. version ();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Vhlversion) </li> <li> **Pulsações:**<br/> (s: sp: hb_ version) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Dados de contexto:**<br/> (a. media. vhlversion) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadados padrão de áudio e vídeo {#section_pfc_hbm_n1b}

### Programa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SHOW </li> <li> **Chave da API:**<br/>media.show </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " Família moderna "" Lista negra "" Nova girl " </li> <li> **Descrição:**<br/> Nome do programa de nome <br/>de programa/série é necessário somente se a exibição fizer parte de uma série.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. show) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. show) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Programa </li> <li> **Dados de contexto:**<br/> (a. media. show) </li> <li> **Feed de dados:**<br/>videoshow </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.show) </li> </ul> |

### Formato de transmissão

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>STREAM_FORMAT </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Live" </li> <li> **Descrição:**<br/> Formato do stream (Live, VOD, Linear).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. format) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. format) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Dados de contexto:**<br/> (a. media. format) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.format) </li> </ul> |

### Temporada

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SEASON </li> <li> **Chave da API:**<br/>media.season </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " 2 " </li> <li> **Descrição:**<br/> O número da temporada ao qual a exibição pertence. A Série de estações só será necessária se a exibição fizer parte de uma série.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. season) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. season) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Temporada </li> <li> **Dados de contexto:**<br/> (a. media. season) </li> <li> **Feed de dados:**<br/>videoseason </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.season) </li> </ul> |

### Episódio

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>EPISODE </li> <li> **Chave da API:**<br/>media.episode </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " 13 " </li> <li> **Descrição:**<br/> O número do episódio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. episode) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. episode) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Episódio </li> <li> **Dados de contexto:**<br/> (a. media. episode) </li> <li> **Feed de dados:**<br/>videoepisode </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.episode) </li> </ul> |

### ID do ativo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>ASSET_ID </li> <li> **Chave da API:**<br/>media.assetId </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " 89745363 " </li> <li> **Descrição:**<br/> Esse é o identificador exclusivo do conteúdo do ativo de mídia, como o identificador de episódio da série de TV, identificador do ativo de filme ou identificador de evento ao vivo. Normalmente, essas IDs são derivadas de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi. Esses identificadores também podem ser de outros sistemas proprietários ou internos.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. asset) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. asset) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> ID de ativo </li> <li> **Dados de contexto:**<br/> (a. media. asset) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.asset) </li> </ul> |

### Gênero

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>GENRE </li> <li> **Chave da API:**<br/>media.genre </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " Drama "," Comédia " </li> <li> **Descrição:**<br/> Tipo ou agrupamento de conteúdo, conforme definido pelo produtor de conteúdo. Os valores devem ser separados por vírgulas na implementação da variável. Nos relatórios, a eVar da lista dividirá cada valor em um item da linha, com cada item recebendo o peso igual de métricas.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. genre) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. genre) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar de lista </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Gênero </li> <li> **Dados de contexto:**<br/> (a. media. genre) </li> <li> **Feed de dados:**<br/>videogenre </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.genre) </li> </ul> |

### Data da primeira exibição

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>FIRST_AIR_DATE </li> <li> **Chave da API:**<br/>media.firstAirDate </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início da mídia </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " 2016-01-25 " </li> <li> **Descrição:**<br/> A data em que o conteúdo primeiro é exibido na televisão. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. airdate) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. airdate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Data da primeira exibição </li> <li> **Dados de contexto:**<br/> (a. media. airdate) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.airDate) </li> </ul> |

### Primeira data digital

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>FIRST_DIGITAL_DATE </li> <li> **Chave da API:**<br/>media.firstDigitalDate </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " 2016-01-25 " </li> <li> **Descrição:**<br/> A data em que o conteúdo primeiro é exibido em qualquer canal digital ou plataforma. Qualquer formato de data é aceitável, mas a Adobe recomenda: DD/MM/AAAA </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. digitaldate) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. digitaldate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> Primeira data digital </li> <li> **Dados de contexto:**<br/> (a. media. digitaldate) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Classificação de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>RATING </li> <li> **Chave da API:**<br/>media.rating </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>TVY, TVG, TVPG, TVMA </li> <li> **Descrição:**<br/> Classificação conforme definido pelas Diretrizes de pais da TV.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. rating) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. rating) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> Classificação de conteúdo </li> <li> **Dados de contexto:**<br/> (a. media. rating) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.rating) </li> </ul> |

### Originador

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>ORIGINATOR </li> <li> **Chave da API:**<br/>media.originator </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Warner Brothers", "Sony", "Disney" </li> <li> **Descrição:**<br/> Criador do conteúdo.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. originator) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. originator) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/> Originador </li> <li> **Dados de contexto:**<br/> (a. media. originator) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.originator) </li> </ul> |

### Rede

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>NETWORK </li> <li> **Chave da API:**<br/>media.network </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Fox", "Bravo", "ESPN" </li> <li> **Descrição:**<br/> O nome da rede/canal.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. network) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. network) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Rede </li> <li> **Dados de contexto:**<br/> (a. media. network) </li> <li> **Feed de dados:**<br/>videonetwork </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.network) </li> </ul> |

### Mostrar tipo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>SHOW_TYPE </li> <li> **Chave da API:**<br/>media.showType </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " 0 " = episódio completo; " 1 " = Visualização/trailer; " 2 " = Clip; " 3 " = Outro. </li> <li> **Descrição:**<br/> Tipo de conteúdo, expresso como um número inteiro entre 0 e 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. type) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. type) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Mostrar tipo </li> <li> **Dados de contexto:**<br/> (a. media. type) </li> <li> **Feed de dados:**<br/>videoshowtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>MVPD </li> <li> **Chave da API:**<br/>media.pass.mvpd </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"Comcast", "DirecTV", "Dish" </li> <li> **Descrição:**<br/> MVPD fornecido pela autenticação da Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. mvpd) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>MVPD </li> <li> **Dados de contexto:**<br/> (a. media. pass. mvpd) </li> <li> **Feed de dados:**<br/>videomvpd </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorizado

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>AUTHORIZED </li> <li> **Chave da API:**<br/>media.pass.auth </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Valor da amostra:**<br/> " TRUE " </li> <li> **Descrição:**<br/> O usuário foi autorizado pela autenticação da Adobe. <br/>**Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. auth) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. pass.<br/>auth) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Autorizado </li> <li> **Dados de contexto:**<br/> (a. media. pass. auth) </li> <li> **Feed de dados:**<br/>videoauthorized </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Faixa de horário

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>DAY_PART </li> <li> **Chave da API:**<br/>media.dayPart </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/> </li> <li> **Descrição:**<br/> Uma propriedade que define a hora do dia em que o conteúdo foi transmitido ou reproduzido. Isso pode ter qualquer valor definido, de acordo com as necessidades dos clientes.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. daypart) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. daypart) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Parte do dia </li> <li> **Dados de contexto:**<br/> (a. media. daypart) </li> <li> **Feed de dados:**<br/>videodaypart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo de feed de mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>FEED </li> <li> **Chave da API:**<br/>media.feed </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 </li> <li> **Exemplo de valor:**<br/>"East-HD", "West-HD", "East-SD" </li> <li> **Descrição:**<br/> Tipo de feed. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. feed) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. feed) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> Tipo de feed de mídia </li> <li> **Dados de contexto:**<br/> (a. media. feed) </li> <li> **Feed de dados:**<br/>videofeedtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.artist </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"The Beatles" </li> <li> **Descrição:**<br/> Nome do artista. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. artist) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. artist) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. artist) </li> <li> **Feed de dados:** <br/>videoaudioartist </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.artist) </li> </ul> |

### Álbum

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.album </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:**<br/>"Revolver" </li> <li> **Descrição:**<br/> Nome do álbum. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. album) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. album) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. album) </li> <li> **Feed de dados:** <br/>videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.album) </li> </ul> |

### Rótulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.label </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:**<br/>"Revolver" </li> <li> **Descrição:**<br/> Nome do rótulo de registro. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. label) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. label) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. label) </li> <li> **Feed de dados:** <br/>videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.label) </li> </ul> |

### Autor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.author </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"John Kennedy Toole" </li> <li> **Descrição:**<br/> Nome do autor (de um público-alvo). <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. author) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. author) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. author) </li> <li> **Feed de dados:** <br/>videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.author) </li> </ul> |

### Estação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/>media.station </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"NPR" </li> <li> **Descrição:**<br/> Nome/ID da estação de rádio. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. station) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. station) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. station) </li> <li> **Feed de dados:**<br/>videoaudiostation </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.station) </li> </ul> |

### Editor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.publisher </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Exemplo de valor:** <br/>"Random Bauhaus" </li> <li> **Descrição:**<br/> Nome do editor de conteúdo de áudio. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. publisher) </li> <li> **Pulsações:**<br/> (s: meta:<br/>a. media. publisher) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. publisher) </li> <li> **Feed de dados:**<br/>videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.publisher) </li> </ul> |

## Métricas de áudio e vídeo {#section_3D5F9C555274428AA6030D07596177E9}

### Inícios da mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set</li> <li> **Chave da API:**<br/>N/A</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/> Início da mídia</li> <li> **Versão mín. do SDK:** Any</li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> Carregar evento para a mídia. (Isso ocorre quando o visualizador clica no botão _Reproduzir_). Isso fará a contagem mesmo se houver anúncios antes da exibição, buffering, erros, etc.  <br/>**Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. view) </li> <li> **Pulsações:**<br/> (s: evento:<br/>type = start) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> Início da mídia </li> <li> **Dados de contexto:**<br/> (a. media. view) </li> <li> **Feed de dados:**<br/>videostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.view) </li> </ul> |

### Início do conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O primeiro quadro da mídia é consumido. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Starts </li> <li> **Dados de contexto:**<br/> (a. media. play) </li> <li> **Feed de dados:**<br/>videoplay </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.play) </li> </ul> |

### Conteúdo concluído {#content-complete}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> Um fluxo assistido para conclusão. Isso não significa necessariamente que o usuário assistiu ou escuta todo o fluxo; podem ter ignorado. Isso significa apenas que o usuário chegou ao fim do fluxo, 100%. <br/>Consulte [também Fim da sessão](quality-parameters.md#session-end)<br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Pulsações:**<br/> (s: evento:<br/>type = complete) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Conclusões de conteúdo </li> <li> **Dados de contexto:**<br/> (a. media. complete) </li> <li> **Feed de dados:**<br/>videocomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.complete) </li> </ul> |

### Tempo gasto no conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 105 </li> <li> **Descrição:**<br/> Inclui a duração do evento (em segundos) para todos os eventos do tipo PLAY no conteúdo principal. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Time Spent </li> <li> **Dados de contexto:**<br/> (a. media. timeplayed) </li> <li> **Feed de dados:**<br/>videotime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tempo gasto com a mídia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 120 </li> <li> **Descrição:**<br/> Contabiliza a duração do evento (em segundos) para todos os eventos do tipo PLAY, tanto o conteúdo principal quanto o de anúncio. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> Tempo gasto com a mídia </li> <li> **Dados de contexto:**<br/> (a. media. totaltimeplayed) </li> <li> **Feed de dados:**<br/>videototaltime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tempo de reprodução exclusivo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 94 </li> <li> **Descrição:**<br/> O valor em segundos dos segmentos únicos de conteúdo reproduzidos durante uma sessão. Exclui o tempo de reprodução em cenários de retorno, nos quais o visualizador assiste a um mesmo segmento de conteúdo várias vezes.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Dados de contexto:**<br/> (a. media. uniquetimeplayed) </li> <li> **Feed de dados:**<br/>videouniquetimeplayed </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. uniquetimeplayed) </li> </ul> |

### Marcador de progresso de dez %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 10% de conteúdo com base em comprimento. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>10% Progress Marker </li> <li> **Dados de contexto:**<br/> (a. media. progress 10) </li> <li> **Feed de dados:**<br/>videoprogress10 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcador de progresso de twenty % %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 25% de conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>25% Progress Marker </li> <li> **Dados de contexto:**<br/> (a. media. progress 25) </li> <li> **Feed de dados:**<br/>videoprogress25 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcador de progresso de cinquenta %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 50% de conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>50% Progress Marker </li> <li> **Dados de contexto:**<br/> (a. media. progress 50) </li> <li> **Feed de dados:**<br/>videoprogress50 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcador de progresso de Sevents a cinco %

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> **N/A** </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 75% de conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>75% Progress Marker </li> <li> **Dados de contexto:**<br/> (a. media. progress 75) </li> <li> **Feed de dados:**<br/>videoprogress75 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcador de progresso de noventa % de progresso

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O indicador de reprodução passa o marcador de 95% de conteúdo com base na duração do conteúdo. O marcador é contado apenas uma vez, mesmo se a busca for regressiva. Se a busca for para frente, os marcadores ignorados não serão contados.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>95% Progress Marker </li> <li> **Dados de contexto:**<br/> (a. media. progress 95) </li> <li> **Feed de dados:**<br/>videoprogress95 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.progress95) </li> </ul> |

### Público-alvo médio por minuto

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>maior que ou igual a 1 </li> <li> **Descrição:**<br/> A métrica de Público-alvo médio de minuto é calculada como Tempo total gasto no conteúdo, para um item de mídia específico, dividido pela duração de todas as sessões de reprodução: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Average Minute Audience </li> <li> **Dados de contexto:**<br/> (a. media. averageminuteaudience) </li> <li> **Feed de dados:**<br/>videoaverageminuteaudience </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Fluxos estimados

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 1 - Para uma reprodução de 19 minutos; <br/>2 - Para uma reprodução de 31 minutos; <br/>3 - Para uma reprodução de 78 minutos. </li> <li> **Descrição:**<br/> O número estimado de fluxos de áudio ou vídeo por cada conteúdo individual. Esse valor é aumentado para cada 30 minutos de reprodução (conteúdo + anúncios). Os clientes devem criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios. <br/><br/>Um fluxo é contado a cada 30 minutos, com base no `ms_s` tempo total (ou totaltimeplayed = Tempo total do vídeo), similar a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>Personalizado </li> <li> **Dados de contexto:**<br/> (a. media. estimatedstreams) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. estimatedstreams) </li> </ul> |

### Fluxos afetados por interrupções

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> Esse valor é verdadeiro ou falso. É verdadeiro se uma ou mais pausas ocorreram durante a reprodução de um único item de mídia.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Pulsações:**<br/> (s: evento:<br/>type = pause) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Paused Impacted Stream </li> <li> **Dados de contexto:**<br/> (a. media. pause) </li> <li> **Feed de dados:**<br/>videopause </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pause) </li> </ul> |

### Eventos interrompidos

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Valor da amostra:**<br/> 2 </li> <li> **Descrição:**<br/> Essa métrica é calculada como uma contagem de períodos de interrupção que ocorreram durante uma sessão de reprodução.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Pulsações:**<br/> (s: evento:<br/>type = pause) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Pause Events </li> <li> **Dados de contexto:**<br/> (a. media. pausecount) </li> <li> **Feed de dados:**<br/>videopausecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Duração total da pausa

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Valor da amostra:**<br/> 190 </li> <li> **Descrição:**<br/> Define a duração (em segundos) de todos os eventos do tipo PAUSE. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/> **Data de lançamento: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Total Pause Duration </li> <li> **Dados de contexto:**<br/> (a. media. pausetime) </li> <li> **Feed de dados:**<br/>videopausetime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Continuação do conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> **media.resume** </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5.6 </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> Um Resumo é contabilizado para cada reprodução que continua após mais de 30 minutos de buffer, pausa ou período de parado OU se esse valor for definido pelo player em videoinfo trackplay. <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Pulsações:**<br/> (s: evento:<br/>type = resume) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Resumes </li> <li> **Dados de contexto:**<br/> (a. media. resume) </li> <li> **Feed de dados:**<br/>videoresume </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.resume) </li> </ul> |

### Visualizações do segmento de conteúdo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/>TRUE </li> <li> **Descrição:**<br/> O número de exibições do conteúdo principal. Uma Visualização do segmento de conteúdo é contabilizada quando há ao menos um quadro exibido.  <br/> **Importante:** somente poderá ser verdadeiro se estiver definido. Se não for definido, nenhum valor será retornado. </li></ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Heartbeats:**<br/>N/A </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Content Segment Views </li> <li> **Dados de contexto:**<br/> (a. media. segmentview) </li> <li> **Feed de dados:**<br/>videosegmentviews </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## Related APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* IOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

