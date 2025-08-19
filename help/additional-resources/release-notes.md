---
title: Notas de versão dos serviços de mídia de streaming
description: Veja as notas de versão dos serviços de streaming de mídia.
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 64%

---

# Notas de versão dos serviços de mídia de streaming (agosto de 2025)

**Última atualização**: quinta-feira, 6 de agosto de 2025

## Recursos relacionados

Para obter informações sobre novos recursos, correções e informações importantes para administradores, consulte os seguintes recursos.

* [Notas de versão do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=pt-BR)
* [Notas de versão do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=pt-BR)
* As atualizações de versão mais recentes para [produtos da Adobe Experience Cloud](https://business.adobe.com/br/products/adobe-experience-cloud-products.html)

* [Tutoriais do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=pt-BR)

## *Notas de versão atuais*

## Recursos novos e atualizados para os serviços de streaming de mídia da Adobe {#cja-features}

| Recurso | Descrição | Data alvo |
| ----------- | ---------- | ------- |
| Campos XDM atualizados para coletar dados de streaming de mídia no Adobe Experience Platform | Ao coletar dados de streaming de mídia no Adobe Experience Platform, os caminhos de campo XDM mostrados no cabeçalho de &quot;Caminho do campo XDM&quot; da documentação de parâmetros de streaming de mídia não devem mais ser usados. Em vez disso, os clientes que implementaram o conector de origem do Analytics para coletar dados de mídia de transmissão na Platform antes de 9 de maio de 2025 devem migrar suas configurações existentes para os caminhos de campo do MediaReporting, como mostrado no cabeçalho de &quot;Caminho do campo XDM do relatório&quot; da documentação de parâmetros da mídia de transmissão.<p> Esses caminhos de campo são encontrados nas seguintes páginas e são marcados como &quot;Obsoletos&quot;: [Parâmetros de áudio e vídeo](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/audio-video-parameters), [Parâmetros de anúncios](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/ad-parameters), [Parâmetros de capítulo](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/chapter-parameters), [Parâmetros de estado do player](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/player-state-parameters) e [Parâmetros de qualidade](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/quality-parameters). (Nenhuma ação é necessária para clientes que implementam o conector de origem do Analytics após 9 de maio de 2025 e já estão usando somente os caminhos XDM do mediaReporting.)</p><p>A assimilação de dados nos caminhos de campo XDM obsoletos continuará até o final de outubro de 2025. Após esse tempo, os caminhos de campo obsoletos serão totalmente removidos e não estarão mais visíveis na interface do esquema do Adobe Experience Platform, e os dados serão enviados somente usando os caminhos de campo mediaReporting.</p><p>Para obter mais informações, consulte [Migrar uma implementação do Analytics Source Connector para campos de mídia de transmissão XDM atualizados](/help/use-cases/xdm-updates/updated-xdm-fields.md).</p><p>Entre em contato com os serviços da Adobe Consulting ou com a equipe de conta para obter suporte à migração. </p> | Outubro de 2025 |
| Enviar dados da Web para o Adobe Experience Platform Edge Network com o Web SDK | Agora você pode [usar o Adobe Experience Platform Web SDK para enviar dados da Web de mídia de streaming ao Adobe Experience Platform Edge Network](/help/implementation/edge/edge-web-sdk.md), permitindo que você crie campanhas mais personalizadas e forneça mais conteúdo personalizado, resultando em mais dados de rastreamento a serem relatados.<p>Esse aprimoramento fornece um método de coleção unificada para implementações da web em todas as soluções da Platform, como Customer Journey Analytics, RT-CDP, AJO e o encaminhamento de eventos. Anteriormente, a única maneira de enviar dados da web de mídia de transmissão para a Edge Network era por meio da API de borda de mídia. | 29 de maio de 2024 |
| Enviar dados do Roku para o Adobe Experience Platform Edge | Agora, ao [instalar a Coleção de mídia de streaming do Customer Journey Analytics com o Experience Platform Edge](/help/implementation/edge/implementation-edge.md), você pode usar o Adobe Experience Platform Roku SDK para enviar dados de mídia de streaming para o Adobe Experience Platform. | 12 de abril de 2024 |
| Coleção de mídia: Integração com a Experience Edge (API e SDK móvel) | Agora você pode usar a API da Experience Edge e o Mobile SDK para implementar a Coleção de mídia de transmissão da Customer Journey Analytics, permitindo criar campanhas mais personalizadas e fornecer conteúdo mais personalizado, resultando em mais dados de rastreamento a serem relatados.<p>Esse aprimoramento fornece um método de coleta unificada em todas as soluções, como relatórios do Customer Journey Analytics, RT-CDP, AJO e encaminhamento de eventos.  [Saiba mais](/help/implementation/edge/implementation-edge.md) | sábado, 12 de maio de 2023 |
| Painel Visualizador simultâneo de mídia | Entenda onde o pico de simultaneidade ocorreu ou onde as quedas ocorreram. Obtenha insights importantes sobre a qualidade do conteúdo e o envolvimento do visualizador, além de ajuda na solução de problemas ou no planejamento de volume e escala. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=pt-BR) | 9 de agosto de 2022 |
| Painel Tempo gasto com a reprodução da mídia | O painel Tempo gasto com a reprodução de mídia fornece informações valiosas sobre o envolvimento do visualizador e permite que as organizações de mídia obtenham insights mais profundos e detalhados sobre o envolvimento do usuário a cada minuto, por meio da análise avançada do tempo gasto com recursos de faixa horária. É possível observar o tempo gasto visualizando seus fluxos de mídia em um período específico. É possível dividir a duração da reprodução por diferentes granularidades, incluindo novas granularidades de 5 minutos, 15 minutos e 30 minutos. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=pt-BR) | 9 de agosto de 2022 |
| Compartilhar anotações em cartões de pontuação para dispositivos móveis | Você pode exibir anotações criadas no Espaço de trabalho, nos Cartões de pontuação para dispositivos móveis. Isso permite compartilhar nuances de dados contextuais e insights sobre sua organização e campanhas diretamente em projetos do Cartão de pontuação para dispositivos móveis, visualizáveis no aplicativo móvel de painéis do Analytics. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=pt-BR) | 15 de junho de 2022 |
| Atualizações do Report Builder para Customer Journey Analytics | Inclui recursos como agendamento e gerenciador de blocos de dados. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=pt-BR) | 18 de maio de 2022 |
| Anotações no Espaço de trabalho | As anotações no Espaço de trabalho permitem comunicar com eficiência nuances de dados contextuais e insights à sua organização. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=pt-BR) | A implantação gradual começa em 23 de março de 2022 |
| Modo de visualização do projeto do cartão de pontuação para dispositivos móveis | Visualize como o cartão de pontuação para dispositivos móveis ficará no aplicativo de painéis do Analytics, diretamente do construtor do cartão de pontuação. O modo de visualização permite que os usuários interajam com filtros e gráficos da mesma forma que fazem no aplicativo, permitindo que visualizem a experiência antes de salvar e compartilhar o cartão de pontuação. Os usuários também podem usar o seletor de dispositivos no modo de visualização para ver como o cartão de pontuação será exibido em diferentes dispositivos. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=pt-BR#preview) | 16 de fevereiro de 2022 |


