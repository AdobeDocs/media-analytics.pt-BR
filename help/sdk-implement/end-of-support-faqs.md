---
title: Saiba quais são as perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics
description: Este tópico inclui perguntas frequentes sobre o fim do suporte para SDKs do Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: ht
source-wordcount: '723'
ht-degree: 100%

---

# Perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics

Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDKs do Media Analytics para iOS e Android. Após 31 de agosto de 2021, a Adobe não fornecerá correções, atualizações relacionadas ao SO ou suporte para o SDK do Media Analytics.  Durante o processo de migração para esses novos SDKs da Experience Platform, lembre-se de que as [extensões do Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) devem ser implementadas para habilitar o Adobe Analytics para Streaming de Mídia.

>[!NOTE]
>A Adobe Experience Platform Launch está sendo reformulada como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=pt-BR) para obter uma referência consolidada das alterações de terminologia.


## 5 principais itens que você deve conhecer

1. Os SDKs v4 móveis não terão mais suporte após 31 de agosto de 2021. Você deve migrar para os SDKs móveis da Adobe Experience Platform (AEP) para iOS e Android. Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte aos SDKs móveis versão 4](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq).

1. A implementação do Analytics para Streaming de Mídia exige o SDK móvel da AEP e o uso das extensões do Analytics e do Media Analytics. A partir de 1º de setembro de 2021, você deverá usar os novos SDKs móveis e extensões da AEP.  As extensões do Media Analytics são configuradas usando o Adobe Launch.  Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html?lang=pt-BR).

1. O desenvolvimento de recursos terminou para os SDKs do Media Analytics para iOS e Android.  Os novos recursos que foram introduzidos a partir do último trimestre de 2019 são ativados usando as extensões do Media Analytics e a API de coleção da mídia.

1. Os SDKs do Roku e Chromecast permanecem disponíveis os clientes do Analytics para Streaming de Mídia. Os SDKs Roku e Chromecast continuarão tendo suporte e serão aprimorados como SDKs independentes.  Se você usar o JS SDK para o Media Analytics, poderá continuar usando o SDK independente ou habilitar a extensão do Media Analytics usando o Adobe Launch.

1. Antes de 1º de setembro de 2021, a Adobe pode, a seu critério exclusivo, desenvolver novas correções para problemas de alto impacto técnico ou exposição dos negócios. Com base na informações fornecidas pelo cliente, a Adobe determinará o grau de impacto e exposição e as atividades resultantes.

Caso tenha alguma dúvida, entre em contato com o Gerente de sucesso de clientes da Adobe.

## Perguntas frequentes

1. **O suporte para SDKs Roku e Chromecast será afetado? &#x200B;**

   Não.  Os SDKs Roku e Chromecast continuarão tendo suporte como SDKs independentes por enquanto.

1. **As implementações do SDK JS do Media Analytics serão afetadas por essa alteração? &#x200B;**

   Não.  Os clientes que usam o JS SDK para o Media Analytics podem continuar a usar o SDK ou ativá-lo por meio do Adobe Launch.
&#x200B;
1. **Qual é o nível de esforço (LOE) para migrar para as extensões do Media Analytics? &#x200B;**

   O LOE depende da implementação de cada cliente, portanto é variável.  Após consultar a documentação de migração abaixo, entre em contato com o Atendimento ao cliente e/ou consultoria para obter suporte adicional.

   [Extensões do Media Analytics: Migração para Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html?lang=pt-BR)

   [Extensões do Media Analytics: Migração do iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html?lang=pt-BR)

   [Extensões do Media Analytics: novas implementações](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Preciso ter o Launch como um sistema de gerenciamento de tags? E se eu não quiser usar o Launch?**

   Para o caso de uso do aplicativo móvel, o Launch não é usado como um sistema de gerenciamento de tags, como é para a Web.  É necessário usar a interface do usuário do Launch para configurar as extensões do SDK. É semelhante à forma como você usa a interface do usuário do Adobe Mobile Services para configurar o SDK v4 móvel. Para instalação, a vantagem de usar o Launch é que ele fornece instruções personalizadas com base na extensão escolhida.

1. **Esse fim do suporte afeta o SDK para tvOS?**

   Sim, para tvOS (versão 10+), a implementação recomendada é a migração para as extensões do Media Analytics.  Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch - iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html?lang=pt-BR).

1. **Esse fim do suporte afeta o SDK para FireTV e AndroidTV? &#x200B;**

   Sim, para FireTV e AndroidTV, a implementação recomendada é a migração para as extensões do Media Analytics.  Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch - Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html?lang=pt-BR).
