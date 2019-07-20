---
seo-title: Ativação de relatórios de mídia
title: Ativação de relatórios de mídia
uuid: d 306068 d-a 308-4 b 6 e -8 a 72-742 dda 0 de 428
translation-type: tm+mt
source-git-commit: 3fed0736b673d024b7a4b07d8324bfc62f747ed7

---


# Ativação de relatórios de mídia{#media-reports-enablement}

Cada conjunto de relatórios que coleta métricas de mídia deve ser configurado antes que os dados de mídia sejam enviados.

>[!TIP]
>
>Para aproveitar os novos recursos, os clientes existentes do Media Analytics devem habilitar novamente o rastreamento de mídia para rsids.

1. In [Reports &amp; Analytics](https://my.omniture.com/login/) click [!UICONTROL Admin] &gt; [!UICONTROL Report Suites].
1. Select the report suite(s) where you are collecting media data and click [!UICONTROL Edit Settings] &gt; [!UICONTROL Media Management] &gt; [!UICONTROL Media Reporting].
   ![](assets/media-reporting.png){width = "400 px"}

1. On the **[!UICONTROL Media Reporting]** page, enable **[!UICONTROL Media Core]**, and optionally enable **[!UICONTROL Media Ads]**, **[!UICONTROL Media Chapters]**, and **[!UICONTROL Media Quality]**.

   A avaliação de mídia inclui os seguintes módulos:

   * **Mídia principal:**

      A medição de mídia principal é usada para conteúdo de mídia. Isso utiliza evars de solução (ou personalizadas) para acompanhar Conteúdo, Tipo de conteúdo, Nome do player de conteúdo e Canal de conteúdo. Os eventos de solução (ou personalizados) serão usados para Inícios de mídia, Inícios de conteúdo, Conclusões de conteúdo e Tempo gasto no conteúdo.

   * **Anúncios de mídia:** A medição de anúncio de mídia é usada para medir anúncios dentro do conteúdo de mídia. Esse recurso utiliza as eVars de solução para avaliar Anúncios, Nome do reprodutor do anúncio, Pod de anúncios e Posição do anúncio no pod. Os eventos de solução serão utilizados para Inícios de anúncio, Conclusões de anúncio, Tempo gasto no anúncio e Tempo de vídeo gasto.
   * **Capítulos da mídia:**

      A avaliação de capítulos de vídeo é usada para medir os capítulos. Um capítulo é uma subdivisão do conteúdo em uma única mídia. Esse recurso utiliza a eVar de solução para armazenar a ID do capítulo. Os eventos de solução serão utilizados para Inícios de capítulo, Conclusões de capítulo e Tempo gasto com capítulo. Metadados adicionais de capítulo do Nome de capítulo e Posição do capítulo serão fornecidos como classificações da ID do capítulo.

   * **Qualidade da mídia:**

      A avaliação de qualidade do vídeo é usada para medir a qualidade da reprodução do conteúdo. Esse recurso utiliza eVars de solução para armazenar Hora de início, Eventos de buffer, Duração total do buffer, Mudanças de taxas de bits, Taxa de bits média, Erros e Queda de quadros. Os eventos da solução serão utilizados para Hora de início, Solta antes de iniciar, Fluxos impactados pelo buffer, Eventos do buffer, Duração total do buffer, A alteração na taxa de bits impactou os fluxos, Alterações na taxa de bits, Média da taxa de bits, Fluxos impactados por erros, Eventos de erro, O quadro solto impactou os fluxos e Quadros soltos.

   * **Metadados de vídeo e anúncio de vídeo:**

      Os metadados podem ser anexados a uma mídia e/ou a um anúncio para descrever e categorizar ainda mais essa mídia/anúncio. Os metadados padronizados de mídia e publicidade serão coletados pelas variáveis e classificações da solução. Os valores para incluir: Programa, Temporada, Episódio, ID do ativo, Gênero, Data da primeira exibição, Data da primeira versão digital, Classificação do conteúdo, Originador, Rede, Tipo de programa, Carregamentos de anúncios, MVPD, Autorizado, Parte do dia, ID de sessão de mídia, Anunciante, ID da campanha e ID de criação.

   * **Metadados de áudio e de anúncio de áudio:**

      Os metadados podem ser anexados a um áudio e/ou anúncio para descreverem e categorizar o áudio e/ou anúncio. Os metadados padrão são coletados por meio das variáveis e classificações da solução. Os valores incluem: Artista, Álbum, Gravadora, Autor, Publicador, Estação de rádio, Programa, Temporada, Episódio, ID do ativo, Gênero, Data da primeira exibição, Data da primeira exibição virtual, Classificação do conteúdo, Originador, Tipo de programa, Parte do dia, ID da sessão de mídia, Anunciante, ID da campanha e ID Creative.
   A habilitação de cada módulo reserva um conjunto de variáveis e cria um novo conjunto de relatórios. Com exceção de Qualidade, não existem dados em relatórios exceto quando a implementação correspondente é concluída. Se habilitada, a implementação do módulo principal também implementa o módulo Qualidade.

   Se você ainda não estiver rastreando anúncios, capítulos ou a qualidade da reprodução, é possível ativar mais opções a qualquer momento.

1. Clique em **[!UICONTROL Salvar]**.

   If this report suite is already configured to collect media data, after you click **[!UICONTROL Save]**, an additional configuration page is displayed. Se você visualizar a página [!UICONTROL Avaliação da mídia principal], continue para a próxima etapa.

1. (Condicional) Na página [!UICONTROL Avaliação do vídeo principal], selecione a opção para continuar a utilizar as variáveis personalizadas ou use variáveis da solução.

   | Opção | Descrição |
   | --- | --- |
   | Continue a utilizar as variáveis personalizadas | <ul> <li> **Vantagens**: as tendências de conteúdo continuam a funcionar após a migração. </li> <li> **Cons:** Exige que você mantenha duas evars personalizadas e três eventos personalizados alocados à mídia. Você pode utilizar novamente uma eVar personalizada e um evento personalizado. </li> </ul> Para continuar a utilizar variáveis personalizadas: <ol> <li>Selecione Usar variáveis personalizadas e clique em Salvar. </li> <li>Quando solicitado, mapeie as eVars personalizadas e os eventos atuais e, em seguida, clique em Salvar: </li> </ol> |
   | Migre para variáveis de solução | <ul> <li> **Vantagens**: você pode utilizar novamente três eVars personalizadas e quatro eventos personalizados. </li> <li> **Desvantagens:** você perde **todas** as tendências e comparações de histórico dos relatórios de mídia. Isso significa que você não poderá observar as tendências de exibições ou tempo de reprodução do conteúdo para as datas antes de migrar para o Heartbeats. </li> </ul> **Restrição:** não migre para as variáveis da solução, a menos que tenha certeza de que não deseja manter essas tendências. Todos os clientes devem utilizar as variáveis da solução e as regras de processamento para inserir os dados de mídia nas props e eVars existentes, somente se for necessário preservar a continuidade do histórico. Para migrar para variáveis de solução: Selecione Usar variáveis de solução e clique em Salvar. |

   >[!IMPORTANT]
   >
   >Migrating to solution variables causes you to lose **all** historical trending and comparison for media reports.

>[!IMPORTANT]
>
>Do not change the classification names for any variables listed in the Metrics and metadata tables (e.g., [Audio and video parameters](../metrics-and-metadata/audio-video-parameters.md)) that are described there under Reporting/Reserved Variable as "classification". As classificações de mídia são definidas quando um conjunto de relatórios é habilitado para rastreamento de mídia. De vez em quando, a Adobe adiciona novas propriedades e, quando isso ocorre, os clientes devem reativar seus conjuntos de relatórios para obter acesso às novas propriedades de mídia. Durante o processo de atualização, a Adobe determina se as classificações são ativadas verificando os nomes das variáveis. Se algum deles estiver ausente, a Adobe adicionará as ausentes novamente.
