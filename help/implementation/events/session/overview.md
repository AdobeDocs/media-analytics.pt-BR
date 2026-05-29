---
title: Rastrear a reprodução do conteúdo
description: Saiba mais sobre o rastreamento da reprodução principal, incluindo o rastreamento da carga de mídia, início da mídia, pausa da mídia e conclusão da mídia.
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# Rastrear a reprodução do conteúdo

O rastreamento de reprodução principal abrange carregamento de mídia, início, pausa, retomada, conclusão e fim de sessão. Embora não seja obrigatório, o rastreamento de buffering e busca também são componentes principais de uma implementação de reprodução completa.

## Eventos do player

| Evento do reprodutor | Ação |
| --- | --- |
| Carregamento de mídia | Criar objeto de mídia; chamar SessionStart |
| Início de mídia | Reprodução de chamada |
| Pausar | Chamar PauseStart |
| Retomar da pausa | Reprodução de chamada |
| Mídia concluída | Chamar SessionComplete |
| Media abort / unload | Chamar SessionEnd |
| Início do buffering | Chamar BufferStart |
| Buffering termina | Reprodução de chamada (retomar) |
| Início da busca | Chamar SeekStart |
| Busca de fins | Chame SeekComplete e, em seguida, chame Play |

## Etapas da implementação

1. **Identifique quando o usuário aciona a reprodução** (o usuário clica em Reproduzir ou a reprodução automática é acionada). Crie um objeto de mídia com nome do conteúdo, ID, comprimento, tipo de fluxo e tipo de mídia. Consulte [Nome do conteúdo](/help/implementation/variables/core/content-name.md), [ID do conteúdo](/help/implementation/variables/core/content-id.md), [Comprimento do conteúdo](/help/implementation/variables/core/content-length.md), [Tipo de fluxo](/help/implementation/variables/core/stream-type.md) e [Tipo de conteúdo](/help/implementation/variables/core/content-type.md) para obter as definições de campo.
1. **Opcionalmente, anexar metadados** — metadados padrão (programa, temporada, episódio etc.) e variáveis de dados de contexto personalizados. Consulte [Programa](/help/implementation/variables/standard-metadata/show.md), [Temporada](/help/implementation/variables/standard-metadata/season.md), [Episódio](/help/implementation/variables/standard-metadata/episode.md), [Gênero](/help/implementation/variables/standard-metadata/genre.md) e [Rede](/help/implementation/variables/standard-metadata/network.md) para obter referências de chave de metadados padrão.
1. **Chame [Início da sessão](/help/implementation/events/session/session-start.md)** para começar a rastrear a sessão. Isso carrega os dados e os metadados e inicia a medição de QoS do tempo para iniciar. SessionStart rastreia a *intenção* de reproduzir, não o primeiro quadro.
1. **Chame [Reproduzir](/help/implementation/events/playback/play.md)** quando o primeiro quadro do conteúdo for renderizado na tela.
1. **Chamar [Início da pausa](/help/implementation/events/playback/pause-start.md)** quando o player pausar. Chame Reproduzir novamente quando a reprodução for retomada. Não há evento de retomada separado.
1. **Chame [Sessão concluída](/help/implementation/events/session/session-complete.md)** quando o visualizador atingir o fim do conteúdo.
1. **Chame [Fim da sessão](/help/implementation/events/session/session-end.md)** quando o player for descarregado ou o visualizador abandonar o conteúdo sem atingir o fim. O SessionEnd fecha imediatamente a sessão; nenhum outro evento poderá ser rastreado depois dele.

>[!IMPORTANT]
>
>`SessionEnd` marca o fim de uma sessão de rastreamento. Se a sessão tiver sido assistida até o fim, chame `SessionComplete` antes de `SessionEnd`. Qualquer outra chamada de rastreamento será ignorada depois de `SessionEnd`, exceto por `SessionStart` para uma nova sessão.

## Reprodução principal

Os exemplos a seguir mostram um fluxo de sessão completo — do início à conclusão da sessão até a conclusão do conteúdo e o fim da sessão.

