---
seo-title: Parâmetros de capítulo
title: Parâmetros de capítulo
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Parâmetros de capítulo{#chapter-parameters}

Este tópico apresenta uma lista de dados de capítulo e/ou segmento, incluindo valores de dados de contexto, que a Adobe coleta por meio de variáveis de solução.

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

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada abaixo descrita em Relatório/Variável reservada como "classificação".\
>As classificações de mídia são definidas quando um conjunto de relatórios é ativado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe adicionará os que estiverem faltando novamente.

## Metadados de capítulo {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### Nome do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>media.chapter.friendlyName </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Início do capítulo, Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> ****<br/> Valor da amostra: "The Big Bang Chapter 2 - Dating" </li><li> **Descrição:**<br/>O nome do capítulo e/ou do segmento.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>friendlyName) </li> <li> ****<br/> Pulsação: (s:stream:chapter_name) </li> </ul> | <ul> <li> **Disponível:**<br/>Created by default...  </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Chapter Name </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>friendlyName) </li> <li> **Feed de dados:**<br/>N/A </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> </ul> |

### Posição do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>media.chapter.index </li> <li> ****<br/> Obrigatório: SDK: Não; API: Sim. </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> ****<br/> Valor da amostra: 2 </li><li> **Descrição:**<br/>A posição (índice, número inteiro) do capítulo dentro do conteúdo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>position) </li> <li> ****<br/> Pulsação: (l:stream:chapter_pos) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Chapter Position </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>position) </li> <li> **Feed de dados:**<br/> </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>position) </li> </ul> |

### Deslocamento do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **Chave da API:**<br/>media.chapter.offset </li> <li> ****<br/> Obrigatório: SDK: Não; API: Sim. </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> ****<br/> Valor da amostra: 58 </li><li> **Descrição:**<br/>O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>offset) </li> <li> ****<br/> Pulsação: (l:stream:chapter_offset) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Chapter Offset </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>offset) </li> <li> **Feed de dados:**<br/> </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>offset) </li> </ul> |

### Extensão do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/> </li> <li> **Chave da API:**<br/>media.chapter.length </li> <li> ****<br/> Obrigatório: SDK: Não; API: Sim. </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> ****<br/> Valor da amostra: 486 </li><li> **Descrição:**<br/>A duração do capítulo, em segundos.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>length) </li> <li> ****<br/> Pulsação: (l:stream:chapter_length) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>Classification </li> <li> **Nome do relatório:**<br/>Chapter Length </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>length) </li> <li> **Feed de dados:**<br/> </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>length) </li> </ul> |

### Capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>No </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>a ID gerada automaticamente do capítulo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>name) </li> <li> ****<br/> Pulsação: (s:stream:chapter_id) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>eVar </li> <li> **Expiração:**<br/>On HIT </li> <li> **Nome do relatório:**<br/>Chapter </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>name) </li> <li> **Feed de dados:**<br/>videochapter </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>name) </li> </ul> |

## Métricas de capítulo {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### Início do capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set  </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> **Envido com:**<br/>Início do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de inícios do capítulo.  **Importante:** se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>exibir) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> ****<br/> Nome do relatório: Capítulo Inicia g </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>exibir) </li> <li> **Feed de dados:**<br/>videochapterstart </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>exibir) </li> </ul> |

### Capítulo concluído

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set  </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>sequência de caracteres </li> <li> ****<br/> Enviado com: Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3</li> <li> ****<br/> Valor da amostra: TRUE </li><li> **Descrição:**<br/>O número de conclusões do capítulo.  **Importante:** se este evento for definido, o único valor possível será VERDADEIRO. Se este evento não for definido, nenhum valor será enviado.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>concluído) </li> <li> ****<br/> Pulsação: (s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> ****<br/> Nome do relatório: Capítulo conclui g </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>concluído) </li> <li> **Feed de dados:**<br/>videochaptercomplete </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>concluído) </li> </ul> |

### Tempo gasto com capítulo

|   Implementação   | Parâmetros de rede | Relatórios |
| --- | --- | --- |
| <ul> <li> **Chave de SDK:**<br/>Automatically set  </li> <li> **Chave da API:**<br/>N/A </li> <li> **Obrigatório:**<br/>Yes </li> <li> **Tipo:**<br/>number </li> <li> ****<br/> Enviado com: Fechamento do capítulo </li> <li> **Versão mín. do SDK:** 1.3 </li> <li> **Valor da amostra:**<br/> </li><li> **Descrição:**<br/>o tempo gasto no capítulo.  O valor será exibido no formato de hora (HH:MM:SS) no Analysis Workspace e nos Reports &amp; Analytics. Nos Feeds de dados, Data Warehouse e APIs de relatórios, os valores serão exibidos em segundos. <br/>**Data de lançamento: 13/09/18**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponível:**<br/>Yes </li> <li> **Variável reservada:**<br/>event </li> <li> ****<br/> Nome do relatório: Tempo gasto no capítulo g </li> <li> ****<br/> Dados de contexto: (a.media.chapter.<br/>timePlayed) </li> <li> **Feed de dados:**<br/>videochaptertime </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> </ul> |

## APIs relacionadas {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
