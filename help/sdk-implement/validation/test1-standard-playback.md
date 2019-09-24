---
seo-title: Test 1  Standard playback
title: Reprodução padrão do teste 1
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Teste 1: reprodução padrão{#test-standard-playback}

Esse caso de teste valida a reprodução e a sequência gerais. É um elemento obrigatório da sua solicitação de certificação.

## Formulário de solicitação de certificação

**Baixe o formulário de solicitação de certificação aqui: ==&gt;Formulário de solicitação** de [certificação.](cert_req_form.docx)

## Visão geral do Teste de certificação 1

As implementações do Media Analytics incluem dois tipos de chamadas de rastreamento:
* Chamadas feitas diretamente no servidor do Adobe Analytics (AppMeasurement) - Essas chamadas ocorrem em eventos "Media Start" e "Ad Start".
* Chamadas feitas ao servidor do Media Analytics (pulsações) - Incluem chamadas em banda e fora de banda:
   * Em banda - O SDK envia chamadas de reprodução programadas ou "ping" em intervalos de 10 segundos durante a reprodução do conteúdo e em intervalos de um segundo durante os anúncios.
   * Fora de banda - Essas chamadas podem ocorrer a qualquer momento e incluem pausa, buffering, erros, conteúdo concluído, anúncio concluído etc.

>[!NOTE]
>O rastreamento de mídia se comporta da mesma maneira em todas as plataformas.

## Procedimento de ensaio

Conclua e registre as seguintes ações (em ordem):

1. **Carregar a página ou o aplicativo**

   **Servidores de rastreamento** (para todos os sites e aplicativos móveis):

   * **Servidor do Adobe Analytics (AppMeasurement) -** É necessário um servidor de rastreamento RDC ou CNAME que seja resolvido para um servidor de rastreamento RDC para o serviço de ID de visitante da Experience Cloud. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Servidor do Media Analytics (Heartbeats) -** Este servidor sempre tem o formato "`[namespace].hb.omtrdc.net`", onde `[namespace]` especifica o nome da sua empresa. Esse nome é fornecido pela Adobe.
   É necessário validar determinadas variáveis principais que são universais em todas as chamadas de rastreamento:

   **Adobe Visitor ID (`mid`):** The `mid` variable is used to capture the value set in the AMCV cookie. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. It is found in both Adobe Analytics (AppMeasurement) and Media Analytics (heartbeats) calls.

   * **Chamada de início do Adobe Analytics**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chamada de página do site**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chamada de ciclo de vida**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chamada de início do Media Analytics**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >On Media Analytics Start calls () the  values may not be present. `s:event:type=start``mid` Isso está certo. They may not appear until the Media Analytics Play calls ( ).`s:event:type=play`

   * **Media Analytics Play call**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Iniciar o media player**

   When the media player starts, the Media SDK sends the key calls to the two servers in the following order:

   1. Adobe Analytics server - Start call
   1. Media Analytics server - Start call
   1. Media Analytics server - "Adobe Analytics Start call requested"
   The first two calls above contain additional metadata and variables. For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   The third call above tells the Media Analytics server that the Media SDK requested that the Adobe Analytics Start call () be sent to the Adobe Analytics server.`pev2=ms_s`

1. **Exibir ad break, se disponível**

   * **Início do anúncio**
   Quando o anúncio é iniciado, as seguintes chamadas principais são enviadas na seguinte ordem:

   1. Adobe Analytics server - Ad Start call
   1. Servidor do Media Analytics - Chamada de início de anúncio
   1. Servidor do Media Analytics - "Chamada de início de anúncio do Adobe Analytics solicitada"
   As primeiras duas chamadas contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   A terceira chamada informa ao servidor do Media Analytics que o SDK de mídia solicitou que a chamada (`pev2=msa_s`) Ad Start do Adobe Analytics fosse enviada para o servidor do Adobe Analytics.

   * **Reprodução do anúncio**

      During ad playback, the Media Analytics SDK sends play events of type "ad" to the Media Analytics server every second.

   * **Anúncio concluído**

      At the 100% point of an ad, a Media Analytics Complete call should be sent.



1. **Pausar a reprodução de anúncio por 30 segundos, se disponível.**  **Pausa do anúncio**

   During Ad Pause, Media Analytics heartbeat or "ping" calls are sent by the SDK to the Media Analytics server every second.

   >[!NOTE]
   >
   >The playhead value should remain constant during the pause.

   Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Reproduzir o conteúdo principal por 10 minutos sem interrupções.**  **Reprodução de conteúdo**

   Durante a reprodução do conteúdo principal, o SDK de mídia envia pulsações (chamadas de Reprodução) para o servidor do Media Analytics a cada 10 segundos.

   Notas:

   * A posição do indicador de reprodução deve aumentar em 10 com cada chamada Play.
   * O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

      Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pausar durante a reprodução por, pelo menos, 30 segundos.** Ao pausar o player de mídia, as chamadas de evento de pausa serão enviadas pelo SDK para o servidor do Media Analytics a cada 10 segundos. Quando a pausa termina, os eventos de reprodução são retomados.

   Para obter parâmetros de chamada e metadados, consulte Detalhes da chamada [de teste.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Buscar/depurar mídia.** Ao depurar o indicador de reprodução de mídia, nenhuma chamada de rastreamento especial é enviada, no entanto, quando a reprodução de mídia é retomada após a depuração, o valor do indicador de reprodução deve refletir a nova posição no conteúdo principal.

1. **Mídia de reprodução (apenas VOD).** Quando a mídia é reproduzida, um novo conjunto de chamadas de Media Start deve ser enviado (como se fosse uma nova inicialização).

1. **Exibir a próxima mídia na lista de reprodução.** No Media Start da próxima mídia em uma lista de reprodução, um novo conjunto de chamadas Media Start deve ser enviado.

1. **Mude mídia ou fluxo.** When switching live streams, a Media Analytics complete call for the first stream should not be sent. The Media Start calls and Play calls should begin with the new show and stream name, and with the correct playhead and duration values for the new show.

