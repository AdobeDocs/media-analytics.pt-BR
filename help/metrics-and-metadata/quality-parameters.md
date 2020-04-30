---
title: Parâmetros de qualidade
description: null
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Parâmetros de qualidade {#quality-parameters}

Este tópico contém a lista de dados de qualidade da experiência (QoE/Qos), incluindo os valores de dados de contexto, coletados pela Adobe por meio das variáveis da solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação
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

## Metadados de qualidade {#quality-metadata}

### Taxa média de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>media.qoe.bitrate</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 800-899</li><li> **Descrição:**<br/>A taxa média de bits (em kbps). O valor é de períodos predefinidos em intervalos de 100 kbps. A taxa média de bits é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bitrateAverageBucket)</li> <li> **Heartbeat:**<br/>(l:stream:bitrate)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Taxa média de bits</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bitrateAverageBucket)</li> <li> **Feed de dados:**<br/>videoqoebitrateaverageevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket)</li> </ul> |


### Hora de início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.timeToStart</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Início de mídia, Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 30.000</li><li> **Descrição:**<br/>Esse valor é definido para o padrão zero se você não configurá-lo pelo QoSObject. Você define esse valor em milissegundos. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Heartbeat:**<br/>(l:stream:startup_time)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Time to Start</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Feed de dados:**<br/>videoqoetimetostartevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>timeToStart)</li> </ul> |


### FPS

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.framesPerSecond</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Início de mídia, Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 24</li><li> **Descrição:**<br/>O valor atual da taxa de quadros do fluxo (em quadros por segundo).</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/>(l:stream:fps)</li> </ul> | <ul> <li> **Disponível:**<br/>Não</li> <li> **Variável reservada:**<br/>N/D</li> <li> **Nome do relatório:**<br/>N/D</li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/> </li> </ul> |



### Queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>droppedFrames</li> <li> **Chave da API:**<br/>media.qoe.droppedFrames</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 3</li><li> **Descrição:**<br/>O número de quadros ignorados (Int). Esse valor é calculado como uma soma de todas as quedas de quadros que ocorreram durante uma sessão de reprodução. Este valor é obtido do último valor de (l:stream:dropped_frames).</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>droppedFrameCount)</li> <li> **Heartbeat:**<br/>(l:stream:<br/>dropped_frames)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Dropped Frames</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>droppedFrameCount)</li> <li> **Feed de dados:**<br/>videoqoedroppedframecountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount)</li> </ul> |



### Eventos de buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 2</li><li> **Descrição:**<br/>O número de eventos de buffer. Essa métrica é calculada como uma contagem dos estados de buffer diferentes ocorridos durante uma sessão de reprodução. Essa é uma contagem de quantas vezes o reprodutor entra em um estado de buffer a partir de outros estados, por exemplo, reprodução ou pausa.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=buffer)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Evento de buffer</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Feed de dados:**<br/>videoqoebuffercountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferCount)</li> </ul> |



### Duração total do buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** </li> <li> **Valor de exemplo:**<br/> 30</li><li> **Descrição:**<br/>A quantidade total de tempo gasto com buffering, em segundos. Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.<br/>**Data de lançamento: 13/09/18**</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Pulsação:**<br/>(l:event:duration)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Total Buffer Duration</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Feed de dados:**<br/>videoqoebuffertimeevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferTime)</li> </ul> |



### Alterações da taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.bitrateChange</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 3</li><li> **Descrição:**<br/>O número de alterações da taxa de bits (número inteiro). Esse valor é calculado como uma soma dos eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=bitrate_change)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Bitrate Changes</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Feed de dados:**<br/>videoqoebitratechangecountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount)</li> </ul> |



### Erros/Eventos de erro

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 1</li><li> **Descrição:**<br/>O número de erros ocorridos (número inteiro). Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Errors</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Feed de dados:**<br/>videoqoeerrorcountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>errorCount)</li> </ul> |



