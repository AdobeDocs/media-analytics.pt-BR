---
seo-title: Reprodução do Test 1 Standard
title: Reprodução do Test 1 Standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Teste 1: reprodução padrão{#test-standard-playback}

Esse caso de teste valida a reprodução e o sequenciamento gerais. É necessário como parte do Formulário de solicitação de certificação.

**Baixe o formulário de solicitação de certificação aqui: = = &gt;**  [Formulário de solicitação de certificação.](cert_req_form.docx)

As implementações de mídia são compostas pelos seguintes tipos de chamadas de rastreamento:
* Chamadas de mídia e anúncio de anúncio são enviadas diretamente para o servidor appmeasurement (Adobe Analytics).
* As chamadas de pulsação do Media Analytics são enviadas no início e a cada dez segundos (para conteúdo) ou um segundo (para anúncios) ao servidor de rastreamento do Media Analytics.

>[!NOTE]
>O rastreamento de mídia comporta-se o mesmo em todas as plataformas.

Você deve concluir e registrar essas ações na seguinte ordem:

1. **Carregar a página ou o aplicativo**

   **Servidores de rastreamento** (para todos os sites e aplicativos móveis):

   * **Appmeasurement (Adobe Analytics) -** Um servidor de rastreamento RDC ou CNAME que resolve um servidor de rastreamento RDC é necessário para o serviço de ID de visitante da Experience Cloud. The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats) -** Este servidor sempre tem o formato "`[namespace].hb.omtrdc.net`, onde `[namespace]` especifica o nome da empresa. Esse nome é fornecido pela Adobe.
   É necessário validar determinadas variáveis principais que são universais em todas as chamadas de rastreamento:

   **ID de visitante da Adobe (`mid`):** `mid` A variável é usada para capturar o valor definido no cookie AMCV. `mid` A variável é o valor de identificação principal para sites e aplicativos móveis, além de indicar que o serviço de ID de visitante da Experience Cloud está configurado adequadamente. Ele é encontrado nas chamadas do appmeasurement e do Media Analytics.

   * **Chamada Play Analytics Play**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Chamada de início do Media Analytics**

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

   * **Chamada de início do heartbeat**

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `s:event:type` | start |

   * **Chamada de início do VA**

      >[!NOTE]
      >
      >On VA Start Calls (`s:event:type=start`) the `mid` values may not be present. Isso está certo. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `pev2` | ms_s |


1. **Iniciar o player de mídia**

   Quando o player de mídia é iniciado, as chamadas-chave são enviadas na seguinte ordem:

   1. Início do Media Analytics
   1. Início do heartbeat
   1. Início do Heartbeat Analytics
   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md)

1. **Exibir ad break, se disponível**

   * **Início do anúncio**
   Quando o anúncio de mídia é iniciado, as seguintes chamadas de chave são enviadas na seguinte ordem:

   1. Início da análise de anúncio de mídia
   1. Início do anúncio de heartbeat
   1. Início da análise de anúncios do heartbeat
   As primeiras duas chamadas contêm metadados e variáveis adicionais. Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Reprodução do anúncio**

      Durante a reprodução do anúncio, as chamadas do Heartbeat são enviadas ao servidor do Heartbeat a cada segundo.

   * **Anúncio concluído**

      No ponto de 100% em uma publicidade de mídia, uma chamada de conclusão de Heartbeat será enviada.



1. **Pausar a reprodução de anúncio por 30 segundos, se disponível.**  **Pausa do anúncio**

   Durante a pausa do anúncio, as chamadas do Heartbeat são enviadas ao servidor do Heartbeat a cada segundo.

   >[!NOTE]
   >
   >O valor do indicador de reprodução deve permanecer constante durante a pausa.

1. **Reproduzir mídia de conteúdo principal por 10 minutos sem interrupções.**  **Reprodução de conteúdo**

   Durante a reprodução do conteúdo principal, as chamadas de pulsação são enviadas para o servidor do Media Analytics a cada dez segundos.

   Notas:

   * A posição do indicador de reprodução deve ser incrementada em 10 com cada chamada de reprodução.
   * O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

      Para obter parâmetros de chamada e metadados, consulte [Detalhes de chamada de teste.](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **Pausar durante a reprodução por, pelo menos, 30 segundos.** Na pausa do player de mídia, as chamadas de evento de pausa serão enviadas a cada 10 segundos. Quando a pausa termina, os eventos de reprodução são retomados.

1. **Mídia de busca/depuração.** No scrubbing do indicador de reprodução de mídia, nenhuma chamada de rastreamento especial é enviada, no entanto, quando a reprodução da mídia é retomada após a depuração do valor do indicador de reprodução deve refletir a nova posição no conteúdo principal.

1. **Reproduzir mídia (somente VOD).** Quando a mídia é respondida, um novo conjunto de chamadas de início de mídia deve ser enviado, como se esta fosse uma exibição de mídia fresca.

1. **Exibir próxima mídia na lista de reprodução.** No início da mídia da próxima mídia em uma lista de reprodução, um novo conjunto de chamadas de início de mídia deve ser enviado.

1. **Trocar mídia ou fluxo.** Ao alternar transmissões em tempo real, uma chamada completa de heartbeat para o primeiro fluxo não deve ser enviada. As chamadas de início de mídia e as chamadas de reprodução de mídia devem começar com o novo nome de exibição e fluxo e com o indicador de reprodução e os valores de duração corretos para a nova exibição.

