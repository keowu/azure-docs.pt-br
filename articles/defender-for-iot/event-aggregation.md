---
title: Agregação de eventos
description: Saiba mais sobre o defender para agregação de eventos de IoT.
services: defender-for-iot
ms.service: defender-for-iot
documentationcenter: na
author: mlottner
manager: rkarlin
editor: ''
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/03/2020
ms.author: mlottner
ms.openlocfilehash: c823f0034db7d5fbe1f6b46f6af74e9fa374a6de
ms.sourcegitcommit: 8be279f92d5c07a37adfe766dc40648c673d8aa8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97832362"
---
# <a name="defender-for-iot-event-aggregation"></a>Agregação de evento do defender para IoT

Os agentes de segurança do defender para IoT coletam dados e eventos do sistema do seu dispositivo local e enviam esses dados para a nuvem do Azure para processamento e análise. O agente de segurança coleta muitos tipos de eventos de dispositivo, incluindo novo processo e novos eventos de conexão. Os novos eventos de processo e de conexão podem ocorrer legitimamente com frequência em um dispositivo em um segundo e, embora sejam importantes para segurança robusta e abrangente, o número de mensagens que os agentes de segurança são forçados a enviar pode atingir rapidamente ou exceder a cota e os limites de custos do Hub IoT. No entanto, esses eventos contêm informações de segurança altamente valiosas que são cruciais para proteger seu dispositivo.

Para reduzir a cota e os custos adicionais enquanto mantém seus dispositivos protegidos, o defender for IoT Agents agrega esses tipos de eventos.

A agregação **de eventos é ativada** por padrão e, embora não seja recomendado, pode ser **desativada manualmente a qualquer** momento.

Atualmente, a agregação está disponível para os seguintes tipos de eventos:

* ProcessCreate
* ConnectionCreate
* ProcessTerminate (somente Windows)

## <a name="how-does-event-aggregation-work"></a>Como funciona a agregação de eventos?

Quando a agregação de **eventos é deixada**, o defender for IOT Agents agrega eventos para o período de intervalo ou a janela de tempo.
Depois que o período de intervalo tiver passado, o agente enviará os eventos agregados para a nuvem do Azure para análise posterior.
Os eventos agregados são armazenados na memória até serem enviados para a nuvem do Azure.

Para reduzir a superfície de memória do agente, sempre que o agente coletar um evento idêntico para um que já esteja sendo mantido na memória, o agente aumentará a contagem de acesso desse evento específico. Quando a janela de tempo de agregação passa, o agente envia a contagem de ocorrências de cada tipo específico de evento ocorrido. A agregação de eventos é simplesmente a agregação das contagens de acertos de cada tipo de evento coletado.

Os eventos são considerados idênticos somente quando as seguintes condições são atendidas:

* Eventos de ProcessCreate-quando **CommandLine**, **executável**, **username** e **userid** são idênticos
* Eventos de ConnectionCreate-quando **CommandLine**, **userid**, **Direction**, **endereço local**, **endereço remoto**, * * protocolo e **porta de destino** são idênticos
* Eventos de ProcessTerminate-quando o **status** **executável** e de saída são idênticos

### <a name="working-with-aggregated-events"></a>Trabalhando com eventos agregados

Durante a agregação, as propriedades de evento que não são agregadas são descartadas e aparecem no log Analytics com um valor de 0.

* Eventos ProcessCreate- **ProcessId** e **parentProcessId** são definidos como 0
* Eventos ConnectionCreate- **ProcessId** e **porta de origem** são definidos como 0

## <a name="event-aggregation-based-alerts"></a>Alertas baseados em agregação de eventos

Após a análise, o defender para IoT cria alertas de segurança para eventos agregados suspeitos. Os alertas criados a partir de eventos agregados aparecem apenas uma vez para cada evento agregado.

A hora de início da agregação, a hora de término e a contagem de acesso para cada evento são registradas no campo **ExtraDetails** de evento dentro log Analytics para uso durante as investigações.

Cada evento agregado representa um período de 24 horas de alertas coletados. Usando o menu de opções de evento no canto superior esquerdo de cada evento, você pode **descartar** cada evento agregado individual.

## <a name="event-aggregation-twin-configuration"></a>Configuração de configurações de agregação de eventos

Faça alterações na configuração do defender para agregação de eventos de IoT dentro do [objeto de configuração do agente](how-to-agent-configuration.md) da identidade de módulo de pesquisa de módulos do módulo **azureiotsecurity** .

| Nome da configuração | Valores possíveis | Detalhes | Comentários |
|:-----------|:---------------|:--------|:--------|
| aggregationEnabledProcessCreate | booleano | Habilitar/desabilitar a agregação de eventos para processar eventos de criação |
| aggregationIntervalProcessCreate | Cadeia de caracteres TimeSpan ISO8601 | Intervalo de agregação para eventos de criação de processo |
| aggregationEnabledConnectionCreate | booleano| Habilitar/desabilitar a agregação de eventos para conexão criar eventos |
| aggregationIntervalConnectionCreate | Cadeia de caracteres TimeSpan ISO8601 | Intervalo de agregação para eventos de criação de conexão |
| aggregationEnabledProcessTerminate | booleano | Habilitar/desabilitar a agregação de eventos para processar eventos de término | Somente Windows|
| aggregationIntervalProcessTerminate | Cadeia de caracteres TimeSpan ISO8601 | Intervalo de agregação para eventos de término do processo | Somente Windows|
|

## <a name="default-configurations-settings"></a>Definições de configurações padrão

| Nome da configuração | Valores padrão |
|:-----------|:---------------|
| aggregationEnabledProcessCreate | true |
| aggregationIntervalProcessCreate | PT1H|
| aggregationEnabledConnectionCreate | true |
| aggregationIntervalConnectionCreate | PT1H|
| aggregationEnabledProcessTerminate | true |
| aggregationIntervalProcessTerminate | PT1H|
|

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu sobre a agregação do agente de segurança do defender para IoT e as opções de configuração de evento disponíveis.

Para continuar a introdução à implantação do defender para IoT, use os seguintes artigos:

- Entender os [métodos de autenticação do agente de segurança](concept-security-agent-authentication-methods.md)
- Selecionar e implantar um [agente de segurança](how-to-deploy-agent.md)
- Examinar os pré-requisitos do [sistema](quickstart-system-prerequisites.md) do defender para IOT
- Saiba como [habilitar o defender para o serviço de IOT em seu hub IOT](quickstart-onboard-iot-hub.md)
- Saiba mais sobre o serviço do [defender for IOT FAQ](resources-frequently-asked-questions.md)
