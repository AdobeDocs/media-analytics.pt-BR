---
title: Saiba quais são as perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics
description: Este tópico inclui perguntas frequentes sobre o fim do suporte para SDKs do Media Analytics.
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/qfM2-x6s-SPf4gw2FpLlg7mPI-h-xZ3Y1TeeVALn3fQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 639
ht-degree: 62%

---

# Perguntas frequentes sobre o fim do suporte ao SDK móvel do Media Analytics

Com o fim do suporte à versão 4 dos SDKs móveis em 31 de agosto de 2021, a Adobe também encerrou o suporte aos SDKs móveis do Media Analytics para iOS e Android. (Isso não inclui o Media Analytics SDK para plataformas da Web (JS) e OTT, como Chromecast e Roku, que ainda são compatíveis.)

Isso significa que o Adobe não fornece mais correções, atualizações relacionadas ao SO ou suporte para o Media Analytics Mobile SDK. Ao migrar para os novos SDKs da Experience Platform, esteja ciente de que as [extensões do Media Analytics](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) devem ser implementadas para habilitar os serviços de streaming de mídia da Adobe.


## 5 principais itens que você deve conhecer

1. A partir de 31 de agosto de 2021, não haverá mais suporte para SDKs v4 móveis. Você deve migrar para os SDKs móveis do Adobe Experience Platform (AEP) para iOS e Android.

1. Uma implementação dos serviços de mídia de transmissão do Adobe exige o AEP Mobile SDK e o uso das extensões do Analytics e do Media Analytics. A partir de 1º de setembro de 2021, você deverá usar os novos SDKs móveis e extensões da AEP.  As extensões do Media Analytics são configuradas usando Tags da Adobe (coleção de dados). Para obter mais informações, consulte [Migração do SDK de mídia independente para o Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md).

1. O desenvolvimento de recursos terminou para os SDKs do Media Analytics para iOS e Android. Os novos recursos que foram introduzidos a partir do último trimestre de 2019 são habilitados usando as extensões do Media Analytics e a API de coleção de mídia.

1. Os SDKs Roku e Chromecast permanecem disponíveis para clientes com o complemento Adobe Analytics para mídia de streaming e o complemento Customer Journey Analytics Streaming Media Collection. Os SDKs do Roku e Chromecast continuarão recebendo suporte e sendo aprimorados como SDKs independentes. Se você utiliza o SDK JS do Media Analytics, poderá continuar a usar o SDK independente ou habilitar a extensão do Media Analytics usando a Coleção de dados da Adobe (antigo Adobe Launch).

Caso tenha alguma dúvida, entre em contato com a equipe de conta da Adobe.

## Perguntas frequentes

1. **O suporte para SDKs Roku e Chromecast será afetado? &#x200B;**

   Não.  Os SDKs Roku e Chromecast continuarão tendo suporte como SDKs independentes por enquanto.&#x200B;
&#x200B;
1. **As implementações do SDK JS do Media Analytics serão afetadas por essa alteração? &#x200B;**

   Não.  Os clientes que usam o JS SDK para Media Analytics podem continuar a usar o SDK ou ativá-lo por meio do Adobe Launch.
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
