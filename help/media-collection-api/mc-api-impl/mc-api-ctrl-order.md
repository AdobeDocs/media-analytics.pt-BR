---
title: Controlar a ordem dos eventos
description: Controlar a ordem dos eventos
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: e0da35f364dc057a241fbb05a718a731ffee1e94
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%

---

# Controlar a ordem dos eventos {#controlling-the-order-of-events}

O rastreamento de vídeo de transmissão é uma operação altamente dependente do tempo e, ocasionalmente, as chamadas de rastreamento da API Media Collection chegam ao back-end fora de ordem. Nessa situação, o back-end tenta enfileirar e reordenar os eventos com base no carimbo de data e hora fornecido no objeto `playerTime`.  Isso ocorre com alguns limites. No momento, a reorganização pode falhar se os atrasos entre chamadas fora de ordem forem maiores que um segundo. Em atualizações futuras, o &quot;tempo de atraso aceitável&quot; pode ser otimizado e configurável.

## Exemplo de evento fora de ordem
Eventos fora de ordem ocorrem quando eventos passam pela rede, o que às vezes causa um atraso.

Por exemplo, você pode enviar um evento `adBreakStart` seguido por um evento `adStart`. Este é um caso de uso comum, pois é necessário que um anúncio comece dentro de um ad break.

Se o anúncio estiver pronto e nenhum buffer for necessário, ambos os eventos ocorrerão quase instantaneamente e o `playerTime.ts` para ambos os eventos estarão muito próximos um do outro, mas nunca deverão ser iguais.

> &quot;playerTime.ts&quot; de eventos nunca deve ser igual para nenhum evento, pois o algoritmo de classificação não saberia o que o evento aconteceu primeiro. Deve haver pelo menos 1 milissegundo de diferença de carimbo de data e hora para cada 2 eventos consecutivos.

Como ambos os eventos ocorrem muito próximos um do outro a tempo ao disparar chamadas de rede, é possível que eles cheguem fora de ordem. Neste exemplo, o evento `adStart` chega antes do evento `adBreakStart` .


Há uma janela cronometrada de eventos: 5 segundos ou no máximo 10 eventos. Os eventos são armazenados em buffer antes de enviá-los para o pipeline de processamento. Quando as condições são atendidas—5 segundos se passaram ou mais de 10 eventos são recebidos, os eventos são reordenados com base no `playerTime.ts` e depois enviados no novo pedido para o pipeline de processamento.

>[!IMPORTANT]
>
>Há um evento de exceção que é enviado imediatamente para o pipeline de processamento, que é o evento `sessionStart` .
