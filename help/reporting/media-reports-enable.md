---
title: Ativação de relatórios de mídia
description: Saiba mais sobre o conjunto de relatórios de mídia que coleta métricas de mídia.  Siga estas etapas para configurar relatórios de mídia antes do envio dos dados de mídia.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 945
ht-degree: 81%

---

# Ativação de relatórios de mídia{#media-reports-enablement}

Cada conjunto de relatórios que coleta métricas de mídia deve ser configurado antes do envio dos dados de mídia.

Os clientes avançados podem usar os painéis de mídia no Analysis Workspace somente após a habilitação do Media Core e do rastreamento para a [Qualidade da experiência](/help/use-cases/track-qos/track-qos-overview.md).

>[!TIP]
>
>Para aproveitar os novos recursos, os clientes de mídia de transmissão existentes devem reativar o rastreamento de mídia para suas RSIDs.

1. Em [Reports &amp; Analytics](https://my.omniture.com/login/), clique em **[!UICONTROL Admin > Conjuntos de relatórios].**
1. Selecione o(s) conjunto(s) de relatórios no(s) qual(is) você está coletando dados de mídia e clique em **[!UICONTROL Editar configurações > Gerenciamento de mídia > Relatórios de mídia].**

   ![](assets/media-reporting.png)

1. Na página **[!UICONTROL Relatórios de mídia]**, ative **[!UICONTROL Mídia principal]** e, como opção, **[!UICONTROL Anúncios de mídia],** **[!UICONTROL Capítulos de mídia],** e **[!UICONTROL Qualidade de mídia].**

   A avaliação de mídia inclui os seguintes módulos:

   * **Mídia principal**

     A medição de mídia principal é usada para conteúdo de mídia. Essa avaliação usará eVars de solução (ou personalizadas) para rastrear conteúdo, tipo de conteúdo, nome do reprodutor de conteúdo e canal de conteúdo. Os eventos de solução (ou personalizados) serão utilizados para Inícios de mídia, Inícios de conteúdo, Conclusões de conteúdo e Tempo gasto no conteúdo.

   * **Anúncios da mídia**

     As avaliações dos anúncios de mídia são utilizadas para avaliar os anúncios no conteúdo de mídia. Essa avaliação usará eVars de solução para medir Anúncio, Nome do player do anúncio, Pod de anúncio e Anúncio na posição do pod. Os eventos de solução serão usados para Inícios de anúncio, Conclusões de anúncio, Tempo gasto no anúncio e Tempo gasto no vídeo.

   * **Capítulos da mídia**

     A medição de capítulos de vídeo é utilizada para medir os capítulos. Um capítulo é uma subdivisão do conteúdo em uma única mídia. O capítulo usará uma eVar de solução para armazenar a ID do capítulo. Os eventos de solução serão usados para Inícios de capítulo, Conclusões de capítulo e Tempo gasto no capítulo. Metadados de capítulo adicionais de Nome do capítulo e Posição do capítulo serão fornecidos como classificações da ID do capítulo.

   * **Qualidade da mídia**

     A avaliação da qualidade do vídeo é utilizada para avaliar a qualidade da reprodução do conteúdo. Essa avaliação usará eVars de solução para armazenar Hora de início, Eventos de buffer, Duração total do buffer, Switches de taxa de bits, Taxa média de bits, Erros e Quadros descartados. Eventos de solução serão usados para Hora de início, Solta antes de iniciar, Fluxos impactados pelo buffer, Eventos do buffer, Duração total do buffer, A alteração na taxa de bits impactou os fluxos, Alterações na taxa de bits, Média da taxa de bits, Fluxos impactados por erros, Eventos de erro, O quadro solto impactou os fluxos e Quadros soltos.

   * **Metadados de vídeo e anúncio de vídeo**

     Os metadados podem ser inseridos em uma mídia e/ou em um anúncio para descrever e classificar ainda mais a mídia ou anúncio. Os metadados de mídia e anúncios padrão serão coletados pelas variáveis e classificações da solução. Os valores para incluir: Programa, Temporada, Episódio, ID do ativo, Gênero, Data da primeira exibição, Data da primeira versão digital, Classificação do conteúdo, Originador, Rede, Tipo de programa, Carregamentos de anúncios, MVPD, Autorizado, Parte do dia, ID de sessão de mídia, Anunciante, ID da campanha e ID de criação.

   * **Metadados de áudio e de anúncio de áudio**

     Os metadados podem ser anexados a um áudio e/ou anúncio para descrever e categorizar ainda mais esse áudio/anúncio. Os metadados de áudio e anúncios padrão serão coletados pelas variáveis e classificações da solução. Os valores para incluir: Artista, Álbum, Gravadora, Autor, Editor, Estação, Programa, Temporada, Episódio, ID do ativo, Gênero, Data da primeira exibição, Data da primeira exibição digital, Classificação do conteúdo, Originador, Tipo de programa, Carregamentos de anúncio, Parte do dia, ID de sessão de mídia, Anunciante, ID da campanha e ID do Creative.

   A habilitação de cada módulo reserva um conjunto de variáveis e cria um novo conjunto de relatórios. Com exceção da Qualidade, não haverá dados nos relatórios, a menos que a implementação correspondente tenha sido concluída. A implementação do módulo Principal também implementa o módulo Qualidade se você habilitá-lo.

   Se você ainda não estiver rastreando anúncios, capítulos ou qualidade de reprodução, será possível habilitar opções adicionais a qualquer momento.

1. Clique em **[!UICONTROL Salvar].**

   Se esse conjunto de relatórios já estiver configurado para coletar dados de mídia, uma página de configuração adicional será exibida depois de clicar em **[!UICONTROL Salvar]**. Se você visualizar a página **[!UICONTROL Avaliação da mídia principal]**, continue para a próxima etapa.

1. (Condicional) Na página **[!UICONTROL Avaliação de mídia principal]**, selecione a opção para continuar a utilizar as variáveis personalizadas ou use variáveis da solução.

   | Opção | Notas |
   | --- | --- |
   | Continue a utilizar as variáveis personalizadas | Vantagens e desvantagens:<ul> <li> **Vantagens:** as tendências de conteúdo continuam a funcionar após a migração. </li> <li> **Desvantagens:** exige que você mantenha duas eVars personalizadas e três eventos personalizados alocados para mídia. Você pode usar novamente uma eVar personalizada e um evento personalizado. </li> </ul> Para continuar usando variáveis personalizadas: <ol> <li>Selecione **[!UICONTROL Usar variáveis personalizadas,]** e clique em **[!UICONTROL Salvar.]** </li> <li>Quando solicitado, mapeie as eVars e os eventos personalizados atuais e, em seguida, clique em **[!UICONTROL Salvar:]** </li> </ol> |
   | Migre para variáveis de solução | Vantagens e desvantagens:<ul> <li> **Vantagens:** você pode usar novamente três eVars personalizadas e quatro eventos personalizados. </li> <li> **Desvantagens:** você perde **todas** as tendências e comparações de histórico dos relatórios de mídia. Isso significa que não é possível direcionar visualizações de conteúdo ou o tempo de reprodução de conteúdo para qualquer data antes de migrar para as pulsações. </li> </ul> **Restrição:** não migre para as variáveis da solução, a menos que tenha certeza de que não deseja manter essas tendências. Todos os clientes devem utilizar as variáveis da solução e as regras de processamento para inserir os dados de mídia nas props e eVars existentes, somente se for necessário preservar a continuidade do histórico. Para migrar para variáveis de solução: Selecione **[!UICONTROL Usar Variáveis de Solução]** e clique em **[!UICONTROL Salvar].** <br><br> IMPORTANTE: a migração para variáveis de solução provoca a perda de **todas** as tendências e comparações de histórico dos relatórios de mídia. |

>[!IMPORTANT]
>
>Não altere os nomes de classificação de nenhuma variável listada na documentação da variável de mídia de streaming (vinculada da [Visão geral dos serviços de mídia de streaming](/help/media-overview.md)) que estão descritos em Relatório/Variável reservada como &quot;classificação&quot;. As classificações de mídia são definidas quando um conjunto de relatórios é habilitado para rastreamento de mídia. Periodicamente, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reabilitar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são habilitadas verificando os nomes das variáveis. Se algum deles estiver faltando, a Adobe os adicionará novamente.