### IDs de erro do SDK do reprodutor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/>As IDs de erro exclusivas geradas pelo SDK do reprodutor. Os clientes devem fornecer os códigos/IDs de erro na implementação por meio das APIs de erro fornecidas.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>playerSdkErrors)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Errors</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>playerSdkErrors)</li> <li> **Feed de dados:**<br/>videoqoeplayersdkerrors</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors)</li> </ul> |



### IDs de erro externo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/>As IDs de erro exclusivas de qualquer origem externa, por exemplo, erros de CDN. Os clientes devem fornecer os códigos/IDs de erro na implementação por meio das APIs de erro fornecidas.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>externalErrors)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Errors</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>externalErrors)</li> <li> **Feed de dados:**<br/>videoqoeextneralerrors</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>externalErrors)</li> </ul> |



### IDs de erro do SDK do Media

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/>As IDs de erro exclusivas geradas pelo SDK do Media durante a reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>mediaSdkErrors)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>eVar</li> <li> **Expiração:**<br/>No HIT</li> <li> **Nome do relatório:**<br/>Errors</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>mediaSdkErrors)</li> <li> **Feed de dados:**<br/>mediaqoeexternalerrors</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors)</li> </ul> |




### Fim da sessão {#session-end}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave de API:**<br/> </li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** 2.1 </li> <li> **Exemplo de valor:**<br/> fim</li><li> **Descrição:**<br/>O evento de fim significa que o SDK está enviando uma chamada de fechamento para o back-end. No recebimento desse evento, o backend encerrará a sessão deste vídeo e não executará mais nenhum processamento.<br/>Se a mídia foi concluída em 100%, isso deve ser enviado após`s:event:type=complete.`Ver[conteúdo concluído](audio-video-parameters.md#content-complete)para obter informações relacionadas.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/D</li> <li> **Heartbeat:**<br/>(s:event:type=end)</li> </ul> | <ul> <li> **Disponível:**<br/>Usar regra de processamento personalizada</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>N/D</li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/> </li> </ul> |



## Métricas de qualidade {#quality-metrics}

### Hora de início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 30.000</li><li> **Descrição:**<br/>Esse valor é definido para o padrão zero se você não configurá-lo pelo QoSObject. Você define esse valor em milissegundos. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.<br/>**Data de lançamento: 13/09/18**</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Heartbeat:**<br/>(l:stream:startup_time)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Time to Start</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>timeToStart)</li> </ul> |



### Eventos de buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 2</li><li> **Descrição:**<br/>O número de eventos de buffer (número inteiro). Essa métrica é calculada como uma contagem dos eventos de buffer que ocorreram durante uma sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=buffer)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Evento de buffer</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferCount)</li> </ul> |



### Duração total do buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 15</li><li> **Descrição:**<br/>A quantidade total de tempo gasto com buffering (segundos; número inteiro). Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.<br/>**Data de lançamento: 13/09/18**</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Pulsação:**<br/>(l:event:duration)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Total Buffer Duration</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferTime)</li> </ul> |



### Alterações da taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>evento</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> &quot;3&quot;</li><li> **Descrição:**<br/>A quantidade de alterações da taxa de bits. Esse valor é calculado como uma soma dos eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=bitrate_change)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Bitrate Changes</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount)</li> </ul> |



### Erros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 1</li><li> **Descrição:**<br/>O número de erros que ocorreram (Número inteiro). Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Eventos de erro</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>errorCount)</li> </ul> |



### Queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 1</li><li> **Descrição:**<br/>O número de quadros ignorados (número inteiro). Esse valor é calculado como uma soma de todas as quedas de quadros que ocorreram durante uma sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>droppedFrameCount)</li> <li> **Heartbeat:**<br/>(l:stream:<br/>dropped_frames)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Dropped Frames</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>droppedFrameCount)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount)</li> </ul> |



### Quedas antes do início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE</li><li> **Descrição:**<br/>O número de vezes que um usuário saiu do vídeo antes de seu início. Essa métrica é definida como 1 somente se nenhum conteúdo foi renderizado, independentemente dos anúncios.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>dropBeforeStart)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=aa_start)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Quedas antes do início</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>dropBeforeStart)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart)</li> </ul> |



