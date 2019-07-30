---
seo-title: O manuseio de aplicativos é interrompido durante a reprodução
title: O manuseio de aplicativos é interrompido durante a reprodução
uuid: 1 ccb 4507-bda 6-462 d-bf 67-e 22978 a 4 db 3 d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# O manuseio de aplicativos é interrompido durante a reprodução{#handling-application-interrupts-during-playback}

A reprodução em um aplicativo de mídia pode ser interrompida de várias formas: um usuário pressiona explicitamente a pausa ou quando um usuário coloca o aplicativo em segundo plano. Independentemente do que causa uma interrupção na reprodução de mídia, as instruções de rastreamento são as mesmas:

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. Isso resulta na reprodução até aquele ponto, não contando com o tempo total de reprodução, juntamente com a perda de marcadores de progresso, segmentos etc. Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## Perguntas frequentes sobre o manuseio de interrupções de aplicativos: {#section_osf_xqs_h2b}

* _Quanto tempo um aplicativo deve ficar em segundo plano para a sessão ser encerrada?_

   Se o aplicativo permitir reprodução em segundo plano, ele poderá continuar a rastrear, chamando nossas APIs, e nós enviaremos nossos pings de rastreamento normais. No entanto, nem muitos aplicativos de vídeo permitem a reprodução em segundo plano, exceto o Youtube, mas todos os aplicativos de áudio permitem isso. Se o aplicativo não permitir a reprodução em segundo plano, é aconselhável permanecer no estado Pause por um minuto e encerrar a sessão de monitoramento. O aplicativo não pode continuar enviando Pausar pings, porque, na maioria dos casos, ele não pode determinar se o usuário retornará para continuar a visualizar a mídia ou determinar quando ela será morta. Também não é recomendado enviar pings em segundo plano.

* _Qual é o jeito certo de lidar com o rastreamento reiniciado depois que o aplicativo entra em segundo plano por muito tempo?_

   O aplicativo precisa chamar `trackSessionEnd` para encerrar a sessão de rastreamento. A partir da versão 2.1, o SDK envia um ping de “fim” para notificar o backend que a sessão de rastreamento foi terminada.

* _E sobre reiniciar a mesma sessão?_

   Para obter instruções mais detalhadas sobre como reiniciar uma sessão de rastreamento, consulte esta página: [Retomar manualmente uma sessão fechada.](/help/sdk-implement/cookbook/resuming-inactive.md) O SDK envia um ping de retomada para notificar o backend que o usuário está retomando manualmente a sessão.

