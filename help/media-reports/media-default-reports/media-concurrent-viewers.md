---
title: Visualizadores simultâneos de mídia
description: null
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Visualizadores simultâneos de mídia {#media-concurrent-viewers}

O painel Visualizadores simultâneos de mídia exibe os visualizadores simultâneos durante um dia. Os dados podem ser filtrados por conteúdo, tipo de dispositivo ou país.

>[!TIP]
>
>Nenhum dado será exibido se o intervalo selecionado não for um dia inteiro.

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

* Não é possível exportar os dados, como o ReportBuilder.
* Não é possível apresentar os dados em um formato de tabela.
* Não é possível enviar um relatório por e-mail.
* Mesmo que não rastreie anúncios, é necessário reativar o rastreamento de mídia e selecionar o módulo Anúncio de mídia.
* Essa funcionalidade fornecerá dados precisos ao usar uma Biblioteca de heartbeats que tenha recursos de rastreamento de pausa.

