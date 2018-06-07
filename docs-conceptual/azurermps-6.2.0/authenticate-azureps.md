---
title: 使用 Azure PowerShell 登录
description: 使用 Azure PowerShell 登录
services: azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.devlang: powershell
ms.topic: conceptual
ms.date: 05/15/2017
ms.openlocfilehash: f7ed78f9908517661001cad7b3eeae8b732640cc
ms.sourcegitcommit: 2eea03b7ac19ad6d7c8097743d33c7ddb9c4df77
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34819756"
---
# <a name="log-in-with-azure-powershell"></a><span data-ttu-id="a244e-103">使用 Azure PowerShell 登录</span><span class="sxs-lookup"><span data-stu-id="a244e-103">Log in with Azure PowerShell</span></span>

<span data-ttu-id="a244e-104">Azure PowerShell 支持多种登录方法。</span><span class="sxs-lookup"><span data-stu-id="a244e-104">Azure PowerShell supports multiple login methods.</span></span> <span data-ttu-id="a244e-105">最简单的初始方法是通过命令行以交互方式登录。</span><span class="sxs-lookup"><span data-stu-id="a244e-105">The simplest way to get started is to log in interactively at the command line.</span></span>

## <a name="interactive-log-in"></a><span data-ttu-id="a244e-106">交互式登录</span><span class="sxs-lookup"><span data-stu-id="a244e-106">Interactive log in</span></span>

1. <span data-ttu-id="a244e-107">键入 `Connect-AzureRmAccount`。</span><span class="sxs-lookup"><span data-stu-id="a244e-107">Type `Connect-AzureRmAccount`.</span></span> <span data-ttu-id="a244e-108">此时会出现一个对话框，要求输入 Azure 凭据。</span><span class="sxs-lookup"><span data-stu-id="a244e-108">You will get dialog box asking for your Azure credentials.</span></span>

2. <span data-ttu-id="a244e-109">键入与帐户关联的电子邮件地址和密码。</span><span class="sxs-lookup"><span data-stu-id="a244e-109">Type the email address and password associated with your account.</span></span> <span data-ttu-id="a244e-110">Azure 将对凭据信息进行身份验证和保存，然后关闭该窗口。</span><span class="sxs-lookup"><span data-stu-id="a244e-110">Azure authenticates and saves the credential information, and then closes the window.</span></span>

## <a name="log-in-with-a-service-principal"></a><span data-ttu-id="a244e-111">使用服务主体登录</span><span class="sxs-lookup"><span data-stu-id="a244e-111">Log in with a service principal</span></span>

<span data-ttu-id="a244e-112">使用服务主体能够创建可用于处理资源的非交互式帐户。</span><span class="sxs-lookup"><span data-stu-id="a244e-112">Service principals provide a way for you to create non-interactive accounts that you can use to manipulate resources.</span></span> <span data-ttu-id="a244e-113">服务主体类似于可以使用 Azure Active Directory 向其应用规则的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="a244e-113">Service principals are like user accounts to which you can apply rules using Azure Active Directory.</span></span> <span data-ttu-id="a244e-114">通过授予服务主体所需的最低权限，可以确保自动化脚本更加安全。</span><span class="sxs-lookup"><span data-stu-id="a244e-114">By granting the minimum permissions needed to a service principal, you can ensure your automation scripts are even more secure.</span></span>

1. <span data-ttu-id="a244e-115">如果尚未创建服务主体，请[创建一个](create-azure-service-principal-azureps.md)。</span><span class="sxs-lookup"><span data-stu-id="a244e-115">If you don't already have a service principal, [create one](create-azure-service-principal-azureps.md).</span></span>

2. <span data-ttu-id="a244e-116">使用服务主体登录。</span><span class="sxs-lookup"><span data-stu-id="a244e-116">Log in with the service principal.</span></span>

    ```azurepowershell-interactive
    Connect-AzureRmAccount -ServicePrincipal -ApplicationId  "http://my-app" -Credential $pscredential -TenantId $tenantid
    ```

    <span data-ttu-id="a244e-117">要获取 TenantId，请以交互方式登录，并从订阅中获取 TenantId。</span><span class="sxs-lookup"><span data-stu-id="a244e-117">To get your TenantId, log in interactively and then get the TenantId from your subscription.</span></span>

    ```azurepowershell-interactive
    Get-AzureRmSubscription
    ```

    ```output
    Environment           : AzureCloud
    Account               : username@contoso.com
    TenantId              : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionId        : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionName      : My Production Subscription
    CurrentStorageAccount :
    ```

### <a name="log-in-using-an-azure-vm-managed-service-identity"></a><span data-ttu-id="a244e-118">使用 Azure VM 托管服务标识登录</span><span class="sxs-lookup"><span data-stu-id="a244e-118">Log in using an Azure VM Managed Service Identity</span></span>

