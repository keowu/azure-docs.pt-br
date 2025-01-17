---
title: 'Início Rápido: Proteger uma API Web ASP.NET Core com a plataforma de identidade da Microsoft | Azure'
titleSuffix: Microsoft identity platform
description: Neste guia de início rápido, você baixará e modificará um exemplo de código que demonstra como proteger uma API Web ASP.NET Core usando a plataforma de identidade da Microsoft para autorização.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 09/22/2020
ms.author: jmprieur
ms.custom: devx-track-csharp, scenarios:getting-started, languages:aspnet-core
ms.openlocfilehash: e85e433e1b1b31470fc8d7dee24353fd719b64e2
ms.sourcegitcommit: 3ea45bbda81be0a869274353e7f6a99e4b83afe2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97031174"
---
# <a name="quickstart-protect-an-aspnet-core-web-api-with-microsoft-identity-platform"></a>Início Rápido: Proteger uma API Web ASP.NET Core com a plataforma de identidade da Microsoft

Neste guia de início rápido, você baixará um exemplo de código da API Web ASP.NET Core e examinará o código que restringe o acesso aos recursos somente às contas autorizadas. O exemplo dá suporte à autorização de contas Microsoft pessoais e contas em qualquer organização do Azure AD (Azure Active Directory).

> [!div renderon="docs"]
> ## <a name="prerequisites"></a>Pré-requisitos
>
> - Uma conta do Azure com uma assinatura ativa. [Crie uma conta gratuitamente](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
> - [Locatário do Azure Active Directory](quickstart-create-new-tenant.md)
> - [SDK do .NET Core 3.1 ou posterior](https://dotnet.microsoft.com/)
> - [Visual Studio 2019](https://visualstudio.microsoft.com/vs/) ou [Visual Studio Code](https://code.visualstudio.com/)
>
> ## <a name="step-1-register-the-application"></a>Etapa 1: Registrar o aplicativo
>
> Primeiro, registre a API Web no seu locatário do Azure AD e adicione um escopo seguindo estas etapas:
>
> 1. Entre no [portal do Azure](https://portal.azure.com).
> 1. Se você tem acesso a vários locatários, use o filtro **Diretório + assinatura** :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false"::: no menu superior para selecionar o locatário no qual você deseja registrar um aplicativo.
> 1. Pesquise **Azure Active Directory** e selecione-o.
> 1. Em **Gerenciar**, selecione **Registros de aplicativo** > **Novo registro**.
> 1. Insira um **Nome** para seu aplicativo, por exemplo, `AspNetCoreWebApi-Quickstart`. Os usuários do seu aplicativo podem ver esse nome e você pode alterá-lo mais tarde.
> 1. Selecione **Registrar**.
> 1. Em **Gerenciar**, selecione **Expor uma API** > **Adicionar um escopo**. Aceite o **URI da ID do Aplicativo** padrão selecionando **Salvar e continuar** e insira os seguintes detalhes:
>    - **Nome do escopo**: `access_as_user`
>    - **Quem pode consentir?** : **Administradores e usuários**
>    - **Nome de exibição de consentimento do administrador**: `Access AspNetCoreWebApi-Quickstart`
>    - **Descrição do consentimento do administrador:** `Allows the app to access AspNetCoreWebApi-Quickstart as the signed-in user.`
>    - **Nome de exibição do consentimento do usuário**: `Access AspNetCoreWebApi-Quickstart`
>    - **Descrição do consentimento do usuário**: `Allow the application to access AspNetCoreWebApi-Quickstart on your behalf.`
>    - **Estado**: **Enabled**
> 1. Selecione **Adicionar escopo** para concluir a adição do escopo.

## <a name="step-2-download-the-aspnet-core-project"></a>Etapa 2: Baixar o projeto do ASP.NET Core

> [!div renderon="docs"]
> [Baixe a solução do ASP.NET Core](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2/archive/aspnetcore3-1.zip) no GitHub.

> [!div renderon="docs"]
> ## <a name="step-3-configure-the-aspnet-core-project"></a>Etapa 3: Configurar o projeto do ASP.NET Core
>
> Nesta etapa, configure o código de exemplo para trabalhar com o registro do aplicativo criado anteriormente.
>
> 1. Extraia o arquivo .zip para uma pasta próxima à raiz da unidade. Por exemplo, em *C:\Azure-Samples*.
> 1. Abra a solução na pasta *webapi* no editor de códigos.
> 1. Abra o arquivo *appsettings.json* e modifique o seguinte:
>
>    ```json
>    "ClientId": "Enter_the_Application_Id_here",
>    "TenantId": "Enter_the_Tenant_Info_Here"
>    ```
>
>    - Substitua `Enter_the_Application_Id_here` pela **ID do aplicativo (cliente)** referente ao aplicativo registrado no portal do Azure. Você pode encontrar **ID do aplicativo (cliente)** na página **Visão geral** do aplicativo.
>    - Substitua `Enter_the_Tenant_Info_Here` por um dos seguintes:
>       - Se o aplicativo der suporte a **Contas somente neste diretório organizacional**, substitua esse valor pela **ID do diretório (locatário)** (um GUID) ou pelo **nome do locatário** (por exemplo, `contoso.onmicrosoft.com`). Você pode encontrar a **ID do diretório (locatário)** na página **Visão geral** do aplicativo.
>       - Se seu aplicativo dá suporte a **Contas em qualquer diretório organizacional**, substitua esse valor por `organizations`
>       - Se o aplicativo der suporte a **Todos os usuários de contas Microsoft**, defina esse valor como `common`
>
> Para este guia de início rápido, não altere nenhum outro valor no arquivo *appsettings.json*.

## <a name="how-the-sample-works"></a>Como o exemplo funciona

A API Web recebe um token de um aplicativo cliente, e o código na API Web valida o token. Esse cenário é explicado mais detalhadamente em [Cenário: API Web protegida](scenario-protected-web-api-overview.md).

### <a name="startup-class"></a>Classe de inicialização

O middleware *Microsoft.AspNetCore.Authentication* usa a classe `Startup` executada quando o processo de hospedagem é inicializado. No método `ConfigureServices`, o método de extensão `AddMicrosoftIdentityWebApi` fornecido pelo *Microsoft.Identity.Web* é chamado.

```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
                .AddMicrosoftIdentityWebApi(Configuration, "AzureAd");
    }
```

O método `AddAuthentication()` configura o serviço para adicionar a autenticação baseada em JwtBearer.

A linha que contém `.AddMicrosoftIdentityWebApi` adiciona a autorização da plataforma de identidade da Microsoft à sua API Web. Em seguida, ela é configurada para validar os tokens de acesso emitidos pelo ponto de extremidade da plataforma de identidade da Microsoft com base nas informações na seção `AzureAD` do arquivo de configuração *appsettings.json*:

| chave *appsettings.json* | Descrição                                                                                                                                                          |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ClientId`             | **ID do aplicativo (cliente)** referente ao aplicativo registrado no portal do Azure.                                                                                       |
| `Instance`             | Ponto de extremidade do STS (serviço de token de segurança) para o usuário se autenticar. Esse valor geralmente é `https://login.microsoftonline.com/`, indicando a nuvem pública do Azure. |
| `TenantId`             | Nome do seu locatário ou sua ID de locatário (um GUID) ou *comum* para conectar usuários que tenham contas corporativas ou de estudante ou contas pessoais Microsoft.                             |

O método `Configure()` contém dois métodos importantes, `app.UseAuthentication()` e `app.UseAuthorization()`, que habilitam a funcionalidade nomeada:

```csharp
// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    // more code
    app.UseAuthentication();
    app.UseAuthorization();
    // more code
}
```

### <a name="protect-a-controller-a-controllers-method-or-a-razor-page"></a>Proteger um controlador, um método do controlador ou uma página Razor

Você pode proteger um controlador ou métodos do controlador usando o atributo `[Authorize]`. Esse atributo restringe o acesso ao controlador ou aos métodos, permitindo apenas usuários autenticados, ou seja, o desafio de autenticação poderá ser iniciado para acessar o controlador se o usuário não estiver autenticado.

```csharp
namespace webapi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
```

### <a name="validate-the-scope-in-the-controller"></a>Validar o escopo no controlador

Em seguida, o código na API verifica se os escopos necessários estão no token usando `HttpContext.VerifyUserHasAnyAcceptedScope(scopeRequiredByApi);`

```csharp
namespace webapi.Controllers
{
    [Authorize]
    [ApiController]
    [Route("[controller]")]
    public class WeatherForecastController : ControllerBase
    {
        // The Web API will only accept tokens 1) for users, and 2) having the "access_as_user" scope for this API
        static readonly string[] scopeRequiredByApi = new string[] { "access_as_user" };

        [HttpGet]
        public IEnumerable<WeatherForecast> Get()
        {
            HttpContext.VerifyUserHasAnyAcceptedScope(scopeRequiredByApi);

            // some code here
        }
    }
}
```

[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]

## <a name="next-steps"></a>Próximas etapas

O repositório GitHub que contém este exemplo de código ASP.NET Core da API Web inclui instruções e mais exemplos de código que mostram como:

- Adicionar autenticação a uma nova API Web ASP.NET Core
- Chamar a API Web em um aplicativo de desktop
- Chamar APIs downstream como o Microsoft Graph e outras APIs da Microsoft

> [!div class="nextstepaction"]
> [Tutoriais da API Web ASP.NET Core no GitHub](https://github.com/Azure-Samples/active-directory-dotnet-native-aspnetcore-v2)
