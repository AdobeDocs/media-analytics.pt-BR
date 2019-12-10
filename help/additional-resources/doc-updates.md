---
title: Atualizações de documentação
description: null
uuid: 1f3e48df-83b6-418c-8cf7-d79466481f79
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Recursos {#resources}

## Notas de versão {#release-notes}

* [Notas de versão](https://docs.adobe.com/content/help/pt-BR/release-notes/experience-cloud/current.html)

## Atualizações de documentação {#documentation-updates}

### Última atualização: Outubro de 2019 {#October-2019-update}

Diversas correções de edição e formatação.
Os tópicos do guia foram expandidos além do SDK do Media, incluindo um novo tópico do guia geral sobre "Dimensões de mídia fora do rastreamento de mídia".


### Última atualização: 7 de março de 2019 {#March-2019-update}

* Esta atualização foi principalmente para o SDK do Media versão 2.2 nas plataformas JavaScript e OTT.
* O SDK do Media versão 2.2 nas plataformas JavaScript e OTT oferece o mesmo suporte descrito abaixo para as plataformas iOS e Android (atualização de 1 de novembro de 2018).

### Última atualização: 1 de novembro de 2018 {#November-2018-update}

* Esta atualização foi principalmente para o SDK do Media versão 2.2 nas plataformas Android e iOS.
* A versão do SDK do Media 2.2 para Android e iOS oferece suporte ao rastreamento de áudio nas plataformas, além de melhorias internas.
* Com a adição do rastreamento de áudio e com ambos os recursos de rastreamento de áudio e vídeo disponíveis no SDK do Media e na API Media Collection, uma atualização de nomenclatura relativamente abrangente é necessária:

   * A solução geral é chamada Adobe Analytics para áudio e vídeo
   * A abreviação utilizada anteriormente nos documentos, "Video Analytics", passou a ser "Media Analytics"
   * No SDK, as referências para a “Biblioteca do Video Heartbeat (VHL)” agora são “SDK do Media”
   * Nomes de arquivo e URLs (por exemplo, links para referências da API) que eram referenciadas como “vídeo” ou “vhl” foram substituídos por “mídia”
   * No código, os nomes das chaves de metadados agora incluem “MÍDIA” no lugar de “VÍDEO”
   * e assim por diante...

* Além disso, foi realizada uma reestruturação adicional na seção do SDK do Media, incluindo a adição das referências e da implementação dos metadados padrão a seus próprios tópicos (tinham sido absorvidos pelos tópicos de *Rastreamento principal* na última atualização do documento). Esses tópicos, juntamente com os tópicos *Rastreamento principal* e *Rastreamento de busca* e *Rastreamento de buffering*, foram agrupados em *Rastreamento da reprodução de áudio e vídeo*.

* O formulário de Federated Analytics foi atualizado para a versão 3.2 para refletir os novos parâmetros envolvidos no rastreamento de áudio.

### Atualizado: 10 de outubro de 2018 {#October-2018-update}

* A estrutura do documento foi "refatorada" na área Implementação do SDK, combinando os guias de implementação de plataformas individuais (mas quase idênticos) em uma única seção de implementação de SDK, com exemplos de rastreamento específicos das plataformas apresentados em subseções nos tópicos de rastreamento.
* Os arquivos foram renomeados em antecipação a uma migração para um novo sistema de documentos. Todos os prefixos DITA (c_, r_, t_ ) indicando os tipos de tópicos de conceito, referência e tarefa, respectivamente) foram eliminados. Todos os sublinhados ('_') foram substituídos por hifens ('-'). Além disso, os nomes de arquivo agora se assemelham mais aos títulos dos tópicos.
* Atualizações nos tópicos de Validação e Certificação.
* Novo material de introdução, incluindo uma apresentação das opções de medição, juntamente com atualizações nos pré-requisitos, caminhos de implementação e ativação do Audience Manager.
* Atualizações nas seções de Métricas e metadados e de Relatórios e análises, refletindo a adição dos recursos do Audio Analytics.
