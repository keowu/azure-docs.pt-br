---
title: Gerar relatórios
description: Conheça a atividade, os riscos, os ataques e as tendências da rede usando o defender para ferramentas de relatório do IoT.
author: shhazam-ms
manager: rkarlin
ms.author: shhazam
ms.date: 12/17/2020
ms.topic: how-to
ms.service: azure
ms.openlocfilehash: d0c3f531ede0a590a6ba7bb21c6edbd768c08069
ms.sourcegitcommit: 8be279f92d5c07a37adfe766dc40648c673d8aa8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97837784"
---
# <a name="generate-reports"></a>Gerar relatórios

Conheça a atividade, os riscos, os ataques e as tendências da rede usando o Azure defender para ferramentas de relatório do IoT. As ferramentas estão disponíveis para gerar relatórios:

- Com base na atividade detectada por sensores individuais.
- Com base na atividade detectada por todos os sensores. 

Esses relatórios são gerados no console de gerenciamento local.

## <a name="reports-for-sensor-risk-assessment"></a>Relatórios de avaliação de risco do sensor

Os relatórios de avaliação de risco permitem gerar uma pontuação de segurança para cada dispositivo de rede, bem como uma pontuação de segurança de rede geral. A pontuação geral representa a porcentagem de segurança de 100 por cento.

Essa Pontuação se baseia nos resultados da inspeção de pacotes, mecanismos de modelagem comportamental e um design de máquina de estado SCADA específico. Uma ampla gama de outras informações está disponível, como:

- Problemas de configuração

- Vulnerabilidade do dispositivo priorizada por nível de segurança

- Problemas de segurança de rede

- Problemas operacionais de rede

- Vetores de ataque

- Conexões com redes ICS

- Conexões com a Internet

- Indicadores de malware industrial

- Problemas de protocolo

  - Dispositivos seguros: dispositivos com uma pontuação de segurança acima de 90%.

- **Dispositivos seguros**: dispositivos com uma pontuação de segurança acima de 90 por cento.

- **Dispositivos vulneráveis**: dispositivos com uma pontuação de segurança abaixo de 70 por cento.

- **Dispositivos que precisam de melhoria**: dispositivos com uma pontuação de segurança entre 70% e 89%.

Para criar um relatório:

1. Selecione **avaliação de risco** no menu lateral.
2. Selecione um sensor na lista suspensa **selecionar sensor** .
3. Selecione **gerar relatório**.
4. Selecione **baixar** na seção relatórios arquivados.

:::image type="content" source="media/how-to-generate-reports/risk-assessment.png" alt-text="Uma exibição da avaliação de risco.":::

Para importar um logotipo da empresa:

Para importar um logotipo da empresa:

- Selecione **importar logotipo**.

## <a name="reports-for-sensor-attack-vector"></a>Relatórios de vetor de ataque de sensor

Os relatórios de vetor de ataque fornecem uma representação gráfica de uma cadeia de vulnerabilidade de dispositivos exploráveis. Essas vulnerabilidades podem dar a um invasor acesso aos principais dispositivos de rede. O simulador de vetor de ataque calcula os vetores de ataque em tempo real e analisa todos os vetores de ataque para um destino específico.

Trabalhar com o vetor de ataque permite avaliar o efeito das atividades de mitigação na sequência de ataque. Em seguida, você pode determinar, por exemplo, se uma atualização do sistema interrompe o caminho do invasor, dividindo a cadeia de ataques ou se um caminho de ataque alternativo permanecer. Essas informações ajudam a priorizar as atividades de correção e mitigação.

:::image type="content" source="media/how-to-generate-reports/control-center.png" alt-text="Exiba seus alertas no centro de controle.":::

> [!NOTE]
> Os administradores e analistas de segurança podem executar os procedimentos descritos nesta seção.

Para criar uma simulação de vetor de ataque:

1. Selecione o :::image type="content" source="media/how-to-generate-reports/plus.png" alt-text="sinal de adição":::no menu lateral para adicionar uma simulação.

 :::image type="content" source="media/how-to-generate-reports/vector.png" alt-text="A simulação do vetor de ataque.":::

