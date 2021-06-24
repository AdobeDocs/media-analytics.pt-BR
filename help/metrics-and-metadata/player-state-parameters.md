---
title: Parâmetros de estado do player
description: '"Saiba mais sobre os parâmetros de rastreamento do estado do player para tela cheia, legenda de fechamento, mudo e propriedades de imagem."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: '"Media Analytics, Variáveis"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '2249'
ht-degree: 98%

---

# Parâmetros de estado do player{#player-state-parameters}

Este tópico apresenta uma lista de dados de estado do player que a Adobe coleta por meio de variáveis de solução.

Descrição dos dados da tabela:

* **Implementação:** Informações sobre valores e requisitos de implementação.
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
   * *Audience Manager* - Nome da característica encontrada no Adobe Audience Manager.

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo descrita em Relatório/Variável reservada como &quot;classificação&quot;.\
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe os adicionará novamente.

## Propriedades do estado do player {#player-state-properties}

Os recursos de rastreamento do estado do player podem ser conectados a um fluxo de áudio ou vídeo. As métricas padronizadas de rastreamento do estado do player são armazenadas como variáveis de solução. Os estados padrão são: tela cheia, mudo, legendas ocultas, picture in picture e em foco.

### Propriedades da Tela cheia

#### Fluxos afetados pela Tela cheia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A quantidade de fluxos afetados pela Tela cheia. Essa métrica é definida como 1 se pelo menos um Estado de tela cheia ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.fullscreen.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Fluxos afetados pela Tela cheia </li> <li> **Dados de contexto:**<br/> a.media.states.fullscreen.set<br/> </li> <li> **Feed de dados:**<br/> videostatefullscreen </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### Contagens de Tela cheia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> O número de vezes que uma Tela cheia é exibida. Essa métrica é definida como 1 se pelo menos um Estado de tela cheia ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se esse evento estiver definido, a contagem será igual ao número de vezes que o vídeo foi exibido no estado Tela cheia. Se este evento não for definido, nenhum valor será enviado.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.fullscreen.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Contagem de Tela cheia </li> <li> **Dados de contexto:**<br/> a.media.states.fullscreen.count<br/> </li> <li> **Feed de dados:**<br/> videostatefullscreencount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.fullscreen.count </li> </ul> |



#### Duração total da Tela cheia

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A duração de tempo em que uma Tela cheia foi exibida. Essa métrica é definida como 1 se pelo menos um Estado de tela cheia ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento estiver definido, o tempo será igual ao tempo em que o vídeo ficou no estado Tela cheia. Se este evento não for definido, nenhum valor será enviado.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.fullscreen.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Duração total da tela cheia </li> <li> **Dados de contexto:**<br/> a.media.states.fullscreen.time<br/> </li> <li> **Feed de dados:**<br/> videostatefullscreentime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.fullscreen.time </li> </ul> |


### Propriedade das legendas ocultas

#### Fluxos afetados pelas Legendas ocultas

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A quantidade de fluxos afetados pelas Legendas ocultas. Essa métrica é definida como 1 se pelo menos um Estado de legendas ocultas ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.closedcaptioning.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Fluxos afetados pelas Legendas ocultas. </li> <li> **Dados de contexto:**<br/> a.media.states.closedcaptioning.set<br/> </li> <li> **Feed de dados:**<br/> videostateclosedcaptioning </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.closedcaptioning.set </li> </ul> |


#### Contagens de Legendas ocultas

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> O número de vezes que as legendas ocultas foram exibidas. Essa métrica é definida como 1 se pelo menos um Estado de legendas ocultas ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se esse evento estiver definido, a contagem será igual ao número de vezes que o vídeo foi exibido no estado de Legendas ocultas. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.states.closedcaptioning.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Contagem de Legendas ocultas </li> <li> **Dados de contexto:**<br/> a.media.states.closedcaptioning.count<br/> </li> <li> **Feed de dados:**<br/> videostateclosedcaptioningcount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### Duração total das Legendas ocultas

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A duração de tempo em que as Legendas ocultas foram exibidas. Essa métrica é definida como 1 se pelo menos um Estado de tela cheia ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se esse evento estiver definido, o tempo será igual ao tempo em que o vídeo ficou no estado de Legendas ocultas. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.closedcaptioning.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Duração total das Legendas ocultas </li> <li> **Dados de contexto:**<br/> a.media.states.closedcaptioning.time<br/> </li> <li> **Feed de dados:**<br/> videostateclosedcaptioningtime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.closedcaptioning.time </li> </ul> |


### Propriedades da função Mudo

#### Fluxos afetados pela função Mudo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A quantidade de fluxos afetados pela função Mudo. Essa métrica é definida como 1 se pelo menos um Estado da função Mudo ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.mute.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Fluxos afetados pela função Mudo </li> <li> **Dados de contexto:**<br/> a.media.states.mute.set<br/> </li> <li> **Feed de dados:**<br/> videostatemute </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.mute.set </li> </ul> |

