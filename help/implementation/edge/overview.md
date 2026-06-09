---
title: Visão geral da implementação do Edge
description: Configure o esquema, o conjunto de dados e a sequência de dados do Adobe Experience Platform necessários para coletar dados de mídia de transmissão por meio da Edge Network.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 4%

---

# Visão geral da implementação do Edge

O Adobe Experience Platform Edge Network permite enviar dados destinados a vários produtos para um único endpoint, que então encaminha as informações apropriadas para cada produto. Essa é a maneira recomendada de implementar a Coleção de mídia de transmissão e é a única abordagem que oferece suporte ao Adobe Analytics e ao Customer Journey Analytics a partir de uma única implementação.

Em contraste com a abordagem herdada do Media SDK, que exigia instrumentação específica do produto para cada solução da Adobe, uma implementação do Edge usa um modelo de dados XDM compartilhado e um único fluxo de dados. Os dados fluem da sua SDK ou API para a Edge Network, que a encaminha para o produto Adobe que estiver configurado na sequência de dados (Analytics, CJA, AJO ou RTCDP). Isso significa que alternar ou adicionar produtos downstream posteriormente não requer a reinstrumentação dos eventos de mídia.

Independentemente da base de código usada, primeiro você deve concluir a configuração da plataforma descrita nesta página: criar um esquema, criar um conjunto de dados e configurar um fluxo de dados.

## Pré-requisitos

1. **Conclua os pré-requisitos gerais.** Consulte os [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme uma solução Adobe compatível.** Você deve ter uma implementação funcional de pelo menos um dos seguintes:
   * [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=pt-BR): o principal destino de relatórios para dados de mídia baseados em Edge
   * [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR): compatível com o CJA ou em vez dele através da mesma sequência de dados
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR) ou [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html): adicione o serviço **[!UICONTROL Adobe Experience Platform]** à sua sequência de dados ao configurar qualquer uma dessas opções

## Configurar o esquema no Adobe Experience Platform

Para padronizar a coleta de dados entre aplicativos que usam o Adobe Experience Platform, a Adobe criou o padrão aberto e publicamente documentado Experience Data Model (XDM).

