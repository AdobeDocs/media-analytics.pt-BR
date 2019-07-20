---
seo-title: Parâmetros de qualidade
title: Parâmetros de qualidade
uuid: 0 d 9 fa 764-edef -4178-8650-90 c 9 a 0852 a 57
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# Parâmetros de qualidade{#quality-parameters}

Este tópico contém a lista de dados de qualidade da experiência (QoE/Qos), incluindo os valores de dados de contexto, coletados pela Adobe por meio das variáveis da solução.

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

## Metadados de qualidade {#section_8467F9729DA04A888A2657712234D7C7}

### Taxa média de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>media.qoe.bitrate </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/>Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 800-899 </li><li> **Descrição:**<br/>A taxa média de bits (em kbps). O valor é de buckets predefinidos em intervalos de 100 kbps. A Taxa média de bits é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução..  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Heartbeat:**<br/> (l: fluxo: bitrate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Average Bitrate </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Feed de dados:**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaveragebucket) </li> </ul> |



### Hora de início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.timeToStart </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 30,000 </li><li> **Descrição:**<br/>Esse valor assumirá como padrão zero se você não a definir por meio do qosobject. Você define esse valor em milissegundos. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: fluxo: startup_ time) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Time to Start </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Feed de dados:**<br/>videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.framesPerSecond </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Início de mídia, Close Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 24 </li><li> **Descrição:**<br/>O valor atual da taxa de quadros do fluxo (em quadros por segundo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l: fluxo: fps) </li> </ul> | <ul> <li> **Disponível:**<br/>não </li> <li> **Variável reservada:**<br/>N/A </li> <li> **Nome do relatório:**<br/>N/A </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>droppedFrames </li> <li> **Chave da API:**<br/>media.qoe.droppedFrames </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 3 </li><li> **Descrição:**<br/>O número de quadros perdidos (Número inteiro). Esse valor é calculado como uma soma de todas as quedas de quadros que ocorreram durante uma sessão de reprodução. Esse valor é obtido a partir do último valor de (l: fluxo: drop_ frames.)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: fluxo:<br/>queda_ quadros) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Dropped Frames </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Feed de dados:**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Eventos de buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 2 </li><li> **Descrição:**<br/>O número de eventos de buffer. Essa métrica é calculada como uma contagem dos estados de buffer diferentes ocorridos durante uma sessão de reprodução. Essa é uma contagem de quantas vezes o reprodutor entra em um estado de buffer a partir de outros estados, por exemplo, reprodução ou pausa.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = buffer) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Buffer Events </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Feed de dados:**<br/>videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Duração total do buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** </li> <li> **Valor da amostra:**<br/> 30 </li><li> **Descrição:**<br/>O tempo total, em segundos, em buffer gasto. Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: evento: duration) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Total Buffer Duration </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Feed de dados:**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Alterações da taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.qoe.bitrateChange </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 3 </li><li> **Descrição:**<br/>O número de alterações de taxa de bits (Número inteiro). Esse valor é calculado como uma soma dos eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Bitrate Changes </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Feed de dados:**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Erros/Eventos de erro

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 1 </li><li> **Descrição:**<br/>O número de erros ocorridos (Número inteiro). Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Feed de dados:**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### IDs de erro do SDK do reprodutor

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>As IDs de erro únicas geradas pelo SDK do player. Os clientes devem fornecer os códigos/IDs de erro na implementação por meio das APIs de erro fornecidas.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Feed de dados:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Playersdkerrors) </li> </ul> |



### IDs de erro externo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>As IDs de erro exclusivas de qualquer fonte externa, por exemplo, erros de CDN. Os clientes devem fornecer os códigos/IDs de erro na implementação por meio das APIs de erro fornecidas.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Feed de dados:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Externalerrors) </li> </ul> |



### IDs de erro do SDK do Media

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>As IDs de erro únicas geradas pelo Media SDK durante a reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Errors </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Feed de dados:** <br/>mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Mediasdkerrors) </li> </ul> |




