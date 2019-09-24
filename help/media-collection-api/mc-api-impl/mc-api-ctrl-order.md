---
seo-title: Controlar a ordem dos eventos
title: Controlar a ordem dos eventos
uuid: 007fcc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Controlar a ordem dos eventos{#controlling-the-order-of-events}

Como a API Media Collection é RESTful e o rastreamento de vídeo é uma operação altamente dependente de tempo, um implementador pode estar preocupado com as chamadas de rastreamento da API Media Collection que chegam ao back-end fora de ordem. O back-end *tenta* enfileirar e reordenar os eventos com base no carimbo de data e hora fornecido no objeto `playerTime`. No entanto, há um limite para esta capacidade. No momento, a reorganização poderá falhar se os atrasos entre as chamadas fora de ordem forem maiores do que um segundo. Esse "tempo de atraso aceitável" pode ser otimizado e/ou ser configurável em atualizações futuras.
