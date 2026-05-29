---
title: Visão geral dos eventos de mídia de transmissão
description: Saiba mais sobre os tipos de evento de mídia e a ordem em que eles devem ser enviados.
feature: Streaming Media
role: Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# Eventos de mídia de transmissão

O rastreamento de streaming de mídia funciona enviando uma sequência de chamadas de evento para um endpoint de coleção de dados da Adobe, cada uma representando uma transição no estado do player. Todos os eventos pertencem a uma sessão ativa aberta por uma chamada [Início de sessão](session/session-start.md). As sessões são fechadas automaticamente até a expiração ou podem ser fechadas imediatamente com uma chamada [Session end](session/session-end.md).

Os eventos são agrupados em seis categorias (sessão, reprodução, anúncios, capítulos, estado do player e qualidade), cada uma cobrindo um aspecto distinto da experiência de mídia.

## Eventos de sessão

Os eventos de sessão se aplicam a qualquer tipo de rastreamento de mídia, incluindo: vídeo sob demanda, fluxos ao vivo, podcasts e audiobooks. Eles definem os limites da própria sessão de rastreamento. O evento de sessão mais importante é [Início da sessão](session/session-start.md), pois quase todos os outros tipos de evento dependem da ID de sessão gerada por ele. Enviá-lo como o primeiro evento quando um usuário inicia uma sessão, como quando ele pressiona Play ou quando o reprodutor começa a reprodução automática.

Quando uma sessão estiver aberta, use [Sessão concluída](session/session-complete.md) ou [Fim de sessão](session/session-end.md) para indicar como a experiência de exibição terminou. Enviar sessão concluída quando o visualizador atingir o fim natural do conteúdo — o vídeo é concluído, o episódio do podcast termina ou o capítulo final de um audiobook é concluído. Sessão concluída não fecha a sessão; ela permanece aberta até expirar naturalmente, portanto, quaisquer eventos finais, como um ping final, ainda são capturados.

Se o visualizador sair antes de atingir o fim, envie [Fim da sessão](session/session-end.md) para fechar a sessão imediatamente. Somente envie o fim da sessão quando nenhum evento adicional for seguido; por exemplo, quando o reprodutor for destruído ou a página for descarregada. O término da sessão é um encerramento permanente: uma vez enviada, a sessão é encerrada e nenhum outro evento pode ser rastreado nela. Na maioria dos casos, é mais seguro permitir que a sessão expire naturalmente. Os exemplos incluem a pausa indefinida do visualizador, o aplicativo em segundo plano ou a falha no carregamento do conteúdo.

Uma sessão expira automaticamente se nenhum evento for recebido por 10 minutos ou se nenhum movimento do indicador de reprodução for detectado por 30 minutos. Se qualquer uma das condições for atendida e o visualizador retornar ao conteúdo, você deverá chamar o Início da sessão novamente para abrir uma nova sessão antes de enviar mais eventos.

## Eventos de reprodução

Os eventos de reprodução rastreiam as transições de estado no reprodutor de mídia durante uma sessão. Eles formam o núcleo do fluxo de eventos e se aplicam a qualquer tipo de conteúdo.

O evento de reprodução principal é [Reproduzir](playback/play.md). Depois de chamar o início da sessão, a reprodução sinaliza que o conteúdo começou a ser reproduzido, seja o início, um acionador de reprodução automática ou qualquer retorno ao estado de reprodução. [Início da pausa](playback/pause-start.md) indica que o usuário pausou a reprodução. Não há evento de retomada dedicado; quando o visualizador for retomado, envie Reproduzir novamente. O Play funciona da mesma forma depois de uma paralisação de buffering — envie [Início do buffer](playback/buffer-start.md) quando o player parar de aguardar dados, depois siga com Play quando o buffering for resolvido.

Envie [Ping](playback/ping.md) a cada 10 segundos durante a reprodução do conteúdo principal e a cada 1 segundo durante a reprodução do anúncio. O ping mantém a sessão ativa e registra o movimento do indicador de reprodução. Nos SDKs móveis, os pings são enviados automaticamente; em todas as outras plataformas, eles devem ser enviados manualmente.

Enviar [Alteração na taxa de bits](playback/bitrate-change.md) sempre que o algoritmo de taxa de bits adaptável do player mudar para um nível de qualidade diferente. A inclusão do novo valor de taxa de bits nos dados de QoE habilita o relatório de taxa de bits média.