### Fim da sessão {#session-end}

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave de API:**<br/> </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 2.1 </li> <li> **Valor da amostra:**<br/> end </li><li> **Descrição:**<br/>O evento final significa que o SDK está enviando uma chamada close para o backend. No recebimento desse evento, o backend encerrará a sessão deste vídeo e não executará mais nenhum processamento. <br/>Se a mídia foi concluída para 100%, isso deve ser enviado depois `s:event:type=complete.` de Consultar [conteúdo concluído](audio-video-parameters.md#content-complete) para informações relacionadas. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>N/A </li> <li> **Pulsações:**<br/> (s: evento: type = end) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>N/A </li> <li> **Dados de contexto:**<br/> </li> <li> **Feed de dados:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Métricas de qualidade {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### Hora de início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 30,000 </li><li> **Descrição:**<br/>Esse valor assumirá como padrão zero se você não a definir por meio do qosobject. Você define esse valor em milissegundos. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: fluxo: startup_ time) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Time to Start </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Feed de dados:**<br/>videoqoetimetostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### Eventos de buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 2 </li><li> **Descrição:**<br/>O número de eventos de buffer (Número inteiro). Essa métrica é calculada como uma contagem dos eventos de buffer que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = buffer) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Buffer Events </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Feed de dados:**<br/>videoqoebuffercount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Duração total do buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 15 </li><li> **Descrição:**<br/>A quantidade total de buffering de tempo gasto (segundos; número inteiro). Esse valor é calculado como uma soma da duração de todos os eventos de buffer que ocorreram durante uma sessão de reprodução. O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: evento: duration) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Total Buffer Duration </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Feed de dados:**<br/>videoqoebuffertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Alterações da taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>evento </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> " 3 " </li><li> **Descrição:**<br/>O número de alterações da taxa de bits. Esse valor é calculado como uma soma dos eventos de alteração da taxa de bits ocorridos durante uma sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Bitrate Changes </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Feed de dados:**<br/>videoqoebitratechangecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Erros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 1 </li><li> **Descrição:**<br/>O número de erros que ocorreram (Número inteiro). Esse valor é calculado como uma soma de todos os eventos de erro que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Eventos de erro </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Errorcount) </li> <li> **Feed de dados:**<br/>videoqoeerrorcount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount) </li> </ul> |



### Queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 1 </li><li> **Descrição:**<br/>O número de quadros perdidos (Número inteiro). Esse valor é calculado como uma soma de todas as quedas de quadros que ocorreram durante uma sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: fluxo:<br/>queda_ quadros) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Dropped Frames </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Feed de dados:**<br/>videoqoedroppedframecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Quedas antes do início

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>O número de vezes que um usuário sai do vídeo antes do início. Essa métrica é definida como 1 somente se nenhum conteúdo foi renderizado, independentemente dos anúncios.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = aa_ start) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Quedas antes do início </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Feed de dados:**<br/>videoqoedropbeforestart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Dropbeforestart) </li> </ul> |



>[!IMPORTANT]
>Se esse evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pelo buffer

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>O número de fluxos afetados por buffering. Essa métrica é definida como 1 se pelo menos um evento de buffer ocorrer durante a sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = buffer) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados pelo buffer </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Feed de dados:**<br/>videoqoebuffer </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Se esse evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pela mudança na taxa de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>O número de fluxos nos quais ocorreram alterações na taxa de bits. Essa métrica é definida como 1 se pelo menos um evento de alteração de taxa de bits ocorrer durante a sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados pela alteração do buffer </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Bitratechange) </li> <li> **Feed de dados:**<br/>videoqoebitratechange </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechange) </li> </ul> |



>[!IMPORTANT]
>Se esse evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Taxa média de bits

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> 3200 </li><li> **Descrição:**<br/>A taxa média de bits (em kbps, integer). Essa métrica é calculada como uma média ponderada de todos os valores de taxa de bits relacionados à duração da reprodução ocorridos durante a sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Heartbeat:**<br/> (l: fluxo: bitrate) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Average Bitrate </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Bitrateaverage) </li> <li> **Feed de dados:**<br/>videoqoebitrateaverage </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaverage) </li> </ul> |



### Fluxos afetados por erros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>O número de fluxos nos quais ocorreram alterações na taxa de bits. Essa métrica é definida como 1 se pelo menos um evento de alteração de taxa de bits ocorrer durante a sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados por erros </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>error) </li> <li> **Feed de dados:**<br/>videoqoeerror </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Se esse evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados pela queda de quadros

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** Any </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>O número de fluxos em que os quadros foram soltos. Essa métrica é definida como 1 se ocorrer pelo menos uma queda de quadro durante a sessão de reprodução.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Heartbeat:**<br/> (l: fluxo:<br/>queda_ quadros) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/>Fluxos impactados por quedas de quadros </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **Feed de dados:**<br/>videoqoedroppedframes </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>Se esse evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Fluxos afetados por bloqueios

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> **Valor da amostra:**<br/> VERDADEIRO </li><li> **Descrição:**<br/>O número de fluxos nos quais um evento delimitado ocorreu. Essa métrica é definida como 1 se tiver ocorrido, pelo menos, uma paralisação durante a reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = stall) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Se esse evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.

### Eventos de paralização

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> **Valor da amostra:**<br/> " 3 " </li><li> **Descrição:**<br/>O número de vezes que a reprodução foi parada durante uma sessão de reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = stall) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stallcount) </li> </ul> |



### Duração total da paralização

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>number </li> <li> **Enviado com:**<br/> Media Close </li> <li> **Versão mín. do SDK:** 1.5+ </li> <li> **Valor da amostra:**<br/> 12 </li><li> **Descrição:**<br/>O tempo total (segundos; número inteiro) a reprodução foi interrompida durante uma sessão de reprodução. Os clientes terão que criar suas próprias regras de processamento para que o valor esteja disponível para os relatórios.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = stall) </li> </ul> | <ul> <li> **Disponível:**<br/>usar regra de processamento personalizada </li> <li> **Variável reservada:**<br/>event </li> <li> **Nome do relatório:**<br/> </li> <li> **Dados de contexto:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Feed de dados:**<br/>N/A </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stalltime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

