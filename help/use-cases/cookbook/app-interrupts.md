---
title: O Manuseio De Aplicativos Interrompe Durante A Reprodução
description: Saiba como lidar com interrupções para rastreamento durante a reprodução da mídia.
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 79%

---

# O manuseio de aplicativos é interrompido durante a reprodução{#handling-application-interrupts-during-playback}

A reprodução em um aplicativo de mídia pode ser interrompida de várias maneiras. Por exemplo, um usuário pode pressionar explicitamente a opção pausar ou pode colocar o aplicativo em segundo plano. Independentemente da causa de uma interrupção na reprodução de uma mídia, as instruções de rastreamento são as mesmas.

1. Chame **`trackPause`** quando o aplicativo for interrompido (entra em segundo plano, mídia pausada, etc.).
1. Chame **`trackPlay`** quando o aplicativo retornar para o primeiro plano e/ou quando a reprodução da mídia for retomada.

>[!NOTE]
>
>A equipe do Media Analytics tem instâncias em que os clientes chamaram `trackSessionStart` quando o aplicativo retornou do segundo plano. Fazer isso resulta na não contabilização da reprodução até esse ponto no tempo total de reprodução, juntamente com marcadores de progresso anteriores, segmentos, etc. Em vez disso, chame `trackPlay` quando o aplicativo retornar e/ou a reprodução da mídia for retomada.

## Perguntas frequentes sobre o manuseio de interrupções de aplicativos: {#faq-about-handling-application-interrupts}

* _Quanto tempo um aplicativo deve ficar em segundo plano para a sessão ser encerrada?_

   Se o aplicativo permitir reprodução em segundo plano, ele poderá continuar a rastrear, chamando nossas APIs, e nós enviaremos nossos pings de rastreamento normais. No entanto, nem todos os aplicativos de áudio permitem a reprodução em segundo plano, exceto o YouTube vermelho. Se o aplicativo não permitir reprodução em segundo plano, é recomendado permanecer no Estado pausado por um minuto e então encerrar a sessão de rastreamento. O aplicativo não pode continuar enviando pings de Pausa porque, na maioria dos casos, ele não poderá determinar se o usuário retornará para continuar visualizando a mídia ou quando ela será fechada. Também não é recomendado enviar pings em segundo plano.

* _Qual é o jeito certo de lidar com o rastreamento reiniciado depois que o aplicativo entra em segundo plano por muito tempo?_

   O aplicativo precisa chamar `trackSessionEnd` para encerrar a sessão de rastreamento. A partir da versão 2.1, o SDK envia um ping de “fim” para notificar o backend que a sessão de rastreamento foi terminada.

* _E sobre reiniciar a mesma sessão?_

   Para obter informações sobre como retomar uma sessão de rastreamento, consulte [Resumo de sessões inativas](resuming-inactive.md).O SDK envia um ping de retomada para notificar o backend que o usuário está retomando manualmente a sessão.
