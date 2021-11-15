---
title: 'Obter dados de relatório JSON de tempo gasto com a reprodução de mídia com as APIs do Analytics 2.0 '
description: Saiba como obter dados de relatório de tempo gasto com a reprodução de mídia usando as APIs do Analytics 2.0. Visualize uma solicitação e uma resposta de exemplo.
uuid: null
exl-id: null
feature: Media Analytics, Reports & Analytics Basics
role: User, Admin, Data Engineer
source-git-commit: 3118a5eeef56c7768d88df7c658468c356921aac
workflow-type: ht
source-wordcount: '205'
ht-degree: 100%

---


# Obter dados de relatório JSON de tempo gasto com a reprodução de mídia com as APIs do Analytics 2.0 {#get-media-playback-time-spent-json-report-data}

É possível obter dados de relatório de tempo gasto com a reprodução de mídia usando as [_*APIs do Analytics 2.0*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html).

1. Filtre os dados usando qualquer segmento criado na interface do usuário. Para filtrar por uma ID de conteúdo específica, crie um novo segmento.
1. Defina os `elements` -> `id` no corpo da solicitação como `metrics/playback_time_spent_seconds` ou `metrics/playback_time_spent_minutes` dependendo se você deseja a saída em segundos ou minutos.
1. Solicite uma quantidade suficiente de dados.

   * O intervalo de dados especificado no relatório reúne todos os dados do visualizador simultâneo _no momento em que a sessão de vídeo terminar._
Você deve considerar as sessões que iniciam um dia e terminam após a meia-noite, ou seja, no dia seguinte.

   * Solicite mais um dia de dados para o período desejado em sua solicitação, mas na análise _*use apenas os dados planejados.*_

Uma carga de solicitação de amostra para um dia de dados seria semelhante à amostra a seguir. A solicitação é feita por 2 dias consecutivos, mas no relatório você só usa o primeiro dia.

## Exemplo de solicitação

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2021-09-02T00:00/2021-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/playback_time_spent_minutes"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## Exemplo de resposta

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2021-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2021-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2021-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2021-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the Media Playback Time Spent report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The Media Playback Time Spent report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
