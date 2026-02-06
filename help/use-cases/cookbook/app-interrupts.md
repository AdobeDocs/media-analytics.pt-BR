---
title: Lidar com interrupções do aplicativo durante a reprodução
description: Saiba como lidar com interrupções do rastreamento durante a reprodução da mídia.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 63%

---

# Lidar com interrupções do aplicativo durante a reprodução {#handling-application-interrupts-during-playback}

A reprodução em um aplicativo de mídia pode ser interrompida de várias maneiras. Por exemplo, um usuário pode pressionar explicitamente o botão de pausa ou colocar o aplicativo em segundo plano. Independentemente da causa de uma interrupção na reprodução de uma mídia, as instruções de rastreamento são as mesmas.

1. Chame **`trackPause`** quando o aplicativo for interrompido (entrar em segundo plano, mídia pausada etc.).
1. Chame **`trackPlay`** quando o aplicativo retornar para o primeiro plano e/ou quando a reprodução da mídia for retomada.

>[!NOTE]
>
>Chamar `trackSessionStart` quando o aplicativo retorna do plano de fundo pode resultar na não contabilização da reprodução até esse ponto no tempo total de reprodução, juntamente com marcadores de progresso anteriores, segmentos, etc. Em vez disso, chame `trackPlay` quando o aplicativo retornar e/ou a reprodução da mídia for retomada.

## Perguntas frequentes sobre o manuseio de interrupções de aplicativos: {#faq-about-handling-application-interrupts}

* _Por quanto tempo um aplicativo deve ser colocado em segundo plano antes do fechamento da sessão?_

  Se o aplicativo permitir reprodução em segundo plano, ele poderá continuar rastreando chamando nossas APIs e enviaremos todos os nossos pings de rastreamento regulares. No entanto, nem todos os aplicativos de áudio permitem a reprodução em segundo plano, exceto o YouTube vermelho. Se o aplicativo não permitir reprodução em segundo plano, é recomendado permanecer no Estado pausado por um minuto e então encerrar a sessão de rastreamento. O aplicativo não pode continuar enviando pings de Pausa porque, na maioria dos casos, ele não poderá determinar se o usuário retornará para continuar visualizando a mídia ou quando ela será fechada. Também é uma experiência ruim manter o envio de pings quando estiver em segundo plano.

* _Qual é a maneira correta de lidar com a reinicialização do rastreamento depois que o aplicativo ficou em segundo plano por um longo tempo?_

  O aplicativo precisa chamar `trackSessionEnd` para encerrar a sessão de rastreamento. A partir da versão 2.1, o SDK envia um ping de &quot;fim&quot; para notificar o back-end que a sessão de rastreamento foi encerrada.

* _Que tal reiniciar a mesma sessão?_

  Para obter informações sobre como retomar uma sessão de rastreamento, consulte [Retomar sessões inativas](resuming-inactive.md). O SDK envia um ping de retomada para notificar o back-end que o usuário está retomando manualmente a sessão.
