---
title: Teste 1 Reprodução Padrão
description: Saiba mais sobre o teste de reprodução padrão usado na validação.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 97%

---

# Teste 1: reprodução padrão {#test-standard-playback}

Esse caso de teste valida a reprodução e a sequência gerais.

As implementações do Media Analytics incluem dois tipos de chamadas de rastreamento:
* Chamadas feitas diretamente no servidor do Adobe Analytics (AppMeasurement) — Essas chamadas ocorrem em eventos &quot;Media Start&quot; e &quot;Ad Start&quot;.
* Chamadas feitas ao servidor do Media Analytics (heartbeats) — Incluem chamadas em banda e fora de banda:
   * Em banda — O SDK envia chamadas de reprodução programadas ou &quot;pings&quot; em intervalos de 10 segundos durante a reprodução do conteúdo e em intervalos de um segundo durante os anúncios.
   * Fora de banda — Essas chamadas podem ocorrer a qualquer momento e incluem pausa, buffering, erros, conteúdo concluído, anúncio concluído, etc.

>[!NOTE]
>O rastreamento de mídia se comporta da mesma maneira em todas as plataformas.

## Procedimento de teste

Conclua e registre as seguintes ações (em ordem):

1. **Carregar a página ou o aplicativo**

   **Servidores de rastreamento** (para todos os sites e aplicativos móveis):

   * **Servidor do Adobe Analytics (AppMeasurement) -** Um servidor de rastreamento RDC ou CNAME que é resolvido para um servidor RDC, é necessário para o serviço de ID do visitante da Experience Cloud. O servidor de rastreamento do Adobe Analytics deve terminar com “`.sc.omtrdc.net`” ou ser um CNAME.

   * **Servidor do Media Analytics (Heartbeats) -** Este servidor sempre tem o formato &quot;`[namespace].hb.omtrdc.net`&quot;, em que `[namespace]` especifica o nome da sua empresa. Esse nome é fornecido pela Adobe.

   É necessário validar determinadas variáveis principais que são universais em todas as chamadas de rastreamento:

   **ID de visitante da Adobe (`mid`):** A variável `mid` é usada para capturar o valor definido no cookie do AMCV. A variável `mid` é o valor de identificação principal de sites e aplicativos móveis e também indica que o serviço de ID de visitante da Experience Cloud está definido corretamente. Ele é encontrado nas chamadas do Adobe Analytics (AppMeasurement) e do Media Analytics (heartbeats).

   * **Chamada de início do Adobe Analytics**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chamada de página do site**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **Chamada de vida útil**

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
      >Nas chamadas de Início do Media Analytics (`s:event:type=start`) os valores `mid` podem não estar presentes. Isso está certo. Eles podem não aparecer até que as chamadas do Media Analytics Play (`s:event:type=play`) sejam exibidas.

   * **Chamada do Media Analytics Play**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **Iniciar o reprodutor de mídia**

   Quando o reprodutor de mídia é iniciado, o SDK do Media envia as chamadas principais para os dois servidores na seguinte ordem:

   1. Servidor do Adobe Analytics — Iniciar chamada
   1. Servidor do Media Analytics -—Iniciar chamada
   1. Servidor do Media Analytics — &quot;Solicitação para iniciar chamada do Adobe Analytics solicitada&quot;

   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   A terceira chamada acima informa ao servidor do Media Analytics que o SDK do Media solicitou que a chamada de Início do Adobe Analytics (`pev2=ms_s`) fosse enviada para o servidor do Adobe Analytics.

1. **Exibir ad break, se disponível**

   * **Início do anúncio**

   Quando o anúncio é iniciado, as chamadas são enviadas na seguinte ordem:

   1. Servidor do Adobe Analytics — Chamada de início de anúncio
   1. Servidor do Media Analytics — Chamada de início de anúncio
   1. Servidor do Media Analytics — &quot;Chamada de início de anúncio do Adobe Analytics solicitada&quot;

   As primeiras duas chamadas contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#view-ad-playback)

   A terceira chamada informa ao servidor do Media Analytics que o SDK do Media solicitou que a chamada de início de anúncio do Adobe Analytics (`pev2=msa_s`) fosse enviada para o servidor do Adobe Analytics.

   * **Reprodução do anúncio**

      Durante a reprodução do anúncio, o SDK do Media Analytics envia eventos de reprodução do tipo &quot;anúncio&quot; para o servidor do Media Analytics a cada segundo.

   * **Anúncio concluído**

      No ponto de 100% de um anúncio, uma chamada do Media Analytics deve ser enviada.



1. **Pausar a reprodução de anúncio por 30 segundos, se disponível.** **Pausa do anúncio**

   Durante a pausa do anúncio, as chamadas de heartbeat ou &quot;pings&quot; do Media Analytics são enviadas pelo SDK para o servidor do Media Analytics a cada segundo.

   >[!NOTE]
   >
   >O valor do indicador de reprodução deve permanecer constante durante a pausa.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **Reproduzir o conteúdo principal por 10 segundos sem interrupções.** **Reprodução de conteúdo**

   Durante a reprodução do conteúdo principal, o SDK do Media envia heartbeats (chamadas de Reprodução) para o servidor do Media Analytics a cada 10 segundos.

   Notas:

   * A posição do indicador de reprodução deve ser incrementada em 10 com cada chamada de reprodução.
   * O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

      Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Pausar durante a reprodução por, pelo menos, 30 segundos.** Ao pausar o reprodutor de mídia, as chamadas de evento de pausa serão enviadas pelo SDK para o servidor do Media Analytics a cada 10 segundos. Quando a pausa termina, os eventos de reprodução são retomados.

   Para obter parâmetros de chamada e metadados, consulte [Detalhes da chamada de teste.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Buscar/movimentar mídia.** Ao movimentar o indicador de reprodução de mídia, nenhuma chamada de rastreamento especial é enviada; no entanto, quando a reprodução de mídia é retomada depois da movimentação, o valor do indicador de reprodução deve refletir a nova posição no conteúdo principal.

1. **Reproduzir mídia (somente VOD).** Quando a mídia é reproduzida, um novo conjunto de chamadas de Media Start deve ser enviado (como se fosse uma nova inicialização).

1. **Exibir a próxima mídia na lista de reprodução.** Quando a próxima mídia de uma lista de reprodução inicia, um novo conjunto de chamadas de início de mídia deve ser enviado.

1. **Alternar mídia ou fluxo.** Ao alternar transmissões em tempo real, uma chamada completa do Media Analytics para o primeiro fluxo não deve ser enviada. As chamadas de início e de reprodução de mídia devem começar com o nome e fluxo do novo programa e com os valores de indicador de reprodução e duração corretos para o novo programa.
