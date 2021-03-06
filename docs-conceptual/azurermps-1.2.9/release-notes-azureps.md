---
title: Azure PowerShell 更改日志 | Microsoft Docs
description: 下面提供了对 Azure PowerShell 最新版本所做更改的历史记录。
author: sptramer
ms.author: sttramer
manager: carmonm
ms.devlang: powershell
ms.topic: conceptual
ms.workload: ''
ms.date: 05/18/2017
ms.openlocfilehash: 91d97260568a36e1135196899503fb0c8e1c6731
ms.sourcegitcommit: c98e3a21037ebd82936828bcb544eed902b24212
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "34853009"
---
# <a name="release-notes"></a>发行说明

下面是此版本中对 Azure PowerShell 所做的更改列表。

## <a name="version-129"></a>版本 1.2.9

此版本的更改

* AzureRm.AzureStackAdmin 模块
    + 更改了 Add-AzureRmResourceProviderRegistration cmdlet，以便支持管理员 Azure Resource Manager 和租户 Azure Resource Manager 的拆分。 添加了新参数 -ResourceManagerType。
    + 从每个 cmdlet 中删除了参数 -AdminUri、-ApiVersion、-SubscriptionId 和 -Token。 我们一直在列显警告消息，指出这些参数即将弃用，并且现在已被删除。
* AzureStackStorage 模块
    + 添加了新的 cmdlet 用于支持容器迁移方案。
    + 删除了引用内部组件和基础功能的 cmdlet。
* AzureRM.BootStrapper
    + 创建了新的模块用于通过版本配置文件管理 Azure PowerShell cmdlet 的版本