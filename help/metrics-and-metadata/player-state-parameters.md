---
title: Parâmetros de estado do player
description: Este tópico descreve os parâmetros de rastreamento do estado do player.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

---


# Parâmetros de estado do player{#player-state-parameters}

Este tópico apresenta uma lista de dados de estado do player que a Adobe coleta por meio de variáveis de solução.

Descrição dos dados da tabela:

* **Implementação:** Informações sobre valores e requisitos de implementação
   * *Chave* - Variável, definida manualmente no aplicativo ou automaticamente pelo SDK do Adobe Media.
   * *Obrigatório* - Indica se o parâmetro é necessário para o rastreamento básico de vídeo.
   * *Tipo* - Especifica o tipo da variável a ser definida, a string ou o número.
   * *Enviado com* - Indica quando os dados são enviados: *Início da mídia* é a chamada do Analytics enviada no início da mídia, *Início do anúncio* é a chamada do Analytics enviada no início do anúncio, e assim por diante; as chamadas de *Fechamento* são as chamadas compiladas do Analytics enviadas diretamente do servidor do heartbeat para o servidor da Analytics no final da sessão de mídia, ou no final do anúncio, do capítulo, etc. As chamadas de fechamento não estão disponíveis nas chamadas do pacote de rede.
   * *Versão mín. Versão do SDK* - Indica qual versão do SDK você precisaria para acessar o parâmetro.
   * *Valor de exemplo* - Fornece exemplo de uso comum de variável.
* **Parâmetros de rede:** exibe os valores passados para os servidores do Adobe Analytics ou Heartbeat. Esta coluna mostra os nomes dos parâmetros que são vistos nas chamadas de rede geradas pelos SDKs do Adobe Media.
* **Relatórios:** informações sobre como visualizar e analisar os dados do vídeo.
   * *Disponível* - Indica se os dados estão disponíveis no relatórios por padrão (*Sim*) ou se exigem configuração personalizada (*Personalizado*)
   * *Variável reservada* - Indica se os dados são capturados como um evento, eVar, prop ou classificação em uma variável reservada.
   * *Nome do relatório* - Nome do relatório do Adobe Analytics para a variável
   * *Dados de contexto* - Nome dos dados de contexto do Adobe Analytics passados para o servidor de relatórios e usados nas regras de processamento.
   * *Feed de dados* - Nome da coluna para variável encontrada nos feeds de dados da sequência de cliques ou transmissão ao vivo
   * *Audience Manager* - Nome da característica encontrada no Adobe Audience Manager

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo descrita em Relatório/Variável reservada como &quot;classificação&quot;.\
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe os adicionará novamente.



## Propriedades do estado do player {#player-state-properties}

As tabelas de propriedades de Rastreamento de estado do player estão organizadas nas cinco seções a seguir:

* Tela cheia
   * Fluxos afetados por tela cheia
   * Contagens de tela cheia
   * Duração total da tela inteira
* Fechar legenda
   * Fluxos afetados por legendagem fechada
   * Contagens de legendas ocultas
   * Duração total das legendas ocultas
* Silenciar
   * Fluxos afetados pelo mudo
   * Contagens de mudo
   * Duração total do mudo
* Imagem em imagem
   * Fluxo impactado por imagem em imagem
   * Imagem em contagens de imagem
   * Duração total da imagem na imagem
* Em foco
   * Fluxos afetados pelo In Focus
   * Contagens de foco
   * Duração total do foco

### Propriedades de tela cheia

#### Fluxos afetados por tela cheia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de fluxos afetados por Tela cheia. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.stats.fullscreen.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Fluxos de nome **<br/>de relatório afetados por tela cheia</li> <li> **Dados **<br/>de contexto (a.media.stats.fullscreen.set)<br/> </li> <li> **Tela de vídeo de feed **<br/>de dados</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.a.media.statlscreen.set)</li> </ul> |

#### Contagens de tela cheia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de vezes que uma tela cheia foi exibida. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreencount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Contagem de tela cheia do nome **<br/>do relatório</li> <li> **Dados **<br/>de contexto (videostatefullscreencount)<br/> </li> <li> **Feed **<br/>de dados videostatefullscreencount</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostatefullscreencount)</li> </ul> |



#### Duração total da tela inteira

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoA duração da exibição de uma tela cheia. This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreentime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Duração da tela cheia do nome **<br/>do relatório</li> <li> **Dados **<br/>de contexto (videostatefullscreentime)<br/> </li> <li> **Feed **<br/>de dados videostatefullscreentime</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostatefullscreentime)</li> </ul> |


### Fechar propriedades da legenda

#### Fluxos afetados por legendagem fechada

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de fluxos afetados pelo recurso de legenda. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.stats.closeCaptioning.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Fluxos de nome **<br/>de relatório afetados por legendagem</li> <li> **Dados **<br/>de contexto (a.media.stats.closeCaptioning.set)<br/> </li> <li> **Video **<br/>Feed de dados videostateclosedcaptioning</li> <li> **Gerenciador **<br/>de Audiências (c_context data.a.media.stats.closeCaptioning.set)</li> </ul> |


