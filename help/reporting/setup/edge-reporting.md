---
title: Configurar relatórios para implementações do Edge
description: Configure o Customer Journey Analytics para relatar os dados de mídia de transmissão coletados pela Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 17%

---

# Configurar relatórios para implementações do Edge

Depois de implementar a Coleção de mídia de transmissão por meio da Edge Network, configure o Customer Journey Analytics para relatar os dados coletados. Esta página descreve como criar uma conexão, uma visualização de dados e um projeto para mídia de transmissão.

>[!NOTE]
>
>Esta página aborda a criação de relatórios no Customer Journey Analytics, o destino recomendado para implementações do Edge. Se, em vez disso, sua sequência de dados enviar dados de mídia de transmissão para a Adobe Analytics, consulte [Configurar relatórios para implementações somente do Analytics](analytics-reporting.md).

* **Pré-requisitos**: conclua uma implementação do Edge e colete alguns dados. Consulte a [visão geral da implementação do Edge](/help/implementation/edge/overview.md) e o método de implementação escolhido.

## Criar uma conexão no Customer Journey Analytics

1. No Customer Journey Analytics, crie uma conexão conforme descrito em [Criar uma conexão](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=pt-BR).

   Ao criar a conexão, as seguintes seleções são necessárias para a mídia de transmissão:

   1. Selecione o conjunto de dados criado durante a implementação.

   1. Verifique se a configuração **[!UICONTROL Importar todos os novos dados]** está habilitada.

1. Continue com [Criar uma exibição de dados no Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics).

## Criar uma visualização de dados no Customer Journey Analytics

1. No Customer Journey Analytics, crie uma visualização de dados conforme descrito em [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=pt_BR).

   1. No campo **[!UICONTROL Conexão]**, selecione a conexão criada anteriormente.

      Pode levar até 15 minutos para que uma nova conexão esteja disponível para seleção.

   1. Na guia **[!UICONTROL Componentes]**, na seção **[!UICONTROL Campos de esquema]**, procure cada componente nas tabelas abaixo e arraste-o para o painel **[!UICONTROL Métricas]**. Se houver vários campos com o mesmo nome, use o caminho XDM para confirmar o campo correto.

      **Conteúdo principal - Métricas de conteúdo**

      | Nome do componente | Caminho XDM |
      |----------|---------|
      | Inícios da mídia | mediaReporting.sessionDetails.isViewed |
      | Visualizações do segmento de mídia | mediaReporting.sessionDetails.hasSegmentView |
      | Início do conteúdo | mediaReporting.sessionDetails.isPlayed |
      | Conteúdo concluído | mediaReporting.sessionDetails.isCompleted |
      | Tempo gasto no conteúdo | mediaReporting.sessionDetails.timePlayed |
      | Tempo gasto com a mídia | mediaReporting.sessionDetails.totalTimePlayed |
      | Tempo de reprodução exclusivo | mediaReporting.sessionDetails.uniqueTimePlayed |
      | Marcador de progresso 10% | mediaReporting.sessionDetails.hasProgress10 |
      | Público-alvo médio por minuto | mediaReporting.sessionDetails.averageMinuteAudience |

      **Capítulo e anúncios - Capítulo e métricas de anúncios**

      | Nome do componente | Caminho XDM |
      |----------|---------|
      | Capítulo iniciado | mediaReporting.chapterDetails.isStarted |
      | Capítulo concluído | mediaReporting.chapterDetails.isCompleted |
      | Tempo de reprodução do capítulo | mediaReporting.chapterDetails.timePlayed |
      | Anúncio iniciado | mediaReporting.advertisingDetails.isStarted |
      | Anúncio concluído | mediaReporting.advertisingDetails.isCompleted |
      | Tempo de reprodução do anúncio | mediaReporting.advertisingDetails.timePlayed |

      **QoE - métricas de QoE**

      | Nome do componente | Caminho XDM |
      |----------|---------|
      | Hora de início | mediaReporting.qoeDataDetails.timeToStart |
      | Quedas antes de começar | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Fluxos afetados pelo buffer | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Fluxos afetados pela mudança na taxa de bits | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Alterações da taxa de bits | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Taxa média de bits | mediaReporting.qoeDataDetails.bitrateAverage |
      | Queda de quadros | mediaReporting.qoeDataDetails.droppedFrames |
      | Erros | mediaReporting.qoeDataDetails.errorCount |
      | Fluxos afetados por erros | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Fluxos afetados pela queda de quadros | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |

      **Estado do player - Métricas do estado do player**

      | Nome do componente | Caminho XDM |
      |----------|---------|
      | Conjunto do estado do player | mediaReporting.states.isSet |
      | Contagem do estado do player | mediaReporting.states.count |
      | Tempo do estado do player | mediaReporting.states.time |

   1. Atualize os rótulos (no menu suspenso **[!UICONTROL Rótulos de contexto]**) dos componentes na tabela a seguir. Procure e arraste para o painel quaisquer componentes que ainda não estejam no painel métricas.

      | Nome do componente | Rótulo do contexto |
      |---------|----------|
      | Tempo limite do servidor de sessão de mídia | Media: Seconds Since Last Call (Mídia: segundos desde a última chamada) |
      | Tempo gasto com a mídia | Mídia: Tempo gasto com a mídia |
      | Duração total do buffer | Media: Total Buffer Duration |
      | Hora de início | Media: Time To Start |
      | Duração total da pausa | Media: Duração Total Da Pausa |

   1. Para adicionar detalhamentos ao seu projeto, adicione as seguintes dimensões ao painel **[!UICONTROL Dimensões]**:

      | Caminho XDM | Nome do componente |
      |---------|----------|
      | mediaReporting.states.name | Nome do estado do player |
      | mediaReporting.sessionDetails.ID | ID da sessão de mídia |

      Além das dimensões nessa tabela, é possível adicionar outras dimensões pelas quais você deseja filtrar dados em seus projetos.

1. Selecione **[!UICONTROL Salvar e continuar]** > **[!UICONTROL Salvar e concluir]** para salvar as alterações.

1. Continuar com [Criar e configurar um projeto no Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Criar e configurar um projeto no Customer Journey Analytics

1. No Customer Journey Analytics, na guia **[!UICONTROL Workspace]**, na área **[!UICONTROL Projetos]**, selecione **[!UICONTROL Criar projeto]**.

1. Selecione **[!UICONTROL Projeto em branco]** > **[!UICONTROL Criar]**.

1. No novo projeto, selecione a visualização de dados criada anteriormente.

   Ao criar painéis no seu projeto, você pode usar quaisquer componentes adicionados à visualização de dados.

1. Selecione o ícone **Painéis** no painel à esquerda e arraste o painel **[!UICONTROL Visualizadores simultâneos de mídia]** e o painel **[!UICONTROL Tempo gasto com a reprodução da mídia]**.

1. (Condicional) Se você adicionou metadados personalizados ao esquema, defina a persistência para os campos personalizados, conforme descrito em [Configurações do componente de Persistência](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) no guia do Customer Journey Analytics.

1. Compartilhe o projeto conforme descrito em [Compartilhar projetos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=pt-BR).

   >[!NOTE]
   >
   >Se os usuários com os quais você deseja compartilhar não estiverem disponíveis, verifique se eles têm acesso de usuário e administrador ao Customer Journey Analytics na Adobe Admin Console.

>[!MORELIKETHIS]
>
>* [Painéis de mídia no Workspace](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [Visão geral das dimensões](/help/reporting/dimensions/overview.md)
>* [Visão geral das métricas](/help/reporting/metrics/overview.md)
