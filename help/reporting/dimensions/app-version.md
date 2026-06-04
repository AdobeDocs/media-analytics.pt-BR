---
title: Versão do aplicativo
description: Informa a versão do aplicativo de reprodutor de mídia usada para cada sessão de transmissão.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---


# Versão do aplicativo

>[!BEGINSHADEBOX]

*Esta página aborda a **versão do aplicativo**&#x200B;dimensão de relatório. Consulte [Versão do aplicativo](/help/implementation/variables/core/app-version.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Versão do aplicativo** informa a cadeia de caracteres da versão do aplicativo do reprodutor de mídia configurado na inicialização do SDK. Use-o para identificar quais versões do player estão em uso ativo, correlacionar alterações de qualidade ou comportamentais com versões específicas e priorizar o suporte para versões amplamente usadas.

>[!NOTE]
>
>Esta dimensão captura a versão do seu **aplicativo de reprodutor de mídia**, não a biblioteca SDK da Adobe. A própria versão da biblioteca SDK do Adobe é coletada automaticamente como um campo interno separado.

## Como essa dimensão é preenchida

A versão do aplicativo é definida uma vez na inicialização do SDK e é incluída automaticamente em cada solicitação de início de sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente por meio do mapeamento de campo XDM ao usar implementações do Edge. Para implementações somente do Analytics, mapeie os dados de contexto `media.sdkVersion` para um eVar personalizado usando uma [regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | Nenhuma coluna de feed de dados dedicada. Para implementações exclusivas do Analytics, use a coluna feed de dados do eVar personalizado configurado por meio da regra de processamento. |
| Audience Manager | `c_contextdata.media.sdkVersion` (implementações somente do Analytics) |

## Itens de dimensão

Cada item é a cadeia de versão literal configurada na inicialização do SDK. Use um esquema consistente de controle de versão em suas implementações para que as cadeias de caracteres de versão sejam acumuladas de forma previsível nos relatórios.
