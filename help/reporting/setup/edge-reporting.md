---
title: Configurar relatórios para implementações do Edge
description: Configure o Customer Journey Analytics para relatar os dados de mídia de transmissão coletados pela Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 6%

---

# Configurar relatórios para implementações do Edge

Depois de implementar a Coleção de mídia de transmissão por meio da Edge Network, configure o Customer Journey Analytics para relatar os dados coletados.

>[!NOTE]
>
>Esta página aborda a criação de relatórios no Customer Journey Analytics, o destino recomendado para implementações do Edge. Se, em vez disso, sua sequência de dados enviar dados de mídia de transmissão para a Adobe Analytics, consulte [Configurar relatórios para implementações somente do Analytics](analytics-reporting.md).

* **Pré-requisitos**: conclua uma implementação do Edge e colete alguns dados. Consulte a [visão geral da implementação do Edge](/help/implementation/edge/overview.md) e o método de implementação escolhido.

## Criar uma conexão no Customer Journey Analytics

1. No Customer Journey Analytics, crie uma conexão conforme descrito em [Criar uma conexão](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-connections/create-connection). Ao criar a conexão, verifique se a caixa de seleção **[!UICONTROL Importar todos os novos dados]** está habilitada.

## Criar uma visualização de dados no Customer Journey Analytics

1. No Customer Journey Analytics, crie uma visualização de dados conforme descrito em [Criar ou editar uma visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/create-dataview).

   1. No campo **[!UICONTROL Conexão]**, selecione a conexão criada anteriormente. As novas conexões podem levar até 15 minutos para serem exibidas.

   1. Na guia **[!UICONTROL Componentes]**, na seção **[!UICONTROL Campos de esquema]**, pesquise cada componente na tabela abaixo e arraste-o para o painel **[!UICONTROL Dimensões]** ou **[!UICONTROL Métricas]** apropriado. Se houver vários campos com o mesmo nome, use o caminho XDM para confirmar o campo correto. Aplique o rótulo de contexto mostrado no menu suspenso **[!UICONTROL Rótulos de contexto]** nas configurações de componente.

      | Componente | Tipo | Caminho XDM | Rótulo do contexto |
      |---|---|---|---|
      | [Conteúdo](/help/reporting/dimensions/content.md) | Dimensão | `mediaReporting.sessionDetails.name` | Media: ID de conteúdo |
      | [Nome do conteúdo](/help/reporting/dimensions/content-name.md) | Dimensão | `mediaReporting.sessionDetails.friendlyName` | Mídia: Nome do vídeo |
      | [Duração do conteúdo](/help/reporting/dimensions/content-length.md) | Dimensão | `mediaReporting.sessionDetails.length` | Mídia: Duração do vídeo |
      | [Programa](/help/reporting/dimensions/show.md) | Dimensão | `mediaReporting.sessionDetails.show` | Media: Show |
      | [Temporada](/help/reporting/dimensions/season.md) | Dimensão | `mediaReporting.sessionDetails.season` | Media: Season |
      | [Episódio](/help/reporting/dimensions/episode.md) | Dimensão | `mediaReporting.sessionDetails.episode` | Mídia: Episódio |
      | Tipo de evento | Dimensão | `eventType` | Mídia: Tipo de evento |
      | [Tempo gasto com o conteúdo](/help/reporting/metrics/content-time-spent.md) | Métrica | `mediaReporting.sessionDetails.timePlayed` | Mídia: Tempo gasto com conteúdo |
      | [Tempo gasto com a mídia](/help/reporting/metrics/media-time-spent.md) | Métrica | `mediaReporting.sessionDetails.totalTimePlayed` | Mídia: Tempo gasto com a mídia |
      | [Duração total da pausa](/help/reporting/metrics/total-pause-duration.md) | Métrica | `mediaReporting.sessionDetails.pauseTime` | Media: Duração Total Da Pausa |
      | [Hora de início](/help/reporting/metrics/time-to-start.md) | Métrica | `mediaReporting.qoeDataDetails.timeToStart` | Media: Time to Start |
      | [Duração total do buffer](/help/reporting/metrics/total-buffer-duration.md) | Métrica | `mediaReporting.qoeDataDetails.bufferTime` | Media: Total Buffer Duration |
      | Tempo limite do servidor de sessão de mídia | Métrica | `mediaReporting.sessionDetails.secondsSinceLastCall` | Media: Seconds Since Last Call (Mídia: segundos desde a última chamada) |

      >[!IMPORTANT]
      >
      >Os rótulos de contexto nesta tabela são necessários para que os painéis de mídia de transmissão funcionem. O Customer Journey Analytics as usa para calcular automaticamente as **Métricas derivadas Tempo de reprodução** e **Tempo gasto com a reprodução** (usadas pelos [Visualizadores simultâneos de mídia](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) e [Tempo gasto com a reprodução de mídia](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)) e para preencher as opções de relatório no painel [Público-alvo médio por minuto da mídia](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel).

      Você pode adicionar qualquer outra [dimensão](/help/reporting/dimensions/overview.md) ou [métrica](/help/reporting/metrics/overview.md) à sua visualização de dados neste momento. Cada página lista o caminho XDM para esse componente.

