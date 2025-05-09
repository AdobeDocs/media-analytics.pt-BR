---
title: Parâmetros de capítulo
description: Saiba mais sobre parâmetros de capítulo para implementação, rede e relatórios.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ebabbe52fe673e3fb6f13da40bbc3c87aef1c7bd
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 91%

---

# Parâmetros de capítulo{#chapter-parameters}

Este tópico apresenta uma lista de dados de capítulo e/ou segmento, incluindo valores de dados de contexto, que a Adobe coleta por meio de variáveis de solução.

Descrição dos dados da tabela:

* **Implementação:** informações sobre valores e requisitos de implementação.
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
>Não altere os nomes de classificação de nenhuma variável listada abaixo descrita em Relatório/Variável reservada como “classificação”.\
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe os adicionará novamente.

## Metadados de capítulo {#chapter-metadata}

### Nome do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/> media.chapter.friendlyName </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Exemplo de valor:**<br/> “The Big Bang Capítulo 2 – Dating” </li><li> **Descrição:**<br/> O nome do capítulo e/ou segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (<code>s:stream:chapter_name</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Created by default...  </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Chapter Name </li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>friendlyName) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetReference._dc.title</li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### Posição do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/> media.chapter.index </li> <li> **Obrigatório:**<br/> SDK: Não; API: Sim. </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor de exemplo:**<br/> 2 </li><li> **Descrição:**<br/> A posição (índice, número inteiro) do capítulo dentro do conteúdo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (<code>l:stream:chapter_pos</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Chapter Position </li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>position) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.index</li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.chapterDetails.index </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### Deslocamento do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/> media.chapter.offset </li> <li> **Obrigatório:**<br/> SDK: Não; API: Sim. </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor de exemplo:**<br/> 58 </li><li> **Descrição:**<br/> O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (<code>l:stream:chapter_offset</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Chapter Offset </li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>offset) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.offset</li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.chapterDetails.offset </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### Extensão do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/> media.chapter.length </li> <li> **Obrigatório:**<br/> SDK: Não; API: Sim. </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor de exemplo:**<br/> 486 </li><li> **Descrição:**<br/> O comprimento do capítulo, em segundos.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (<code>l:stream:chapter_length)</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> Classification </li> <li> **Nome do relatório:**<br/> Chapter Length </li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>length) </li> <li> **Feed de dados:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>length) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetReference._xmpDM.duration</li> <li> **Caminho do campo XDM da coleção:**<br/> mediaCollection.chapterDetails.length </li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### Capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Não </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/> A ID gerada automaticamente do capítulo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (<code>s:stream:chapter_id</code>) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> eVar </li> <li> **Expiração:**<br/> No HIT </li> <li> **Nome do relatório:**<br/> Chapter </li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>name) </li> <li> **Feed de dados:**<br/> videochapter </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>name) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>chapterAssetReference._id</li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## Métricas de capítulo {#chapter-Metrics}

### Início do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Exemplo de valor:**<br/> TRUE </li><li> **Descrição:**<br/> O número de inícios de capítulo.  **Importante:** se este evento for definido, o único valor possível será TRUE. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (<code>s:event:</code><br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Chapter Starts</li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>view) </li> <li> **Feed de dados:**<br/> videochapterstart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>view) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>impressões.value > 0 => &quot;TRUE&quot;</li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### Capítulo concluído

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> sequência de caracteres </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3</li> <li> **Exemplo de valor:**<br/> TRUE </li><li> **Descrição:**<br/> O número de conclusões de capítulo.  **Importante:** se este evento for definido, o único valor possível será TRUE. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Heartbeat:**<br/> (<code>s:event:</code><br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Chapter Completes</li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>complete) </li> <li> **Feed de dados:**<br/> videochaptercomplete </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>completes.value</li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### Tempo gasto com capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **Chave de SDK:**<br/> Definida automaticamente  </li> <li> **Chave da API:**<br/> N/D </li> <li> **Obrigatório:**<br/> Sim </li> <li> **Tipo:**<br/> número </li> <li> **Enviado com:**<br/> Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor de exemplo:**<br/>  </li><li> **Descrição:**<br/> O tempo gasto com capítulo.  O valor será exibido no formato de hora (<code>HH:MM:SS</code>) no Analysis Workspace. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos.</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/> Sim </li> <li> **Variável reservada:**<br/> event </li> <li> **Nome do relatório:**<br/> Tempo gasto com capítulo</li> <li> **Dados de contexto:**<br/> (a.media.chapter.<br/>timePlayed) </li> <li> **Feed de dados:**<br/> videochaptertime </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **Caminho do campo XDM:** (obsoleto)<br/>media.mediaTimed.mediaChapter.<br/>timePlayed.value</li> <li> **Caminho do campo XDM do relatório:**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## APIs relacionadas {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
