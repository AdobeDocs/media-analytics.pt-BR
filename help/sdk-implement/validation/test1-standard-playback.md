---
seo-title: Reprodução do Test 1 Standard
title: Reprodução do Test 1 Standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Teste 1: reprodução padrão{#test-standard-playback}

Esse caso de teste valida a reprodução e o sequenciamento gerais. É um elemento obrigatório da solicitação de certificação.

## Formulário de solicitação de certificação

**Baixe o formulário de solicitação de certificação aqui: = = &gt;**  [Formulário de solicitação de certificação.](cert_req_form.docx)

## Visão geral do Test Test 1

As implementações do Media Analytics incluem dois tipos de chamadas de rastreamento:
* Chamadas feitas diretamente ao servidor do Adobe Analytics (appmeasurement) - essas chamadas ocorrem nos eventos «Início de mídia» e «Início do anúncio».
* Chamadas feitas ao servidor do Media Analytics (heartbeats) - incluem chamadas em banda e fora de banda:
   * Em banda - o SDK envia chamadas de play cronometradas ou "pings" em intervalos de 10 segundos durante a reprodução do conteúdo e intervalos de um segundo durante os anúncios.
   * Fora da banda - Essas chamadas podem ocorrer em qualquer momento e incluem Pausar, Buffering, erros, conteúdo concluído, anúncio concluído etc.

>[!NOTE]
>O rastreamento de mídia comporta-se o mesmo em todas as plataformas.

## Procedimento de teste

Complete e grave as seguintes ações (na ordem):

1. **Carregar a página ou o aplicativo**

   **Servidores de rastreamento** (para todos os sites e aplicativos móveis):

   * **Servidor do Adobe Analytics (appmeasurement) -** um servidor de rastreamento RDC ou CNAME que resolve um servidor de rastreamento RDC é necessário para o serviço de ID de visitante da Experience Cloud. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Servidor de Media Analytics (Heartbeats) -** este servidor sempre tem o formato "`[namespace].hb.omtrdc.net`, onde `[namespace]` especifica o nome da empresa. Esse nome é fornecido pela Adobe.
   É necessário validar determinadas variáveis principais que são universais em todas as chamadas de rastreamento:

   **ID de visitante da Adobe (`mid`):** `mid` A variável é usada para capturar o valor definido no cookie AMCV. `mid` A variável é o valor de identificação principal para sites e aplicativos móveis, além de indicar que o serviço de ID de visitante da Experience Cloud está configurado adequadamente. Ele é encontrado nas chamadas do Adobe Analytics (appmeasurement) e do Media Analytics (heartbeats).

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
      >Nas chamadas de início do Media Analytics (`s:event:type=start`) os `mid` valores podem não estar presentes. Isso está certo. Elas podem não aparecer até que as chamadas do Media Analytics Play ( `s:event:type=play`).

   * **Chamada Play Analytics Play**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Iniciar o player de mídia**

   Quando o player de mídia é iniciado, o Media SDK envia as principais chamadas para os dois servidores na seguinte ordem:

   1. Servidor do Adobe Analytics - Iniciar chamada
   1. Servidor do Media Analytics - Iniciar chamada
   1. Servidor do Media Analytics - "Chamada do Adobe Analytics Start solicitada"
   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   A terceira chamada acima diz ao servidor Media Analytics que o Media SDK solicitou que a chamada de início do Adobe Analytics (`pev2=ms_s`) seja enviada para o servidor do Adobe Analytics.

1. **Exibir ad break, se disponível**

   * **Início do anúncio**
   Quando o anúncio é iniciado, as seguintes chamadas de chave são enviadas na seguinte ordem:

   1. Servidor do Adobe Analytics - Chamada Ad Start
   1. Servidor do Media Analytics - Chamada Ad Start
   1. Servidor do Media Analytics - "Chamada do Adobe Analytics Ad Start solicitada"
   As primeiras duas chamadas contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   A terceira chamada diz ao servidor Media Analytics que o Media SDK solicitou que a chamada do Adobe Analytics Ad Start (`pev2=msa_s`) seja enviada para o servidor do Adobe Analytics.

   * **Reprodução do anúncio**

      Durante a reprodução do anúncio, o SDK do Media Analytics envia eventos de play do tipo "anúncio" ao servidor do Media Analytics a cada segundo.

   * **Anúncio concluído**

      No ponto de 100% de uma publicidade, uma chamada Media Analytics Complete deve ser enviada.



1. **Pausar a reprodução de anúncio por 30 segundos, se disponível.**  **Pausa do anúncio**

   Durante a Pausa de anúncio, as chamadas de pulsação do Media Analytics ou "ping" são enviadas pelo SDK ao servidor do Media Analytics a cada segundo.

   >[!NOTE]
   >
   >O valor do indicador de reprodução deve permanecer constante durante a pausa.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **Reproduzir o conteúdo principal por 10 minutos sem interrupções.**  **Reprodução de conteúdo**

   Durante a reprodução do conteúdo principal, o Media SDK envia pulsações (chamadas Reproduzir) ao servidor do Media Analytics a cada 10 segundos.

   Notas:

   * A posição do indicador de reprodução deve incrementar por 10 com cada chamada Play.
   * O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

      Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Pausar durante a reprodução por, pelo menos, 30 segundos.** Na pausa do player de mídia, as chamadas de evento de pausa serão enviadas pelo SDK ao servidor do Media Analytics a cada 10 segundos. Quando a pausa termina, os eventos de reprodução são retomados.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **Mídia de busca/depuração.** No scrubbing do indicador de reprodução de mídia, nenhuma chamada de rastreamento especial é enviada, no entanto, quando a reprodução da mídia é retomada após a depuração, o valor do indicador de reprodução deve refletir a nova posição no conteúdo principal.

1. **Reproduzir mídia (somente VOD).** Quando a mídia é respondida, um novo conjunto de chamadas de início de mídia deve ser enviado (como se fosse um início de início).

1. **Exibir próxima mídia na lista de reprodução.** No início da mídia da próxima mídia em uma lista de reprodução, um novo conjunto de chamadas de início de mídia deve ser enviado.

1. **Trocar mídia ou fluxo.** Ao alternar fluxos ao vivo, uma chamada completa do Media Analytics para o primeiro fluxo não deve ser enviada. As chamadas de início de mídia e de Play devem começar com o novo nome de exibição e fluxo, bem como com o indicador de reprodução e os valores de duração corretos para a nova exibição.