## Recursos novos e atualizados para os serviços de streaming de mídia da Adobe {#sm-features}

| Recurso | Descrição | Data alvo |
| ----------- | ---------- | ------- |
| Rastreamento de vários estados do player | Use a API de coleção de mídia para implementar o rastreamento de vários estados do player. [Saiba mais](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=pt-BR) | Setembro de 2022 |
| Campos XDM renomeados | Nomes de campos XDM renomeados para fins de consistência:<br>* Parâmetros de áudio e vídeo<br>* Parâmetros de anúncio<br>* Parâmetros de capítulo<br>* Parâmetros de estado do player<br>* Parâmetros de qualidade | Setembro de 2022 |
| Referência ao Device Co-op | Remoção da referência ao Adobe Experience Cloud Device Co-op e ao requisito do serviço da Experience Cloud ID. | Agosto de 2022 |
| Nomes de campos e caminhos XDM atualizados para coleção e relatórios | Atualização do seguinte:<br>* Parâmetros de áudio e vídeo<br>* Parâmetros de anúncio<br>* Parâmetros de capítulo<br>* Parâmetros de estado do player<br>* Parâmetros de qualidade | Agosto de 2022 |
| Público-alvo médio por minuto | Os clientes do Media Analytics podem usar o painel Audiência média por minuto para entender melhor o consumo médio de seu conteúdo. <br>A Audiência média por minuto permite as comparações da programação de qualquer comprimento ou gênero. Além disso, é possível comparar ou anexar essa audiência média por minuto digital às métricas de média por minuto lineares de TV. Esse painel oferece mais flexibilidade para medir a audiência média em períodos de tempo personalizados, bem como quando a classificação de duração for atualizada.  [Saiba mais](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=pt-BR) | 16 de março de 2022 |
| Painel Tempo gasto com a reprodução da mídia | Saiba como o Painel de tempo gasto com a reprodução de mídia permite que os usuários de mídia entendam suas visualizações pelo tempo de exibição durante o dia em relação a uma granularidade escolhida. <br>[Painel Tempo gasto com a reprodução da mídia (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=pt-BR) | Janeiro de 2022 |


## *Notas de versão anteriores*

| Recurso | Descrição | Data de direcionamento ou atualização |
| ----------- | ---------- | -------------- |
| Tempo gasto com a reprodução da mídia | O recurso Tempo gasto com a reprodução da mídia de streaming da Adobe fornece informações valiosas sobre o envolvimento do visualizador e permite que as organizações de mídia obtenham insights mais profundos e detalhados sobre o engajamento do usuário a cada minuto, por meio da análise avançada de tempo gasto com recursos de faixa horária. É possível observar o tempo gasto visualizando seus fluxos de mídia em um período específico. É possível dividir a duração da reprodução em diferentes granularidades, incluindo as novas granularidades de 5, 15 e 30 minutos. [Saiba mais...](/help/reporting/workspace/media-playback-time-spent.md) | Setembro de 2021 |
| Painel Visualizador simultâneo de mídia no Analytics Workspace | Entenda onde o pico de simultaneidade ocorreu ou onde as quedas ocorreram. Obtenha insights importantes sobre a qualidade do conteúdo e o envolvimento do visualizador, além de ajuda na solução de problemas ou no planejamento de volume e escala. [Saiba mais...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Painel Visualizadores simultâneos de mídia no Analytics Workspace (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=pt-BR#analysis-workspace) | Setembro de 2020 <br><br><br>Janeiro de 2021 |
| Dispositivos e plataformas compatíveis | A Extensão Media Launch com SDK AEP agora é compatível com os seguintes dispositivos OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Junho de 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
