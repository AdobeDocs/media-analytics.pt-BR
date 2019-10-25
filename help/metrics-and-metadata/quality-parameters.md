---
seo-title: Parâmetros de qualidade
title: Parâmetros de qualidade
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Parâmetros de qualidade{#quality-parameters}

Este tópico contém a lista de dados de qualidade da experiência (QoE/Qos), incluindo os valores de dados de contexto, coletados pela Adobe por meio das variáveis da solução.

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

## Metadados de qualidade {#quality-metadata}

### Taxa média de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>media.qoe.bitrate </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 800-899 </li><li> **Descrição:**<br/>A taxa de bits média (em kbps). O valor é de buckets predefinidos em intervalos de 100 kbps. A Taxa média de bits é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução..  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> Pulsação: (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Average Bitrate </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Feed de dados:**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |



### Hora de início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.timeToStart </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 30 000 </li><li> **Descrição:**<br/>Esse valor assumirá zero como padrão se você não o definir por meio de QoSObject. Você define esse valor em milissegundos. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Pulsação: (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Time to Start </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>timeToStart) </li> <li> **Feed de dados:**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.framesPerSecond </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Start, Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 24 </li><li> **Descrição:**<br/>O valor atual da taxa de quadros do fluxo (em quadros por segundo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> ****<br/> Pulsação: (l:stream:fps) </li> </ul> | <ul> <li> **Disponível:**<br/>não </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>N/A </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>droppedFrames </li> <li> **Chave da API:**<br/>media.qoe.droppedFrames </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 3 </li><li> **Descrição:**<br/>O número de quadros ignorados (Int). Esse valor é calculado como uma soma de todas as quedas de quadros que ocorreram durante uma sessão de reprodução. Esse valor é obtido do último valor de (l:stream:dropped_frames).  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> Pulsação: (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Dropped Frames </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Feed de dados:**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Eventos de buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 2 </li><li> **Descrição:**<br/>O número de eventos de buffer. Essa métrica é calculada como uma contagem dos estados de buffer diferentes ocorridos durante uma sessão de reprodução. Essa é uma contagem de quantas vezes o reprodutor entra em um estado de buffer a partir de outros estados, por exemplo, reprodução ou pausa.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Buffer Events </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bufferCount) </li> <li> **Feed de dados:**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Duração total do buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** </li> <li> ****<br/> Valor da amostra: 30 </li><li> **Descrição:**<br/>A quantidade total de tempo, em segundos, gasto no buffer. Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Pulsação: (l:event:duration) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Total Buffer Duration </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bufferTime) </li> <li> **Feed de dados:**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Alterações da taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.bitrateChange </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 3 </li><li> **Descrição:**<br/>O número de alterações na taxa de bits (Número inteiro). Esse valor é calculado como uma soma dos eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Bitrate Changes </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Feed de dados:**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Erros/Eventos de erro

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 1 </li><li> **Descrição:**<br/>O número de erros ocorridos (Número inteiro). Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>errorCount) </li> <li> **Feed de dados:**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### IDs de erro do SDK do reprodutor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>as IDs de erro exclusivas geradas pelo SDK do player. Os clientes devem fornecer os códigos/IDs de erro na implementação por meio das APIs de erro fornecidas.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Feed de dados: videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### IDs de erro externo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>as IDs de erro exclusivas de qualquer fonte externa, por exemplo, erros de CDN. Os clientes devem fornecer os códigos/IDs de erro na implementação por meio das APIs de erro fornecidas.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Feed de dados: videoqoeextneralerrors </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### IDs de erro do SDK do Media

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>as IDs de erro exclusivas geradas pelo SDK de mídia durante a reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Feed de dados:** <br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul> |




