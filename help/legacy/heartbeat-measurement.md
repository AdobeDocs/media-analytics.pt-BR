---
title: Sobre a medição de pulsação
description: Saiba como as pulsações são usadas para coletar métricas de vídeo.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 75%

---

# Sobre a medição de pulsação

Os serviços de mídia de transmissão da Adobe usam &quot;heartbeats&quot; para coletar métricas de vídeo. Durante a reprodução do vídeo, as pulsações são enviadas ao servidor de rastreamento de pulsação para medir o tempo de reprodução. As chamadas de pulsação são enviadas a cada dez segundos. As pulsações resultam em métricas de engajamento granulares com o vídeo e relatórios de fallout de vídeo mais precisos. os serviços de mídia de transmissão medem as pulsações usando o Adobe Launch com a extensão do Media Analytics, o Media SDK e a API Media Collection. Os componentes `AppMeasurement` e `VisitorID` são usados para receber dados de vídeo.

Usar pulsações nos serviços de streaming de mídia oferece os seguintes benefícios:

| Recurso | Descrição |
|---|---|
| Eventos de mídia | Eventos detalhados e personalizados são enviados a cada 10 segundos para o conteúdo principal e a cada 1 segundo para anúncios |
| Métricas e dimensões | Métricas, dimensões e parâmetros de comparação padronizados e claros para todos os fornecedores. Com uma solução padronizada em todas as plataformas, você pode usar variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores. |
| Integrações | O Experience Cloud ID é vinculado à Adobe Experience Cloud para facilitar a análise cruzada. Com a integração automática da Adobe Experience Cloud, você pode segmentar os públicos-alvos de mídia, direcioná-los e criar recomendações de mídia de acordo com as preferências do usuário. |
| Preços | Rastreamento transparente por fluxo de mídia (único) |
| Implementação e suporte | Configuração simplificada com atualizações e melhorias contínuas. Com um processo de implementação simplificado, você pode mapear variáveis rapidamente por meio da API do player e validar implementações usando a ferramenta Adobe Debug para garantir que todas as variáveis necessárias sejam rastreadas com precisão. |
| Compartilhamento de parceiros | Federated Media e Métricas certificadas. Com dados compartilhados por meio da Federated Media, você pode capitalizar nossos recursos de compartilhamento de mídia, pioneiros no setor, para avaliar dados de forma holística em todos os seus parceiros de distribuição de mídia: operadores, programadores e distribuidores. |
| Rastreamento avançado | Rastreamento de conteúdo baixado, rastreamento de recuperação de erros e visualizadores simultâneos. Você pode rastrear o conteúdo de mídia de streaming que é baixado e reproduzido em um dispositivo, independentemente de sua conexão. |