## Eventos de publicidade

Os eventos de publicidade rastreiam a publicidade em uma sessão de mídia. Cenários comuns incluem anúncios antes da exibição, anúncios no meio da exibição inseridos em intervalos durante um vídeo de longa duração ou transmissão ao vivo e anúncios após a exibição após o término do conteúdo. Um único ad break pode conter um ou vários anúncios individuais.

Cada ad break segue a mesma estrutura. [Ad break start](ads/ad-break-start.md) abre a interrupção e [Ad break complete](ads/ad-break-complete.md) a fecha. Esses dois eventos atuam como delimitadores que envolvem todos os eventos de anúncios individuais. Dentro do intervalo, envie [Início do anúncio](ads/ad-start.md) quando cada anúncio individual começar a ser reproduzido. Siga-o com [Anúncio concluído](ads/ad-complete.md) se o anúncio for reproduzido em sua duração total ou [Anúncio ignorado](ads/ad-skip.md) se o visualizador selecionar o botão Ignorar. A omissão de qualquer um dos delimitadores faz com que todos os eventos de anúncio no intervalo sejam ignorados e a duração do anúncio é atribuída incorretamente ao conteúdo principal.

O exemplo a seguir mostra a sequência de eventos correta para um único ad break contendo três anúncios, em que o visualizador ignorou o terceiro:

1. Início de ad break
2. Início do anúncio
3. Anúncio concluído
4. Início do anúncio
5. Anúncio concluído
6. Início do anúncio
7. Ignorar anúncio
8. Ad break concluído

## Eventos de capítulo

Os eventos de capítulo são opcionais e rastreiam segmentos de conteúdo nomeados em uma sessão. Eles são bem adequados para o conteúdo naturalmente dividido em partes distintas. Exemplos comuns incluem capítulos em um audiobook, atos em um documentário, lições em um curso de vídeo ou segmentos em um episódio de podcast. Use eventos de capítulo quando quiser entender o envolvimento do visualizador no nível do segmento, como identificar quais capítulos os públicos-alvo tendem a ignorar.

Enviar [Início do capítulo](chapters/chapter-start.md) quando um capítulo começar. Se o visualizador observar até o final do capítulo, envie [Capítulo concluído](chapters/chapter-complete.md). Se o visualizador ultrapassar o limite do capítulo sem observá-lo até a conclusão, envie [Capítulo ignorado](chapters/chapter-skip.md). Um capítulo deve ser fechado com Capítulo concluído ou Capítulo ignorado antes que um novo possa ser aberto; os capítulos não podem se sobrepor.

## Eventos de estado do player

Os eventos de estado do player rastreiam como os visualizadores interagem com os controles do player em toda a sessão. Eles são úteis para entender o uso de recursos de acessibilidade, como a frequência com que os visualizadores ativam as legendas ocultas ou a função mudo. Elas também revelam padrões de comportamento de visualização como tela cheia versus visualização em linha e multitarefa picture-in-picture.

Os cinco estados rastreáveis são: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` e `inFocus`. Enviar [Início do estado](player-state/state-start.md) quando o player entrar em qualquer um desses estados e [Fim do estado](player-state/state-end.md) quando ele sair. Vários estados podem estar ativos ao mesmo tempo; um visualizador pode estar em tela cheia e sem áudio simultaneamente, e vários estados podem ser encerrados na mesma chamada de evento.

## Eventos de erro

O evento [Erro](error.md) registra uma falha de reprodução durante uma sessão — uma solicitação de fluxo com falha, um erro de codec ou uma falha de entrega externa. Enviá-lo sempre que ocorrer um erro significativo. Um evento de erro não fecha a sessão; a reprodução pode continuar e os eventos subsequentes são rastreados na mesma sessão. Se o erro for irrecuperável, siga-o com Session end para fechar explicitamente a sessão.

>[!MORELIKETHIS]
>
>* [Visão geral das variáveis](/help/implementation/variables/overview.md): os dados que os eventos carregam para o Adobe
>* [Visão geral das dimensões](/help/reporting/dimensions/overview.md): as dimensões de relatório que os eventos preenchem
>* [Visão geral das métricas](/help/reporting/metrics/overview.md): as métricas de relatório que os eventos preenchem
