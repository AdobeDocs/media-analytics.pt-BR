---
title: Sobre a medição de pulsação
description: Saiba como as pulsações são usadas para coletar métricas de vídeo.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e6c28e30-8689-4bf4-8fa8-561343d308a9
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# Sobre a medição de pulsação

Os serviços de mídia de transmissão da Adobe usam &quot;heartbeats&quot; para coletar métricas de vídeo. Durante a reprodução do vídeo, as pulsações são enviadas ao servidor de rastreamento de pulsação para medir o tempo de reprodução. As chamadas de pulsação são enviadas a cada dez segundos. As pulsações resultam em métricas de engajamento granulares com o vídeo e relatórios de fallout de vídeo mais precisos. os serviços de mídia de transmissão medem as pulsações usando o Adobe Launch com a extensão do Media Analytics, o Media SDK e a API Media Collection. Os componentes `AppMeasurement` e `VisitorID` são usados para receber dados de vídeo.

Usar pulsações nos serviços de streaming de mídia oferece os seguintes benefícios:

| Recurso | Descrição |
|---|---|
| Eventos de mídia | Eventos detalhados e personalizados são enviados a cada 10 segundos para o conteúdo principal e a cada 1 segundo para anúncios |
| Métricas e dimensões | Métricas, dimensões e benchmarks padronizados e claros para todos os fornecedores. Com uma solução padronizada em todas as plataformas, você pode usar variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores. |
| Integrações | A Experience Cloud ID está vinculada ao Adobe Experience Cloud para facilitar a análise cruzada. Com a integração automática do Adobe Experience Cloud, você pode segmentar os públicos de mídia, direcioná-los e fazer recomendações de mídia com base nas preferências do usuário. |
| Preços | Rastreamento transparente por fluxo de mídia (único) |
| Implementação e suporte | Configuração simplificada com atualizações e melhorias contínuas. Com um processo de implementação simplificado, você pode mapear variáveis rapidamente por meio da API do player e validar implementações usando a ferramenta de depuração da Adobe para garantir que todas as variáveis necessárias sejam rastreadas com precisão. |
| Compartilhamento de parceiros | Federated Media e Métricas certificadas. Com dados compartilhados por meio da Federated Media, você pode capitalizar nossos recursos de compartilhamento de mídia, pioneiros no setor, para avaliar dados de forma holística em todos os seus parceiros de distribuição de mídia: operadores, programadores e distribuidores. |
| Rastreamento avançado | Rastreamento de conteúdo baixado, rastreamento de recuperação de erros e visualizadores simultâneos. Você pode rastrear o conteúdo de streaming de mídia que é baixado e reproduzido em um dispositivo, independentemente de sua conectividade. |