### Fim da sessão {#session-end}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 2.1 </li> <li> ****<br/> Valor da amostra: end </li><li> **Descrição:**<br/>o evento end significa que o SDK está enviando uma chamada de fechamento para o backend. No recebimento desse evento, o backend encerrará a sessão deste vídeo e não executará mais nenhum processamento. <br/>Se a mídia foi concluída para 100%, isso deve ser enviado após `s:event:type=complete.` Ver [conteúdo concluído](audio-video-parameters.md#content-complete) para obter informações relacionadas. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> ****<br/> Pulsações: (s:event:type=end) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>N/A </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Métricas de qualidade {#quality-metrics}

### Hora de início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 30 000 </li><li> **Descrição:**<br/>Esse valor assumirá zero como padrão se você não o definir por meio de QoSObject. Você define esse valor em milissegundos. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Pulsação: (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Time to Start </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>timeToStart) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Eventos de buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 2 </li><li> **Descrição:**<br/>O número de eventos de buffer (Número inteiro). Essa métrica é calculada como uma contagem dos eventos de buffer que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Buffer Events </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bufferCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Duração total do buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 15 </li><li> **Descrição:**<br/>A quantidade total de tempo gasto no buffer (segundos; integer). Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Pulsação: (l:event:duration) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Total Buffer Duration </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bufferTime) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Alterações da taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>evento </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: "3" </li><li> **Descrição:**<br/>O número de alterações na taxa de bits. Esse valor é calculado como uma soma dos eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Bitrate Changes </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Erros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 1 </li><li> **Descrição:**<br/>O número de erros que ocorreram (Número inteiro). Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Eventos de erro </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>errorCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 1 </li><li> **Descrição:**<br/>O número de quadros ignorados (Número inteiro). Esse valor é calculado como uma soma de todas as quedas de quadros que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> Pulsação: (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Dropped Frames </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> </ul> |



### Quedas antes do início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de vezes que um usuário saiu do vídeo antes de iniciá-lo. Essa métrica é definida como 1 somente se nenhum conteúdo foi renderizado, independentemente dos anúncios.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Quedas antes do início </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pelo buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de fluxos afetados pelo buffer. Essa métrica é definida como 1 se pelo menos um evento de buffer ocorrer durante a sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>buffer) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados pelo buffer </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>buffer) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pela mudança na taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de fluxos nos quais ocorreram alterações na taxa de bits. Essa métrica é definida como 1 se pelo menos um evento de alteração de taxa de bits ocorrer durante a sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> ****<br/> Nome do relatório: Fluxos afetados pela alteração na taxa de bits </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bitrateChange) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Taxa média de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: 3200 </li><li> **Descrição:**<br/>A taxa de bits média (em kbps, inteiro). Essa métrica é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> Pulsação: (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Average Bitrate </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>bitrateAverage) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Fluxos afetados por erros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de fluxos nos quais um evento de erro ocorreu (isto é, `trackError` foi chamado durante a sessão de reprodução e uma chamada de `type=error` pulsação foi gerada). </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>error) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados por erros </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>error) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pela queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de fluxos nos quais os quadros foram descartados. Essa métrica é definida como 1 se ocorrer pelo menos uma queda de quadro durante a sessão de reprodução.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>droppedFrames) </li> <li> ****<br/> Pulsação: (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados por quedas de quadros </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>droppedFrames) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados por bloqueios

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de fluxos nos quais um evento parado ocorreu. Essa métrica é definida como 1 se tiver ocorrido, pelo menos, uma paralisação durante a reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stall) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Se esse evento estiver definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Eventos de paralização

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> ****<br/> Valor da amostra: "3" </li><li> **Descrição:**<br/>O número de vezes que a reprodução foi parada durante uma sessão de reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stallCount) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>stallCount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul> |



### Duração total da paralização

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Media Close </li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> ****<br/> Valor da amostra: 12 </li><li> **Descrição:**<br/>O tempo total (segundos; integer) a reprodução foi parada durante uma sessão de reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stallTime) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> </li> <li> ****<br/> Dados de contexto: (a.media.qoe.<br/>stallTime) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> |



## APIs relacionadas {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

