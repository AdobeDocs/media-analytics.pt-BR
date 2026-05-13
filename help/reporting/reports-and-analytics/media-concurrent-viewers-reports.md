---
title: Visualizadores simultâneos de mídia
description: Saiba mais sobre o painel Visualizadores simultâneos de mídia usado para exibir visualizadores simultâneos durante um dia. Os dados podem ser filtrados por conteúdo, tipo de dispositivo ou país.
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 91%

---

# Relatórios dos visualizadores simultâneos da mídia {#media-concurrent-viewers}

O painel Visualizadores simultâneos de mídia exibe os visualizadores simultâneos durante um dia. Os dados podem ser filtrados por conteúdo, tipo de dispositivo ou país.

>[!TIP]
>
> Este relatório se baseia em sessões de mídia ativas simultâneas.  Para ver visualizadores simultâneos por visitante único, com os recursos adicionais para aplicar um segmento, detalhar e comparar, use o [Painel Visualizadores simultâneos de mídia no Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=pt-BR).
>

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
* Mesmo que não rastreie anúncios, é necessário reabilitar o rastreamento de mídia e selecionar o módulo Anúncio de mídia.
* Essa funcionalidade fornecerá dados precisos ao usar uma Biblioteca de heartbeats que tenha recursos de rastreamento de pausa.
