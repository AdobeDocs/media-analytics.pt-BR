---
title: Notas de versão dos serviços de mídia de streaming
description: Veja as notas de versão dos serviços de streaming de mídia.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1516
ht-degree: 79%

---

# Notas de versão dos serviços de mídia de streaming (outubro de 2025)

**Última atualização**: quarta-feira, 7 de outubro de 2025

## Recursos relacionados

Para obter informações sobre novos recursos, correções e informações importantes para administradores, consulte os seguintes recursos.

* [Notas de versão do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=pt-BR)
* [Notas de versão do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=pt-BR)
* As últimas atualizações da versão do [Adobe CX Enterprise](https://business.adobe.com/br/products/adobe-experience-cloud-products.html)

* [Tutoriais do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=pt-BR)

## *Notas de versão atuais*

## Recursos novos e atualizados para os serviços de streaming de mídia da Adobe {#cja-features}

| Recurso | Descrição | Data alvo |
| ----------- | ---------- | ------- |
| **Serviços de mídia de streaming: suporte aos dados do cronograma** | Agora é possível fazer upload de dados agendados de conteúdo antigo de mídias de streaming ao vivo para acompanhar com mais facilidade e precisão o número de visualizadores.<p>Veja a seguir alguns exemplos de conteúdo ao vivo que são compatíveis com o upload de dados de programação:</p><ul><li>Plataformas FAST (TV com suporte a anúncios gratuitos)</li><li>Transmissões locais</li><li>Esportes ao vivo</li></ul><p>O upload de dados de programação permite acompanhar os dados de de número de visualizadores de programas individuais que foram executados durante o período designado no arquivo de upload. É possível até coletar dados do número de visualizadores para tópicos ou segmentos de programa específicos.</p><p>Esses recursos estão disponíveis independentemente de como você implementou a coleta de mídias de transmissão.</p><p>Anteriormente, era difícil vincular com precisão uma determinada sessão a programas específicos ao analisar o conteúdo ao vivo e não era possível vincular uma determinada sessão a tópicos ou segmentos de programa individuais.</p><p>Para obter mais informações, consulte [Fazer upload de dados de agendamento para rastrear conteúdo ao vivo](/help/use-cases/track-schedule-data.md)</p> | Início da implantação: 29 de outubro de 2025<p>Disponibilidade geral: primeiro semestre de 2026</p><p>(Planejado originalmente para disponibilização geral em 29 de outubro de 2025)</p> |
| Campos XDM atualizados para coletar dados de streaming de mídia no Adobe Experience Platform | Ao coletar dados de mídia de streaming na Adobe Experience Platform, os caminhos do campo XDM mostrados no cabeçalho de “Caminho de campo XDM” da documentação de parâmetros de mídia de streaming não devem mais ser usados. Em vez disso, os clientes que implementaram o conector de origem do Analytics para coletar dados de mídia de streaming na Platform antes de 9 de maio de 2025 devem migrar suas configurações para os caminhos de campo mediaReporting, conforme mostrado no cabeçalho de “Caminho de campo XDM do relatório” da documentação de parâmetros da mídia de streaming.<p> Esses caminhos de campo estão documentados nas páginas de variáveis de mídia de streaming vinculadas da [Visão geral dos serviços de mídia de streaming](../media-overview.md) e estão marcados como &quot;Obsoleto&quot;. (Nenhuma ação será necessária para clientes que implementarem o conector de origem do Analytics após 9 de maio de 2025 e já estiverem usando somente os caminhos de XDM de mediaReporting.)</p><p>A assimilação de dados nos caminhos de campo XDM obsoletos continuará até o final de outubro de 2025. Após esse período, os caminhos de campo obsoletos serão totalmente removidos e não serão mais visíveis na interface de esquema da Adobe Experience Platform, e os dados serão enviados usando somente os caminhos de campo do mediaReporting.</p><p>Para obter mais informações, consulte [Mapeamento de parâmetros do Media Analytics para Adobe Experience Platform e Customer Journey Analytics](/help/implementation/edge/migrate/parameters-mapping.md).</p><p>Entre em contato com os serviços da Adobe Consulting ou com a equipe de conta para obter suporte à migração. </p> | Outubro de 2025 |
| Enviar dados da Web para o Adobe Experience Platform Edge Network com o Web SDK | Agora você pode [usar o Adobe Experience Platform Web SDK para enviar dados da Web de mídia de streaming ao Adobe Experience Platform Edge Network](/help/implementation/edge/web-sdk.md), permitindo que você crie campanhas mais personalizadas e forneça mais conteúdo personalizado, resultando em mais dados de rastreamento a serem relatados.<p>Esse aprimoramento fornece um método de coleção unificada para implementações da web em todas as soluções da Platform, como Customer Journey Analytics, RT-CDP, AJO e o encaminhamento de eventos. Anteriormente, a única maneira de enviar dados da web de mídia de transmissão para a Edge Network era por meio da API de borda de mídia. | 29 de maio de 2024 |
| Enviar dados do Roku para o Adobe Experience Platform Edge | Agora, ao [instalar a Coleção de mídia de streaming do Customer Journey Analytics com o Experience Platform Edge](/help/implementation/edge/overview.md), você pode usar o Adobe Experience Platform Roku SDK para enviar dados de mídia de streaming para o Adobe Experience Platform. | 12 de abril de 2024 |
| Coleção de mídia: Integração com a Experience Edge (API e SDK móvel) | Agora você pode usar a API da Experience Edge e o Mobile SDK para implementar a Coleção de mídia de transmissão da Customer Journey Analytics, permitindo criar campanhas mais personalizadas e fornecer conteúdo mais personalizado, resultando em mais dados de rastreamento a serem relatados.<p>Esse aprimoramento fornece um método de coleta unificada em todas as soluções, como relatórios do Customer Journey Analytics, RT-CDP, AJO e encaminhamento de eventos.  [Saiba mais](/help/implementation/edge/overview.md) | sábado, 12 de maio de 2023 |
| Painel Visualizador simultâneo de mídia | Entenda onde o pico de simultaneidade ocorreu ou onde as quedas ocorreram. Obtenha insights importantes sobre a qualidade do conteúdo e o engajamento do visualizador, além de ajuda na solução de problemas ou no planejamento de volume e escala. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=pt-BR) | 9 de agosto de 2022 |
| Painel Tempo gasto com a reprodução da mídia | O painel Tempo gasto com a reprodução de mídia fornece informações valiosas sobre o engajamento do visualizador e permite que as organizações de mídia obtenham insights mais profundos e detalhados sobre o engajamento do usuário a cada minuto, por meio da análise avançada do tempo gasto com recursos de faixa horária. É possível observar o tempo gasto visualizando seus fluxos de mídia em um período específico. É possível dividir a duração da reprodução por diferentes granularidades, incluindo novas granularidades de 5 minutos, 15 minutos e 30 minutos. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=pt-BR) | 9 de agosto de 2022 |
| Compartilhar anotações em cartões de pontuação para dispositivos móveis | Você pode exibir anotações criadas no Espaço de trabalho, nos Cartões de pontuação para dispositivos móveis. Isso permite compartilhar nuances de dados contextuais e insights sobre sua organização e campanhas diretamente em projetos do Cartão de pontuação para dispositivos móveis, visualizáveis no aplicativo móvel de painéis do Analytics. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=pt-BR) | 15 de junho de 2022 |
| Atualizações do Report Builder para Customer Journey Analytics | Inclui recursos como agendamento e gerenciador de blocos de dados. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=pt-BR) | 18 de maio de 2022 |
| Anotações no Espaço de trabalho | As anotações no Espaço de trabalho permitem comunicar com eficiência nuances de dados contextuais e insights à sua organização. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=pt-BR) | A implantação gradual começa em 23 de março de 2022 |
| Modo de visualização do projeto do cartão de pontuação para dispositivos móveis | Visualize como o cartão de pontuação para dispositivos móveis ficará no aplicativo de painéis do Analytics, diretamente do construtor do cartão de pontuação. O modo de visualização permite que os usuários interajam com filtros e gráficos da mesma forma que fazem no aplicativo, permitindo que visualizem a experiência antes de salvar e compartilhar o cartão de pontuação. Os usuários também podem usar o seletor de dispositivos no modo de visualização para ver como o cartão de pontuação será exibido em diferentes dispositivos. [Saiba mais](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=pt-BR#preview) | 16 de fevereiro de 2022 |


## Recursos novos e atualizados para os serviços de streaming de mídia da Adobe {#sm-features}

| Recurso | Descrição | Data alvo |
| ----------- | ---------- | ------- |
| Rastreamento de vários estados do player | Use a API de coleção de mídia para implementar o rastreamento de vários estados do player. [Saiba mais](/help/implementation/events/player-state/overview.md) | Setembro de 2022 |
| Campos XDM renomeados | Nomes de campos XDM renomeados para fins de consistência:<br>* Parâmetros de áudio e vídeo<br>* Parâmetros de anúncio<br>* Parâmetros de capítulo<br>* Parâmetros de estado do player<br>* Parâmetros de qualidade | Setembro de 2022 |
| Referência ao Device Co-op | Remoção da referência ao Device Co-op e ao requisito do serviço de ID. | Agosto de 2022 |
| Nomes de campos e caminhos XDM atualizados para coleção e relatórios | Atualização do seguinte:<br>* Parâmetros de áudio e vídeo<br>* Parâmetros de anúncio<br>* Parâmetros de capítulo<br>* Parâmetros de estado do player<br>* Parâmetros de qualidade | Agosto de 2022 |
| Público-alvo médio por minuto | Os clientes do Media Analytics podem usar o painel Audiência média por minuto para entender melhor o consumo médio de seu conteúdo. <br>A Audiência média por minuto permite as comparações da programação de qualquer comprimento ou gênero. Além disso, é possível comparar ou anexar essa audiência média por minuto digital às métricas de média por minuto lineares de TV. Esse painel oferece mais flexibilidade para medir a audiência média em períodos de tempo personalizados, bem como quando a classificação de duração for atualizada.  [Saiba mais](/help/reporting/workspace/average-minute-audience.md) | 16 de março de 2022 |
| Painel Tempo gasto com a reprodução da mídia | Saiba como o Painel de tempo gasto com a reprodução de mídia permite que os usuários de mídia entendam suas visualizações pelo tempo de exibição durante o dia em relação a uma granularidade escolhida. <br>[Painel Tempo gasto com a reprodução da mídia (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=pt-BR) | Janeiro de 2022 |


## *Notas de versão anteriores*

| Recurso | Descrição | Data de direcionamento ou atualização |
| ----------- | ---------- | -------------- |
| Tempo gasto com a reprodução da mídia | O recurso Tempo gasto com a reprodução da mídia de streaming da Adobe fornece informações valiosas sobre o envolvimento do visualizador e permite que as organizações de mídia obtenham insights mais profundos e detalhados sobre o engajamento do usuário a cada minuto, por meio da análise avançada de tempo gasto com recursos de faixa horária. É possível observar o tempo gasto visualizando seus fluxos de mídia em um período específico. É possível dividir a duração da reprodução em diferentes granularidades, incluindo as novas granularidades de 5, 15 e 30 minutos. [Saiba mais...](/help/reporting/workspace/media-playback-time-spent.md) | Setembro de 2021 |
| Painel Visualizador simultâneo de mídia no Analytics Workspace | Entenda onde o pico de simultaneidade ocorreu ou onde as quedas ocorreram. Obtenha insights importantes sobre a qualidade do conteúdo e o engajamento do visualizador, além de ajuda na solução de problemas ou no planejamento de volume e escala. [Saiba mais...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Painel Visualizadores simultâneos de mídia no Analytics Workspace (tutorial)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=pt-BR#analysis-workspace) | Setembro de 2020 <br><br><br>Janeiro de 2021 |
| Dispositivos e plataformas compatíveis | A Extensão Media Launch com SDK AEP agora é compatível com os seguintes dispositivos OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Junho de 2020 |


<!--
## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | 
-->
