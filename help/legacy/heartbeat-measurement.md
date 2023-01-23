---
title: Sobre a medição de pulsação
description: Saiba como as pulsações são usadas para coletar métricas de vídeo.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: ht
source-wordcount: '311'
ht-degree: 100%

---

# Sobre a medição de pulsação

O Adobe Analytics usa “pulsações” (“heartbeats”) para coletar métricas de vídeo. Durante a reprodução do vídeo, as pulsações são enviadas ao servidor de rastreamento de pulsação para medir o tempo de reprodução. As chamadas de pulsação são enviadas a cada dez segundos. As pulsações resultam em métricas de envolvimento granulares com o vídeo e relatórios de fallout de vídeo mais precisos. O Adobe Analytics para mídia de streaming mede as pulsações usando o Adobe Launch com a extensão do Media Analytics, o SDK de mídia e a API de coleção de mídia. Os componentes `AppMeasurement` e `VisitorID` são usados para receber dados de vídeo.

Usar pulsações, o Adobe Analytics para streaming de mídia oferece os seguintes benefícios:

| Recurso | Descrição |
|---|---|
| Eventos de mídia | Eventos detalhados e personalizados são enviados a cada 10 segundos para o conteúdo principal e a cada 1 segundo para anúncios |
| Métricas e dimensões | Métricas, dimensões e parâmetros de comparação padronizados e claros para todos os fornecedores. Com uma solução padronizada em todas as plataformas, você pode usar variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores. |
| Integrações | O Experience Cloud ID é vinculado à Adobe Experience Cloud para facilitar a análise cruzada. Com a integração automática da Adobe Experience Cloud, você pode segmentar os públicos de mídia, direcioná-los e criar recomendações de mídia de acordo com as preferências do usuário. |
| Preços | Rastreamento transparente por fluxo de mídia (único) |
| Implementação e suporte | Configuração simplificada com atualizações e melhorias contínuas. Com um processo de implementação simplificado, você pode mapear variáveis rapidamente por meio da API do player e validar implementações usando a ferramenta Adobe Debug para garantir que todas as variáveis necessárias sejam rastreadas com precisão. |
| Compartilhamento de parceiros | Federated Analytics e métricas certificadas. Com dados compartilhados por meio do Federated Analytics, você pode capitalizar sobre nossos recursos de compartilhamento de mídia líderes de setor, para avaliar dados de maneira integral em todos os seus parceiros de distribuição de mídia, sejam eles operadores, programadores ou distribuidores. |
| Rastreamento avançado | Rastreamento de conteúdo baixado, rastreamento de recuperação de erros e visualizadores simultâneos. Você pode rastrear o conteúdo de mídia de streaming que é baixado e reproduzido em um dispositivo, independentemente de sua conexão. |