1. No Adobe Experience Platform, comece a criar o esquema conforme descrito em [Criar e editar esquemas na interface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

1. Na página Detalhes do esquema, escolha **[!UICONTROL Evento de experiência]** como a classe base do esquema.

   ![Grupos de campos adicionados](assets/schema-experience-event.png)

1. Selecione **[!UICONTROL Próximo]**.

1. Especifique um nome para exibição de esquema e uma descrição e selecione **[!UICONTROL Concluir]**.

1. Na área **[!UICONTROL Composição]**, na seção **[!UICONTROL Grupos de campos]**, selecione **[!UICONTROL Adicionar]**, procure e adicione os seguintes grupos de campos ao esquema:
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Após adicionar os grupos de campos, eles são exibidos na seção **[!UICONTROL Grupos de campos]**:

   ![Grupos de campos adicionados](assets/schema-field-groups-added.png)

1. Selecione **[!UICONTROL Salvar]** para salvar suas alterações.

1. (Opcional) Você pode ocultar determinados campos da interface do esquema. Esses campos são campos de relatórios calculados pelo servidor que o Adobe preenche no back-end; eles não são enviados pela SDK ou API e não afetam a coleta de dados. Ocultá-los não tem impacto funcional; isso só reduz o ruído visual ao navegar pelo esquema na interface do usuário do AEP. Esses campos se referem apenas àqueles no grupo de campos `MediaAnalytics Interaction Details`.

   +++ Expanda para exibir instruções nos campos que você pode ocultar.

   1. Na área **[!UICONTROL Estrutura]**, selecione o campo `Media Collection Details` e **[!UICONTROL Gerenciar campos relacionados]**.

      ![gerenciar-relacionados-campos](assets/manage-related-fields.png)

   1. Habilite a opção para **[!UICONTROL Mostrar nomes para exibição para campos]** e atualize o esquema da seguinte maneira:

      * No campo `Media Collection Details` > `Advertising Details`, oculte os seguintes campos de relatório: `Ad Completed`, `Ad Started` e `Ad Time Played`.

      * No campo `Media Collection Details` > `Advertising Pod Details`, oculte o seguinte campo de relatório: `Ad Break ID`

      * No campo `Media Collection Details` > `Chapter Details`, oculte os seguintes campos de relatórios: `Chapter Completed`, `Chapter ID`, `Chapter Started` e `Chapter Time Played`.

      * No campo `Media Collection Details`, oculte o campo `List Of States`.

        ![ocultar estados da coleção de mídia](assets/schema-hide-media-collection-states.png)

      * No campo `Media Collection Details` > `List Of States End` e `Media Collection Details` > `List Of States Start`, oculte os seguintes campos de relatório: `Player State Count`, `Player State Set` e `Player State Time`.

        ![campos a ocultar](assets/schema-hide-listofstates.png)

      * No campo `Media Collection Details` > `Qoe Data Details`, oculte os seguintes campos de relatórios: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` e `Total Stalling Duration`.

      * No campo `Media Collection Details` > `Session Details`, oculte os seguintes campos de relatórios: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID`, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played` e `Video Segment`.

   1. Selecione **[!UICONTROL Confirmar]** para salvar suas alterações.

   1. Na área **[!UICONTROL Estrutura]**, habilite a opção para **[!UICONTROL Mostrar nomes para exibição para campos]** e selecione o campo `List Of Media Collection Downloaded Content Events`.

   1. Selecione **[!UICONTROL Gerenciar campos relacionados]** e atualize o esquema da seguinte maneira:

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details`, oculte os seguintes campos de relatório: `Ad Completed`, `Ad Started` e `Ad Time Played`.

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details`, oculte o seguinte campo de relatório: `Ad Break ID`

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details`, oculte os seguintes campos de relatório: `Chapter Completed`, `Chapter ID`, `Chapter Started` e `Chapter Time Played`.

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details`, oculte o campo `List Of States`.

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` e `Media Collection Details` > `List Of States Start`, oculte os seguintes campos de relatórios: `Player State Count`, `Player State Set` e `Player State Time`.

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details`, oculte os seguintes campos de relatórios: `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` e `Total Stalling Duration`.

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details`, oculte os seguintes campos de relatórios: `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID`, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played` e `Video Segment`.

      * No campo `List Of Media Collection Downloaded Content Events` > `Media Details`, oculte o campo `Media Session ID`.

   1. Selecione **[!UICONTROL Confirmar]** para salvar suas alterações.

   1. Na área **[!UICONTROL Estrutura]**, selecione o campo `Media Reporting Details` e **[!UICONTROL Gerenciar campos relacionados]**.

   1. Habilite a opção para **[!UICONTROL Mostrar nomes para exibição para campos]** e atualize o esquema da seguinte maneira:

      * No campo `Media Reporting Details`, oculte os seguintes campos: `Error Details`, `List Of States End`, `List of States Start` e `Media Session ID`.

   1. Selecione **[!UICONTROL Confirmar]** > **[!UICONTROL Salvar]** para salvar as alterações.

   +++

1. (Opcional) É possível adicionar metadados personalizados ao esquema. Isso permite incluir metadados adicionais definidos pelo usuário para necessidades ou contextos específicos. Para obter mais informações sobre metadados personalizados com a API do Media Edge, consulte [Suporte a metadados personalizados](custom-metadata.md).

   +++ Expanda para exibir instruções sobre como adicionar metadados personalizados ao esquema.

   1. Localize o nome do locatário da organização selecionando **[!UICONTROL Informações da conta]** > **[!UICONTROL Orgs atribuídas]** > [!UICONTROL _**nome da organização**_] > **[!UICONTROL locatário]**.

      Campos personalizados são recebidos por meio desse caminho. (Por exemplo, nome do locatário: _dcbl → caminho myCustomField: _dcbl.myCustomField.)

   1. Adicione um grupo de campos personalizado ao esquema de mídia definido.

      ![adicionar-metadados-personalizados](assets/add-custom-metadata-fieldgroup.png)

   1. Adicione campos personalizados que deseja rastrear ao grupo de campos.

      ![adicionar-metadados-personalizados](assets/add-custom-fields.png)

   1. [Use o caminho gerado](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties) para o campo personalizado na carga da sua solicitação.

      ![adicionar-metadados-personalizados](assets/custom-fields-path.png)

   +++

## Criar um conjunto de dados na Adobe Experience Platform

1. No Adobe Experience Platform, comece a criar o conjunto de dados conforme descrito no [guia da interface do usuário de conjuntos de dados](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=pt-BR#create).

   Ao selecionar um esquema para seu conjunto de dados, escolha o esquema criado anteriormente.

## Configurar um fluxo de dados no Adobe Experience Platform

1. Crie uma nova sequência de dados conforme descrito em [Configurar uma sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=pt-BR).

   Ao criar o fluxo de dados, faça as seguintes seleções:

   * No campo **[!UICONTROL Esquema de Evento]**, selecione o esquema criado em [Configurar o esquema no Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

     >[!IMPORTANT]
     >
     >Selecione **[!UICONTROL Salvar]**; não selecione **[!UICONTROL Salvar e Adicionar Mapeamento]**. Selecionar **[!UICONTROL Salvar e Adicionar Mapeamento]** causa erros de mapeamento para o campo Carimbo de data/hora.

     ![Criar sequência de dados e selecionar esquema](assets/datastream-create-schema.png)

   * Adicione os serviços apropriados à sequência de dados com base em sua solução da Adobe. Para obter informações sobre como adicionar um serviço, consulte &quot;Adicionar serviços a uma sequência de dados&quot; em [Configurar uma sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

      * **[!UICONTROL Adobe Analytics]** (se estiver usando o Adobe Analytics): defina um conjunto de relatórios conforme descrito em [Criar um conjunto de relatórios](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * **[!UICONTROL Adobe Experience Platform]** (se estiver usando o Customer Journey Analytics, Adobe Journey Optimizer ou Real-Time Customer Data Platform)

     ![Adicionar o serviço Adobe Analytics](assets/datastream-add-service.png)

   * Expanda **[!UICONTROL Opções Avançadas]** e habilite a opção **[!UICONTROL Media Analytics]**.

     ![Opção do Media Analytics](assets/datastream-media-check.png)

## Escolha seu método de implementação

Com o esquema, o conjunto de dados e o fluxo de dados em vigor, implemente uma das seguintes bases de código para começar a enviar dados de mídia de transmissão para a Edge Network. Cada página aborda a configuração específica de mídia de transmissão; o código por evento e por variável está em [Eventos](/help/implementation/events/overview.md) e [Variáveis](/help/implementation/variables/overview.md).

As implementações **No código** gravam chamadas SDK diretamente no código fonte do aplicativo. **Usando Tags** implementações usam [Tags do Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home), que permitem configurar e implantar regras de rastreamento sem modificar o código do aplicativo. Escolha a abordagem que se ajuste ao seu fluxo de trabalho de implantação.

| Base de código | No código | Uso de tags |
|---|---|---|
| Web | [Web SDK](web-sdk.md) | [Extensão de tag do Web SDK](web-sdk-tags.md) |
| iOS | [iOS](ios.md) | [iOS (Marcas)](ios-tags.md) |
| Android | [Android](android.md) | [Android (Marcas)](android-tags.md) |
| Roku | [Roku Edge](roku.md) | — |
| API | [API do Media Edge](media-edge-api.md) | — |

## Próxima etapa

Depois de começar a coletar dados, é possível configurar os relatórios:

* [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md) (Customer Journey Analytics)
* [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md) (se a sua sequência de dados alimentar o Adobe Analytics)

>[!MORELIKETHIS]
>
>* [Suporte a metadados personalizados](custom-metadata.md)
>* [Esquema de relatórios XDM](reporting-schema.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