2. Insira as propriedades de simulação:

   - **Nome**: nome da simulação.

   - **Vetores máximos**: o número máximo de vetores em uma única simulação.

   - **Mostrar no mapa do dispositivo**: mostra o vetor de ataque como um filtro no mapa do dispositivo.

   - **Todos os dispositivos de origem**: o vetor de ataque considerará todos os dispositivos como uma fonte de ataque.

   - **Origem do ataque**: o vetor de ataque considerará apenas os dispositivos especificados como uma fonte de ataque.

   - **Todos os dispositivos de destino**: o vetor de ataque considerará todos os dispositivos como um alvo de ataque.

   - **Alvo do ataque**: o vetor de ataque considerará apenas os dispositivos especificados como um alvo de ataque.

   - **Excluir dispositivos**: os dispositivos especificados serão excluídos da simulação de vetor de ataque.

   - **Excluir sub-redes**: as sub-redes especificadas serão excluídas da simulação de vetor de ataque.

3. Selecione **Adicionar simulação**. A simulação será adicionada à lista simulações.

   :::image type="content" source="media/how-to-generate-reports/new-simulation.png" alt-text="Adicione uma nova simulação.":::

4. Selecione :::image type="icon" source="media/how-to-generate-reports/edit-a-simulation-icon.png" border="false"::: se você deseja editar a simulação.

   Selecione :::image type="icon" source="media/how-to-generate-reports/delete-simulation-icon.png" border="false"::: se você deseja excluir a simulação.

   Selecione :::image type="icon" source="media/how-to-generate-reports/make-a-favorite-icon.png" border="false"::: se você deseja marcar a simulação como um favorito.

5. Uma lista de vetores de ataque é exibida e inclui A pontuação vetorial (de 100), dispositivo de origem de ataque e dispositivo de destino de ataque. Selecione um ataque específico para a representação gráfica dos vetores de ataque.

   :::image type="content" source="media/how-to-generate-reports/sample-attack-vectors.png" alt-text="Vetores de ataque.":::

## <a name="sensor-data-mining-queries"></a>Dados do sensor – consultas de mineração

As ferramentas de mineração de dados permitem que você gere informações abrangentes e granulares sobre seus dispositivos de rede em várias camadas. Por exemplo, você pode criar uma consulta com base em:

- Períodos de tempo

- Conexões com a Internet

- Portas

- Protocolos

- Versões de firmware

- Comandos de programação

- Inatividade do dispositivo

Você pode ajustar o relatório com base em filtros. Por exemplo, você pode consultar uma sub-rede específica na qual o firmware foi atualizado.

:::image type="content" source="media/how-to-generate-reports/active-device-list-v2.png" alt-text="Lista de dispositivos ativos.":::

Várias ferramentas estão disponíveis para gerenciar consultas. Por exemplo, você pode exportar e salvar.

> [!NOTE]
> Os administradores e analistas de segurança têm acesso às opções de mineração de dados.

### <a name="dynamic-updates"></a>Atualizações dinâmicas

As consultas de mineração de dados que você cria são atualizadas dinamicamente sempre que você as abre. Por exemplo:

- Se você criar um relatório para versões de firmware em dispositivos em 1º de junho e abrir o relatório novamente em 10 de junho, esse relatório será atualizado com informações precisas para 10 de junho.

- Se você criar um relatório para detectar novos dispositivos descobertos nos últimos 30 dias em 1º de junho e abrir o relatório em 30 de junho, os resultados serão exibidos nos últimos 30 dias.

### <a name="data-mining-use-cases"></a>Casos de uso de mineração de dados

Você pode usar consultas para lidar com uma ampla gama de necessidades de segurança para várias equipes de segurança:

- **Resposta a incidentes SOC**: gere um relatório em tempo real para ajudar a lidar com resposta imediata a incidentes. Por exemplo, gere um relatório para uma lista de dispositivos que podem exigir aplicação de patch.

- **Análise forense**: gere um relatório com base em dados históricos para relatórios investigativos.

- **Integridade da rede de ti**: gere um relatório que ajude a melhorar a segurança geral da rede. Por exemplo, gere um relatório que liste os dispositivos com credenciais de autenticação fracas.

- **Visibilidade**: gere um relatório que cubra todos os itens de consulta para exibir todos os parâmetros de linha de base da sua rede.

### <a name="data-mining-storage"></a>Armazenamento de mineração de dados

