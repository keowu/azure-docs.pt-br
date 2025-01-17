---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 12/09/2020
ms.author: alkohli
ms.openlocfilehash: 9ea5fb26a52c967c5296f1a83976e748c86c9e18
ms.sourcegitcommit: 799f0f187f96b45ae561923d002abad40e1eebd6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97763733"
---
O tamanho da VM determina a quantidade de recursos de computação, como memória, CPU e GPU que estão disponíveis para a VM. As máquinas virtuais devem ser criadas usando um tamanho de VM adequado para a carga de trabalho. Embora todos os computadores sejam executados no mesmo hardware, os tamanhos de máquina têm limites diferentes para o acesso ao disco, o que pode ajudá-lo a gerenciar o acesso geral ao disco em suas VMs. Se uma carga de trabalho aumentar, uma máquina virtual existente também poderá ser redimensionada.

As VMs a seguir têm suporte para a criação no dispositivo Azure Stack Edge.

### <a name="dv2-series"></a>Série Dv2
|Tamanho     |vCPU     |Memória (GiB) | Tamanho do disco do recurso (GiB)  | Tamanho do disco do so (GiB) | Discos de dados máximos | Máximo de NICs |
|-------------------|----|----|-----|----|------|------------|
|**Standard_D1_v2** |1   |3,5 |50   |1000| 4    |2 |
|**Standard_D2_v2** |2   |7   |100  |1000| 8    |4 |
|**Standard_D3_v2** |4   |14  |200  |1000| 16  |4 |
|**Standard_D4_v2** |8   |28  |400  |1000| 32  |8 |
|**Standard_D5_v2** |16  |56  |800  |1000| 64  |8 |
|**Standard_D11_v2** |2   |14  |100  |1000| 8     |2 |
|**Standard_D12_v2** |4   |28  |200  |1000| 16   |4 |
|**Standard_D13_v2** |8   |56  |400  |1000| 32  |8 |

### <a name="dsv2-series"></a>Série DSv2
|Tamanho     |vCPU     |Memória (GiB) |  Tamanho do disco do recurso (GiB)  | Tamanho do disco do so (GiB) | Discos de dados máximos| Máximo de NICs |
|--------------------|----|----|----|-----|------|-------------|
|**Standard_DS1_v2** |1   |3,5 |7  |4000  |1000 |4  |2 |
|**Standard_DS2_v2** |2   |7   |14 |8000  |1000 |8  |4 |
|**Standard_DS3_v2** |4   |14  |28 |16000 |1000 |16 |4 |
|**Standard_DS4_v2** |8   |28  |56 |32000 |1000 |32 |8 |
|**Standard_DS5_v2** |16  |56  |112|64000 |1000 |64 |8 |
|**Standard_DS11_v2**|2   |14  |28 |8000  |1000 |4  |2 |
|**Standard_DS12_v2**|4   |28  |56 |16000 |1000 |8  |4 |
|**Standard_DS13_v2**|8   |56  |112|32000 |1000 |16 |8 |


Para obter mais informações, acesse a [série Dv2 em uso geral tamanhos de VM](../articles/virtual-machines/dv2-dsv2-series.md#dv2-series).

### <a name="ncast4_v3-series-preview"></a>Série NCasT4_v3 (versão prévia)

Esses tamanhos têm suporte para VMs de GPU em seu dispositivo e são otimizados para aplicativos com aceleração de GPU com uso intensivo de computação. Esta série se concentra em cargas de trabalho de inferência com a GPU Tesla T4 da NVIDIA. 

|Tamanho     |vCPU     |Memória (GiB) | Tamanho do disco do recurso (GiB)  |Tamanho do disco do so (GiB)| GPU | Memória GPU (GiB) | Máximo de NICs |
|---------------------|----|----|-----|-----|-------|--------------|
|**Standard_NC4as_T4_v3** |4   |28  |180   |1000|1 |16   |4 |
|**Standard_NC8as_T4_v3** |8   |56  |360   |1000|1 |16  |8 |

Para obter mais informações, vá para a [série de NCasT4_v3 em tamanhos de VM otimizados para GPU](../articles/virtual-machines/nct4-v3-series.md).

### <a name="f-series"></a>Série F

Essas séries são otimizadas para cargas de trabalho computacionais e são executadas em processadores Intel Xeon. 

| Tamanho | da vCPU | Memória: GiB |Tamanho do disco do recurso (GiB) |Tamanho do disco do so (GiB)|  Discos de dados máximos | Máximo de NICs |
|---|---|---|---|---|---|---|---|---|
| Standard_F1  | 1  | 2   |16      |1000| 4  |  2 |
| Standard_F2 | 2  | 4 |32      |1000| 8  |  4 |
| Standard_F4  | 4  | 8 |64   |1000| 16 |  4 |
| Standard_F8 | 8 | 16  |132    |1000| 32 |  8 |
| Standard_F16 | 16 | 32  |262   |1000| 64 |  8 |
| Standard_F1s | 1 | 2  | 4  |1000| 4 | 1 |
| Standard_F2s | 2 | 4 |8   |1000| 8 | 4 |
| Standard_F4s | 4 | 8 |16 |1000| 16 |  4 |
| Standard_F8s | 8 | 16 |32 |1000| 32 |  8 |
| Standard_F16s | 16 | 32 |64 |1000| 64 |  8 |

Para obter mais informações, acesse [Fsv2 em tamanhos de VM otimizados para computação](../articles/virtual-machines/fsv2-series.md).

