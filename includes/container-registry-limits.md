---
title: incluir arquivo
description: incluir arquivo
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: include
ms.date: 06/18/2020
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 3fe1b966b56142fd312850ac5d77839b7d9db434
ms.sourcegitcommit: e7152996ee917505c7aba707d214b2b520348302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2020
ms.locfileid: "97706210"
---
| Recurso | Basic | Standard | Premium |
|---|---|---|---|
| Armazenamento incluído<sup>1</sup> (GiB) | 10 | 100 | 500 |
| Limite de armazenamento (TiB) | 20| 20 | 20 |
| Tamanho máximo da camada de imagem (GiB) | 200 | 200 | 200 |
| ReadOps por minuto<sup>2, 3</sup> | 1,000 | 3\.000 | 10.000 |
| WriteOps por minuto<sup>2, 4</sup> | 100 | 500 | 2\.000 |
| Mbps de largura de banda de download<sup>2</sup> | 30 | 60 | 100 |
| Mbps de largura de banda de upload<sup>2</sup> | 10 | 20 | 50 |
| Webhooks | 2 | 10 | 500 |
| Replicação geográfica | N/D | N/D | [Com suporte][geo-replication] |
| Zonas de disponibilidade | N/D | N/D | [Visualização][zones] |
| Confiança em conteúdo | N/D | N/D | [Com suporte][content-trust] |
| Link privado com pontos de extremidade privados | N/D | N/D | [Com suporte][plink] |
| &bull; Pontos de extremidade privados | N/D | N/D | 10 |
| Acesso VNet do ponto de extremidade de serviço | N/D | N/D | [Visualização][vnet] |
| Chaves gerenciadas pelo cliente | N/D | N/D | [Com suporte][cmk] |
| Permissões no escopo do repositório | N/D | N/D | [Visualização][token]|
| &bull; Tokens | N/D | N/D | 20,000 |
| &bull; Mapas de escopo | N/D | N/D | 20,000 |
| &bull; Repositórios por mapa de escopo | N/D | N/D | 500 |


<sup>1</sup> Armazenamento incluído na taxa diária de cada camada. Para obter um armazenamento adicional, será cobrada uma taxa diária adicional por GiB, até o limite de armazenamento. Para obter informações de taxa, confira [Preço de Registro de Contêiner do Azure][pricing].

<sup>2</sup>*ReadOps*, *WriteOps* e *Largura de Banda* são estimativas mínimas. O Registro de Contêiner do Azure se esforça para aprimorar o desempenho conforme os requisitos de uso.

<sup>3</sup>Um [docker pull](https://docs.docker.com/registry/spec/api/#pulling-an-image) se traduz em várias operações de leitura com base no número de camadas na imagem, além da recuperação do manifesto.

<sup>4</sup>Um [docker push](https://docs.docker.com/registry/spec/api/#pushing-an-image) se traduz em várias operações de gravação com base no número de camadas que devem ser enviadas por push. Um `docker push` inclui *ReadOps* para recuperar um manifesto para uma imagem existente.

<!-- LINKS - External -->
[pricing]: https://azure.microsoft.com/pricing/details/container-registry/

<!-- LINKS - Internal -->
[geo-replication]: ../articles/container-registry/container-registry-geo-replication.md
[content-trust]: ../articles/container-registry/container-registry-content-trust.md
[vnet]: ../articles/container-registry/container-registry-vnet.md
[plink]: ../articles/container-registry/container-registry-private-link.md
[cmk]: ../articles/container-registry/container-registry-customer-managed-keys.md
[token]: ../articles/container-registry/container-registry-repository-scoped-permissions.md
[zones]: ../articles/container-registry/zone-redundancy.md
