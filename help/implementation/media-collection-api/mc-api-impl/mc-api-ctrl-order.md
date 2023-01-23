---
title: Controlar a ordem dos eventos
description: Saiba mais sobre o controle da ordem dos eventos e como, em alguns casos, os eventos são reordenados com base no carimbo de data e hora fornecido no objeto playerTime.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '326'
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