<span data-ttu-id="a244e-119">托管服务标识 (MSI) 是 Azure Active Directory 的预览版功能。</span><span class="sxs-lookup"><span data-stu-id="a244e-119">Managed Service Identity (MSI) is a preview feature of Azure Active Directory.</span></span> <span data-ttu-id="a244e-120">可以使用 MSI 服务主体进行登录，并获取仅限应用的访问令牌来访问其他资源。</span><span class="sxs-lookup"><span data-stu-id="a244e-120">You can use an MSI service principal for sign-in, and acquire an app-only access token to access other resources.</span></span>

<span data-ttu-id="a244e-121">有关 MSI 的详细信息，请参阅[如何使用 Azure VM 托管服务标识 (MSI) 登录和获取令牌](/azure/active-directory/msi-how-to-get-access-token-using-msi)。</span><span class="sxs-lookup"><span data-stu-id="a244e-121">For more information about MSI, see [How to use an Azure VM Managed Service Identity (MSI) for sign-in and token acquisition](/azure/active-directory/msi-how-to-get-access-token-using-msi).</span></span>

## <a name="log-in-to-another-cloud"></a><span data-ttu-id="a244e-122">登录到其他云</span><span class="sxs-lookup"><span data-stu-id="a244e-122">Log in to another Cloud</span></span>

<span data-ttu-id="a244e-123">Azure 云服务提供遵循各政府的数据处理法规的不同环境。</span><span class="sxs-lookup"><span data-stu-id="a244e-123">Azure cloud services provide different environments that adhere to the data-handling regulations of various governments.</span></span> <span data-ttu-id="a244e-124">如果 Azure 帐户在政府云中，登录时需指定环境。</span><span class="sxs-lookup"><span data-stu-id="a244e-124">If your Azure account is in one the government clouds, you need to specify the environment when you sign in.</span></span> <span data-ttu-id="a244e-125">例如，如果帐户在中国云中，请使用以下命令登录：</span><span class="sxs-lookup"><span data-stu-id="a244e-125">For example, if you account is in the China cloud you sign on using the following command:</span></span>

```azurepowershell-interactive
Connect-AzureRmAccount -Environment AzureChinaCloud
```

<span data-ttu-id="a244e-126">使用以下命令获取可用环境的列表：</span><span class="sxs-lookup"><span data-stu-id="a244e-126">Use the following command to get a list of available environments:</span></span>

```azurepowershell-interactive
Get-AzureRmEnvironment | Select-Object Name
```

```output
Name
----
AzureCloud
AzureChinaCloud
AzureUSGovernment
AzureGermanCloud
```

## <a name="learn-more-about-managing-azure-role-based-access"></a><span data-ttu-id="a244e-127">详细了解如何管理 Azure 基于角色的访问</span><span class="sxs-lookup"><span data-stu-id="a244e-127">Learn more about managing Azure role-based access</span></span>

<span data-ttu-id="a244e-128">有关 Azure 中的身份验证和订阅管理的详细信息，请参阅[管理帐户、订阅和管理角色](/azure/active-directory/role-based-access-control-configure)。</span><span class="sxs-lookup"><span data-stu-id="a244e-128">For more information about authentication and subscription management in Azure, see [Manage Accounts, Subscriptions, and Administrative Roles](/azure/active-directory/role-based-access-control-configure).</span></span>

<span data-ttu-id="a244e-129">用于角色管理的 Azure PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="a244e-129">Azure PowerShell cmdlets for role management</span></span>

* [<span data-ttu-id="a244e-130">Get-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="a244e-130">Get-AzureRmRoleAssignment</span></span>](/powershell/module/AzureRM.Resources/Get-AzureRmRoleAssignment)
* [<span data-ttu-id="a244e-131">Get-AzureRmRoleDefinition</span><span class="sxs-lookup"><span data-stu-id="a244e-131">Get-AzureRmRoleDefinition</span></span>](/powershell/module/AzureRM.Resources/Get-AzureRmRoleDefinition)
* [<span data-ttu-id="a244e-132">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="a244e-132">New-AzureRmRoleAssignment</span></span>](/powershell/module/AzureRM.Resources/New-AzureRmRoleAssignment)
* [<span data-ttu-id="a244e-133">New-AzureRmRoleDefinition</span><span class="sxs-lookup"><span data-stu-id="a244e-133">New-AzureRmRoleDefinition</span></span>](/powershell/module/AzureRM.Resources/New-AzureRmRoleDefinition)
* [<span data-ttu-id="a244e-134">Remove-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="a244e-134">Remove-AzureRmRoleAssignment</span></span>](/powershell/module/AzureRM.Resources/Remove-AzureRmRoleAssignment)
* [<span data-ttu-id="a244e-135">Remove-AzureRmRoleDefinition</span><span class="sxs-lookup"><span data-stu-id="a244e-135">Remove-AzureRmRoleDefinition</span></span>](/powershell/module/AzureRM.Resources/Remove-AzureRmRoleDefinition)
* [<span data-ttu-id="a244e-136">Set-AzureRmRoleDefinition</span><span class="sxs-lookup"><span data-stu-id="a244e-136">Set-AzureRmRoleDefinition</span></span>](/powershell/moduel/AzureRM.Resources/Set-AzureRmRoleDefinition)