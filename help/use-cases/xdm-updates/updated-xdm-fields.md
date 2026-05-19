---
title: Atualizar uma implementação do conector de origem do Analytics para novos campos XDM para serviços de mídia de transmissão
description: Saiba mais sobre como migrar uma implementação do conector de origem do Analytics para campos atualizados de mídia de transmissão XDM
feature: Streaming Media
role: User, Admin, Developer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
TQID: https://experienceleague.adobe.com/cEIBTufYRaIusKjm-CszVvsFmZNfMS-RAvOm3wbbBgc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 886
ht-degree: 1%

---

# Atualizar uma implementação do conector de origem do Analytics para novos campos XDM para serviços de mídia de transmissão

>[!NOTE]
>
>Estas informações são destinadas às organizações que estão usando o [conector de origem do Analytics](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics) para trazer dados de streaming de mídia do Adobe Analytics para a Adobe Experience Platform para uso com relatórios do Customer Journey Analytics ou qualquer outro serviço da Platform.
>
>As alterações não afetam o Adobe Analytics como um aplicativo independente, incluindo a coleta de dados, o processamento e os relatórios. Ferramentas como Feeds de dados e Regras de processamento não são afetadas, portanto, não são necessárias atualizações na implementação do Analytics.

Uma nova implementação da Coleta de dados do Adobe (conector de origem do Analytics) para o serviço de mídia de transmissão agora está disponível e migra de um conjunto de campos XDM para outro.

## Novo caminho do campo XDM

Como parte dessa migração, o caminho do campo XDM `mediaReporting` foi adicionado aos esquemas XDM usados nos fluxos da Coleção de dados do Adobe (conector de origem do Analytics). Qualquer esquema de coleta de dados do Adobe existente e recém-gerado incluirá automaticamente esse novo campo.

## Substituição do antigo caminho do campo XDM

Todos os fluxos de Coleta de dados do Adobe (conector de origem do Analytics) que transferem dados de mídia de transmissão do Adobe Analytics para o Adobe Experience Platform estão enviando dados no momento no novo caminho do campo XDM `mediaReporting` e no caminho do campo XDM `media.mediaTimed` antigo. Ambos os caminhos de campo estarão disponíveis por três meses, até o final de outubro de 2025. Após outubro, os campos `media.mediaTimed` serão totalmente descontinuados, e os dados assimilados após outubro incluirão apenas `mediaReporting`. Após a desativação, os campos `media.mediaTimed` não estarão mais visíveis na interface do esquema do Adobe Experience Platform e a assimilação de dados nesses campos será interrompida. Consequentemente, esses campos não estarão mais disponíveis para uso em nenhum serviço do Adobe Experience Platform.

Os dados assimilados antes dessa data permanecerão disponíveis para relatório.

## Diferenças adicionais com o novo caminho do campo XDM

Com a nova implementação do conector de origem do Adobe para mídia de transmissão, as chamadas keep-alive do Adobe Analytics agora são assimiladas no Adobe Experience Platform.

Anteriormente, essas chamadas não eram refletidas nos aplicativos da Platform, como o Customer Journey Analytics. Como resultado, sua organização pode observar as seguintes diferenças nos relatórios:

* **Contagens precisas de sessões**: em alguns casos, isso pode significar deflação nas contagens de sessões, pois as chamadas keep-alive ajudam a manter sessões de usuários ativas, mesmo na ausência de interações diretas de mídia. Essas chamadas keep-alive são geradas a cada 20 minutos após o último evento, por reprodução de mídia, com o objetivo de manter a visita aberta. Para garantir um rastreamento de sessão ideal no Customer Journey Analytics, é recomendável configurar a expiração da visita para 30 minutos na visualização de dados.

* **Um aumento no número de eventos**: porque as chamadas keep-alive agora são contadas na métrica Eventos do Customer Journey Analytics. Se você quiser excluir chamadas keep-alive dos relatórios, crie um filtro que exclua eventos com o Tipo de Evento `media.keepalive`.

Essa alteração garante um maior alinhamento entre os relatórios do Analytics e do CJA.

## Migrar sua configuração existente

Para garantir uma transição sem problemas, todos os clientes devem migrar as configurações existentes dos campos `media.mediaTimed` para os campos `mediaReporting` antes do final de outubro de 2025. As áreas afetadas são aquelas que dependem do uso do `media.mediaTimed` e devem ser migradas conforme descrito nas seções a seguir.

### Customer Journey Analytics**

Há duas maneiras de migrar os relatórios do CJA:

>[!NOTE]
>
>Depois de escolher uma das seguintes opções, você deve substituir manualmente cada campo `media.mediaTimed` usado nos relatórios do Customer Journey Analytics pelo seu campo derivado correspondente ou Caminho do campo XDM do relatório.

* **Para reter dados históricos**: as equipes do Adobe desenvolveram um modelo predefinido do Customer Journey Analytics que introduz um conjunto de campos derivados que combinam os campos XDM antigos e novos em um único campo. Esse template pode ser ativado por conexão Customer Journey Analytics mediante solicitação. Entre em contato com a equipe de suporte da Adobe para ajudá-lo a ativar os novos campos. Esses campos derivados não contam para o limite de campos derivados da sua organização.

  Para exibir uma lista de mapeamentos, consulte [Mapeamento de parâmetros do Media Analytics para Adobe Experience Platform e Customer Journey Analytics](/help/use-cases/xdm-updates/parameters-mapping.md).

* **Se os dados históricos não forem obrigatórios**: é suficiente usar o Caminho do Campo XDM do Relatório no momento do relatório. Para obter mais informações, consulte [Migrar Customer Journey Analytics para usar os novos campos de mídia de streaming](/help/use-cases/xdm-updates/migrate-cja-setup.md).

### Real-Time CDP

Todos os públicos e perfis devem se basear em `mediaReporting`. Para obter mais informações, consulte [Migrar perfis para os novos campos de mídia de streaming](/help/use-cases/xdm-updates/migrate-profiles.md).

### Fluxo de dados e coleta de dados

Configurações dinâmicas e mapeamento de dados devem usar `mediaReporting`. Para obter mais informações, consulte [Migrar Preparo de Dados de campos personalizados para os novos campos de mídia de streaming](/help/use-cases/xdm-updates/migrate-dataprep.md).

### Outros serviços que devem ser migrados

* Adobe Journey Optimizer: as configurações de campanha e jornada precisam incorporar o `mediaReporting`.

* Encaminhamento de eventos: somente `mediaReporting` campos devem ser incluídos nas configurações.

* Serviços de consulta: as consultas devem referenciar `mediaReporting` campos.

* Configurações de marcas: qualquer configuração de marcação deve fazer referência a `mediaReporting` campos.

* Conexões e Destinos: os fluxos de dados de importação e exportação devem ser estruturados em torno de `mediaReporting` campos.

Esteja ciente de que qualquer outro fluxo que dependa dos campos `media.mediaTimed` será afetado e exigirá atualizações lógicas.

## Próximas etapas e suporte

Todos os clientes que usam a Coleta de dados do Adobe para streaming de mídia devem concluir suas migrações dentro do período de transição designado.

Se tiver dúvidas ou precisar de suporte, entre em contato com a equipe de suporte da Adobe.
