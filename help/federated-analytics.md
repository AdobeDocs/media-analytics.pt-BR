---
seo-title: Federated Analytics
title: Federated Analytics
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: 498546566d1dcb8c4ad84482332d46142eecd1ca

---


# Federated Analytics{#federated-analytics}

O serviço Federated Analytics fornece um sistema para compartilhar dados do Adobe Media Analytics (áudio e vídeo) entre dois parceiros.
Os dados de avaliação de vídeo padronizados criados pelo Media Analytics são a marca do Federated Analytics e permitem que os mesmos dados fluam em um único relatório de várias fontes.
Por meio das regras e lógicas que regem o Federated Analytics, os dados são facilmente controlados e individualizados para atender às necessidades de cada parceria.
O Federated Analytics torna a avaliação de áudio e vídeo mais eficiente, simplificada e acionável.

## Benefícios {#section_804FFE8671594A6FB769CBE79EF9D627}

* **Transparente:** elimine a “caixa preta” em relação à criação de dados usando uma mesma lógica entre empresas
* **Abrangente:** entenda o alcance total e o impacto do consumo de áudio e vídeo em parcerias, plataformas e dispositivos
* **Seguro:** controle o compartilhamento de dados no lado do servidor por meio de regras e lógica
* **Padronizado:** fale a mesma linguagem de dados que seus parceiros
* **Acionável:** quantifique os dados de áudio e vídeo em relação a reprodutores de referência, rastreie tendências e detecte anomalias por meio do Adobe Analytics
* **Centralizado:** colete dados de avaliação de áudio e vídeo em um único local da Adobe
* **Contratual:** cumpra facilmente os requisitos legais de compartilhamento de dados
* **Tempo hábil:** envie e receba dados em tempo real
* **Fácil:** marque reprodutores com os SDKs da Adobe, compartilhe dados com vários parceiros

## Definições {#section_ypl_mb3_vbb}

* **Remetente:** o cliente que gera os dados de análise de áudio e vídeo em reprodutores particulares
* **Destinatário:** o cliente que recebe os dados de análise de áudio e vídeo do remetente

## Requisitos {#section_4758843A8941441B9A4D0D7A61077A6E}

* **Contrato de fluxos de mídia:** o destinatário e o remetente precisam contratar o Adobe Analytics para fluxos de mídia para obterem acesso aos dados de áudio e vídeo no Adobe Analytics. Entre em contato com a equipe de conta para obter mais detalhes.
* **Adendo federado:** cada Remetente e Destinatário deve ter um adendo assinado em vigor com a Adobe para enviar ou receber dados. Um adendo por cliente é necessário, e não um adendo por parceria. Entre em contato com a equipe de conta para obter mais detalhes.
* **Implementação do Media Analytics:** o Remetente deve ter o Media Analytics implementado em todos os reprodutores que farão parte do conjunto de dados federados. Somente os dados do Media Analytics estão disponíveis para federação. See documentation: [Measuring audio and video in Adobe Analytics](/help/media-overview.md)

* **Contrato de consultoria da Adobe:** para a configuração inicial de regras federadas entre o destinatário e o remetente, é valioso trabalhar com os serviços de consultoria para analisar os dados e criar o contrato de compartilhamento de dados.

## Download do formulário do Federated Analytics

Baixe a versão atual deste formulário aqui: Acordo de Regras de [Federação](https://github.com/AdobeDocs/media-analytics.en/blob/master/help/federated-analytics-form.pdf)

## Processo {#section_byb_kb3_vbb}

1. O Remetente e o Destinatário trabalham juntos para preencher o formulário do Contrato de regras de federação. O formulário do Contrato de regras federadas contém campos especiais para nossa equipe de engenharia e deve ser editado SOMENTE usando o Adobe Acrobat. [Baixe o Acrobat gratuitamente.](https://get.adobe.com/reader/)
1. Os serviços de consultoria fornecem um exemplo de arquivo de dados para o Destinatário contendo dados reais dos reprodutores do Remetente para voltar a confirmar que as regras corretas de compartilhamento de dados estão definidas, desde que os arquivos de dados estejam disponíveis.
1. O Remetente e o Destinatário garantem que o contrato de compartilhamento de dados atende a todos os requisitos contratuais entre as duas partes.
1. Os serviços de consultoria enviam o formulário preenchido à engenharia da Adobe para configurar as regras de compartilhamento de dados.
1. Os dados são compartilhados no conjunto de relatórios de desenvolvimento que o Destinatário analisará e validará.
1. Quando o Destinatário confirma que os dados estão corretos, a engenharia da Adobe atualiza as regras para apontar para um conjunto de relatórios de produção.
1. O Destinatário revisará e validará os dados no conjunto de relatórios de produção.
1. Se ocorrerem alterações no conjunto de dados no futuro, o Remetente ou o Destinatário poderão enviar um tíquete de atendimento ao cliente para obter suporte.

