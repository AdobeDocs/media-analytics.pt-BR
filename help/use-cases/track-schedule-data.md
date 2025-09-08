---
title: Carregar dados de agendamento para rastrear conteúdo ao vivo
description: Saiba como fazer upload dos dados de agendamento para rastrear o conteúdo ao vivo.
feature: Streaming Media
role: User, Admin, Data Engineer
hide: true
hidefromtoc: true
source-git-commit: e38a83853e85418611e17015b661d8592a7c95a1
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 2%

---

# Carregar dados de agendamento para rastrear conteúdo ao vivo

Você pode fazer upload dos dados de programação do conteúdo de streaming de mídia ao vivo anterior para rastrear a visualização do conteúdo ao vivo com mais facilidade e precisão. Você pode rastrear a audiência de programas individuais e até mesmo de tópicos ou segmentos de programas específicos.

Veja a seguir alguns exemplos de conteúdo ao vivo que são compatíveis com o upload de dados de programação:

* Plataformas FAST (TV com suporte a anúncios gratuitos)

* Transmissões locais

* Esportes ao vivo

* Notícias ou programação temática

## Recursos

Vários recursos estão disponíveis ao usar uploads de dados programados de conteúdo de mídia de transmissão ao vivo anteriores. Esta seção descreve alguns dos principais recursos que ajudam a analisar o desempenho do programa.

Esses recursos estão disponíveis independentemente de como você implementou a coleta de mídias de transmissão.

* **Rastrear com precisão as agendas de programa**: identifique as horas de início e término de cada programa individual no stream ao vivo para o período que deseja analisar. Com horas de início e término precisas, o tempo de execução preciso é refletido com precisão e pode ser analisado em relação a cada sessão do visualizador.

  Por exemplo, horários precisos de início e término nem sempre são conhecidos para um evento esportivo ao vivo até que o evento termine. Os uploads de dados agendados permitem obter relatórios precisos, atualizando os horários de início e término após a conclusão do programa.

* **Rastrear tópicos individuais ou segmentos de programa**: crie novas dimensões baseadas em tempo para tópicos ou segmentos de programa específicos (intervalos de tempo) em um determinado programa. Essas dimensões baseadas em tempo permitem analisar a visibilidade de um programa em um nível mais específico, ajudando a coletar insights sobre quais tópicos ou segmentos de programa tiveram melhor repercussão.

  Por exemplo, ao analisar um evento esportivo ao vivo, como uma partida de futebol, você pode criar dimensões separadas para o primeiro semestre, meio período e segundo semestre. O rastreamento de tópicos ou segmentos específicos em um programa permite detalhamentos mais detalhados do comportamento do visualizador.

* **Criar jornadas de usuário no Journey Optimizer**: controle quais programas uma pessoa visualizou em determinada sessão (ou até mesmo quais tópicos ou segmentos de programa a pessoa visualizou) e use esses dados no Adobe Journey Optimizer para criar jornadas de usuário para clientes que assistiram a determinado programa ou que demonstraram interesse em um tópico específico.

## Entenda como os dados de programação funcionam para mídia de streaming

A funcionalidade de agendamento de dados para mídia de streaming funciona da seguinte maneira:

1. Lê do conjunto de dados do programa de agendamento para registros do programa de agendamento, filtrando pela data do agendamento.

   Funciona somente para programas que ocorreram de 24 a 48 horas no passado.

2. Lê os eventos de fechamento de mídia no conjunto de dados de mídia, filtrando por data e pelo caminho XDM nos registros do programa de agendamento.

3. Para cada evento de fechamento de mídia, o mesmo número de eventos de início de agendamento de mídia é gerado, pois há exibições sobrepostas à sessão de mídia.

   Cada evento de início de agendamento de mídia contém o nome e a duração do agendamento.

   Além disso, uma nova métrica de tempo chamada **scheduleTimePlayed** contém o número de segundos que a sessão de mídia se sobrepôs ao programa agendado. O carimbo de data e hora do evento de agendamento de início é o carimbo de data e hora de quando o programa foi iniciado.

4. Grava os novos eventos de início de agendamento no conjunto de dados de mídia do AEP.

## Pré-requisitos

Para fazer upload dos dados do agendamento de conteúdo antigo em tempo real, o ambiente de mídia de streaming deve atender aos seguintes pré-requisitos:

* A Coleção de Mídia de Streaming deve estar habilitada para rastreamento no conteúdo para o qual você deseja carregar dados de agendamento, conforme descrito em [Visão geral do rastreamento](/help/use-cases/track-av-playback/track-core-overview.md). <!--specifics??? -->

* Use a coleção de mídia de transmissão com o Customer Journey Analytics. A capacidade de carregar dados de agendamento não está disponível com o Adobe Analytics.

## Criar um conjunto de dados de agendamento de programa no AEP

Antes de enviar informações de agendamento, você deve criar um conjunto de dados de agendamento de programa no Experience Platform:

1. Crie um esquema com base na **classe XDM do Programa Agendado do Media Analytics**.

   ![Esquema do programa de agendamento do Media Analytics](assets/media_schedule_finish_schema_creation.png)

   Esta é a definição XDM da classe de programa Agendado do Media Analytics.

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. Crie um conjunto de dados com base no esquema criado.

