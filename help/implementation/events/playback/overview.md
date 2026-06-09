---
title: Rastrear reprodução
description: Saiba mais sobre eventos de reprodução e como implementar o rastreamento de alterações de reprodução, pausa, buffer, ping e taxa de bits.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 2%

---


# Rastrear reprodução

Os eventos de reprodução rastreiam as transições de estado no reprodutor de mídia durante uma sessão. Eles formam o núcleo do fluxo de eventos e se aplicam a qualquer tipo de conteúdo.

## Eventos do player

| Evento do reprodutor | Ação |
| --- | --- |
| A mídia é reproduzida ou retomada | Reprodução de chamada |
| Pausas de mídia | Chamar início da pausa |
| Início do buffering | Início do Buffer de Chamadas |
| Buffering termina | Reprodução de chamada |
| Alterações na taxa de bits | Alteração na taxa de bits da chamada |
| Disparos do temporizador | Ping de chamada |

## Etapas da implementação

1. **Chame [Reproduzir](play.md)** após [Início da sessão](../session/session-start.md) quando o primeiro quadro do conteúdo for renderizado na tela. Também envia a opção Reproduzir quando a reprodução é retomada após uma pausa ou paralisação de buffer. Não há evento de retomada separado.
1. **Chamar [Início da pausa](pause-start.md)** quando o usuário pausar a reprodução. Enviar Reprodução quando a reprodução for retomada.
1. **Chame [Início do buffer](buffer-start.md)** quando o player parar de aguardar dados. Nas APIs baseadas em XDM, o fim do buffer é inferido ao enviar o próximo evento Play. No Mobile SDK, também chame `BufferComplete` explicitamente quando o buffer for resolvido.
1. **Chame [Ping](ping.md)** a cada 10 segundos durante a reprodução do conteúdo principal e a cada 1 segundo durante a reprodução do anúncio. O ping mantém a sessão ativa e registra o movimento do indicador de reprodução. Os SDKs móveis enviam pings automaticamente; todas as outras plataformas devem enviá-los manualmente.
1. **Chame [Alteração na taxa de bits](bitrate-change.md)** sempre que o player negociar uma nova taxa de bits. Inclua os dados de QoE atuais (taxa de bits, quadros por segundo, quadros ignorados) para que o back-end possa calcular a [taxa de bits média](/help/reporting/metrics/average-bitrate.md) e as métricas de qualidade relacionadas.
