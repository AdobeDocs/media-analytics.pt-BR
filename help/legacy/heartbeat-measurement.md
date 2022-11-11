---
title: Sobre a medição de pulsação
description: Saiba como as pulsações são usadas para coletar métricas de vídeo.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# Sobre a medição de pulsação

O Adobe Analytics usa &quot;pulsações&quot; para coletar métricas de vídeo. Durante a reprodução do vídeo, as pulsações são enviadas ao servidor de rastreamento de pulsação para medir o tempo de reprodução. As chamadas de pulsação são enviadas a cada dez segundos. As pulsações resultam em métricas de envolvimento granulares com o vídeo e relatórios de fallout de vídeo mais precisos. O Adobe Analytics for Streaming Media mede as pulsações usando o Adobe Launch com a extensão do Media Analytics, o SDK de mídia e a API de coleção de mídia. Os componentes `AppMeasurement` e `VisitorID` são usados para receber dados de vídeo.

Usar pulsações, o Adobe Analytics para streaming de mídia oferece os seguintes benefícios:

| Recurso | Descrição |
|---|---|
| Eventos de mídia | Eventos detalhados e personalizados são enviados a cada 10 segundos para o conteúdo principal e a cada 1 segundo para anúncios |
| Métricas e dimensões | Métricas, dimensões e benchmarks padronizados e claros para todos os fornecedores. Com uma solução padronizada em todas as plataformas, você pode usar variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores. |
| Integrações | A ID do Experience Cloud está vinculada ao Adobe Experience Cloud para facilitar a análise cruzada. Com a integração automática do Adobe Experience Cloud, você pode segmentar seus públicos de mídia, direcioná-los e fazer recomendações de mídia com base nas preferências do usuário. |
| Preços | Rastreamento transparente por fluxo de mídia (único) |
| Implementação e suporte | Configuração simplificada com atualizações e melhorias contínuas. Com um processo de implementação simplificado, você pode mapear variáveis rapidamente por meio da API do player e validar implementações usando a ferramenta de depuração do Adobe para garantir que todas as variáveis necessárias sejam rastreadas com precisão. |
| Compartilhamento de parceiros | Federated Analytics e métricas certificadas. Com dados compartilhados por meio do Federated Analytics, você pode capitalizar nossos recursos de compartilhamento de mídia, o primeiro do setor, para avaliar dados de forma holística em todos os seus parceiros de distribuição de mídia: operadores, programadores e distribuidores. |
| Rastreamento avançado | Rastreamento de conteúdo baixado, Rastreamento de recuperação de erros e Visualizadores simultâneos. Você pode rastrear o conteúdo de mídia de transmissão que é baixado e reproduzido em um dispositivo, independentemente de sua conectividade. |