Para obter detalhes sobre a implementação por plataforma, consulte [Início da sessão](/help/implementation/events/session/session-start.md), [Reprodução](/help/implementation/events/playback/play.md), [Início da pausa](/help/implementation/events/playback/pause-start.md), [Conclusão da sessão](/help/implementation/events/session/session-complete.md) e [Término da sessão](/help/implementation/events/session/session-end.md).

## Buffering

O início do buffer indica que o reprodutor está aguardando dados. O fim do buffer é inferido quando você envia um evento Play após BufferStart (APIs baseadas em XDM). No Mobile SDK, chame também BufferComplete explicitamente.

Para obter detalhes sobre a implementação, consulte [Início do buffer](/help/implementation/events/playback/buffer-start.md).

## Busca

O início da busca indica que o visualizador está depurando. O fim da busca é seguido por Reproduzir para retomar a reprodução do conteúdo.

Para obter detalhes sobre a implementação, consulte [Início da pausa](/help/implementation/events/playback/pause-start.md) (início da busca) e [Reprodução](/help/implementation/events/playback/play.md) (fim da busca).

## Manipulação de interrupções de aplicativos

A reprodução em um aplicativo de mídia pode ser interrompida de várias maneiras: o usuário pressiona pausar, o aplicativo vai para o segundo plano e é recebida uma chamada telefônica. Independentemente da causa, as instruções de rastreamento são as mesmas:

1. Chame **PauseStart** quando o aplicativo for interrompido (entra em segundo plano, mídia pausada, etc.).
1. Chame **Reproduzir** quando o aplicativo retornar para o primeiro plano e/ou quando a reprodução da mídia for retomada.

>[!NOTE]
>
>Não chame SessionStart quando o aplicativo retornar do segundo plano. Chamar SessionStart faz com que a reprodução até esse ponto não seja contabilizada no tempo total de reprodução e os marcadores de progresso, segmentos e limites de capítulo anteriores são perdidos.

**Quando uma sessão pausada deve terminar?** Se o aplicativo não permitir reprodução em segundo plano, chame PauseStart imediatamente e SessionEnd após aproximadamente um minuto em segundo plano. O aplicativo não pode continuar enviando pings de pausa em segundo plano, e manter a sessão aberta indefinidamente fornece uma experiência ruim. Se o aplicativo oferecer suporte à reprodução em segundo plano (aplicativos de áudio, podcast de vídeo), continue enviando pings enquanto estiver em segundo plano.

**Reiniciando após um longo período em segundo plano:** Se o aplicativo tiver sido colocado em segundo plano por tempo suficiente para que a sessão expirasse (inatividade de 30 minutos), chame SessionEnd para fechar qualquer sessão remanescente de maneira limpa e, em seguida, chame SessionStart para iniciar uma nova sessão quando o visualizador retornar.

## Resumo de sessões inativas

Uma sessão expira automaticamente se nenhum evento for recebido por 10 minutos ou se não houver movimento do indicador de reprodução por 30 minutos. Se o usuário retornar depois que uma sessão expirar, chame SessionStart novamente para abrir uma nova sessão.

**Retomando entre dispositivos (entrega entre dispositivos):** Quando um visualizador transfere a reprodução entre dispositivos (por exemplo, convertendo de um telefone para uma TV), use o sinalizador de retomada para unir as sessões nos relatórios do Analytics:

1. No **dispositivo de origem**, chame SessionEnd quando o visualizador iniciar a conversão. Não chame SessionComplete — o conteúdo não é concluído.
1. No **dispositivo de destino**, chame SessionStart com o sinalizador de retomada definido como `true` e passe os mesmos metadados de conteúdo e a posição do indicador de reprodução do dispositivo de origem.

Definir o sinalizador de retomada faz com que o Analytics incremente [retomas de conteúdo](/help/reporting/metrics/content-resumes.md) em vez de [inícios da mídia](/help/reporting/metrics/media-starts.md) para o segundo trecho da entrega.

**Retomando manualmente uma sessão fechada anteriormente:** Se o aplicativo armazenar dados do usuário e puder retomar uma sessão fechada anteriormente, defina o sinalizador de retomada no início da sessão. Consulte [Início da sessão](/help/implementation/events/session/session-start.md#resuming-a-session) para obter detalhes sobre a implementação em todas as plataformas.
