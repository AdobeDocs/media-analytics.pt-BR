---
title: Controlar a ordem dos eventos
description: Controlar a ordem dos eventos
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# Controlar a ordem dos eventos {#controlling-the-order-of-events}

Como a API Media Collection é RESTful, e o rastreamento de vídeo é uma operação altamente dependente do tempo, um implementador pode se preocupar com chamadas de rastreamento da API Media Collection que chegam no back-end fora de serviço. O back-end *tenta* enfileirar e reordenar os eventos com base no carimbo de data e hora fornecido no objeto `playerTime`. No entanto, há um limite para esta capacidade. No momento, a reorganização poderá falhar se os atrasos entre as chamadas fora de ordem forem maiores do que um segundo. Esse &quot;tempo de atraso aceitável&quot; pode ser otimizado e/ou ser configurável em atualizações futuras.
