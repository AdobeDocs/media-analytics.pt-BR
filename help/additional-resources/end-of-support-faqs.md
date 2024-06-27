---
title: Saiba quais são as perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics
description: Este tópico inclui perguntas frequentes sobre o fim do suporte para SDKs do Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 76%

---

# Perguntas frequentes sobre o fim do suporte ao SDK móvel do Media Analytics

Com o fim do suporte à versão 4 dos SDKs móveis em 31 de agosto de 2021, o Adobe também encerrou o suporte aos SDKs móveis do Media Analytics para iOS e Android. (Isso não inclui o SDK do Media Analytics para plataformas da Web (JS) e OTT, como Chromecast e Roku, que ainda são compatíveis.)

Isso significa que o Adobe não fornece mais correções, atualizações relacionadas ao SO ou suporte para o SDK móvel do Media Analytics. Ao migrar para os novos SDKs do Experience Platform, esteja ciente de que a variável [Extensões do Media Analytics](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) deve ser implementado para habilitar o Complemento Adobe Streaming Media Collection.


## 5 principais itens que você deve conhecer

1. A partir de 31 de agosto de 2021, não haverá mais suporte para SDKs v4 móveis. Você deve migrar para os SDKs móveis da Adobe Experience Platform (AEP) para iOS e Android.

1. A implementação do Analytics para Streaming de Mídia exige o SDK móvel da AEP e o uso das extensões do Analytics e do Media Analytics. A partir de 1º de setembro de 2021, você deverá usar os novos SDKs móveis e extensões da AEP.  As extensões do Media Analytics são configuradas usando Tags da Adobe (coleção de dados). Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. O desenvolvimento de recursos terminou para os SDKs do Media Analytics para iOS e Android. Os novos recursos que foram introduzidos a partir do último trimestre de 2019 são ativados usando as extensões do Media Analytics e a API de coleção de mídia.

1. Os SDKs do Roku e Chromecast permanecem disponíveis os clientes do Analytics para Streaming de Mídia. Os SDKs do Roku e Chromecast continuarão recebendo suporte e sendo aprimorados como SDKs independentes. Se você utiliza o SDK JS do Media Analytics, poderá continuar a usar o SDK independente ou habilitar a extensão do Media Analytics usando a Coleção de dados da Adobe (antigo Adobe Launch).

Caso tenha alguma dúvida, entre em contato com a equipe de conta do Adobe.

## Perguntas frequentes

1. **O suporte para SDKs Roku e Chromecast será afetado? &#x200B;**

   Não.  Os SDKs Roku e Chromecast continuarão tendo suporte como SDKs independentes por enquanto.

1. **As implementações do SDK JS do Media Analytics serão afetadas por essa alteração? &#x200B;**

   Não.  Os clientes que usam o JS SDK para o Media Analytics podem continuar a usar o SDK ou ativá-lo por meio do Adobe Launch.
&#x200B;
1. **Qual é o nível de esforço (LOE) para migrar para as extensões do Media Analytics? &#x200B;**

   O LOE depende da implementação de cada cliente, portanto é variável.  Após consultar a documentação de migração abaixo, entre em contato com o Atendimento ao cliente e/ou consultoria para obter suporte adicional.

[Extensões do Media Analytics: Migração para Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Extensões do Media Analytics: Migração para iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Extensões do Media Analytics: novas implementações](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **Preciso ter o Launch como um sistema de gerenciamento de tags? E se eu não quiser usar o Launch?**

   No caso de uso do aplicativo móvel, o Launch não é usado como um sistema de gerenciamento de tags, como é para a Web. É necessário usar a interface do usuário do Launch para configurar as extensões do SDK. É semelhante à forma como você usa a interface do usuário do Adobe Mobile Services para configurar o SDK v4 móvel. Para instalação, a vantagem de usar o Launch é que ele fornece instruções personalizadas com base na extensão escolhida.

1. **Esse fim do suporte afeta o SDK para tvOS?**

   Sim, para tvOS (versão 10+), a implementação recomendada é a migração para as extensões do Media Analytics. Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md).

1. **Este fim de suporte afeta o SDK do Fire TV e Android TV?**

   Sim, para o Fire TV e Android TV, a implementação recomendada é a migração para as extensões do Media Analytics. Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md).
