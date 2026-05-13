---
title: Controlar a ordem dos eventos
description: Saiba mais sobre o controle da ordem dos eventos e como, em alguns casos, os eventos são reordenados com base no carimbo de data e hora fornecido no objeto playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 100%

---

# Controlar a ordem dos eventos{#controlling-the-order-of-events}

O rastreamento de vídeo de streaming é uma operação altamente dependente do tempo e, ocasionalmente, as chamadas de rastreamento da API de coleção de mídia chegam ao back-end fora de ordem. Nesses casos, o back-end tenta enfileirar e reordenar os eventos com base no carimbo de data e hora fornecido no objeto `playerTime`.  Isso ocorre com algumas limitações. No momento, a reorganização poderá falhar se os atrasos entre as chamadas fora de ordem forem maiores do que um segundo. Em atualizações futuras, o “tempo de atraso aceitável” poderá ser otimizado e configurado.

## Exemplo de evento fora de ordem

Eventos fora de ordem ocorrem quando estes passam pela rede, o que pode causar um atraso.

Por exemplo, você pode enviar um evento `adBreakStart`, seguido por um evento `adStart`. Este é um caso de uso comum, pois é necessário para que um anúncio seja iniciado dentro de um ad break.

Se o anúncio estiver pronto e nenhum buffer for necessário, ambos os eventos ocorrerão quase que instantaneamente e o `playerTime.ts` de ambos os eventos serão muito próximos, mas nunca deverão ser iguais.

> O “playerTime.ts” dos eventos nunca deve ser igual para nenhum evento, pois o algoritmo de classificação não saberia que evento aconteceu primeiro. Deve haver pelo menos 1 milissegundo de diferença no carimbo de data e hora para cada 2 eventos consecutivos.

Como ambos os eventos ocorrem muito próximos um do outro quando as chamadas de rede são acionadas, é possível que eles cheguem fora de ordem. Neste exemplo, o evento `adStart` chega antes do evento `adBreakStart`.


Há uma janela cronometrada de eventos: 5 segundos ou um máximo de 10 eventos. Os eventos são armazenados em buffer antes de serem enviados para o pipeline de processamento. Quando as condições são cumpridas, 5 segundos se passam ou mais de 10 eventos são recebidos, os eventos são reordenados com base no `playerTime.ts` e, em seguida, são enviados para o pipeline de processamento na nova ordem.

>[!IMPORTANT]
>
>O evento `sessionStart` é uma exceção, pois ele é enviado para o pipeline de processamento imediatamente.