As informações de mineração de dados são salvas e armazenadas continuamente, exceto quando um dispositivo é excluído. Os resultados de mineração de dados podem ser exportados e armazenados externamente em um servidor seguro. Além disso, o sensor executa backups diários automáticos para garantir a continuidade do sistema e a preservação de dados.

### <a name="data-mining-and-reports"></a>Mineração de dados e relatórios 

Relatórios regulares, acessados a partir da opção de **relatórios** , são relatórios de mineração de dados predefinidos. Elas não são consultas dinâmicas, como estão disponíveis no Data Mining, mas uma representação estática dos resultados da consulta de mineração de dados.

Os resultados da consulta de mineração de dados não estão disponíveis para usuários do RO. Os administradores e analistas de segurança que desejam que os usuários do RO tenham acesso às informações geradas por Data Mining consultas devem salvar as informações como relatório.

### <a name="predefined-queries"></a>Consultas predefinidas

As consultas predefinidas a seguir estão disponíveis. Essas consultas são geradas em tempo real.

- **CVEs**: uma lista de dispositivos detectados com vulnerabilidades conhecidas nas últimas 24 horas.

- **CVEs excluído**: uma lista de todos os CVEs que foram excluídos manualmente. Para obter resultados mais precisos em relatórios e vetores de ataque do VA, você pode personalizar a lista de CVE manualmente, incluindo e excluindo CVEs.

- **Atividade de Internet**: dispositivos que estão conectados à Internet.

- **Dispositivos não ativos**: dispositivos que não se comunicaram nos últimos sete dias.

- **Dispositivos ativos**: dispositivos de rede ativos nas últimas 24 horas.

- **Acesso remoto**: dispositivos que se comunicam por meio de protocolos de sessão remota.

- **Comandos de programação**: dispositivos que enviam programação industrial.

Esses relatórios são acessíveis automaticamente na tela de **relatórios** , onde os usuários e outros usuários podem exibi-los. Os usuários de RO não podem acessar os relatórios de mineração de dados.

:::image type="content" source="media/how-to-generate-reports/data-mining-screeshot-v2.png" alt-text="A tela de Data Mining.":::

### <a name="create-a-data-mining-report"></a>Criar um relatório de mineração de dados

Para criar um relatório de mineração de dados:

1. Selecione **mineração de dados** no menu lateral. Relatórios sugeridos predefinidos são exibidos automaticamente.

 :::image type="content" source="media/how-to-generate-reports/data-mining-screeshot-v2.png" alt-text="Selecione Data Mining no painel lateral.":::

2. Selecione :::image type="icon" source="media/how-to-generate-reports/plus-icon.png" border="false":::.

3. Selecione **novo relatório** e defina o relatório.

   :::image type="content" source="media/how-to-generate-reports/create-new-report-screen.png" alt-text="Crie um novo relatório preenchendo esta tela.":::

   Os seguintes parâmetros estão disponíveis:

   - Forneça um nome de relatório e uma descrição.

   - Para categorias, selecione:

      - **Categorias (tudo)** para exibir todos os resultados do relatório sobre todos os dispositivos em sua rede.

      - **Genérico** para escolher categorias padrão.

   - Selecione os parâmetros de relatório específicos de seu interesse.

   - Escolha uma ordem de classificação (**ordenar por**). Classificar resultados com base na atividade ou categoria.

   - Selecione **salvar em páginas do relatório** para salvar os resultados do relatório como um relatório que é acessível na página do **relatório** . Isso permitirá que os usuários do RO executem o relatório que você criou.

   - Selecione **filtros (Adicionar)** para adicionar mais filtros. Há suporte para solicitações curinga.

   - Especifique um grupo de dispositivos (definido no mapa do dispositivo).

   - Especifique um endereço IP.

   - Especifique uma porta.

   - Especifique um endereço MAC.

4. Clique em **Salvar**. Os resultados do relatório são abertos na página de **mineração de dados** .

:::image type="content" source="media/how-to-generate-reports/data-mining-page.png" alt-text="Relatar resultados como visto na página de mineração de dados.":::

### <a name="manage-data-mining-reports"></a>Gerenciar relatórios de mineração de dados

A tabela a seguir descreve as opções de gerenciamento para Data Mining:

