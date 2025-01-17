---
title: Solucionar problemas de segurança e controle de acesso
description: Saiba como solucionar problemas de segurança e controle de acesso no Azure Data Factory.
services: data-factory
author: lrtoyou1223
ms.service: data-factory
ms.topic: troubleshooting
ms.date: 01/05/2021
ms.author: lle
ms.reviewer: craigg
ms.openlocfilehash: fac4f3029d783e9257d00466ddb9fc9741b0f5a2
ms.sourcegitcommit: d7d5f0da1dda786bda0260cf43bd4716e5bda08b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97895641"
---
# <a name="troubleshoot-azure-data-factory-security-and-access-control-issues"></a>Solucionar problemas Azure Data Factory segurança e controle de acesso

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Este artigo explora métodos comuns de solução de problemas de segurança e controle de acesso no Azure Data Factory.

## <a name="common-errors-and-messages"></a>Erros e mensagens comuns

### <a name="connectivity-issue-in-the-copy-activity-of-the-cloud-datastore"></a>Problema de conectividade na atividade de cópia do repositório de armazenamento de nuvem

#### <a name="symptoms"></a>Sintomas

Várias mensagens de erro podem ser retornadas quando ocorrem problemas de conectividade no repositório de armazenamento de origem ou de coletor.

#### <a name="cause"></a>Causa 

O problema geralmente é causado por um dos seguintes fatores:

* A configuração de proxy no nó do tempo de execução de integração (IR) auto-hospedado, se você estiver usando um IR de hospedagem interna.

* A configuração de firewall no nó IR auto-hospedado, se você estiver usando um IR de hospedagem interna.

* A configuração de firewall no repositório de armazenamento de nuvem.

#### <a name="resolution"></a>Resolução

* Para garantir que esse é um problema de conectividade, verifique os seguintes pontos:

   - O erro é gerado a partir dos conectores de origem ou de coletor.
   - A falha está no início da atividade de cópia.
   - A falha é consistente para Azure IR ou o IR auto-hospedado com um nó, pois pode ser uma falha aleatória em um IR de vários nós hospedados automaticamente se apenas alguns dos nós tiverem o problema.

