---
seo-title: Reprodução do Test 1 Standard
title: Reprodução do Test 1 Standard
uuid: c 4 b 3 fead -1 b 27-484 b-ab 6 a -39 f 1 ae 0 f 03 f 2
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Teste 1: reprodução padrão{#test-standard-playback}

Esse caso de teste valida a reprodução e o sequenciamento geral, e é obrigatório como parte do formulário de solicitação de certificação. Baixe o formulário de solicitação de certificação aqui:[ formulário de solicitação de certificação.](cert_req_form_nielsen.docx)

As implementações de vídeo são compostas pelos seguintes tipos de chamadas de rastreamento:
* Chamadas de Início de vídeo e anúncio são enviadas diretamente para o servidor AppMeasurement.
* As chamadas de pulsação de mídia (MA) são enviadas no início e a cada dez segundos para o servidor de rastreamento Adobe VA.

>[!NOTE]
>O rastreamento de vídeo se comportará da mesma forma em todas as plataformas, desktops e dispositivos móveis.

Você deve concluir e registrar as ações na seguinte ordem:

1. **Carregar a página ou o aplicativo**

   **Servidores de rastreamento** (para todos os sites e aplicativos móveis):

   * **AppMeasurement (Adobe Analytics) -** Um servidor de rastreamento RDC ou CNAME que é resolvido para um servidor RDC, é necessário para o serviço de ID do visitante da Experience Cloud. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics (Heartbeats) -** Este servidor sempre tem o formato `[namespace].hb.omtrdc.net`, onde `[namespace]` é definido pela empresa de logon e é fornecido pela Adobe.
   Você precisa validar determinadas chaves, que são variáveis universais nas chamadas de rastreamento:

   **ID de visitante da Adobe (`mid`):** `mid` A variável é usada para capturar o valor definido no cookie AMCV. `mid` A variável é o valor de identificação principal para sites e aplicativos móveis, além de indicar que o serviço de ID de visitante da Experience Cloud está configurado adequadamente. Ele é encontrado nas chamadas de appmeasurement e Media Analytics (MA).

   * **Chamada Heartbeat Play**

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
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. Isso está certo. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | Parâmetro | Valor (exemplo) |
      |---|---|
      | `pev2` | ms_s |


1. **Iniciar o reprodutor de vídeo**

   Quando o reprodutor de vídeo é iniciado, as chamadas são enviadas na seguinte ordem:

   1. Início da análise de vídeo
   1. Início do heartbeat
   1. Início do Heartbeat Analytics
   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Exibir ad break, se disponível**

   * **Início do anúncio**
   Quando o anúncio de vídeo é iniciado, as chamadas são enviadas na seguinte ordem:

   1. Início da análise de anúncio de vídeo
   1. Início do anúncio de heartbeat
   1. Início da análise de anúncios do heartbeat
   As primeiras duas chamadas contêm metadados e variáveis adicionais. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **Reprodução do anúncio**

      Durante a reprodução do anúncio, as chamadas do Heartbeat são enviadas ao servidor do Heartbeat a cada segundo.

   * **Anúncio concluído**

      No ponto de 100% em um anúncio de vídeo, uma chamada de heartbeat completa será enviada.



1. **Pausar a reprodução de anúncio por 30 segundos, se disponível.**  **Pausa do anúncio**

   Durante a pausa do anúncio, as chamadas do Heartbeat são enviadas ao servidor do Heartbeat a cada segundo.

   >[!NOTE]
   >
   >O valor do indicador de reprodução deve permanecer constante durante a pausa.

1. **Reproduzir o vídeo do conteúdo principal por 10 minutos sem interrupções.** **Reprodução de conteúdo **

   Durante a reprodução regular do conteúdo principal, as chamadas do Heartbeat são enviadas ao servidor Heartbeat a cada dez segundos.

   Notas:

   * A posição do indicador de reprodução deve ser incrementada em 10 com cada chamada de reprodução.
   * O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

      For call parameters and metadata, see [Test call details](../../sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Pausar durante a reprodução por, pelo menos, 30 segundos.** Quando o reprodutor de vídeo estiver pausado, as chamadas de evento de pausa serão enviadas a cada 10 segundos. Quando a pausa termina, os eventos de reprodução são retomados.

1. **Buscar/movimentar-se no vídeo.** Ao movimentar o indicador de reprodução de vídeo, nenhuma chamada de rastreamento especial é enviada; no entanto, quando a reprodução de vídeo é retomada depois da movimentação, o valor do indicador de reprodução deve refletir a nova posição no conteúdo principal.

1. **Reproduzir o vídeo novamente (somente VOD).** Quando um vídeo é reproduzido, um novo conjunto de chamadas de início de vídeo deve ser enviado, como se fosse uma nova exibição de vídeo.

1. **Exibir o próximo vídeo na lista de reprodução.** Quando o próximo vídeo de uma lista de reprodução inicia, um novo conjunto de chamadas de início de vídeo deve ser enviado.

1. **Alternar vídeo ou fluxo.** Ao alternar transmissões em tempo real, uma chamada completa de heartbeat para o primeiro fluxo não deve ser enviada. As chamadas de início e de reprodução de vídeo devem começar com o nome e fluxo do novo programa e com os valores de indicador de reprodução e duração corretos para o novo programa.