| Imagem do ícone | Descrição |
|--|--|
| :::image type="icon" source="media/how-to-generate-reports/edit-a-simulation-icon.png" border="false"::: | Edite os parâmetros do relatório. |
| :::image type="icon" source="media/how-to-generate-reports/export-as-pdf-icon.png" border="false"::: | Exportar como PDF. |
| :::image type="icon" source="media/how-to-generate-reports/csv-export-icon.png" border="false"::: |Exportar como CSV. |
| :::image type="icon" source="media/how-to-generate-reports/information-icon.png" border="false"::: | Mostrar informações adicionais, como a data da última modificação. Use esse recurso para criar um instantâneo de resultado da consulta. Talvez seja necessário fazer isso para uma investigação mais detalhada com os líderes da equipe ou os analistas do SOC, por exemplo. |
| :::image type="icon" source="media/how-to-generate-reports/pin-icon.png" border="false"::: | Exiba na página **relatórios** ou oculte na página **relatórios** . :::image type="content" source="media/how-to-generate-reports/hide-reports-page.png" alt-text="Oculte ou revele seus relatórios."::: |
| :::image type="icon" source="media/how-to-generate-reports/delete-simulation-icon.png" border="false"::: | Exclua o relatório. |

#### <a name="create-customized-directories"></a>Criar diretórios personalizados 

Você pode organizar as informações extensivas para consultas de mineração de dados Criando diretórios para categorias. Por exemplo, você pode criar diretórios para protocolos ou locais.

Para criar um novo diretório:

1. Selecione :::image type="icon" source="media/how-to-generate-reports/plus-icon.png" border="false"::: para adicionar um novo diretório.

2. Selecione **novo diretório** para exibir o novo formulário de diretório.

3. Nomeie o novo diretório.

4. Arraste os relatórios necessários para o novo diretório. A qualquer momento, você pode arrastar o relatório de volta para o modo de exibição principal.

5. Clique com o botão direito do mouse no novo diretório para abri-lo, editá-lo ou excluí-lo.

#### <a name="create-snapshots-of-report-results"></a>Criar instantâneos dos resultados do relatório

Talvez seja necessário salvar determinados resultados da consulta para uma investigação mais detalhada. Por exemplo, talvez seja necessário compartilhar resultados com várias equipes de segurança.

Os instantâneos são salvos nos resultados do relatório e não geram consultas dinâmicas.

:::image type="content" source="media/how-to-generate-reports/report-results-report.png" alt-text="Instantâneos.":::

Para criar um instantâneo:

1. Abra o relatório necessário.

2. Selecione o ícone de informações :::image type="icon" source="media/how-to-generate-reports/information-icon.png" border="false"::: .

3. Selecione **obter novo**.

4. Insira um nome para o instantâneo e selecione **salvar**.

:::image type="content" source="media/how-to-generate-reports/take-a-snapshot.png" alt-text="Faça um instantâneo.":::

#### <a name="customize-the-cve-list"></a>Personalizar a lista de CVEs

Você pode personalizar manualmente a lista de CVE da seguinte maneira:

  - Incluir/excluir CVEs

  - Alterar a pontuação de CVE

Para executar alterações manuais no relatório de CVE:

1.  No menu lateral, selecione **mineração de dados**.

2. Selecione :::image type="icon" source="media/how-to-generate-reports/plus-icon.png" border="false"::: no canto superior esquerdo da janela de **mineração de dados** . Em seguida, selecione **novo relatório**.

   :::image type="content" source="media/how-to-generate-reports/create-a-new-report-screen.png" alt-text="Crie um novo relatório.":::

3. No painel esquerdo, selecione uma das seguintes opções:

   - **Vulnerabilidades conhecidas**: seleciona ambas as opções e apresenta resultados nas duas tabelas do relatório, uma com CVEs e outra com CVEs excluído.

   - **CVEs**: Selecione esta opção para apresentar uma lista de todos os CVEs.

   - **CVEs excluído**: Selecione esta opção para apresentar uma lista de todos os CVEs excluídos.

4. Preencha as informações de **nome** e **Descrição** e selecione **salvar**. O novo relatório é exibido na janela de **mineração de dados** .

5. Para excluir CVEs, abra o relatório de mineração de dados para CVEs. A lista de todos os CVEs é exibida.

   :::image type="content" source="media/how-to-generate-reports/cves.png" alt-text="Relatório C V E.":::

