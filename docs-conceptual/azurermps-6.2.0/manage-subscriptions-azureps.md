---
title: 使用 Azure PowerShell 管理 Azure 订阅 | Microsoft Docs
description: 使用 Azure PowerShell 管理 Azure 订阅
keywords: Azure PowerShell, 订阅
author: sptramer
ms.author: sttramer
manager: carmonm
ms.devlang: powershell
ms.topic: conceptual
ms.date: 03/30/2017
ms.openlocfilehash: 4f066118373c9ea7deffe7c6474552f1ce91cb56
ms.sourcegitcommit: 2eea03b7ac19ad6d7c8097743d33c7ddb9c4df77
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34820589"
---
# <a name="manage-multiple-azure-subscriptions"></a><span data-ttu-id="1ab14-104">管理多个 Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="1ab14-104">Manage multiple Azure subscriptions</span></span>

<span data-ttu-id="1ab14-105">如果是 Azure 的新手，也许只有一个订阅。</span><span class="sxs-lookup"><span data-stu-id="1ab14-105">If you are brand new to Azure, you probably only have a single subscription.</span></span> <span data-ttu-id="1ab14-106">但如果使用 Azure 有一段时间，可能已创建了多个 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="1ab14-106">But if you have been using Azure for a while, you may have created multiple Azure subscriptions.</span></span> <span data-ttu-id="1ab14-107">可将 Azure PowerShell 配置为针对特定的订阅执行命令。</span><span class="sxs-lookup"><span data-stu-id="1ab14-107">You can configure Azure PowerShell to execute commands against a particular subscription.</span></span>

1. <span data-ttu-id="1ab14-108">获取帐户中所有订阅的列表。</span><span class="sxs-lookup"><span data-stu-id="1ab14-108">Get a list of all subscriptions in your account.</span></span>

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

    Environment           : AzureCloud
    Account               : username@contoso.com
    TenantId              : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionId        : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionName      : My DevTest Subscription
    CurrentStorageAccount :

    Environment           : AzureCloud
    Account               : username@contoso.com
    TenantId              : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionId        : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionName      : My Demos
    CurrentStorageAccount :
    ```

2. <span data-ttu-id="1ab14-109">设置默认值。</span><span class="sxs-lookup"><span data-stu-id="1ab14-109">Set the default.</span></span>

    ```azurepowershell-interactive
    Select-AzureRmSubscription -SubscriptionName "My Demos"
    ```

3. <span data-ttu-id="1ab14-110">通过运行 `Get-AzureRmContext` cmdlet 验证更改。</span><span class="sxs-lookup"><span data-stu-id="1ab14-110">Verify the change by running the `Get-AzureRmContext` cmdlet.</span></span>

    ```azurepowershell-interactive
    Get-AzureRmContext
    ```

    ```output
    Environment           : AzureCloud
    Account               : username@contoso.com
    TenantId              : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionId        : XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
    SubscriptionName      : My Demos
    CurrentStorageAccount :
    ```

<span data-ttu-id="1ab14-111">设置默认订阅后，所有后续 Azure PowerShell 命令将针对此订阅运行。</span><span class="sxs-lookup"><span data-stu-id="1ab14-111">Once you set your default subscription, all subsequent Azure PowerShell commands run against this subscription.</span></span>