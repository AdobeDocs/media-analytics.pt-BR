---
title: Visualizadores simultâneos de mídia
description: '"Saiba mais sobre o painel Visualizadores simultâneos de mídia usado para exibir visualizadores simultâneos durante um dia. Os dados podem ser filtrados por conteúdo, tipo de dispositivo ou país."'
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: '"Noções básicas do Media Analytics, Reports & Analytics"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 89%

---

# Visualizadores simultâneos de mídia{#media-concurrent-viewers}

O painel Visualizadores simultâneos de mídia exibe os visualizadores simultâneos durante um dia. Os dados podem ser filtrados por conteúdo, tipo de dispositivo ou país.

>[!TIP]
>
> Este relatório se baseia em sessões de mídia ativas simultâneas.  Para ver visualizadores simultâneos por visitante único, com os recursos adicionais para aplicar um segmento, detalhar e comparar, use o [Painel Visualizadores simultâneos de mídia no Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=pt-BR).


![](assets/video-concurrent-viewers.png)

## Recursos do relatório {#report-features}

Estes são alguns recursos deste relatório:

* Não é em tempo real. Ele tem a latência normal do Adobe Analytics.
* O relatório cobre um período de 24 horas. O eixo x é a hora do dia com base no fuso horário do conjunto de relatórios.
* Ele mostra os visualizadores simultâneos com granularidade mínima.
* Existe um *Relatório de visualizadores simultâneos de mídia* que mostra quantos visualizadores estão assistindo ou ouvindo todo o conteúdo.
* Há um relatório de Visualizadores simultâneos no relatório de *Detalhes de mídia* que mostra quantos visualizadores estão assistindo ou ouvindo um item de mídia específico.
* O relatório só funciona por um dia.
* O cliente pode consultar os relatórios históricos do visualizador simultâneo (limitados a um único dia).

## Limitações {#limitations}

Estas são algumas limitações desse relatório:

* Nenhum dado será exibido se o intervalo selecionado não for um dia inteiro.
* Não é possível exportar os dados, como o ReportBuilder.
* Não é possível apresentar os dados em um formato de tabela.
* Não é possível enviar um relatório por e-mail.
* Mesmo que não rastreie anúncios, é necessário reativar o rastreamento de mídia e selecionar o módulo Anúncio de mídia.
* Essa funcionalidade fornecerá dados precisos ao usar uma Biblioteca de heartbeats que tenha recursos de rastreamento de pausa.