6. Para habilitar a seleção de itens na lista, selecione :::image type="icon" source="media/how-to-generate-reports/enable-selecting-icon.png" border="false"::: e selecione o CVEs que você deseja personalizar. A barra de **operações** aparece na parte inferior.

   :::image type="content" source="media/how-to-generate-reports/operations-bar-appears.png" alt-text="Captura de tela da barra de operações de mineração de dados.":::

7. Selecione o CVEs que você deseja excluir e, em seguida, selecione **excluir registros**. O CVEs que você selecionou não aparece na lista de CVEs e aparecerá na lista de CVEs excluídos quando você gerar um.

8. Para incluir o CVEs excluído na lista de CVEs, gere o relatório para CVEs excluídos e exclua dessa lista os itens que você deseja incluir de volta na lista de CVEs.

9. Selecione o CVEs no qual você deseja alterar a pontuação e, em seguida, selecione **Atualizar Pontuação de CVE**.

   :::image type="content" source="media/how-to-generate-reports/set-new-score-screen.png" alt-text="Atualize a pontuação de CVE.":::

10. Insira a nova pontuação e selecione **OK**. A pontuação atualizada é exibida no CVEs que você selecionou.

### <a name="reports-based-on-data-mining"></a>Relatórios com base em Data Mining

Os relatórios refletem informações geradas por Data Mining resultados da consulta. Isso inclui relatórios de Data Mining padrão, que estão disponíveis no modo de exibição relatórios. Os analistas de administrador e segurança também podem gerar consultas de Data Mining personalizadas e salvá-las como relatórios. Esses relatórios também estão disponíveis para usuários do RO.

Para gerar um relatório:

1. Selecione **relatórios** no menu lateral.

2. Escolha o relatório necessário a ser exibido. A escolha pode ser relatórios **personalizados** ou **gerados automaticamente** , como comandos de **programação** e **acesso remoto**.

3. Você pode exportar o relatório selecionando um dos ícones no canto superior direito da tela:

   :::image type="icon" source="media/how-to-generate-reports/export-to-pdf-icon.png" border="false"::: Exportar para um arquivo PDF.

   :::image type="icon" source="media/how-to-generate-reports/export-to-csv-icon.png" border="false"::: Exportar para um arquivo CSV.

> [!NOTE] 
> O usuário RO pode ver apenas os relatórios criados para eles.

:::image type="content" source="media/how-to-generate-reports/select-a-report-screen.png" alt-text="Selecione o relatório a ser gerado.":::

:::image type="content" source="media/how-to-generate-reports/remote-access-report.png" alt-text="Relatório de acesso remoto gerado.":::

## <a name="reports-for-sensor-trends-and-statistics"></a>Relatórios para estatísticas e tendências do sensor

Você pode criar gráficos de widgets e gráficos de pizza para obter informações sobre as tendências e as estatísticas da rede. Os widgets podem ser agrupados em painéis definidos pelo usuário.

> [!NOTE]
> Somente administradores e analistas de segurança podem executar os procedimentos nesta seção.

Para ver painéis e widgets, selecione **tendências & estatísticas** no menu lateral.

:::image type="content" source="media/how-to-generate-reports/investigation-screenshot.png" alt-text="Captura de tela de uma investigação.":::

O painel consiste em widgets que descrevem graficamente os seguintes tipos de informações:

- Tráfego por porta
- Largura de banda do canal
- Largura de banda total
- Conexão TCP ativa
- Dispositivos:
  - Novos dispositivos
  - Dispositivos ocupados
  - Dispositivos por fornecedor
  - Dispositivos por sistema operacional
  - Dispositivos desconectados
- Descartar conectividade por horas
- Alertas para incidentes por tipo
- Acesso à tabela do banco de dados
- Widgets de desseção de protocolo
- Ethernet e endereço IP:
  - Tráfego de endereço IP e Ethernet pelo serviço CIP
  - Tráfego de endereço IP e Ethernet por classe CIP
  - Tráfego de endereço IP e Ethernet por comando
- OPC
  - Operações de gerenciamento superior do OPC
  - Operações de e/s superiores do OPC
- Siemens S7:
  - Tráfego S7 por função de controle
  - Tráfego S7 por subfunção
- SRTP
  - Tráfego de SRTP por código de serviço
  - Erros de SRTP por dia