1. Selecione **[!UICONTROL Salvar e continuar]** → **[!UICONTROL Salvar e concluir]** para salvar suas alterações.

## Criar e configurar um projeto no Customer Journey Analytics

1. No Customer Journey Analytics, na guia **[!UICONTROL Workspace]**, na área **[!UICONTROL Projetos]**, selecione **[!UICONTROL Criar projeto]**.

1. Selecione **[!UICONTROL Projeto em branco]** → **[!UICONTROL Criar]**.

1. No novo projeto, selecione a visualização de dados criada anteriormente.

   Ao criar painéis no seu projeto, você pode usar quaisquer componentes adicionados à visualização de dados.

1. Selecione o ícone **Painéis** no painel à esquerda e arraste os painéis **[!UICONTROL Público-alvo médio por minuto da mídia]**, **[!UICONTROL Visualizadores simultâneos de mídia]** e **[!UICONTROL Tempo gasto com a reprodução da mídia]**.

1. (Condicional) Se você adicionou metadados personalizados ao esquema, defina a persistência para os campos personalizados, conforme descrito em [Configurações do componente de Persistência](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) no guia do Customer Journey Analytics.

1. Compartilhe o projeto conforme descrito em [Compartilhar projetos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=pt-BR).

   >[!NOTE]
   >
   >Se os usuários com os quais você deseja compartilhar não estiverem disponíveis, verifique se eles têm acesso de usuário e administrador ao Customer Journey Analytics na Adobe Admin Console.

## Painéis de mídia disponíveis no Customer Journey Analytics

O Analysis Workspace no Customer Journey Analytics inclui três painéis de mídia dedicados para clientes com o complemento Coleção de mídia de transmissão. Esses painéis fornecem visualizações pré-construídas para as necessidades mais comuns de relatórios de mídia de transmissão.

* **[Público-alvo médio por minuto da mídia](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**: compara o consumo médio de conteúdo entre programas de qualquer duração ou gênero. Oferece suporte aos modos de conteúdo específico (com base na duração) e período personalizado e permite a atualização das classificações de duração após o fato.
* **[Visualizadores simultâneos de mídia](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**: analisa visualizadores simultâneos ao longo do tempo para identificar pico de simultaneidade e pontos de devolução. Suporta detalhamento de séries e granularidade configurável por segmentos, dimensões ou intervalos de datas.
* **[Tempo gasto com a reprodução da mídia](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**: analisa a duração da reprodução ao longo do tempo com detalhes sobre os períodos de pico e vale. Suporta granularidade configurável e formato de saída (horas ou minutos).

>[!MORELIKETHIS]
>
>* [Visão geral das dimensões](/help/reporting/dimensions/overview.md)
>* [Visão geral das métricas](/help/reporting/metrics/overview.md)
