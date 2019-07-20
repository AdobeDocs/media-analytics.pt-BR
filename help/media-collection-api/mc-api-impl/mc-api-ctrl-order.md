---
seo-title: Controlar a ordem dos eventos
title: Controlar a ordem dos eventos
uuid: 007 fccc 6-be 72-4 b 79-826 d -588 c 957 ccf 15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Controlar a ordem dos eventos{#controlling-the-order-of-events}

Como a API de coleta de mídia é restabeso, e o rastreamento de vídeo é uma operação altamente dependente de tempo, um implementador pode ser preocupado com as chamadas de rastreamento de API da coleta de mídia chegando ao fim de fora de ordem. O back-end *tenta* enfileirar e reordenar os eventos com base no carimbo de data e hora fornecido no objeto `playerTime`. No entanto, há um limite para esta capacidade. No momento, a reorganização poderá falhar se os atrasos entre as chamadas fora de ordem forem maiores do que um segundo. Esse "tempo de atraso aceitável" pode ser otimizado e/ou ser configurável em atualizações futuras.
