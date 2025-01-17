---
title: Glossário do backup do Azure
description: Este artigo define os termos úteis para uso com o backup do Azure.
ms.topic: conceptual
ms.date: 12/21/2020
ms.openlocfilehash: 8baa47667e86b99ebbbf273610809814e768c077
ms.sourcegitcommit: a89a517622a3886b3a44ed42839d41a301c786e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2020
ms.locfileid: "97733275"
---
# <a name="azure-backup-glossary"></a>Glossário do backup do Azure

Este glossário de termos pode ser útil ao usar o backup do Azure.

>[!NOTE]
>
> - Os termos que são marcados com o prefixo "(termo específico da carga de trabalho)" referem-se aos termos que são relevantes apenas no contexto de um subconjunto específico de cargas de trabalho que o backup do Azure dá suporte.
> - Para termos que são usados normalmente na documentação do backup do Azure, mas consulte outros serviços do Azure, um link direto é fornecido à documentação do serviço do Azure relevante.

## <a name="afs-azure-file-shares"></a>AFS (compartilhamentos de arquivos do Azure)

Consulte a [documentação dos arquivos do Azure](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="alternate-location-recovery"></a>Recuperação em local alternativo

Uma recuperação feita a partir do ponto de recuperação para um local diferente do local original onde os backups foram feitos. Ao usar o backup de VM do Azure, isso significaria restaurar a VM para um servidor que não seja o servidor original em que os backups foram feitos. Ao usar o backup de compartilhamento de arquivos do Azure, isso significa restaurar dados para um compartilhamento de arquivos diferente do compartilhamento de arquivos de backup.

## <a name="application-consistent-backup"></a>Backup consistente com o aplicativo

(Termo específico da carga de trabalho)

Backups consistentes com o aplicativo capturam conteúdo de memória e operações de e/s pendentes. Os instantâneos consistentes com o aplicativo usam um gravador [VSS VSS (](#vss-windows-volume-shadow-copy-service) ou scripts anteriores ou posteriores para Linux) para garantir a consistência dos dados do aplicativo antes que ocorra um backup. [Saiba mais](backup-azure-vms-introduction.md).

## <a name="azure-resource-manager-arm-templates"></a>Modelos do Azure Resource Manager (ARM)

Consulte a [documentação de modelos ARM](https://docs.microsoft.com/azure/azure-resource-manager/templates/overview).

## <a name="autoprotection-for-databases"></a>Autoproteção (para bancos de dados)

(Termo específico da carga de trabalho)

A proteção automática é um recurso que permite proteger automaticamente todos os bancos de dados em uma instância SQL Server autônoma ou um SQL Server Always On grupo de disponibilidade. Ele não apenas permite backups para os bancos de dados existentes, mas também protege todos os bancos de dados que você pode adicionar no futuro.

## <a name="availability-storage-replication-types"></a>Disponibilidade (tipos de replicação de armazenamento)

O backup do Azure oferece três tipos de replicação para manter o armazenamento e os dados altamente disponíveis:

### <a name="lrs"></a>LRS

O [LRS (armazenamento com redundância local)](https://docs.microsoft.com/azure/storage/common/storage-redundancy#locally-redundant-storage) Replica seus dados de backup três vezes (ele cria três cópias dos dados de backup) em uma unidade de escala de armazenamento em um datacenter. Todas as cópias dos dados de backup existem na mesma região. O LRS é uma opção de baixo custo para proteger seus dados de backup de falhas de hardware local.

### <a name="grs"></a>GRS

O [GRS (armazenamento com redundância geográfica)](https://docs.microsoft.com/azure/storage/common/storage-redundancy#geo-redundant-storage) é a opção de replicação padrão e recomendada. O GRS Replica seus dados de backup para uma região secundária, a centenas de quilômetros de distância do local principal dos dados de origem. O GRS custa mais do que o LRS, mas o GRS fornece um nível mais alto de durabilidade para seus dados de backup, mesmo se houver uma interrupção regional.

>[!NOTE]
>Para cofres GRS que têm o recurso de restauração entre regiões habilitado, o armazenamento de backup é atualizado de GRS para RA-GRS (armazenamento de Geo-Redundant de acesso de leitura).

### <a name="zrs"></a>ZRS

O [ZRS (armazenamento com redundância de zona)](https://docs.microsoft.com/azure/storage/common/storage-redundancy#zone-redundant-storage) Replica seus dados de backup em [zonas de disponibilidade](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones), garantindo a residência e a resiliência dos dados de backup na mesma região. Portanto, é possível fazer backup de suas cargas de trabalho críticas que exigem [residência de dados](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure/) no ZRS.

## <a name="azure-command-line-interface-cli"></a>CLI (interface de linha de comando) do Azure

Consulte a [documentação do CLI do Azure](https://docs.microsoft.com/cli/azure/what-is-azure-cli).

## <a name="azure-policy"></a>Azure Policy

Consulte a [documentação do Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview).

## <a name="azure-powershell"></a>Azure PowerShell

Consulte a [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/).

## <a name="azure-resource-manager-arm"></a>Azure Resource Manager (ARM)

Consulte a [documentação do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview).

## <a name="azure-disk-encryption-ade"></a>Azure Disk Encryption (ADE)

Consulte a [documentação do Azure Disk Encryption](https://docs.microsoft.com/azure/security/fundamentals/azure-disk-encryption-vms-vmss).

## <a name="backend-storage--cloud-storage--backup-storage"></a>Armazenamento de back-end/armazenamento na nuvem/armazenamento de backup

O armazenamento real usado por uma instância de backup. Inclui o tamanho de todos os pontos de retenção que existem para a instância de backup (conforme definido pela política de backup e retenção).

## <a name="bare-metal-backup"></a>Backup bare-metal

Backup de arquivos do sistema operacional e todos os dados em volumes críticos, exceto para dados do usuário. Por definição, um backup bare-metal inclui um backup de estado do sistema. Ele oferece proteção quando um computador não será iniciado e você precisa recuperar tudo. [Saiba mais](backup-mabs-system-state-and-bmr.md).

## <a name="backup-extensions--vm-extensions"></a>Extensões de backup/extensões de VM

(Específico para o tipo de carga de trabalho de VM do Azure)

As extensões da máquina virtual (VM) do Azure são pequenos aplicativos que fornecem tarefas de configuração e automação pós-implantação nas VMs do Azure. O Backup do Azure faz backup de VMs do Azure instalando uma extensão para o agente de VM do Azure em execução no computador. O backup do Azure gerencia automaticamente essas extensões e os usuários não precisam atualizar manualmente essas extensões.

## <a name="backup-instance--backup-item"></a>Instância de backup/item de backup

Um backup de fonte de dado com backup em um cofre com uma política de retenção e reserva específica constitui uma instância de backup ou um item de backup.

## <a name="backup-rule--backup-policy"></a>Regra de backup/política de backup

Uma regra de backup é uma regra definida pelo usuário que especifica quando e com que frequência os backups devem ser executados em uma fonte de fontes. Para alguns tipos de carga de trabalho, a política de backup também fornece uma maneira de especificar o método de instantâneo a ser aplicado na fonte de origem (completa, incremental, diferencial). As políticas de backup geralmente são criadas como uma combinação de regras de backup e regras de retenção.

## <a name="backup-vault"></a>Cofre de backup

Um recurso de Azure Resource Manager do tipo *Microsoft. dataprotection/BackupVaults*. Atualmente, os cofres de backup são usados para fazer backup de bancos de dados do Azure para o servidor PostgreSQL. [Saiba mais sobre cofres de backup](backup-azure-recovery-services-vault-overview.md).

## <a name="bcdr-business-continuity-and-disaster-recovery"></a>BCDR (continuidade dos negócios e recuperação de desastres)

O BCDR envolve um conjunto de processos que uma organização deve adotar para garantir que aplicativos e cargas de trabalho estejam em funcionamento durante o serviço planejado e não planejado ou interrupções do Azure, com interrupção mínima dos negócios. [Saiba mais](https://azure.microsoft.com/solutions/backup-and-disaster-recovery/#overview) sobre os vários serviços que o Azure oferece para ajudá-lo a criar uma estratégia de BCDR de som.

## <a name="churn"></a>Rotatividade

A porcentagem de alterações nos dados que estão sendo submetidos a backup entre dois backups consecutivos. Isso pode ser devido à adição de novos dados ou à modificação ou exclusão de dados existentes.

## <a name="crash-consistent-backup"></a>Backup consistente com falhas

(Termo específico da carga de trabalho)

Instantâneos com consistência de falhas normalmente ocorrem se uma VM do Azure é desligada no momento do backup. Apenas os dados que já existem no disco no momento do backup são capturados e copiados em backup. [Saiba mais](backup-azure-vms-introduction.md#snapshot-consistency).

## <a name="cross-region-restore-crr"></a>CRR (restauração entre regiões)

Como uma das [Opções de restauração](backup-azure-arm-restore-vms.md#restore-options), a CRR (restauração entre regiões) permite que você restaure itens de backup em uma região secundária, que é uma [região emparelhada do Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions#what-are-paired-regions).

## <a name="data-box"></a>Caixa de dados

Consulte a [documentação da caixa de dados](https://docs.microsoft.com/azure/databox/data-box-overview).

## <a name="datasource"></a>Fonte de dados

Um recurso (recurso do Azure, recurso de proxy ou recurso local) que é um candidato para fazer backup. Por exemplo, uma VM do Azure ou um compartilhamento de arquivos do Azure.

## <a name="dpm-data-protection-manager"></a>DPM (Data Protection Manager)

(Termo específico da carga de trabalho)

Consulte a [documentação do DPM](https://docs.microsoft.com/system-center/dpm/dpm-overview).

## <a name="expressroute"></a>ExpressRoute

Consulte a [documentação do ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction).

## <a name="file-system-consistent-backup"></a>Backup consistente do sistema de arquivos

(Termo específico da carga de trabalho)

Os backups consistentes do sistema de arquivos fornecem consistência ao tirar um instantâneo de todos os arquivos ao mesmo tempo. [Saiba mais](backup-azure-vms-introduction.md#snapshot-consistency).

## <a name="frontend-storage--source-size"></a>Tamanho do armazenamento/origem do front-end

O tamanho dos dados a serem submetidos a backup para uma DataSource. O tamanho de front-end de uma fonte de fontes determina sua contagem de [instâncias protegidas](#protected-instance) .

## <a name="full-backup"></a>Backup completo

Em backups completos, uma cópia da fonte de dados inteira é armazenada para cada backup.

## <a name="gfs-backup-policy"></a>Política de backup do GFS

Uma política de backup do GFS (avô-pai-filho) é aquela que permite que você defina agendas de backup semanais, mensais e anuais, além do agendamento de backup diário. Os backups semanais são conhecidos como "filhos", os backups mensais são conhecidos como "Fathers" e os backups anuais são conhecidos como "avôs". Cada um desses conjuntos de cópias de backup pode ser configurado para ser mantido por diferentes durações de tempo, permitindo mais personalização de opções de retenção para cópias de backup. As políticas do GFS são úteis na retenção de backups por um longo período de tempo em uma maneira mais eficiente de armazenamento.

## <a name="iaas-vms--azure-vms"></a>VMs IaaS/VMs do Azure

Consulte a [documentação da VM do Azure](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="incremental-backup"></a>Backup incremental

Backups incrementais armazenam apenas os blocos que foram alterados desde o backup anterior.

## <a name="instant-restore"></a>Restauração instantânea

A restauração instantânea envolve a restauração de um computador diretamente de seu instantâneo de backup em vez da cópia do instantâneo no cofre. Restaurações instantâneas são mais rápidas do que restaurações de um cofre. O número de pontos de restauração instantâneas disponíveis depende da duração da retenção configurada para instantâneos.

## <a name="iops"></a>IOPS

Operações de entrada/saída por segundo.

## <a name="item-level-restore"></a>Restauração em nível de item

(Termo específico da carga de trabalho)

Restaurar arquivos ou pastas individuais dentro do computador a partir do ponto de recuperação.

## <a name="job"></a>Trabalho

Uma tarefa relacionada ao backup que é criada por um usuário ou o serviço de backup do Azure. Os trabalhos podem ser agendados ou sob demanda (ad-hoc). Há diferentes tipos de trabalhos – backup, restauração, proteção e assim por diante. [Saiba mais sobre os trabalhos](backup-azure-monitoring-built-in-monitor.md#backup-jobs-in-recovery-services-vault).

## <a name="mabs--azure-backup-server"></a>MABS/Servidor de Backup do Azure

(Termo específico da carga de trabalho)

Com o Servidor de Backup do Azure, você pode proteger cargas de trabalho do aplicativo como VMs do Hyper-V, o Microsoft SQL Server, o SharePoint Server, o Microsoft Exchange e os clientes do Windows em um único console. Ele herda grande parte da funcionalidade de backup de carga de trabalho do DPM, mas com algumas diferenças. [Saiba mais](backup-azure-microsoft-azure-backup.md)

## <a name="managed-disks"></a>Discos gerenciados

Consulte a [documentação dos Managed disks](https://docs.microsoft.com/azure/virtual-machines/managed-disks-overview).

## <a name="mars-agent"></a>Agente MARS

(Termo específico da carga de trabalho)

Também conhecido como **agente de backup do Azure** ou **agente de serviços de recuperação**, o agente Mars é usado pelo backup do Azure para fazer backup de dados de máquinas locais e VMs do Azure para um cofre de serviços de recuperação de backup no Azure. [Saiba mais](backup-support-matrix-mars-agent.md).

## <a name="nsg-network-security-group"></a>NSG (grupo de segurança de rede)

Consulte a [documentação do NSG](https://docs.microsoft.com/azure/virtual-network/network-security-groups-overview).

## <a name="offline-seeding"></a>Propagação offline

A propagação offline refere-se ao processo de transferência do backup inicial (completo) offline, sem o uso da largura de banda da rede. Ele fornece um mecanismo para copiar dados de backup em dispositivos de armazenamento físico, que são enviados para um datacenter do Azure próximo e carregados em um cofre de serviços de recuperação. [Saiba mais](offline-backup-overview.md).

## <a name="on-demand-backup--ad-hoc-backup"></a>Backup por demanda/backup ad hoc

Um trabalho de backup que é disparado por um usuário em uma base única necessária e não com base na agenda de backup (política) que foi configurada para o recurso.

## <a name="original-location-recovery-olr"></a>OLR (recuperação de local original)

Uma recuperação feita do ponto de restauração para o local de origem de onde os backups foram feitos, substituindo-o pelo estado armazenado no ponto de recuperação. Ao usar o backup de VM do Azure, isso significa restaurar a VM para o servidor original onde os backups foram feitos. Ao usar o backup de compartilhamento de arquivos do Azure, isso significa restaurar dados para o compartilhamento de arquivos de backup.

## <a name="passphrase"></a>Senha

(Termo específico da carga de trabalho)

Uma frase secreta é usada para criptografar e descriptografar dados durante o backup ou a restauração do seu computador local ou localmente usando o agente MARS para ou do Azure.

## <a name="point-in-time-restore"></a>Recuperação pontual

Restaurar um item para seu estado em um ponto no tempo (PIT) específico.

## <a name="private-endpoint"></a>Ponto de extremidade privado

Consulte a [documentação do ponto de extremidade privado](https://docs.microsoft.com/azure/private-link/private-endpoint-overview).

## <a name="protected-instance"></a>Instância protegida

Uma instância protegida refere-se ao computador, servidor físico ou virtual que você usa para configurar o backup para o Azure.  De um **ponto de vista de cobrança**, a contagem de instâncias protegidas para um computador é uma função de seu tamanho de front-end. [Saiba mais](https://azure.microsoft.com/pricing/details/backup/).

## <a name="rbac-role-based-access-control"></a>RBAC (controle de acesso baseado em função)

Consulte a [documentação do RBAC](https://docs.microsoft.com/azure/role-based-access-control/overview).

## <a name="recovery-point-restore-point-retention-point"></a>Ponto de recuperação/ponto de restauração/ponto de retenção

Uma cópia dos dados originais que estão sendo submetidos a backup. Um ponto de retenção é associado a um carimbo de data/hora para que você possa usá-lo para restaurar um item para um determinado ponto no tempo.

## <a name="recovery-services-vault"></a>Cofre dos Serviços de Recuperação

Um recurso de Azure Resource Manager do tipo *Microsoft. recoveryservices/cofres*. Atualmente, os cofres dos serviços de recuperação são usados para fazer backup das seguintes cargas de trabalho: VMs do Azure, SQL em VMs do Azure, SAP HANA em VMs do Azure e compartilhamentos de arquivos do Azure. Ele também é usado para fazer backup de cargas de trabalho locais usando MARS, Servidor de Backup do Azure (MABS) e System Center DPM. [Saiba mais sobre os cofres dos serviços de recuperação](backup-azure-recovery-services-vault-overview.md).

## <a name="resource-group"></a>Grupo de recursos

Consulte a [documentação do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal#what-is-a-resource-group).

## <a name="rest-api"></a>API REST

Consulte a [documentação da API REST do Azure](https://docs.microsoft.com/rest/api/azure/).

## <a name="retention-rule"></a>Regra de retenção

Uma regra definida pelo usuário que especifica por quanto tempo os backups devem ser mantidos.

## <a name="rpo-recovery-point-objective"></a>RPO (objetivo de ponto de recuperação)

O RPO indica a perda máxima de dados aceitável em um cenário de perda de dados. Isso é determinado pela frequência de backup.

## <a name="rto-recovery-time-objective"></a>RTO (objetivo de tempo de recuperação)

O RTO indica o tempo máximo aceitável em que os dados podem ser restaurados para o último ponto no tempo disponível após um cenário de perda de dados.

## <a name="scheduled-backup"></a>Backup agendado

Um trabalho de backup que é disparado automaticamente pela política de backup configurada para o item especificado.

## <a name="secondary-region--paired-region"></a>Região secundária/região emparelhada

Um par regional consiste em duas regiões na mesma geografia. Uma é a região primária e a outra é a região secundária. As regiões emparelhadas são usadas por alguns serviços do Azure (incluindo o backup do Azure com configurações de GRS) para garantir a continuidade dos negócios e proteger contra perda de dados. [Saiba mais](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

## <a name="soft-delete"></a>Exclusão reversível

A exclusão reversível é um recurso que ajuda a proteger contra a exclusão acidental de dados de backup. Com a exclusão reversível, mesmo se um ator mal-intencionado excluir um backup (ou os dados de backup forem excluídos acidentalmente), os dados de backup serão mantidos por um período de tempo adicional, permitindo a recuperação desse item de backup sem perda de dados. [Saiba mais](backup-azure-security-feature-cloud.md).

## <a name="snapshot"></a>Instantâneo

Um instantâneo é uma cópia completa, somente leitura de um disco rígido virtual (VHD). [Saiba mais](https://docs.microsoft.com/azure/virtual-machines/windows/snapshot-copy-managed-disk).

## <a name="storage-account"></a>Conta de armazenamento

Consulte a [documentação da conta de armazenamento](https://docs.microsoft.com/azure/storage/common/storage-account-overview).

## <a name="subscription"></a>Assinatura

Uma assinatura do Azure é um contêiner lógico usado para provisionar recursos no Azure. Ele contém os detalhes de todos os seus recursos, como VMs (máquinas virtuais), bancos de dados e muito mais.

## <a name="system-state-backup"></a>Backup de estado do sistema

(Termo específico da carga de trabalho)

Faz backup de arquivos do sistema operacional. Esse backup permite que você recupere quando um computador é iniciado, mas os arquivos do sistema e do registro são perdidos. [Saiba mais](backup-mabs-system-state-and-bmr.md).

## <a name="tenant"></a>Locatário

Um locatário é uma representação de uma organização. É uma instância dedicada do Azure AD que uma organização ou um desenvolvedor de aplicativos recebe ao criar uma relação com a Microsoft, como inscrever-se no Azure, no Microsoft Intune ou no Microsoft 365.

## <a name="unmanaged-disk"></a>Disco não gerenciado

Consulte a [documentação discos não gerenciados](https://docs.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance#azure-unmanaged-disks).

## <a name="vault"></a>Cofre

Uma entidade de armazenamento no Azure que hospeda dados de backup. Também é uma unidade de RBAC e cobrança. Atualmente, há dois tipos de cofres – cofre de serviços de recuperação e cofre de backup.

## <a name="vault-credentials"></a>Credenciais do cofre

O arquivo de credenciais do cofre é um certificado gerado pelo portal para cada cofre. Isso é usado ao registrar um servidor no cofre. [Saiba mais](backup-azure-dpm-introduction.md).

## <a name="vnet-virtual-network"></a>VNET (rede virtual)

Consulte a [documentação da VNET](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

## <a name="vss-windows-volume-shadow-copy-service"></a>VSS (Windows Serviço de Cópias de Sombra de Volume)

Consulte a [documentação do VSS](https://docs.microsoft.com/windows-server/storage/file-server/volume-shadow-copy-service).

## <a name="next-steps"></a>Próximas etapas

- [Visão geral do backup do Azure](backup-overview.md)
- [Arquitetura e componentes de backup do Azure](backup-architecture.md)