* Se você estiver usando um **ir auto-hospedado**, verifique as configurações de proxy, firewall e rede, pois a conexão com o mesmo repositório de armazenamento poderá ter sucesso se você estiver usando um Azure ir. Para solucionar esse problema, consulte:

   * [Portas e firewalls de IR hospedados internamente](https://docs.microsoft.com/azure/data-factory/create-self-hosted-integration-runtime#ports-and-firewalls)
   * [Conector de Azure Data Lake Storage](https://docs.microsoft.com/azure/data-factory/connector-azure-data-lake-store)
  
* Se você estiver usando uma **Azure ir**, tente desabilitar a configuração de firewall do repositório de armazenamento. Essa abordagem pode resolver os problemas nas duas situações a seguir:
  
   * [Azure ir endereços IP](https://docs.microsoft.com/azure/data-factory/azure-integration-runtime-ip-addresses) não estão na lista de permissões.
   * O recurso *permitir que os serviços Microsoft confiáveis acessem este conta de armazenamento* está desativado para o [armazenamento de BLOBs do Azure](https://docs.microsoft.com/azure/data-factory/connector-azure-blob-storage#supported-capabilities) e o [Azure data Lake Storage Gen 2](https://docs.microsoft.com/azure/data-factory/connector-azure-data-lake-storage#supported-capabilities).
   * A configuração *permitir acesso aos serviços do Azure* não está habilitada para Azure data Lake Storage Gen1.

Se nenhum dos métodos anteriores funcionar, contate a Microsoft para obter ajuda.


### <a name="invalid-or-empty-authentication-key-issue-after-public-network-access-is-disabled"></a>Problema de chave de autenticação inválido ou vazio após o acesso à rede pública ser desabilitado

#### <a name="symptoms"></a>Sintomas

Depois de desabilitar o acesso à rede pública para Data Factory, o Integration Runtime de hospedagem interna gera o seguinte erro: "a chave de autenticação é inválida ou está vazia".

#### <a name="cause"></a>Causa

O problema é provavelmente causado por um problema de resolução de DNS (sistema de nomes de domínio), pois desabilitar a conectividade pública e estabelecer um ponto de extremidade privado impede a reconexão.

Para verificar se o FQDN (nome de domínio totalmente qualificado) do Data Factory é resolvido para o endereço IP público, faça o seguinte:

1. Confirme que você criou a VM (máquina virtual) do Azure na mesma rede virtual que o ponto de extremidade Data Factory privado.

2. Execute PsPing e ping da VM do Azure para o Data Factory FQDN:

   `psping.exe <dataFactoryName>.<region>.datafactory.azure.net:443`
   `ping <dataFactoryName>.<region>.datafactory.azure.net`

   > [!Note]
   > Você deve especificar uma porta para o comando PsPing. A porta 443 é mostrada aqui, mas não é necessária.

3. Verifique se ambos os comandos são resolvidos para um Azure Data Factory IP público com base em uma região especificada. O IP deve estar no seguinte formato: `xxx.xxx.xxx.0`

#### <a name="resolution"></a>Resolução

Para resolver o problema, faça o seguinte:
- Consulte o [link privado do Azure para Azure data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-private-link#dns-changes-for-private-endpoints) artigo. A instrução é para configurar a zona DNS privada ou o servidor para resolver o Data Factory FQDN para um endereço IP privado.

- É recomendável usar um DNS personalizado como a solução de longo prazo. No entanto, se você não quiser configurar a zona DNS privada ou o servidor, tente a seguinte solução temporária:

  1. Altere o arquivo de host no Windows e mapeie o IP privado (o Azure Data Factory ponto de extremidade privado) para o Azure Data Factory FQDN.
  
     Na VM do Azure, vá para `C:\Windows\System32\drivers\etc` e abra o arquivo de *host* no bloco de notas. Adicione a linha que mapeia o IP privado ao FQDN no final do arquivo e salve a alteração.
     
     ![Captura de tela do mapeamento do IP privado para o host.](media/self-hosted-integration-runtime-troubleshoot-guide/add-mapping-to-host.png)

  1. Execute novamente os mesmos comandos das etapas de verificação anteriores para verificar a resposta, que deve conter o IP privado.

  1. Registre novamente o tempo de execução de integração auto-hospedado e o problema deve ser resolvido.

### <a name="unable-to-register-ir-authentication-key-on-self-hosted-vms-due-to-private-link"></a>Não é possível registrar a chave de autenticação IR em VMs auto-hospedadas devido ao link privado

#### <a name="symptoms"></a>Sintomas

Você não pode registrar a chave de autenticação IR na VM auto-hospedada porque o link privado está habilitado. Você vê a seguinte mensagem de erro:

"Falha ao obter o token de serviço do serviço ADF com a chave * * * * * * * * * * * * * * * e o custo de tempo é: 0,1250079 segundos, o código de erro é: InvalidGatewayKey, ActivityId é: XXXXXXX e a mensagem de erro detalhada é que o endereço IP do cliente não é um IP privado válido, pois o data Factory não pôde acessar a rede pública, portanto, não é capaz de acessar a nuvem para fazer a conexão bem-sucedida."

#### <a name="cause"></a>Causa

O problema pode ser causado pela VM na qual você está tentando instalar o IR auto-hospedado. Para se conectar à nuvem, verifique se acesso à rede pública está habilitado.

#### <a name="resolution"></a>Resolução

**Solução 1**
 
Para resolver o problema, faça o seguinte:

1. Vá para a página [fábricas – atualização](https://docs.microsoft.com/rest/api/datafactory/Factories/Update) .

1. No canto superior direito, selecione o botão **experimentar** .
1. Em **parâmetros**, conclua as informações necessárias. 
1. Em **corpo**, Cole a seguinte propriedade:

    ```
    { "tags": { "publicNetworkAccess":"Enabled" } }
    ```
1. Selecione **executar** para executar a função. 

1. Em **parâmetros**, conclua as informações necessárias. 

1. Em **corpo**, Cole a seguinte propriedade:
    ```
    { "tags": { "publicNetworkAccess":"Enabled" } }
    ``` 

1. Selecione **executar** para executar a função. 
1. Confirme se o **código de resposta: 200** é exibido. A propriedade colada também deve ser exibida na definição de JSON.

1. Adicione a chave de autenticação IR novamente no Integration Runtime.


**Solução 2**

Para resolver o problema, vá para o [link privado do Azure para Azure data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-private-link).

Tente habilitar o acesso à rede pública na interface do usuário, conforme mostrado na seguinte captura de tela:

![Captura de tela do controle "habilitado" para "permitir acesso à rede pública" no painel de rede.](media/self-hosted-integration-runtime-troubleshoot-guide/enable-public-network-access.png)

### <a name="pipeline-runtime-varies-when-basing-on-different-ir"></a>O tempo de execução do pipeline varia quando baseia-se em um IR diferente

#### <a name="symptoms"></a>Sintomas

Simplesmente alternar a lista suspensa serviço vinculado no conjunto de um executa as mesmas atividades de pipeline, mas tem tempos de execução drasticamente diferentes. Quando o conjunto de informações é baseado na Integration Runtime de rede virtual gerenciada, demora mais de 2 minutos para concluir a execução, mas leva aproximadamente 20 segundos para ser concluído quando baseado no Integration Runtime padrão.

#### <a name="cause"></a>Causa

Verificando os detalhes das execuções de pipeline, você pode ver que o pipeline lento está em execução no IR (rede virtual) da VNet gerenciada enquanto o normal está em execução no Azure IR. Por design, o IR para VNet gerenciada leva tempo de fila maior do que Azure IR, pois não estamos reservando um nó de computação por data factory, portanto, há um aquecimento de cerca de 2 minutos para que cada atividade de cópia seja iniciada e ela ocorre principalmente na junção VNet, em vez de Azure IR.

## <a name="next-steps"></a>Próximas etapas

Para obter mais ajuda com a solução de problemas, experimente os seguintes recursos:

*  [Link privado para Data Factory](data-factory-private-link.md)
*  [Blog de Data Factory](https://azure.microsoft.com/blog/tag/azure-data-factory/)
*  [Solicitações de recurso do Data Factory](https://feedback.azure.com/forums/270578-data-factory)
*  [Vídeos do Azure](https://azure.microsoft.com/resources/videos/index/?sort=newest&services=data-factory)
*  [Microsoft Q&uma página](/answers/topics/azure-data-factory.html)
*  [Fórum do Stack Overflow para Data Factory](https://stackoverflow.com/questions/tagged/azure-data-factory)
*  [Informações do Twitter sobre o Data Factory](https://twitter.com/hashtag/DataFactory)
