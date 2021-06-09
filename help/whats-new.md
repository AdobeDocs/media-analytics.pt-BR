---
title: Novidades do Media Analytics
description: As novidades incluem informações sobre novos recursos e notificações.
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 94%

---


# Novidades do Media Analytics {#whats-new}

![Banner](assets/media_analytics_banner.png)


Esta página descreve novos recursos, correções e avisos importantes no Media Analytics. Ela também destaca a nova documentação, cursos de treinamento e tutoriais em vídeo para ajudar você a aproveitar ao máximo o Media Analytics.


## Notas de versão

Notas de versão da Adobe Experience Cloud

As Notas de versão da Adobe Experience Cloud descrevem novos recursos, correções e avisos importantes na Adobe Experience Cloud. Isso inclui as alterações mais recentes no Media Analytics. Ela também destaca a nova documentação, cursos de treinamento e tutoriais em vídeo para ajudar você a aproveitar ao máximo a Experience Cloud.

## Novos recursos

| Recurso | [Disponibilidade geral](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) - Data do Target | Descrição |
| ----------- | ---------- | ---------- |
| [Painel Visualizador simultâneo de mídia](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 17 de setembro de 2020 | O painel Visualizadores simultâneos de mídia no Workspace permite compreender onde ocorreu o pico de simultaneidade ou onde as quedas ocorreram. Ele fornece informações importantes sobre a qualidade do conteúdo e o engajamento do visualizador, além de ajudar na solução de problemas ou no planejamento de volume/escala. |
| [Dispositivos e plataformas compatíveis](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 18 de junho de 2020 | A [!UICONTROL Extensão Media Launch] com o SDK móvel da AEP agora é compatível com os seguintes dispositivos OTT:<ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [Rastreamento do estado do player](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html) | 29 de maio de 2020 | Os clientes do [!UICONTROL Media Analytics] podem capturar a interação do visualizador durante a reprodução usando um conjunto padrão de variáveis de solução para tela cheia, legendas ocultas, mudo, picture-in-picture e em foco. Você também tem flexibilidade para criar estados personalizados do player. As variáveis de [!UICONTROL Rastreamento de estado do player] agora estão disponíveis para relatórios no [!UICONTROL Analysis Workspace]. Esse recurso exige um dos seguintes: <ul><li>Media [!DNL JavaScript] SDK 3.0 ou superior</li><li>Para uso com o SDK [!DNL Adobe Experience Platform] (AEP):</li><li>[!UICONTROL Extensão do Media Analytics] (para Web): [!UICONTROL Adobe Media Analytics] (SDK 3.x) for Audio and Video v1.0 ou superior</li><li>[!UICONTROL Extensão do Media Analytics] (para dispositivos móveis): [!UICONTROL Adobe Media Analytics for Audio] and Video v2.0 ou superior</li><li>[!UICONTROL Coleção de mídia]</li></ul> |


## Notificações importantes

| Recurso | [Disponibilidade geral](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html) - Data do Target | Descrição |
| ----------- | ---------- | ---------- |
| [Dispositivos e plataformas compatíveis](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 31 de agosto de 2021 | Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDK do Media Analytics para iOS e Android. Para obter mais informações, consulte Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics. |
| [Perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics](sdk-implement/end-of-support-faqs.md) | Outono de 2019 | O desenvolvimento de recursos foi encerrado para os SDKs do Media Analytics para iOS e Android.  Os novos recursos que foram introduzidos a partir do último trimestre de 2019 são ativados usando as extensões do Media Analytics e a API de coleção da mídia. |
| [Visão geral da mídia](media-overview.md) | 20 de fevereiro de 2019 | A Adobe dá suporte apenas ao TLS 1.1 ou posterior. Com essa alteração, a Adobe não coletará mais dados de usuários finais com dispositivos mais antigos ou navegadores da Web que tenham o TLS 1.0 implantado. |
| [Dispositivos e plataformas compatíveis](https://experienceleague.adobe.com/docs/media-analytics/using/supported-devices.html) | 19 de fevereiro de 2019 | As versões mínimas da plataforma compatíveis com cada SDK estão listadas abaixo. <br>- iOS: iOS 6+ <br>- Android: Android 5.0+ - Lollipop <br>- Chrome: v22+<br>- Mozilla: v27+<br>- Safari: v7+<br>- IE: v1+ |
| [Parâmetros de áudio e vídeo](metrics-and-metadata/audio-video-parameters.md) | 7 de fevereiro de 2019 | O Adobe Analytics para vídeo e áudio lançou uma mudança de nome de métrica. <i>Inicializações da mídia</i> agora será chamada <i>Inícios da mídia</i>. Essa mudança foi feita para refletir os padrões do setor em métricas e relatórios e para facilitar a identificação da métrica nos relatórios. |
| [Parâmetros de áudio e vídeo](metrics-and-metadata/audio-video-parameters.md) | 13 de setembro de 2018 | Uma mudança foi feita nos rótulos de algumas dimensões, métricas e relatórios para permitir o rastreamento entre conteúdo das análises de áudio e vídeo. Os rótulos que mudaram incluem: *inicializações de vídeo* para *inicializações de mídia*, *duração do vídeo* para *duração do conteúdo* e *nome do vídeo* para *nome do conteúdo*. Os relatórios de vídeo nos Reports and Analytics foram atualizados para usar o nome “Mídia” no lugar de “Vídeo”. As mudanças nos rótulos não afetaram a coleção de dados nem os dados de histórico. Observe essas alterações caso você as esteja usando no Report Builder ou em qualquer outra extração automática de dados externa que possa ser afetada por essa alteração. |




<!-- | title | date | description | -->
