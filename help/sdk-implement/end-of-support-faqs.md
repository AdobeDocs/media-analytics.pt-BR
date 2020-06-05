---
title: Perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics
description: Este tópico inclui perguntas frequentes sobre o fim do suporte para SDKs do Media Analytics.
translation-type: tm+mt
source-git-commit: 38adc54438f85ca8ece8c77d9ff0d0aa14eb6605
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 3%

---


# Perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics

Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para os SDKs do Media Analytics para iOS e Android. Após 31 de agosto de 2021, a Adobe não fornecerá correções, atualizações relacionadas ao SO ou suporte para o SDK do Media Analytics.  Durante o processo de migração para esses novos SDKs da plataforma de experiência, lembre-se de que as extensões [do](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) Media Analytics devem ser implementadas para habilitar o Adobe Analytics para áudio e vídeo.

## 5 principais coisas a serem conhecidas

1. Os SDKs v4 móveis não serão mais suportados após 31 de agosto de 2021. Você deve migrar para os SDKs da Adobe Experience Platform (AEP) para iOS e Android. Para obter informações adicionais, consulte Perguntas frequentes sobre [o fim do suporte dos SDKs móveis](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)versão 4.

1. A implementação do Analytics para áudio e vídeo exige o AEP SDK e o uso das extensões do Analytics e do Media Analytics. A partir de 1º de setembro de 2021, você deverá usar os novos SDKs e extensões do AEP.  As extensões do Media Analytics são configuradas usando o Adobe Launch.  Para obter informações adicionais, consulte [Migração do SDK de mídia independente para o Adobe Launch](https://docs.adobe.com/content/help/pt-BR/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. O desenvolvimento de recursos terminou para os SDKs do Media Analytics para iOS e Android.  Os novos recursos que foram introduzidos a partir do último trimestre de 2019 são ativados usando as extensões do Media Analytics e a API de coleta de mídia.

1. Os SDKs Roku e Chromecast permanecem disponíveis para clientes do Analytics para áudio e vídeo. Os SDKs Roku e Chromecast continuarão a ser aprimorados e suportados como SDKs independentes.  Se você usar o JS SDK para o Media Analytics, poderá continuar usando o SDK independente ou habilitar a extensão do Media Analytics usando o Adobe Launch.

1. Antes de 1º de setembro de 2021, a Adobe pode, a seu critério exclusivo, desenvolver novas correções para problemas de alto impacto técnico ou exposição dos negócios. Com base na entrada do cliente, a Adobe determinará o grau de impacto e exposição e as atividades consequentes.

Entre em contato com seu Gerente de sucesso de cliente da Adobe se tiver dúvidas.

## Perguntas frequentes

1. **O suporte para SDKs Roku e Chromecast será afetado? &#x200B;**

   Não.  Os SDKs Roku e Chromecast continuarão a ser suportados como SDKs independentes por enquanto. &#x200B; &#x200B;
1. **As implementações do SDK JS do Media Analytics serão afetadas por essa alteração? &#x200B;**

   Não.  Os clientes que usam o JS SDK para o Media Analytics podem continuar a usar o SDK ou ativá-lo por meio do Adobe Launch.
&#x200B;
1. **Qual é o nível de esforço para migrar para as extensões do Media Analytics? &#x200B;**

   A LOE depende da implementação de cada cliente, portanto ela variará.  Após consultar a documentação de migração abaixo, consulte o Atendimento ao cliente e/ou consultoria para obter suporte adicional.

   [Extensões do Media Analytics: Migração para Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Extensões do Media Analytics: Migração do iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Extensões do Media Analytics: novas implementações](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **Preciso ter o Launch como um sistema de gerenciamento de tags? E se eu não quiser usar o Launch?**

   Para o caso de uso do aplicativo móvel, o Launch não é usado como um sistema de gerenciamento de tags, como é para a Web.  É necessário usar a interface do usuário Iniciar para configurar as extensões do SDK. É semelhante à forma como você usa a interface do usuário do Adobe Mobile Services para configurar o SDK v4 móvel. Para instalação, a vantagem de usar o Launch é que ele fornece instruções personalizadas de instalação com base na extensão escolhida.

1. **Esse fim do suporte afeta o SDK para tvOS?**

   Sim, para tvOS (versão 10+), a implementação recomendada é migrar para as extensões do Media Analytics.  O suporte ao AEP SDK e à extensão do Media Analytics está planejado para junho de 2020.  Para obter informações adicionais, consulte [Migração do SDK de mídia independente para o Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html).

1. **Esse fim do suporte afeta o SDK para FireTV e AndroidTV? &#x200B;**

   Sim, para FireTV e AndroidTV, a implementação recomendada é migrar para as extensões do Media Analytics.  O suporte ao AEP SDK e à extensão do Media Analytics está planejado para junho de 2020.  Para obter informações adicionais, consulte [Migração do SDK de mídia independente para o Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html).