#### Contagens da função Mudo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> O número de vezes que a função Mudo foi exibida. Essa métrica é definida como 1 se pelo menos um Estado da função Mudo ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se esse evento estiver definido, a contagem será igual ao número de vezes que o vídeo foi colocado no estado Mudo. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.mute.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Contagem da função Mudo </li> <li> **Dados de contexto:**<br/> a.media.states.mute.count<br/> </li> <li> **Feed de dados:**<br/> videostatemutecount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.mute.count </li> </ul> |

#### Duração total da função Mudo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A duração de tempo em que a função Mudo foi exibida. Essa métrica é definida como 1 se pelo menos um Estado da função Mudo ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento estiver definido, o tempo será igual ao tempo em que o vídeo ficou no estado Mudo. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.mute.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Duração total da função Mudo </li> <li> **Dados de contexto:**<br/> a.media.states.mute.time<br/> </li> <li> **Feed de dados:**<br/> videostatemutetime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.mute.time </li> </ul> |


### Propriedades do Picture in Picture


#### Fluxos afetados pelo Picture in Picture

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> O número de fluxos afetados pelo Picture in Picture. Essa métrica é definida como 1 se pelo menos um Estado de Picture in Picture ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.pictureinpicture.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Fluxos afetados pelo Picture in Picture </li> <li> **Dados de contexto:**<br/> a.media.states.pictureinpicture.set<br/> </li> <li> **Feed de dados:**<br/> videostatepictureinpicture </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.pictureinpicture.set </li> </ul> |


#### Contagens de Picture in Picture

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> O número de vezes que o Picture in Picture foi exibido. Essa métrica é definida como 1 se pelo menos um Estado de Picture in Picture ocorrer durante a sessão de reprodução. <br/> **Importante:** <br/> Se este evento estiver definido, a contagem é igual ao número de vezes que o vídeo esteve no estado Picture in Picture. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.pictureinpicture.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Contagem de Picture in Picture </li> <li> **Dados de contexto:**<br/> a.media.states.pictureinpicture.count<br/> </li> <li> **Feed de dados:**<br/> videostatepictureinpicturecount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.pictureinpicture.count </li> </ul> |


#### Duração total do Picture in Picture

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A duração de tempo em que o Picture in Picture foi exibido. Essa métrica é definida como 1 se pelo menos um Estado de Picture in Picture ocorrer durante a sessão de reprodução. <br/> **Importante:** <br/> Se este evento estiver definido, o tempo é igual à duração do vídeo no estado Picture in Picture. Se este evento não for definido, nenhum valor será enviado..   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.pictureinpicture.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Duração total do Picture in Picture </li> <li> **Dados de contexto:**<br/> a.media.states.pictureinpicture.time<br/> </li> <li> **Feed de dados:**<br/> videostatepictureinpicturetime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.pictureinpicture.time </li> </ul> |


### Propriedades da função Em foco

#### Fluxos afetados pela função Em foco

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A quantidade de fluxos afetados pela função Em foco. Essa métrica é definida como 1 se pelo menos um Estado da função Em foco ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.infocus.set<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Fluxos afetados pela função Em foco </li> <li> **Dados de contexto:**<br/> a.media.states.infocus.set<br/> </li> <li> **Feed de dados:**<br/> videostateinfocus </li> <li> **Audience Manager:**<br/> c_contextdata.a.media.states.infocus.set </li> </ul> |


#### Contagens da função Em foco

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> O número de vezes que a função Em foco foi exibida. Essa métrica é definida como 1 se pelo menos um Estado da função Em foco ocorrer durante a sessão de reprodução. <br/> **Importante:**<br/> Se esse evento estiver definido, a contagem será igual ao número de vezes que o vídeo foi exibido no estado Em foco. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.infocus.count<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Contagem da função Em foco </li> <li> **Dados de contexto:**<br/> a.media.states.infocus.count<br/> </li> <li> **Feed de dados:**<br/> videostateinfocuscount </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.infocus.count </li> </ul> |


#### Duração total da função Em foco

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave de API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento de mídia </li> <li> **Versão mín. do SDK:**<br/> 3.0</li> <li> **Exemplo de valor:**<br/> VERDADEIRO </li><li> **Descrição:**<br/> A duração de tempo em que a função Em foco foi exibida. Essa métrica é definida como 1 se pelo menos um Estado da função Em foco ocorrer durante a sessão de reprodução. <br/> **Importante:** <br/> Se esse evento estiver definido, o tempo será igual ao tempo em que o vídeo ficou no estado Em foco. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> a.media.states.infocus.time<br/></li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Duração total da função Em foco </li> <li> **Dados de contexto:**<br/> a.media.states.infocus.time<br/> </li> <li> **Feed de dados:**<br/> videostateinfocustime </li> <li> **Audience Manager:**<br/> c_contextdata.media.states.infocus.time </li> </ul> |

## Lista de propriedades para identidades XDM

Os dados armazenados no Analytics podem ser usados para qualquer finalidade e as métricas do estado do player podem ser importadas para a Adobe Experience Platform usando o XDM e usadas com o Customer Journey Analytics.

| Propriedade do estado do player | Mapeamento |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## APIs relacionadas {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
