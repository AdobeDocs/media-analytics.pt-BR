---
title: Sobre o rastreamento do estado do player
description: Saiba mais sobre o recurso de rastreamento do estado do player, incluindo requisitos e diretrizes para implementar e informar os estados do player.
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 100%

---

# Sobre o rastreamento do estado do player

Para otimizar a experiência do seu produto e o valor da sua empresa, é importante entender o comportamento do cliente ao exibir vídeos, como analisar o tempo gasto em diferentes estados do player.  Também é importante ter a flexibilidade para criar e medir novos estados e eventos do player, conforme necessário.

O Rastreamento de estado do player oferece a capacidade de capturar a interação do visualizador durante a reprodução usando um conjunto padrão de variáveis de solução para as funções de tela cheia, legendas ocultas, mudo, picture in picture e em foco.  O Rastreamento de estado do player também oferece a flexibilidade para criar estados personalizados do player. Você pode usar variáveis de Rastreamento do estado do player em relatórios no Analysis Workspace.

Para capturar alterações, o Rastreamento de estado do player atualiza os metadados de medição de vídeo. Por exemplo, para determinar o engajamento de vídeo “true”, o Rastreamento de estado do player mede o tempo gasto com o som em relação às visualizações de vídeo passivas ou não engajadas quando o som está desligado ou o tempo gasto no modo Normal versus Tela cheia.

O Rastreamento de estado do player oferece os seguintes benefícios:

* Fornece variáveis padrão que medem estados comuns, como tela cheia ou legendas ocultas
* Fornece variáveis personalizáveis para medir estados personalizados durante uma sessão de reprodução
* Mede o tempo gasto em um estado de player personalizado
* Mede vários estados que podem ser simultâneos

![Rastreamento do estado do player](assets/player_state_tracking.png)

## Requisitos

O Rastreamento do estado do player exige um dos seguintes itens para a coleta de dados:
* Media JS SDK 3.0+
* SDK do Chromecast 3.0 para Soluções da Adobe Marketing Cloud
* Extensão do Media Analytics (para usar com o SDK da Adobe Experience Platform (AEP))
   * Web: Adobe Media Analytics (SDK 3.x) para áudio e vídeo v1.0+
   * Móvel: Adobe Media Analytics para áudio e vídeo v2.0+
* API da coleção de mídia

## Diretrizes

Antes de implementar o Rastreamento do estado do player, considere as seguintes diretrizes.

* O estado do player é calculado em todos os estados de reprodução (sem divisão).
* Você pode medir vários estados do player ao mesmo tempo.
* O número máximo de estados do player que podem ser rastreados durante uma reprodução é 10.
* As métricas de estado do player são enviadas ao Analytics para relatórios somente na chamada Fechamento de mídia.
* O conhecimento do status do aplicativo não é mantido depois que um estado é interrompido. Após o término de um estado, ele deve ser iniciado novamente para continuar o rastreamento. Para cada novo estado de reprodução, o estado do player deve ser reiniciado.
* Os estados do player são capturados para cada sessão de reprodução individual; o estado do player não é calculado entre as reproduções.
