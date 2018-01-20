# <a name="breaking-changes-for-microsoft-azure-powershell-400"></a><span data-ttu-id="dd432-101">Microsoft Azure PowerShell 4.0.0 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-101">Breaking changes for Microsoft Azure PowerShell 4.0.0</span></span>

<span data-ttu-id="dd432-102">本文档是面向 Microsoft Azure PowerShell cmdlet 的使用者的重大更改通知和迁移指南。</span><span class="sxs-lookup"><span data-stu-id="dd432-102">This document serves as both a breaking change notification and migration guide for consumers of the Microsoft Azure PowerShell cmdlets.</span></span> <span data-ttu-id="dd432-103">每部分都介绍了重大更改的影响和最简便的迁移路径。</span><span class="sxs-lookup"><span data-stu-id="dd432-103">Each section describes both the impetus for the breaking change and the migration path of least resistance.</span></span> <span data-ttu-id="dd432-104">有关深入的上下文，请参考与每个更改关联的拉取请求。</span><span class="sxs-lookup"><span data-stu-id="dd432-104">For in-depth context, please refer to the pull request associated with each change.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="dd432-105">目录</span><span class="sxs-lookup"><span data-stu-id="dd432-105">Table of Contents</span></span>

- [<span data-ttu-id="dd432-106">计算 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-106">Breaking changes to Compute cmdlets</span></span>](#breaking-changes-to-compute-cmdlets)
- [<span data-ttu-id="dd432-107">EventHub cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-107">Breaking changes to EventHub cmdlets</span></span>](#breaking-changes-to-eventhub-cmdlets)
- [<span data-ttu-id="dd432-108">见解 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-108">Breaking changes to Insights cmdlets</span></span>](#breaking-changes-to-insights-cmdlets)
- [<span data-ttu-id="dd432-109">网络 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-109">Breaking changes to Network cmdlets</span></span>](#breaking-changes-to-network-cmdlets)
- [<span data-ttu-id="dd432-110">ServiceBus cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-110">Breaking changes to ServiceBus cmdlets</span></span>](#breaking-changes-to-servicebus-cmdlets)
- [<span data-ttu-id="dd432-111">Sql cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-111">Breaking changes to Sql cmdlets</span></span>](#breaking-changes-to-sql-cmdlets)
- [<span data-ttu-id="dd432-112">存储 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-112">Breaking changes to Storage cmdlets</span></span>](#breaking-changes-to-storage-cmdlets)
- [<span data-ttu-id="dd432-113">配置文件 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-113">Breaking Changes to Profile Cmdlets</span></span>](#breaking-changes-to-profile-cmdlets)
## <a name="breaking-changes-to-compute-cmdlets"></a><span data-ttu-id="dd432-114">计算 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-114">Breaking changes to Compute cmdlets</span></span>

<span data-ttu-id="dd432-115">此版本影响以下输出类型：</span><span class="sxs-lookup"><span data-stu-id="dd432-115">The following output types were affected this release:</span></span>

### <a name="psvirtualmachine"></a><span data-ttu-id="dd432-116">PSVirtualMachine</span><span class="sxs-lookup"><span data-stu-id="dd432-116">PSVirtualMachine</span></span>
- <span data-ttu-id="dd432-117">`PSVirtualMachine` 对象的顶级属性 `DataDiskNames` 和 `NetworkInterfaceIDs` 已从输出类型中删除。</span><span class="sxs-lookup"><span data-stu-id="dd432-117">Top level properties `DataDiskNames` and `NetworkInterfaceIDs` of nthe `PSVirtualMachine` object have been removed from the output type.</span></span> <span data-ttu-id="dd432-118">这些属性始终在 `PSVirtualMachine` 对象的 `StorageProfile` 和 `NetworkProfile` 属性中提供，并且以后这将是访问它们时需要使用的方式。</span><span class="sxs-lookup"><span data-stu-id="dd432-118">These properties have always been available in the `StorageProfile` and `NetworkProfile` properties of the `PSVirtualMachine` object and will be the way they will need to be accessed going forward.</span></span>
- <span data-ttu-id="dd432-119">此更改影响以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dd432-119">This change affects the following cmdlets:</span></span>
    - `Add-AzureRmVMDataDisk`
    - `Add-AzureRmVMNetworkInterface`
    - `Get-AzureRmVM`
    - `Remove-AzureRmVMDataDisk`
    - `Remove-AzureRmVMNetworkInterface`
    - `Set-AzureRmVMDataDisk`

```powershell
# Old
$vm.DataDiskNames
$vm.NetworkInterfaceIDs

# New
$vm.StorageProfile.DataDisks | Select -Property Name
$vm.NetworkProfile.NetworkInterfaces | Select -Property Id
```

## <a name="breaking-changes-to-eventhub-cmdlets"></a><span data-ttu-id="dd432-120">EventHub cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-120">Breaking changes to EventHub cmdlets</span></span>

<span data-ttu-id="dd432-121">此版本影响以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dd432-121">The following cmdlets were affected this release:</span></span>

### <a name="get-azurermeventhubnamespace"></a><span data-ttu-id="dd432-122">Get-AzureRmEventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="dd432-122">Get-AzureRmEventHubNamespace</span></span>
- <span data-ttu-id="dd432-123">属性 `ResourceGroupName` 已从输出类型 `NamespaceAttributes` 中删除</span><span class="sxs-lookup"><span data-stu-id="dd432-123">The property `ResourceGroupName` has been removed from the output type `NamespaceAttributes`</span></span>

### <a name="new-azurermeventhubnamespace"></a><span data-ttu-id="dd432-124">New-AzureRmEventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="dd432-124">New-AzureRmEventHubNamespace</span></span>
- <span data-ttu-id="dd432-125">属性 `ResourceGroupName` 已从输出类型 `NamespaceAttributes` 中删除</span><span class="sxs-lookup"><span data-stu-id="dd432-125">The property `ResourceGroupName` has been removed from the output type `NamespaceAttributes`</span></span>

## <a name="breaking-changes-to-insights-cmdlets"></a><span data-ttu-id="dd432-126">见解 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-126">Breaking changes to Insights cmdlets</span></span>

<span data-ttu-id="dd432-127">此版本影响以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dd432-127">The following cmdlets were affected this release:</span></span>
    
### <a name="get-azurermusage"></a><span data-ttu-id="dd432-128">Get-AzureRmUsage</span><span class="sxs-lookup"><span data-stu-id="dd432-128">Get-AzureRmUsage</span></span>
- <span data-ttu-id="dd432-129">此 cmdLet 已弃用。</span><span class="sxs-lookup"><span data-stu-id="dd432-129">This cmdlet has been deprecated.</span></span>

### <a name="remove-azurermalertrule"></a><span data-ttu-id="dd432-130">Remove-AzureRmAlertRule</span><span class="sxs-lookup"><span data-stu-id="dd432-130">Remove-AzureRmAlertRule</span></span>
- <span data-ttu-id="dd432-131">此 cmdlet 的输出已从内含单个对象的列表更改为单个对象；此对象包括 requestId 和状态代码。</span><span class="sxs-lookup"><span data-stu-id="dd432-131">The output of this cmdlet has changed from a list with a single object to a single object; this object includes the requestId, and status code.</span></span>
    
```powershell
# Old  
$s1 = Remove-AzureRmAlertRule -ResourceGroup $resourceGroup -name chiricutin
if ($s1 -ne $null)
{
    $r = $s1(0).RequestId
    $s = $s1(0).StatusCode
}

# New
$s1 = Remove-AzureRmAlertRule -ResourceGroup $resourceGroup -name chiricutin
$r = $s1.RequestId
$s = $s1.StatusCode
```
    
### <a name="add-azurermlogalertrule"></a><span data-ttu-id="dd432-132">Add-AzureRmLogAlertRule</span><span class="sxs-lookup"><span data-stu-id="dd432-132">Add-AzureRmLogAlertRule</span></span>
- <span data-ttu-id="dd432-133">此 cmdLet 已弃用。</span><span class="sxs-lookup"><span data-stu-id="dd432-133">This cmdlet has been deprecated.</span></span>
    
### <a name="get-azurermalertrule"></a><span data-ttu-id="dd432-134">Get-AzureRmAlertRule</span><span class="sxs-lookup"><span data-stu-id="dd432-134">Get-AzureRmAlertRule</span></span>
- <span data-ttu-id="dd432-135">此 cmdlet 的输出（一个对象列表）的每个元素都是平展的，也就是说，它不采用结构 `{ Id, Location, Name, Tags, Properties }` 返回对象，而是将采用结构 `{ Id, Location, Name, Tags, Type, Description, IsEnabled, Condition, Actions, LastUpdatedTime, ...}` 返回对象，这是 Azure 资源的所有属性外加 AlertRuleResource 顶层的所有属性。</span><span class="sxs-lookup"><span data-stu-id="dd432-135">Each element of the the output (a list of objects) of this cmdlet is flattened, i.e. instead of returning objects with the structure `{ Id, Location, Name, Tags, Properties }` it will return objects with the structure `{ Id, Location, Name, Tags, Type, Description, IsEnabled, Condition, Actions, LastUpdatedTime, ...}`, which is all of the attributes of an Azure Resource plus all of the attributes of an AlertRuleResource at the top level.</span></span>
    
```powershell
# Old
$rules = Get-AzureRmAlertRule -ResourceGroup $resourceGroup
if ($rules -and $rules.count -ge 1)
{
    Write-Host -fore red "Error updating alert rule"
      
    Write-Host $rules(0).Id
    Write-Host $rules(0).Properties.IsEnabled
    Write-Host $rules(0).Properties.Condition
}

# New
$rules = Get-AzureRmAlertRule -ResourceGroup $resourceGroup
if ($rules -and $rules.count -ge 1)
{
    Write-Host -fore red "Error updating alert rule"
 
    Write-Host $rules(0).Id
      
    # Properties will remain for a while
    Write-Host $rules(0).Properties.IsEnabled
      
    # But the properties will be at the top level too. Later Properties will be removed
    Write-Host $rules(0).IsEnabled
    Write-Host $rules(0).Condition
}
```
    
### <a name="get-azurermautoscalesetting"></a><span data-ttu-id="dd432-136">Get-AzureRmAutoscaleSetting</span><span class="sxs-lookup"><span data-stu-id="dd432-136">Get-AzureRmAutoscaleSetting</span></span>
- <span data-ttu-id="dd432-137">`AutoscaleSettingResourceName` 字段已弃用，因为它始终具有与 `Name` 字段相同的值。</span><span class="sxs-lookup"><span data-stu-id="dd432-137">The `AutoscaleSettingResourceName` field is deprecated since it always has the same value as the `Name` field.</span></span>

```powershell
# Old  
$s1 = Get-AzureRmAutoscaleSetting -ResourceGroup $resourceGroup -Name MySetting
if ($s1.AutoscaleSettingResourceName -ne $s1.Name)
{
    Write-Host "There is something wrong with the name"
}

# New
$s1 = Get-AzureRmAutoscaleSetting -ResourceGroup $resourceGroup -Name MySetting
    
# There won't be a AutoscaleSettingResourceName
Write-Host $s1.Name
```
    
### <a name="remove-azurermlogprofile"></a><span data-ttu-id="dd432-138">Remove-AzureRmLogProfile</span><span class="sxs-lookup"><span data-stu-id="dd432-138">Remove-AzureRmLogProfile</span></span>
- <span data-ttu-id="dd432-139">此 cmdlet 的输出将从 `Boolean` 更改为包含 `RequestId` 和 `StatusCode` 的对象</span><span class="sxs-lookup"><span data-stu-id="dd432-139">The output of this cmdlet will change from `Boolean` to and object containing `RequestId` and `StatusCode`</span></span>

```powershell
# Old  
$s1 = Remove-AzureRmLogProfile -Name myLogProfile
if ($s1 -eq $true)
{
    Write-Host "Removed"
}
else
{
    Write-Host "Failed"
}

# New
$s1 = Remove-AzureRmLogProfile -Name myLogProfile
$r = $s1.RequestId
$s = $s1.StatusCode
```
    
### <a name="add-azurermlogprofile"></a><span data-ttu-id="dd432-140">Add-AzureRmLogProfile</span><span class="sxs-lookup"><span data-stu-id="dd432-140">Add-AzureRmLogProfile</span></span>
- <span data-ttu-id="dd432-141">此 cmdlet 的输出将从包含 requestId 的对象更改为包含 requestId、状态代码以及更新的或新建的资源的对象</span><span class="sxs-lookup"><span data-stu-id="dd432-141">The output of this cmdlet will change from an object that includes the requestId, status code, and the updated or newly created resource</span></span>
    
```powershell
# Old  
$s1 = Add-AzureRmLogProfile -Name default -StorageAccountId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/JohnKemTest/providers/Microsoft.Storage/storageAccounts/johnkemtest8162 -Locations Global -categ Delete, Write, Action -retention 3
$r = $s1.ServiceBusRuleId

# New
$s1 = Add-AzureRmLogProfile -Name default -StorageAccountId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/JohnKemTest/providers/Microsoft.Storage/storageAccounts/johnkemtest8162 -Locations Global -categ Delete, Write, Action -retention 3
$r = $s1.RequestId
$s = $s1.StatusCode
$a = $s1.NewResource.ServiceBusRuleId
    
```
    
### <a name="set-azurermdiagnosticsettings"></a><span data-ttu-id="dd432-142">Set-AzureRmDiagnosticSettings</span><span class="sxs-lookup"><span data-stu-id="dd432-142">Set-AzureRmDiagnosticSettings</span></span>
- <span data-ttu-id="dd432-143">此命令将重命名为 `Update-AzureRmDiagnsoticSettings`</span><span class="sxs-lookup"><span data-stu-id="dd432-143">The command is going to be renamed to `Update-AzureRmDiagnsoticSettings`</span></span>

```powershell
# Old
Set-AzureRmDiagnosticSettings

# New
Update-AzureRmDiagnosticSettings
```

## <a name="breaking-changes-to-network-cmdlets"></a><span data-ttu-id="dd432-144">网络 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-144">Breaking changes to Network cmdlets</span></span>

<span data-ttu-id="dd432-145">此版本影响以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dd432-145">The following cmdlets were affected this release:</span></span>

### <a name="new-azurermvirtualnetworkgatewayconnection"></a><span data-ttu-id="dd432-146">New-AzureRmVirtualNetworkGatewayConnection</span><span class="sxs-lookup"><span data-stu-id="dd432-146">New-AzureRmVirtualNetworkGatewayConnection</span></span>
- <span data-ttu-id="dd432-147">`EnableBgp` 参数已更改为采用 `boolean` 而非 `string`</span><span class="sxs-lookup"><span data-stu-id="dd432-147">`EnableBgp` parameter has been changed to take a `boolean` instead of a `string`</span></span>

```powershell
# Old
New-AzureRmVirtualNetworkGatewayConnection -ResourceGroupName "RG" -name "conn1" -VirtualNetworkGateway1 $vnetGateway -LocalNetworkGateway2 $localnetGateway -ConnectionType IPsec -SharedKey "key" -EnableBgp "true"

# New
New-AzureRmVirtualNetworkGatewayConnection -ResourceGroupName "RG" -name "conn1" -VirtualNetworkGateway1 $vnetGateway -LocalNetworkGateway2 $localnetGateway -ConnectionType IPsec -SharedKey "key" -EnableBgp $true
```

## <a name="breaking-changes-to-servicebus-cmdlets"></a><span data-ttu-id="dd432-148">ServiceBus cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-148">Breaking changes to ServiceBus cmdlets</span></span>

<span data-ttu-id="dd432-149">此版本影响以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dd432-149">The following cmdlets were affected this release:</span></span>

### <a name="get-azurermservicebusnamespace"></a><span data-ttu-id="dd432-150">Get-AzureRmServiceBusNamespace</span><span class="sxs-lookup"><span data-stu-id="dd432-150">Get-AzureRmServiceBusNamespace</span></span>
- <span data-ttu-id="dd432-151">属性 `ResourceGroupName` 已从输出类型 `NamespaceAttributes` 中删除</span><span class="sxs-lookup"><span data-stu-id="dd432-151">The property `ResourceGroupName` has been removed from the output type `NamespaceAttributes`</span></span>

### <a name="new-azurermservicebusnamespace"></a><span data-ttu-id="dd432-152">New-AzureRmServiceBusNamespace</span><span class="sxs-lookup"><span data-stu-id="dd432-152">New-AzureRmServiceBusNamespace</span></span>

- <span data-ttu-id="dd432-153">属性 `ResourceGroupName` 已从输出类型 `NamespaceAttributes` 中删除</span><span class="sxs-lookup"><span data-stu-id="dd432-153">The property `ResourceGroupName` has been removed from the output type `NamespaceAttributes`</span></span>

## <a name="breaking-changes-to-sql-cmdlets"></a><span data-ttu-id="dd432-154">Sql cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-154">Breaking changes to Sql cmdlets</span></span>

<span data-ttu-id="dd432-155">此版本影响以下 cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dd432-155">The following cmdlets were affected this release:</span></span>

### <a name="new-azurermsqldatabasefailovergroup"></a><span data-ttu-id="dd432-156">New-AzureRmSqlDatabaseFailoverGroup</span><span class="sxs-lookup"><span data-stu-id="dd432-156">New-AzureRmSqlDatabaseFailoverGroup</span></span>
- <span data-ttu-id="dd432-157">`Tag` 参数已删除</span><span class="sxs-lookup"><span data-stu-id="dd432-157">`Tag` parameter has been removed</span></span>
- <span data-ttu-id="dd432-158">`GracePeriodWithDataLossHour` 参数已重命名为 `GracePeriodWithDataLossHours`</span><span class="sxs-lookup"><span data-stu-id="dd432-158">`GracePeriodWithDataLossHour` parameter has been renamed to `GracePeriodWithDataLossHours`</span></span>

```powershell
# Old
New-AzureRmSqlDatabaseFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -PartnerServerName server2 -FailoverPolicy Automatic -GracePeriodWithDataLossHour 1 -Tag @{ Environment="Test" }

# New
New-AzureRmSqlDatabaseFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -PartnerServerName server2 -FailoverPolicy Automatic -GracePeriodWithDataLossHours 1
```

### <a name="set-azurermsqldatabasefailovergroup"></a><span data-ttu-id="dd432-159">Set-AzureRmSqlDatabaseFailoverGroup</span><span class="sxs-lookup"><span data-stu-id="dd432-159">Set-AzureRmSqlDatabaseFailoverGroup</span></span>
- <span data-ttu-id="dd432-160">`Tag` 参数已删除</span><span class="sxs-lookup"><span data-stu-id="dd432-160">`Tag` parameter has been removed</span></span>
- <span data-ttu-id="dd432-161">`GracePeriodWithDataLossHour` 参数已重命名为 `GracePeriodWithDataLossHours`</span><span class="sxs-lookup"><span data-stu-id="dd432-161">`GracePeriodWithDataLossHour` parameter has been renamed to `GracePeriodWithDataLossHours`</span></span>

```powershell
# Old
Set-AzureRmSqlDatabaseFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -FailoverPolicy Automatic -GracePeriodWithDataLossHour 1 -Tag @{ Environment="Test" }

# New
Set-AzureRmSqlDatabaseFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -FailoverPolicy Automatic -GracePeriodWithDataLossHours 1
```

### <a name="add-azurermsqldatabasetofailovergroup"></a><span data-ttu-id="dd432-162">Add-AzureRmSqlDatabaseToFailoverGroup</span><span class="sxs-lookup"><span data-stu-id="dd432-162">Add-AzureRmSqlDatabaseToFailoverGroup</span></span>
- <span data-ttu-id="dd432-163">`Tag` 参数已删除</span><span class="sxs-lookup"><span data-stu-id="dd432-163">`Tag` parameter has been removed</span></span>

```powershell
# Old
Add-AzureRmSqlDatabaseToFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -Database $db1 -Tag @{ Environment="Test" }

# New
Add-AzureRmSqlDatabaseToFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -Database $db1
```

###  <a name="remove-azurermsqldatabasefromfailovergroup"></a><span data-ttu-id="dd432-164">Remove-AzureRmSqlDatabaseFromFailoverGroup</span><span class="sxs-lookup"><span data-stu-id="dd432-164">Remove-AzureRmSqlDatabaseFromFailoverGroup</span></span>
- <span data-ttu-id="dd432-165">`Tag` 参数已删除</span><span class="sxs-lookup"><span data-stu-id="dd432-165">`Tag` parameter has been removed</span></span>

```powershell
# Old
Remove-AzureRmSqlDatabaseFromFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -Database $db1 -Tag @{ Environment="Test" }

# New
Remove-AzureRmSqlDatabaseFromFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -Database $db1
```

### <a name="remove-azurermsqldatabasefailovergroup"></a><span data-ttu-id="dd432-166">Remove-AzureRmSqlDatabaseFailoverGroup</span><span class="sxs-lookup"><span data-stu-id="dd432-166">Remove-AzureRmSqlDatabaseFailoverGroup</span></span>
- <span data-ttu-id="dd432-167">`PartnerResourceGroupName` 参数已删除</span><span class="sxs-lookup"><span data-stu-id="dd432-167">`PartnerResourceGroupName` parameter has been removed</span></span>
- <span data-ttu-id="dd432-168">`PartnerServerName` 参数已删除</span><span class="sxs-lookup"><span data-stu-id="dd432-168">`PartnerServerName` parameter has been removed</span></span>

```powershell
# Old
Remove-AzureRmSqlDatabaseFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg -PartnerServerName server2 -PartnerResourceGroupName rg

# New
Remove-AzureRmSqlDatabaseFailoverGroup -ResourceGroupName rg -ServerName server1 -FailoverGroupName fg
```

### <a name="set-azurermsqldatabasethreatdetectionpolicy"></a><span data-ttu-id="dd432-169">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="dd432-169">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>
- <span data-ttu-id="dd432-170">值 `Usage_Anomaly` 对参数 `ExcludedDetectionType` 不再有效</span><span class="sxs-lookup"><span data-stu-id="dd432-170">The value `Usage_Anomaly` is no longer valid for the parameter `ExcludedDetectionType`</span></span>

### <a name="set-azurermsqlserverthreatdetectionpolicy"></a><span data-ttu-id="dd432-171">Set-AzureRmSqlServerThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="dd432-171">Set-AzureRmSqlServerThreatDetectionPolicy</span></span>
- <span data-ttu-id="dd432-172">值 `Usage_Anomaly` 对参数 `ExcludedDetectionType` 不再有效</span><span class="sxs-lookup"><span data-stu-id="dd432-172">The value `Usage_Anomaly` is no longer valid for the parameter `ExcludedDetectionType`</span></span>

## <a name="breaking-changes-to-storage-cmdlets"></a><span data-ttu-id="dd432-173">存储 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-173">Breaking changes to Storage cmdlets</span></span>

<span data-ttu-id="dd432-174">此版本影响以下输出类型属性：</span><span class="sxs-lookup"><span data-stu-id="dd432-174">The following output type properties were affected this release:</span></span>

### <a name="azurestorageblobicloudblobserviceclient"></a><span data-ttu-id="dd432-175">AzureStorageBlob.ICloudBlob.ServiceClient</span><span class="sxs-lookup"><span data-stu-id="dd432-175">AzureStorageBlob.ICloudBlob.ServiceClient</span></span>
- <span data-ttu-id="dd432-176">以下属性已从此类型中删除（_注意_：它们仍然存在于 `DefaultRequestOptions` 属性中）：</span><span class="sxs-lookup"><span data-stu-id="dd432-176">The following properties were removed from this type (_note_: they can still be found in `DefaultRequestOptions` property):</span></span>
    - `LocationMode`
    - `MaximumExecutionTime`
    - `ServerTimeout`
    - `ParallelOperationThreadCount`
    - `SingleBlobUploadThresholdInBytes`
- <span data-ttu-id="dd432-177">此更改影响以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dd432-177">This change affects the following cmdlets:</span></span>
    - `Get-AzureStorageBlob`
    - `Get-AzureStorageBlobContent`
    - `Get-AzureStorageBlobCopyState`
    - `Set-AzureStorageBlobContent`
    - `Start-AzureStorageBlobCopy`
    - `Stop-AzureStorageBlobCopy`
    
### <a name="azurestoragecontainercloudblobcontainerserviceclient"></a><span data-ttu-id="dd432-178">AzureStorageContainer.CloudBlobContainer.ServiceClient</span><span class="sxs-lookup"><span data-stu-id="dd432-178">AzureStorageContainer.CloudBlobContainer.ServiceClient</span></span>
- <span data-ttu-id="dd432-179">以下属性已从此类型中删除（_注意_：它们仍然存在于 `DefaultRequestOptions` 属性中）：</span><span class="sxs-lookup"><span data-stu-id="dd432-179">The following properties were removed from this type (_note_: they can still be found in the `DefaultRequestOptions` property):</span></span>
    - `LocationMode`
    - `MaximumExecutionTime`
    - `ServerTimeout`
    - `ParallelOperationThreadCount`
    - `SingleBlobUploadThresholdInBytes`
- <span data-ttu-id="dd432-180">此更改影响以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dd432-180">This change affects the following cmdlets:</span></span>
    - `Get-AzureStorageContainer`
    - `New-AzureStorageContainer`
    - `Set-AzureStorageContainerAcl`
    
### <a name="azurestoragequeuecloudqueueserviceclient"></a><span data-ttu-id="dd432-181">AzureStorageQueue.CloudQueue.ServiceClient</span><span class="sxs-lookup"><span data-stu-id="dd432-181">AzureStorageQueue.CloudQueue.ServiceClient</span></span>
- <span data-ttu-id="dd432-182">以下属性已从此类型中删除（_注意_：它们仍然存在于 `DefaultRequestOptions` 属性中）：</span><span class="sxs-lookup"><span data-stu-id="dd432-182">The following properties were removed from this type (_note_: they can still be found in the `DefaultRequestOptions` property):</span></span>
    - `LocationMode`
    - `MaximumExecutionTime`
    - `RetryPolicy`
    - `ServerTimeout`
- <span data-ttu-id="dd432-183">此更改影响以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dd432-183">This change affects the following cmdlets:</span></span>
    - `Get-AzureStorageQueue`
    - `New-AzureStorageQueue`
    
### <a name="azurestoragetablecloudtableserviceclient"></a><span data-ttu-id="dd432-184">AzureStorageTable.CloudTable.ServiceClient</span><span class="sxs-lookup"><span data-stu-id="dd432-184">AzureStorageTable.CloudTable.ServiceClient</span></span>
- <span data-ttu-id="dd432-185">以下属性已从此类型中删除（_注意_：它们仍然存在于 `DefaultRequestOptions` 属性中）：</span><span class="sxs-lookup"><span data-stu-id="dd432-185">The following properties were removed from this type (_note_: they can still be found in the `DefaultRequestOptions` property):</span></span>
    - `LocationMode`
    - `MaximumExecutionTime`
    - `PayloadFormat`
    - `RetryPolicy`
    - `ServerTimeout`
- <span data-ttu-id="dd432-186">此更改影响以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dd432-186">This change affects the following cmdlets:</span></span>
    - `Get-AzureStorageTable`
    - `New-AzureStorageTable`
    
```powershell
# Old
$LocationMode = (Get-AzureStorageBlob -Container $containername)[0].ICloudBlob.ServiceClient.LocationMode       
$ParallelOperationThreadCount = (Get-AzureStorageContainer -Container $containername).CloudBlobContainer.ServiceClient.ParallelOperationThreadCount
$PayloadFormat = (Get-AzureStorageTable -Name $tablename).CloudTable.ServiceClient.PayloadFormat
$RetryPolicy = (Get-AzureStorageQueue -Name $queuename).CloudQueue.ServiceClient.RetryPolicy

# New
$LocationMode = (Get-AzureStorageBlob -Container $containername)[0].ICloudBlob.ServiceClient.DefaultRequestOptions.LocationMode     
$ParallelOperationThreadCount = (Get-AzureStorageContainer -Container $containername).CloudBlobContainer.ServiceClient.DefaultRequestOptions.ParallelOperationThreadCount
$PayloadFormat = (Get-AzureStorageTable -Name $tablename).CloudTable.ServiceClient.DefaultRequestOptions.PayloadFormat
$RetryPolicy = (Get-AzureStorageQueue -Name $queuename).CloudQueue.ServiceClient.DefaultRequestOptions.RetryPolicy
```

## <a name="breaking-changes-to-profile-cmdlets"></a><span data-ttu-id="dd432-187">配置文件 cmdlet 的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-187">Breaking Changes to Profile Cmdlets</span></span>

<span data-ttu-id="dd432-188">以下 cmdlet 和 cmdlet 输出类型在此版本中已更改。</span><span class="sxs-lookup"><span data-stu-id="dd432-188">The following cmdlets and cmdlet output types were changed in this release.</span></span>

### <a name="add-azurermaccount-breaking-changes"></a><span data-ttu-id="dd432-189">Add-AzureRmAccount 重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-189">Add-AzureRmAccount breaking changes</span></span>

- <span data-ttu-id="dd432-190">```EnvironmentName``` 参数已删除并替换为 ```Environment```，```Environment``` 现在采用字符串而非 ```AzureEnvironment``` 对象</span><span class="sxs-lookup"><span data-stu-id="dd432-190">```EnvironmentName``` parameter has been removed and replaced with ```Environment```, the ```Environment``` now takes a string and not an ```AzureEnvironment``` object</span></span>

```powershell
# Old
Add-AzureRmAccount -EnvironmentName AzureChinaCloud

# New
Add-AzureRmAccount -Environment AzureChinaCloud
```

### <a name="select-azurermprofile-was-renamed-to-import-azurermcontext"></a><span data-ttu-id="dd432-191">Select-AzureRmProfile 已重命名为 Import-AzureRmContext</span><span class="sxs-lookup"><span data-stu-id="dd432-191">Select-AzureRmProfile was renamed to Import-AzureRmContext</span></span>

<span data-ttu-id="dd432-192">```Select-AzureRmProfile``` 已重命名为 ```Import-AzureRmContext```</span><span class="sxs-lookup"><span data-stu-id="dd432-192">```Select-AzureRmProfile``` was renamed to ```Import-AzureRmContext```</span></span>

```powershell
# Old
Select-AzureRmProfile -Path c:\mydir\myprofile.json

# New
Import-AzureRmContext -Path c:\mydir\myprofile.json
```

### <a name="save-azurermprofile-was-renamed-to-save-azurermcontext"></a><span data-ttu-id="dd432-193">Save-AzureRmProfile 已重命名为 Save-AzureRmContext</span><span class="sxs-lookup"><span data-stu-id="dd432-193">Save-AzureRmProfile was renamed to Save-AzureRmContext</span></span>

<span data-ttu-id="dd432-194">```Save-AzureRmProfile``` 已重命名为 ```Save-AzureRmContext```</span><span class="sxs-lookup"><span data-stu-id="dd432-194">```Save-AzureRmProfile``` was renamed to ```Save-AzureRmContext```</span></span>

```powershell
# Old
Save-AzureRmProfile -Path c:\mydir\myprofile.json

# New
Save-AzureRmContext -Path c:\mydir\myprofile.json
```
### <a name="breaking-changes-to-output-psazurecontext-type"></a><span data-ttu-id="dd432-195">输出 PSAzureContext 类型的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-195">Breaking Changes to output PSAzureContext Type</span></span>

- <span data-ttu-id="dd432-196">```TokenCache``` 属性已更改为实现 ```IAzureTokenCache``` 而非 ```byte[]``` 的类型</span><span class="sxs-lookup"><span data-stu-id="dd432-196">The ```TokenCache``` property changed to a type that implements ```IAzureTokenCache``` instead of a ```byte[]```</span></span>

```powershell
# Old
$bytes = (Get-AzureRmContext).TokenCache
$bytes = (Set-AzureRmContext -SubscriptionId xxx-xxx-xxx-xxx).TokenCache
$bytes = (Add-AzureRmAccount).Context.TokenCache

# New
$bytes = (Get-AzureRmContext).TokenCache.CacheData
$bytes = (Set-AzureRmContext -SubscriptionId xxx-xxx-xxx-xxx).TokenCache.CacheData
$bytes = (Add-AzureRmAccount).Context.TokenCache.CacheData
```

### <a name="breaking-changes-to-the-output-psazureaccount-type"></a><span data-ttu-id="dd432-197">输出 PSAzureAccount 类型的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-197">Breaking Changes to the output PSAzureAccount Type</span></span>

- <span data-ttu-id="dd432-198">```AccountType``` 属性已更改为 ```Type```</span><span class="sxs-lookup"><span data-stu-id="dd432-198">The ```AccountType``` property was changed to ```Type```</span></span>

```powershell
# Old
$type = (Get-AzureRmContext).Account.AccountType
$type = (Set-AzureRmContext -SubscriptionId xxx-xxx-xxx-xxx).Account.AccountType
$type = (Add-AzureRmAccount).Context.Account.AccountType

# New 
$type = (Get-AzureRmContext).Account.Type
$type = (Set-AzureRmContext -SubscriptionId xxx-xxx-xxx-xxx).Account.Type
$type = (Add-AzureRmAccount).Context.Account.Type
```

### <a name="breaking-changes-to-the-output-psazuresubscription-type"></a><span data-ttu-id="dd432-199">输出 PSAzureSubscription 类型的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-199">Breaking Changes to the output PSAzureSubscription Type</span></span>
- <span data-ttu-id="dd432-200">```SubscriptionId``` 属性已更改为 ```Id```</span><span class="sxs-lookup"><span data-stu-id="dd432-200">The ```SubscriptionId``` property was changed to ```Id```</span></span>

```powershell
# Old
$id =(Get-AzureRmSubscription -SubscriptionId xxxx-xxxx-xxxx-xxxx).SubscriptionId
$id =(Add-AzureRmAccount -SubscriptionId xxxx-xxxx-xxxx-xxxx).Context.Subscription.SubscriptionId
$id =(Get-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.SubscriptionId
$id =(Set-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.SubscriptionId

# New
$id =(Get-AzureRmSubscription -SubscriptionId xxxx-xxxx-xxxx-xxxx).Id
$id =(Add-AzureRmAccount -SubscriptionId xxxx-xxxx-xxxx-xxxx).Context.Subscription.Id
$id =(Get-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.Id
$id =(Set-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.Id
```

- <span data-ttu-id="dd432-201">```SubscriptionName``` 属性已更改为 ```Name```</span><span class="sxs-lookup"><span data-stu-id="dd432-201">The ```SubscriptionName``` property was changed to ```Name```</span></span>

```powershell
# Old
$name =(Get-AzureRmSubscription -SubscriptionId xxxx-xxxx-xxxx-xxxx).SubscriptionName
$name =(Add-AzureRmAccount -SubscriptionId xxxx-xxxx-xxxx-xxxx).Context.Subscription.SubscriptionName
$name =(Get-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.SubscriptionName
$name =(Set-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.SubscriptionName

# New
$name =(Get-AzureRmSubscription -SubscriptionId xxxx-xxxx-xxxx-xxxx).Name
$name =(Add-AzureRmAccount -SubscriptionId xxxx-xxxx-xxxx-xxxx).Context.Subscription.Name
$name =(Get-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.Name
$name =(Set-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Subscription.Name
```

### <a name="breaking-changes-to-the-output-psazuretenant-type"></a><span data-ttu-id="dd432-202">输出 PSAzureTenant 类型的重大更改</span><span class="sxs-lookup"><span data-stu-id="dd432-202">Breaking Changes to the output PSAzureTenant Type</span></span>

- <span data-ttu-id="dd432-203">```TenantId``` 属性已更改为 ```Id```</span><span class="sxs-lookup"><span data-stu-id="dd432-203">The ```TenantId``` property was changed to ```Id```</span></span>

```powershell
# Old
$id =(Get-AzureRmTenant -TenantId xxxx-xxxx-xxxx-xxxx).TenantId
$id =(Add-AzureRmAccount -SubscriptionId xxxx-xxxx-xxxx-xxxx).Context.Tenant.TenantId
$id =(Get-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Tenant.TenantId
$id =(Set-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Tenant.TenantId

# New
$id =(Get-AzureRmTenant -TenantId xxxx-xxxx-xxxx-xxxx).Id
$id =(Add-AzureRmAccount -SubscriptionId xxxx-xxxx-xxxx-xxxx).Context.Tenant.Id
$id =(Get-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Tenant.Id
$id =(Set-AzureRmContext -SubscriptionId xxxx-xxxx-xxxx-xxxx).Tenant.Id
```

- <span data-ttu-id="dd432-204">```Domain``` 属性已更改为 ```Directory```</span><span class="sxs-lookup"><span data-stu-id="dd432-204">The ```Domain``` property was changed to ```Directory```</span></span>

```powershell
# Old
$tenantName =(Get-AzureRmTenant -TenantId xxxx-xxxx-xxxx-xxxx).Domain

# New
$tenantName =(Get-AzureRmTenant -TenantId xxxx-xxxx-xxxx-xxxx).Directory
```