>[!IMPORTANT]
>Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pelo buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE</li><li> **Descrição:**<br/>A quantidade de fluxos afetados pelo buffer. Essa métrica é definida como 1 se pelo menos um evento de buffer ocorrer durante a sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>buffer)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=buffer)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Fluxos impactados pelo buffer</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>buffer)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>buffer)</li> </ul> |



>[!IMPORTANT]
>Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pela mudança na taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE</li><li> **Descrição:**<br/>A quantidade de fluxos nos quais ocorreram as mudanças de taxa de bits. Essa métrica é definida como 1 se pelo menos um evento de alteração de taxa de bits ocorrer durante a sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bitrateChange)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=bitrate_change)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Fluxos impactados pela alteração da taxa de bits</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bitrateChange)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateChange)</li> </ul> |



>[!IMPORTANT]
>Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Taxa média de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor de exemplo:**<br/> 3200</li><li> **Descrição:**<br/>A taxa média de bits (em kbps, número inteiro). Essa métrica é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>bitrateAverage)</li> <li> **Heartbeat:**<br/>(l:stream:bitrate)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Taxa média de bits</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>bitrateAverage)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage)</li> </ul> |



### Fluxos afetados por erros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE</li><li> **Descrição:**<br/>O número de fluxos nos quais um evento de erro ocorreu (isto é,`trackError`foi chamado durante a sessão de reprodução e uma chamada de`type=error`heartbeat foi gerada).</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>error)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Fluxos impactados por erros</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>error)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>error)</li> </ul> |



>[!IMPORTANT]
>Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pela queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** Any </li> <li> **Exemplo de valor:**<br/> TRUE</li><li> **Descrição:**<br/>A quantidade de fluxos com quedas de quadros. Essa métrica é definida como 1 se ocorrer pelo menos uma queda de quadro durante a sessão de reprodução.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>droppedFrames)</li> <li> **Heartbeat:**<br/>(l:stream:<br/>dropped_frames)</li> </ul> | <ul> <li> **Disponível:**<br/>Sim</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/>Fluxos impactados por quedas de quadros</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>droppedFrames)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>droppedFrames)</li> </ul> |



>[!IMPORTANT]
>Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados por bloqueios

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> **Exemplo de valor:**<br/> TRUE</li><li> **Descrição:**<br/>O número de fluxos nos quais ocorreram eventos de paralisação. Essa métrica é definida como 1 se pelo menos um stall ocorrer durante a reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>stall)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=stall)</li> </ul> | <ul> <li> **Disponível:**<br/>Usar regra de processamento personalizada</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/> </li> <li> **Feed de dados:**<br/>N/D</li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>stall)</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>stall)</li> </ul> |



>[!IMPORTANT]
>Se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Eventos de paralisação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>sequência de caracteres</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> **Valor de exemplo:**<br/> &quot;3&quot;</li><li> **Descrição:**<br/>O número de vezes que a reprodução foi paralisada durante uma sessão de reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>stallCount)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=stall)</li> </ul> | <ul> <li> **Disponível:**<br/>Usar regra de processamento personalizada</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>stallCount)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>stallCount)</li> </ul> |



### Duração total da paralisação

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Definida automaticamente</li> <li> **Chave da API:**<br/>N/D</li> <li> **Obrigatório:**<br/>Não</li> <li> **Tipo:**<br/>número</li> <li> **Enviado com:**<br/>Fechamento de mídia</li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> **Valor de exemplo:**<br/> 12</li><li> **Descrição:**<br/>O tempo total (segundos; número inteiro) que a reprodução ficou paralisada durante uma sessão de reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/>(a.media.qoe.<br/>stallTime)</li> <li> **Heartbeat:**<br/>(s:event:<br/>type=stall)</li> </ul> | <ul> <li> **Disponível:**<br/>Usar regra de processamento personalizada</li> <li> **Variável reservada:**<br/>event</li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/>(a.media.qoe.<br/>stallTime)</li> <li> **Feed de dados:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>stallTime)</li> </ul> |



## APIs relacionadas {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

