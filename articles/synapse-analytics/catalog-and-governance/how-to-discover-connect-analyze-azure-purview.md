---
title: Descobrir, conectar e explorar dados no Synapse usando o Azure alcance
description: Guia sobre como descobrir dados, conectá-los e explorá-los no Synapse
services: synapse-analytics
author: ArnoMicrosoft
ms.service: synapse-analytics
ms.topic: how-to
ms.date: 12/16/2020
ms.author: acomet
ms.reviewer: jrasnick
ms.openlocfilehash: 7c6b25fd3615fa76bc76e6d360f4c76a21a9ad02
ms.sourcegitcommit: 67b44a02af0c8d615b35ec5e57a29d21419d7668
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97918073"
---
# <a name="discover-connect-and-explore-data-in-synapse-using-azure-purview"></a>Descobrir, conectar e explorar dados no Synapse usando o Azure alcance 

> [!IMPORTANT]
> A integração entre o Azure Synapse Analytics e o Azure alcance está atualmente em versão prévia. Se você estiver interessado em experimentar o Azure alcance no Synapse, conecte-se com seu representante de vendas da Microsoft. 

Neste documento, você aprenderá o tipo de interações que pode executar ao registrar uma conta do Azure alcance no Synapse. 

## <a name="prerequisites"></a>Pré-requisitos 

- [Conta do Azure alcance](../../purview/create-catalog-portal.md) 
- [Espaço de trabalho Synapse](../quickstart-create-workspace.md) 
- [Conectar uma conta do Azure alcance ao Synapse](quickstart-connect-azure-purview.md) 

## <a name="using-azure-purview-in-synapse"></a>Usando o Azure alcance no Synapse 

O uso do Azure alcance no Synapse exige que você tenha acesso a essa conta do alcance. Synapse passa pela sua permissão alcance. Por exemplo, se você tiver uma função de permissão de curador, poderá editar metadados verificados pelo Azure alcance. 

### <a name="data-discovery-search-datasets"></a>Data Discovery: pesquisar conjuntos de dados 

Para descobrir os dados registrados e verificados pelo Azure alcance, você pode usar a barra de pesquisa no centro superior do espaço de trabalho Synapse. Certifique-se de selecionar alcance do Azure para pesquisar todos os dados da sua organização. 

## <a name="azure-purview-actions"></a>Ações do Azure alcance 

Aqui está uma lista dos recursos do Azure alcance que estão disponíveis no Synapse: 
- **Visão geral** dos metadados 
- Exibir e editar o **esquema** dos metadados com classificações, termos do glossário, tipos de dados e descrições 
- Exibir a **linhagem** para entender as dependências e realizar a análise de impacto. Para obter mais informações sobre o, consulte [linhagem](../../purview/catalog-lineage-user-guide.md)
- Exibir e editar **contatos** para saber quem é um proprietário ou especialista em um conjunto de uma 
- **Relacionado** para entender as dependências hierárquicas de um conjunto de um específico. Essa experiência é útil para navegar pela hierarquia de dados.

## <a name="actions-that-you-can-perform-over-datasets-with-synapse-resources"></a>Ações que você pode executar sobre conjuntos de os com recursos Synapse 

### <a name="connect-data-to-synapse"></a>Conectar dados ao Synapse 

- Você pode criar um **novo serviço vinculado** para Synapse. Essa ação será necessária para copiar dados para o Synapse ou tê-los em seu hub de dados (para fontes de dados com suporte, como ADLSg2) 
- Para objetos como arquivos, pastas ou tabelas, você pode criar diretamente um **novo conjunto de uma nova integração** e utilizar um serviço vinculado existente, se já tiver sido criado 

Ainda não podemos inferir se há um serviço vinculado existente ou um conjunto de uma integração. 

###  <a name="develop-in-synapse"></a>Desenvolver em Synapse 

Há três ações que você pode executar: **novo script SQL**, **novo bloco de anotações** e **novo fluxo de dados**. 

Com o **novo script SQL**, dependendo do tipo de suporte, você pode: 
- Exiba as 100 principais linhas para entender a forma dos dados. 
- Criar uma tabela externa do banco de dados SQL Synapse 
- Carregar os dados em um Synapse SQL Database 
 
Com o **novo bloco de anotações**, você pode: 
- Carregar dados em um dataframe do Spark 
- Criar uma tabela do Spark (se você fizer isso acima do formato parquet, ele também criará uma tabela de pools SQL sem servidor). 
 
Com o **novo fluxo de dados**, você pode criar um conjunto de dado de integração que pode ser usado como uma origem em um pipeline de fluxo de dados. O fluxo de dados é uma funcionalidade de desenvolvedor sem código para executar a transformação de dados. Para obter mais informações sobre como [usar o fluxo de dados no Synapse](../quickstart-data-flow.md).

##  <a name="nextsteps"></a>Próximas etapas 

- [Registrar e verificar ativos Synapse do Azure no Azure alcance](../../purview/register-scan-azure-synapse-analytics.md)
- [Como pesquisar dados no catálogo de dados do Azure alcance](../../purview/how-to-search-catalog.md)