1. Continue com a seguinte seção, [Informações de agendamento de push](#push-schedule-information).

## Informações da programação de push

Depois de [Criar um conjunto de dados de agendamento de programa](#create-a-program-schedule-dataset-in-aep), você poderá enviar informações de agendamento:

1. Crie um arquivo .json com as informações de agendamento.

   O arquivo .json deve conter uma matriz de objetos Programar programa, de acordo com o esquema XDM.

1. Faça upload do arquivo .json:

   >[!NOTE]
   >
   >Os exemplos de cURL nesta seção usam as seguintes variáveis:
   >
   >* Para autenticação com o Adobe Developer:
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* id da organização: CUSTOMER_ORG_ID
   >* ID do conjunto de dados do registro criado na configuração: DATASET_ID
   >* id do lote criado na primeira solicitação usada no upload do arquivo: BATCH_ID
   >* O nome do arquivo usado para enviar registros: FILE_NAME

   1. Crie um novo lote e obtenha a ID do lote da resposta.

      Considere o exemplo a seguir de uso de cURL para criar um novo Lote do AEP:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. Envie o arquivo .json que contém os registros de dados de agendamento de programa usando a ID do lote.

      Para enviar informações de agendamento por push você deve usar APIs em lote do AEP, conforme descrito na [Visão geral da API de assimilação em lote](https://experienceleague.adobe.com/pt-br/docs/experience-platform/ingestion/batch/overview).

      Considere o exemplo a seguir de uso de cURL para enviar um arquivo com os registros de agendamento:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. Conclua o lote.

      Considere o exemplo a seguir de uso de cURL para concluir o lote:

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. Continue com a seguinte seção, [Registre um tíquete de suporte no Atendimento ao cliente da Adobe](#log-a-support-ticket-with-adobe-customer-care).

## Registre um tíquete de suporte no Atendimento ao cliente da Adobe

Registre um tíquete de suporte no Atendimento ao cliente da Adobe com as seguintes informações:

* **Conjunto de dados de mídia**: especifique a ID do conjunto de dados do qual os dados das sessões de mídia são lidos.

* **Conjunto de dados de agendamento**: especifique a ID do conjunto de dados para o qual os registros de agendamento são enviados.

* **Conjunto de dados de mídia de saída**: especifique a ID do conjunto de dados no qual os eventos de início de agendamento são salvos.

  Essa ID do conjunto de dados pode ser a mesma ID do conjunto de dados usada para o conjunto de dados Mídia. Se for uma ID de conjunto de dados diferente, ela ainda deverá ter o mesmo esquema XDM que o conjunto de dados do Media.

* **ID da organização**: especifique a ID da organização.

## Exemplo de um arquivo .json de agendamento com dois registros

O exemplo a seguir é de um arquivo .json de agendamento com dois registros. Cada arquivo .json deve conter todos os programas agendados para um dia.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### Entender os campos de programa de agendamento no exemplo

1. **mediaProgramDetails**: deve conter as informações mínimas necessárias para criar o evento de início de agendamento:
   * **startTimestamp**: a hora em que o programa foi iniciado.
   * **nome**: o nome amigável do programa.
   * **duração**: o número de segundos que o programa durou.

     >[!IMPORTANT]
     >
     >Se você tiver várias solicitações de dados de agendamento, elas não poderão ter horas de início e término sobrepostas.

1. **scheduleDate**: A data em que o programa foi exibido. O formato deve ser AAAA-MM-DD. É usado para filtrar o conjunto de dados de agendamento e obter todos os agendamentos para os quais a adobe cria agendamentos iniciados.
1. **scheduleFilter**: usado para filtrar todos os eventos de fechamento de sessão de mídia.
   * **filterPath**: um caminho XDM para o campo usado para filtragem.
   * **filterValue**: o valor usado para filtragem.
1. **customMetadata**: os metadados personalizados que você deseja adicionar aos eventos de início de agendamento. Esses metadados são usados para substituir os metadados personalizados presentes nos eventos de fechamento da sessão.
1. **defaultMetadata**: uma lista específica de dimensões que podem adicionar ou substituir os metadados padrão presentes nas chamadas de fechamento de mídia.

   Considere os seguintes exemplos de dimensões que você pode criar e criar relatórios no Customer Journey Analytics:

   * **[&quot;_Nome do episódio_&quot;](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**: essa dimensão pode ajudá-lo a saber quais episódios de uma determinada série têm melhor desempenho.

   * **[ID do ativo](https://experienceleague.adobe.com/pt-br/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. Continuar com [Analisar dados no Customer Journey Analytics](#analyze-data-in-customer-journey-analytics).

## Analisar dados no Customer Journey Analytics

Dentro de um dia após o upload do seu arquivo de dados, conforme descrito em [Solicitar e carregar o arquivo de dados de agendamento](#request-and-upload-the-schedule-data-file), seus dados estarão prontos para serem relatados no Customer Journey Analytics.

Para relatar seus dados de streaming de mídia ao vivo anteriores no Customer Journey Analytics:

1. Crie um novo projeto ou abra um projeto existente.

1. Crie o projeto criando as tabelas ou as visualizações necessárias para analisar os dados anteriores de mídia de transmissão ao vivo.

   Ao criar o projeto, use as informações incluídas no arquivo de dados do cronograma e enviadas ao Atendimento ao cliente da Adobe. Isso inclui a chave correspondente, as dimensões e quaisquer metadados adicionais. Para obter mais informações, consulte [Solicitar e carregar o arquivo de dados de agendamento](#request-and-upload-the-schedule-data-file).




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->