- SuiteLink:
  - SuiteLink principais marcas consultadas
  - Comportamento de marca numérica SuiteLink
- Tráfego IEC-60870 por ASDU
- Tráfego DNP3 por função
- Tráfego de MMS por serviço
- Tráfego Modbus por função
- Tráfego OPC-UA por serviço

> [!NOTE]
>  A hora nos widgets é definida de acordo com o tempo do sensor.

## <a name="reports-for-the-on-premises-management-console"></a>Relatórios para o console de gerenciamento local

O console de gerenciamento local permite gerar relatórios para cada sensor conectado a ele. Os relatórios são baseados em consultas de mineração de dados de sensor que são executadas.

Você pode gerar os seguintes relatórios:

- **Dispositivos ativos (últimas 24 horas)**: apresenta uma lista de dispositivos que mostram a atividade de rede em um período de 24 horas.

- **Dispositivos não ativos (últimos 7 dias)**: apresenta uma lista de dispositivos que não mostram nenhuma atividade de rede nos últimos sete dias.

- **Comandos de programação**: apresenta uma lista de dispositivos que enviaram comandos de programação nas últimas 24 horas.

- **Acesso remoto**: apresenta uma lista de dispositivos que as fontes remotas acessadas nas últimas 24 horas.

:::image type="content" source="media/how-to-generate-reports/reports-view.png" alt-text="Captura de tela da exibição de relatórios.":::

Quando você escolhe o sensor no console de gerenciamento local, todos os relatórios personalizados configurados nesse sensor aparecem na lista de relatórios. Para cada sensor, você pode gerar um relatório padrão ou um relatório personalizado configurado nesse sensor.

Para gerar um relatório:

1. No painel esquerdo, selecione **relatórios**. A janela **relatórios** é exibida.

2. Na lista suspensa **sensores** , selecione o sensor para o qual você deseja gerar o relatório.

   :::image type="content" source="media/how-to-generate-reports/sensor-drop-down-list.png" alt-text="Captura de tela da exibição de sensores.":::

3. Na lista suspensa à direita, selecione o relatório que deseja gerar.

4. Para criar um PDF dos resultados do relatório, selecione :::image type="icon" source="media/how-to-generate-reports/pdf-report-icon.png" border="false"::: .

## <a name="risk-assessment-reports-for-the-on-premises-management-console"></a>Relatórios de avaliação de risco para o console de gerenciamento local

Gere um relatório de avaliação de risco para cada sensor conectado ao seu console de gerenciamento local. Este relatório fornece informações sobre cada uma das redes que seus sensores estão monitorando.

Os relatórios de avaliação de risco permitem gerar uma pontuação de segurança para cada dispositivo de rede, bem como uma pontuação de segurança de rede geral. A pontuação geral se baseia na inspeção profunda de pacotes, nos mecanismos de modelagem comportamental e em um design de máquina de estado SCADA específico. Uma ampla gama de outras informações está disponível. Por exemplo:

- Problemas de configuração

- Vulnerabilidade do dispositivo priorizada por nível de segurança

- Problemas de segurança de rede

- Problemas operacionais de rede

- Vetores de ataque

- Conexões com redes ICS

- Conexões com a Internet

- Indicadores de malware industrial

- Problemas de protocolo

O relatório fornece recomendações de mitigação que ajudarão você a melhorar sua pontuação de segurança.

- Dispositivos seguros: dispositivos com uma pontuação de segurança acima de 90%.

- **Dispositivos vulneráveis**: dispositivos com uma pontuação de segurança abaixo de 70 por cento.

- **Dispositivos que precisam de melhoria**: dispositivos com uma pontuação de segurança entre 70% e 89%.

Para criar um relatório:

1. Selecione **avaliação de risco** no menu lateral.

2. Selecione um sensor na lista suspensa **selecionar sensor** .

3. Selecione **gerar relatório**.

4. Selecione **baixar** na seção **relatórios arquivados** .

Para importar um logotipo da empresa:

- Selecione **importar logotipo**.

:::image type="content" source="media/how-to-generate-reports/import-logo-screenshot.png" alt-text="Importe seu logotipo por meio da exibição de avaliação de risco.":::

## <a name="see-also"></a>Consulte também
[Trabalhar com exibições de mapa do site](how-to-gain-insight-into-global-regional-and-local-threats.md#work-with-site-map-views)
