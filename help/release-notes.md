---
title: Notas de versão dos serviços de mídia de streaming
description: Veja as notas de versão para serviços de mídia de transmissão.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 36%

---

# Notas de versão dos serviços de mídia de streaming

**Última atualização**: 4 de junho de 2026

## 2026

| Recurso | Descrição | Data |
| --- | --- | --- |
| **Dados do agendamento de suporte** | Faça upload dos dados agendados do conteúdo antigo em tempo real para rastrear a audiência por programa ou segmento. Os tipos de conteúdo compatíveis incluem:<ul><li>Plataformas FAST (TV com suporte a anúncios gratuitos)</li><li>Transmissões locais</li><li>Esportes ao vivo</li></ul>Consulte o caso de uso [Carregar dados do agendamento para rastrear conteúdo ao vivo](/help/use-cases/track-schedule-data.md) para obter mais informações. | Início da implantação: 29 de outubro de 2025<p>Disponibilidade geral: outubro de 2026</p> |

## 2025

| Recurso | Descrição | Data |
| --- | --- | --- |
| **`mediaTimed`descontinuação de campo XDM** | O objeto XDM `mediaTimed` foi substituído em favor dos caminhos de campo `mediaReporting`. Os clientes que implementaram o conector de origem do Analytics antes de 9 de maio de 2025 devem migrar suas configurações. Consulte os seguintes guias de migração para obter mais informações:<ul><li>[Migrar públicos-alvo para os novos campos de mídia de streaming](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[Migrar o Customer Journey Analytics para usar os novos campos de mídia de streaming](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[Migrar Preparo de Dados para campos personalizados para os novos campos de mídia de streaming](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[Migrar perfis para os novos campos de mídia de streaming](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | Outubro de 2025 |

## 2024

| Recurso | Descrição | Data |
| --- | --- | --- |
| **Suporte ao Web SDK** | Envie dados da Web de mídia de transmissão para o Adobe Experience Platform Edge Network usando a extensão de tag da Web SDK ou Web SDK, habilitando um método de coleta unificada em soluções de plataforma, como Customer Journey Analytics, Real-time CDP, Journey Optimizer e encaminhamento de eventos. Consulte [Configurar o Web SDK para mídia de streaming](/help/implementation/edge/web-sdk.md) ou [Configurar a extensão de tag do Web SDK para mídia de streaming](/help/implementation/edge/web-sdk-tags.md) para obter mais informações. | 29 de maio de 2024 |
| **Suporte ao Roku** | Envie dados de mídia de transmissão para o Adobe Experience Platform usando o Roku SDK. Consulte [Configurar Roku para mídia de streaming](/help/implementation/edge/roku.md) para obter mais informações. | 12 de abril de 2024 |

## 2023

| Recurso | Descrição | Data |
| --- | --- | --- |
| **Suporte à Experience Edge** | Implemente a coleção de mídia de transmissão usando a API do Media Edge ou SDKs móveis para iOS e Android.<ul><li>[Configurar a API do Media Edge para mídia de streaming](/help/implementation/edge/media-edge-api.md)</li><li>[Configurar iOS para mídia de streaming](/help/implementation/edge/ios.md) ou [Configurar iOS para mídia de streaming com Tags](/help/implementation/edge/ios-tags.md)</li><li>[Configurar Android para mídia de streaming](/help/implementation/edge/android.md) ou [Configurar Android para mídia de streaming com Tags](/help/implementation/edge/android-tags.md)</li></ul> | sábado, 12 de maio de 2023 |

## 2022

| Recurso | Descrição | Data |
| --- | --- | --- |
| **Rastreamento de vários estados do player** | Use a API de Coleção de mídia para implementar vários [rastreamento de estado do player](/help/implementation/events/player-state/overview.md). | Setembro de 2022 |
| Campos XDM renomeados | Nomes de campos XDM renomeados para fins de consistência:<ul><li>Parâmetros de áudio e vídeo</li><li>Parâmetros de publicidade</li><li>Parâmetros de capítulo</li><li>Parâmetros de estado do player</li><li>Parâmetros de qualidade</li></ul> | Setembro de 2022 |
| **Painéis adicionados ao Customer Journey Analytics** | Adição do [painel de visualizadores simultâneos de mídia](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) e do [painel Tempo gasto com a reprodução da mídia](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) ao Customer Journey Analytics. | 9 de agosto de 2022 |
| **Audiência média por minuto** | Você pode usar o [painel Audiência média por minuto](https://experienceleague.adobe.com/pt-br/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel) para entender melhor o consumo médio de conteúdo. <br>A Audiência média por minuto permite as comparações da programação de qualquer comprimento ou gênero. Além disso, é possível comparar ou anexar essa audiência média por minuto digital às métricas de média por minuto lineares de TV. Esse painel oferece mais flexibilidade para medir a audiência média em períodos de tempo personalizados, bem como quando a classificação de duração for atualizada. | 16 de março de 2022 |

## 2021

| Recurso | Descrição | Data |
| --- | --- | --- |
| **Tempo gasto com reprodução de mídia** | O [painel Tempo gasto com a reprodução](https://experienceleague.adobe.com/pt-br/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent) oferece um insight valioso para o envolvimento do visualizador e permite que as organizações de mídia obtenham insights mais profundos e detalhados sobre o engajamento do usuário a cada minuto, por meio da análise avançada de tempo gasto com recursos de faixa horária. É possível observar o tempo gasto visualizando seus fluxos de mídia em um período específico. É possível dividir a duração da reprodução em diferentes granularidades, incluindo as novas granularidades de 5, 15 e 30 minutos. | Setembro de 2021 |

## 2020

| Recurso | Descrição | Data |
| --- | --- | --- |
| **Painel Visualizador simultâneo de mídia** | O [Painel de visualizadores simultâneos](https://experienceleague.adobe.com/en/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers) ajuda você a entender onde ocorreu o pico de simultaneidade ou onde as quedas ocorreram. Obtenha insights importantes sobre a qualidade do conteúdo e o engajamento do visualizador, além de ajuda na solução de problemas ou no planejamento de volume e escala.<br><br>[Painel Visualizadores Simultâneos de Mídia (tutorial)](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | Setembro de 2020; janeiro de 2021 |
| **Dispositivos e plataformas compatíveis** | A Extensão Media Launch com SDK AEP agora é compatível com os seguintes dispositivos OTT: <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | Junho de 2020 |
