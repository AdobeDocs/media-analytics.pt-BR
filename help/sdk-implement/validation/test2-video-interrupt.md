---
seo-title: Interrupção do vídeo Test 2
title: Interrupção do vídeo Test 2
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Teste 2: interrupção do vídeo{#test-video-interruption}

Esse caso de teste é necessário como parte do formulário de solicitação de certificação e valida o comportamento de interrupção móvel.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

Você deve concluir e registrar essas tarefas na seguinte ordem:

1. **Iniciar o reprodutor de vídeo**

   Quando o reprodutor de vídeo é iniciado, as seguintes chamadas são enviadas na seguinte ordem:

   1. Início do Media Analytics
   1. Início do heartbeat
   1. Início do Heartbeat Analytics
   As primeiras duas chamadas acima contêm metadados e variáveis adicionais. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Reproduzir o vídeo do conteúdo principal por, pelo menos, 5 minutos sem interrupções**

   **Reprodução de conteúdo**

   Durante a reprodução regular do conteúdo principal, as chamadas do Heartbeat são enviadas ao servidor Heartbeat a cada dez segundos.

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Mover o aplicativo ou o navegador para o segundo plano**

   Enquanto o aplicativo é executado em segundo plano, somente as chamadas main:pause devem ser enviadas para o servidor de Heartbeat, a partir da versão 1.6.6 do VHL.

1. **Colocar o aplicativo ou o navegador em segundo plano**

   Ao voltar para o primeiro plano, a reprodução do conteúdo deve ser retomada.

1. **Reproduzir o vídeo do conteúdo principal por, pelo menos, 5 minutos sem interrupções**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **Fechar o reprodutor de vídeo**

   Nenhuma chamada de rastreamento adicional deve ser acionada após o fechamento do reprodutor de vídeo.

