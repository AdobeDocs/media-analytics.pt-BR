---
title: Controlar a ordem dos eventos
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Controlar a ordem dos eventos {#controlling-the-order-of-events}

Como a API Media Collection é RESTful, e o rastreamento de vídeo é uma operação altamente dependente do tempo, um implementador pode se preocupar com chamadas de rastreamento da API Media Collection que chegam no back-end fora de serviço. O back-end *tenta* enfileirar e reordenar os eventos com base no carimbo de data e hora fornecido no objeto `playerTime`. No entanto, há um limite para esta capacidade. No momento, a reorganização poderá falhar se os atrasos entre as chamadas fora de ordem forem maiores do que um segundo. Esse "tempo de atraso aceitável" pode ser otimizado e/ou ser configurável em atualizações futuras.
