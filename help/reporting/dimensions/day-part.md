---
title: Faixa de horário
description: Reporta o período do dia (Manhã, Tarde, Horário nobre, Tarde da Noite) quando o conteúdo era transmitido ou reproduzido.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 8%

---


# Faixa de horário

>[!BEGINSHADEBOX]

*Esta página abrange a **Parte do dia**&#x200B;da dimensão de relatório. Consulte [Parte do dia](/help/implementation/variables/standard-metadata/day-part.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Parte do dia** informa o intervalo da hora do dia em que o conteúdo foi transmitido ou reproduzido. Os valores comuns são `"Morning"`, `"Afternoon"`, `"Primetime"` e `"Late Night"`. Use-o para comparar o engajamento em partes do dia independentemente do fuso horário local do visualizador.

## Como essa dimensão é preenchida

A parte do dia é definida pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.dayPart` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## Itens de dimensão

Cada item é o rótulo literal do daypart relatado no início da sessão. Use um conjunto fixo de valores em todas as implementações para manter os itens de linha consistentes.
