---
title: Sobre o rastreamento de estado do player
description: Este tópico descreve o recurso de rastreamento do estado do player, incluindo requisitos e diretrizes para implementar e relatórios estados do player.
translation-type: tm+mt
source-git-commit: d317188ef664c836c7125e8bbe195baa924c0d80
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---


# Sobre o rastreamento de estado do player

Para otimizar a experiência do seu produto e o valor da sua empresa, é importante entender o comportamento do cliente ao exibir vídeos. Isso inclui o tempo gasto em diferentes estados do player.  Também é importante ter a flexibilidade para criar e medir novos estados e eventos de jogadores, conforme necessário.

O Rastreamento de estado do player oferece a capacidade de capturar a interação do visualizador durante a reprodução usando um conjunto padrão de variáveis de solução para tela cheia, legendagem fechada, silêncio, imagem na imagem e em foco.  O Rastreamento de estado do player também oferece a flexibilidade para criar estados personalizados do player. Você pode usar variáveis de Rastreamento de estado do player para relatórios na área de trabalho da Análise.

Para capturar alterações no estado do player, o Rastreamento de estado do player atualiza os metadados de medição de vídeo. Por exemplo, para determinar o envolvimento de vídeo &quot;verdadeiro&quot;, o Rastreamento de estado do player mede o tempo gasto com o som em relação às visualizações de vídeo passivas ou não ativas quando o som está desligado ou o tempo gasto no modo Normal versus Tela cheia.

O Rastreamento de estado do player oferece os seguintes benefícios:

* Fornece variáveis padrão que medem estados comuns, como tela cheia ou legendas ocultas
* Fornece variáveis personalizáveis para medir estados personalizados durante uma sessão de reprodução
* Mede o tempo gasto em um estado de player personalizado
* Mede vários estados que podem ser simultâneos

![Rastreamento de estado do player](assets/player_state_tracking.png)

## Requisitos

O Rastreamento de estado do player exige um dos seguintes para a coleta de dados:
* Media JS SDK 3.0+
* Extensão do Media Analytics (para uso com o SDK do Adobe Experience Platform (AEP))
   * Web: Adobe Media Analytics (SDK 3.x) para áudio e vídeo v1.0+
   * Dispositivo móvel: Adobe Media Analytics para áudio e vídeo v2.0+
* API da coleção de mídia

## Diretrizes

Antes de implementar o rastreamento de estado do Player, considere as seguintes diretrizes.

* O estado do player é calculado em todos os estados de reprodução - (sem divisão)
* Você pode medir vários estados de player ao mesmo tempo
* O número máximo de estados do player que podem ser rastreados durante uma reprodução é 10 
* As métricas de estado do player são enviadas ao Analytics para relatórios SOMENTE na chamada Media Close
* Os estados do player são capturados para cada sessão de reprodução individual — o estado do player não é calculado entre as reproduções 