#### Contagens de legendas ocultas

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de vezes em que o recurso Legenda foi selecionado. This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Contagem de legendas de nome **<br/>de relatório</li> <li> **Dados **<br/>de contexto (videostateclosedcaptioningcount)<br/> </li> <li> **Feed **<br/>de dados videostateclosedcaptioningcount</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostateclosedcaptioningcount)</li> </ul> |


#### Duração total das legendas ocultas

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO tempo de legendagem foi selecionado. This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Duração da legenda do nome **<br/>do relatório</li> <li> **Dados **<br/>de contexto (videostateclosedcaptioningtime)<br/> </li> <li> **Feed **<br/>de dados videostateclosedcaptioningtime</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostateclosedcaptioningtime)</li> </ul> |


### Silenciar propriedades

#### Fluxos afetados pelo mudo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de fluxos afetados pelo Silenciar. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.stats.mute.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Fluxos de nomes **<br/>de relatórios afetados pelo mudo</li> <li> **Dados **<br/>de contexto (a.media.stats.mute.set)<br/> </li> <li> **Videostatemute do Feed **<br/>de dados</li> <li> **Gerenciador **<br/>de Audiências (c_context data.a.media.stats.mute.set)</li> </ul> |

#### Contagens de mudo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de vezes que Mudo foi selecionado. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutecount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Contagem de Mudo de Nome **<br/>de Relatório</li> <li> **Dados **<br/>de contexto (videostatemutecount)<br/> </li> <li> **Feed **<br/>de dados videostatemutecount</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostatemutecount)</li> </ul> |

#### Duração total do mudo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoA duração do Mudo foi selecionada. This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemutetime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Duração do mudo do nome **<br/>do relatório</li> <li> **Dados **<br/>de contexto (videostatemutetime)<br/> </li> <li> **Feed **<br/>de dados videostatemutetime</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostatemutetime)</li> </ul> |


### Imagem em Propriedades de Imagem


#### Fluxos afetados pela imagem em imagem

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de fluxos afetados por Picture in Picture. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.stats.pictureinpicture.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Fluxos de nomes **<br/>de relatórios afetados por imagem em imagem</li> <li> **Dados **<br/>de contexto (a.media.stats.pictureinpicture.set)<br/> </li> <li> **Feed **<br/>de dados videostatepictureinpicture</li> <li> **Gerenciador **<br/>de Audiências (c_context data.a.media.stats.pictureinpicture.set)</li> </ul> |


#### Imagem em contagens de imagem

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de vezes que a Imagem na Imagem foi exibida. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturecount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Imagem do Nome **<br/>do Relatório na Contagem de Imagens</li> <li> **Dados **<br/>de contexto (videostatepictureinpicturecount)<br/> </li> <li> **Feed **<br/>de dados videostatepictureinpicturecount</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostatepictureinpicturecount)</li> </ul> |


#### Duração total da imagem na imagem

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO tempo de exibição da Imagem em Imagem. This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturetime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Nome **<br/>do Relatório Imagem na Duração da Imagem</li> <li> **Dados **<br/>de contexto (videostatepictureinpicturetime)<br/> </li> <li> **Feed **<br/>de dados videostatepictureinpicturetime</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostatepictureinpicturetime)</li> </ul> |


### Propriedades em foco

#### Fluxos afetados pelo In Focus

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de fluxos afetados pelo In Focus. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.stats.infocus.set)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Fluxos de nomes **<br/>de relatórios afetados pelo foco</li> <li> **Dados **<br/>de contexto (a.media.stats.infocus.set)<br/> </li> <li> **Feed **<br/>de dados videostateinfocus</li> <li> **Gerenciador **<br/>de Audiências (c_context data.a.media.stats.infocus.set)</li> </ul> |


#### Contagens de foco

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO número de vezes em que o foco foi exibido. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Nome **<br/>Do Relatório Na Contagem De Foco</li> <li> **Dados **<br/>de contexto (videostateinfocuscount)<br/> </li> <li> **Feed **<br/>de dados videostateinfocuscount</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostateinfocuscount)</li> </ul> |


#### Duração total do foco

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave **<br/>SDK definida automaticamente</li> <li> **Chave **<br/>API N/A</li> <li> **Obrigatório **<br/>Não</li> <li> **Número do tipo **<br/></li> <li> **Enviado com **<br/>Media Close</li> <li> **Versão mín. SDK Version **<br/>3.0</li> <li> **Valor **<br/>de amostra TRUE</li><li> ****<br/>DescriçãoO tempo em foco foi exibido. This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **Importante** Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **Heartbeat **<br/>N/A</li> </ul> | <ul> <li> **Disponível **<br/>Sim</li> <li> **evento de variável **<br/>reservada</li> <li> **Nome **<br/>Do Relatório Na Duração Do Foco</li> <li> **Dados **<br/>de contexto (videostateinfocustime)<br/> </li> <li> **Feed **<br/>de dados videostateinfocustime</li> <li> **Gerenciador **<br/>de Audiências (c_contextdata.videostateinfocustime)</li> </ul> |



## APIs relacionadas {#related_apis_section}

NECESSIDADE: Adicionar links de API a documentos:
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)
