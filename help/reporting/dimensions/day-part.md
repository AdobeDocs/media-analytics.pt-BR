---
title: Faixa de horário
description: Reporta o período do dia (Manhã, Tarde, Horário nobre, Tarde da Noite) quando o conteúdo era transmitido ou reproduzido.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 9%
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.dayPart` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## Itens de dimensão

Cada item é o rótulo literal do daypart relatado no início da sessão. Use um conjunto fixo de valores em todas as implementações para manter os itens de linha consistentes.
