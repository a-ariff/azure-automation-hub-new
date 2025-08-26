# Getting Started with Azure Automation Hub

Welcome to the Azure Automation Hub! This guide will help you quickly set up and start using the automation tools to streamline your Azure infrastructure management.

## 📝 Prerequisites

Before you begin, ensure you have the following:

### Required Software
- **PowerShell 5.1 or later** (PowerShell 7+ recommended)
- **Azure PowerShell Module (Az)**
- **Git** for repository cloning
- **Azure CLI** (optional, for additional Azure management)

### Azure Requirements
- **Azure subscription** with appropriate permissions
- **Azure Automation Account** (if using Azure Automation)
- **Resource groups** for organizing your resources
- **Service Principal** or **Managed Identity** for authentication

### Permissions Needed
- **Contributor** or **Owner** role on target Azure resources
- **User Access Administrator** for role assignments (if managing users)
- **Security Admin** for security-related automations

## 🚀 Quick Start (5 Minutes)

### Step 1: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/a-ariff/azure-automation-hub-new.git

# Navigate to the directory
cd azure-automation-hub-new
```

### Step 2: Install Required Modules

```powershell
# Install Azure PowerShell (if not already installed)
Install-Module -Name Az -AllowClobber -Force -Scope CurrentUser

# Install additional dependencies
Install-Module -Name AzureAD -Force -Scope CurrentUser
Install-Module -Name Microsoft.Graph -Force -Scope CurrentUser

# Import the modules
Import-Module Az
Import-Module AzureAD
```

### Step 3: Authenticate to Azure

```powershell
# Interactive login
Connect-AzAccount

# Set your subscription context
Set-AzContext -SubscriptionId "your-subscription-id"

# Verify your connection
Get-AzContext
```

### Step 4: Test Your First Automation

```powershell
# Import the common functions module
Import-Module ./modules/common-functions.psm1
Import-Module ./modules/azure-helpers.psm1

# Test with a simple resource group listing
Get-AzResourceGroup | Select-Object ResourceGroupName, Location
```

## 🛠️ Setup Options

### Option A: Local Development Environment

**Recommended for**: Development, testing, and small-scale operations

1. **Clone the repository** (as shown above)
2. **Install PowerShell modules** locally
3. **Configure authentication** using your user account
4. **Run scripts directly** from your machine

### Option B: Azure Automation Account

**Recommended for**: Production environments and scheduled operations

1. **Create an Automation Account** in Azure Portal
2. **Import runbooks** from the `runbooks/` directory
3. **Install required modules** in the Automation Account
4. **Configure authentication** using Managed Identity or Service Principal
5. **Schedule runbooks** as needed

#### Setting up Azure Automation Account:

```powershell
# Create resource group (if needed)
New-AzResourceGroup -Name "rg-automation" -Location "East US"

# Create Automation Account
New-AzAutomationAccount -Name "aa-automation-hub" \
    -ResourceGroupName "rg-automation" \
    -Location "East US"
```

## 📚 Common Usage Scenarios

### User Management Automation

```powershell
# Create a new user
.\runbooks\user-management\create-user.ps1 \
    -UserName "jane.doe" \
    -Department "HR" \
    -Location "New York"

# Bulk user operations from CSV
.\runbooks\user-management\bulk-user-operations.ps1 \
    -CsvPath "./users.csv" \
    -Operation "Create"

# Disable inactive users
.\runbooks\user-management\disable-user.ps1 \
    -InactiveDays 90
```

### Device Monitoring

```powershell
# Run health check on all devices
.\runbooks\device-monitoring\health-check.ps1 \
    -ResourceGroup "rg-devices"

# Generate compliance report
.\runbooks\device-monitoring\compliance-report.ps1 \
    -OutputPath "./reports/"

# Scan device inventory
.\runbooks\device-monitoring\inventory-scan.ps1 \
    -Subscription "your-subscription-id"
```

### Infrastructure Management

```powershell
# Provision new virtual machine
.\runbooks\infrastructure\vm-provisioning.ps1 \
    -VMName "vm-web-01" \
    -ResourceGroup "rg-web" \
    -Size "Standard_B2s"

# Configure network settings
.\runbooks\infrastructure\network-config.ps1 \
    -VNetName "vnet-main" \
    -SubnetName "subnet-web"
```

## 🔧 Configuration

### Environment Configuration

1. **Copy the sample configuration**:
   ```powershell
   Copy-Item "config\settings.sample.json" "config\settings.json"
   ```

2. **Edit your settings**:
   ```json
   {
     "Azure": {
       "SubscriptionId": "your-subscription-id",
       "TenantId": "your-tenant-id",
       "ResourceGroup": "rg-automation"
     },
     "Automation": {
       "LogLevel": "Information",
       "RetryCount": 3,
       "TimeoutMinutes": 30
     }
   }
   ```

### Security Configuration

- **Store secrets** in Azure Key Vault
- **Use Managed Identities** when possible
- **Enable audit logging** for all operations
- **Follow principle of least privilege**

## 📊 Monitoring and Logging

### Enable Logging

```powershell
# Configure logging
Set-LoggingLevel -Level "Information"
Set-LoggingOutput -Path "./logs/automation.log"
```

### Monitor Operations

- **Azure Monitor**: Set up alerts and dashboards
- **Log Analytics**: Aggregate logs for analysis
- **Application Insights**: Track performance and errors

## ❗ Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| **Authentication Failed** | Verify Azure credentials and permissions |
| **Module Not Found** | Install required PowerShell modules |
| **Permission Denied** | Check Azure RBAC roles and assignments |
| **Script Execution Policy** | Set execution policy: `Set-ExecutionPolicy RemoteSigned` |

### Getting Help

1. **Check the logs** in `./logs/` directory
2. **Review the documentation** in the main README
3. **Search existing issues** on GitHub
4. **Create a new issue** if you can't find a solution

## 📚 Additional Resources

### Documentation
- **[Main README](../README.md)** - Complete project documentation
- **[Architecture Overview](../README.md#-repository-architecture)** - Understanding the system design
- **[Security Guide](../SECURITY.md)** - Security best practices
- **[Contributing Guidelines](../CONTRIBUTING.md)** - How to contribute

### External Resources
- **[Azure PowerShell Documentation](https://docs.microsoft.com/powershell/azure/)**
- **[Azure Automation Documentation](https://docs.microsoft.com/azure/automation/)**
- **[PowerShell Best Practices](https://docs.microsoft.com/powershell/scripting/developer/cmdlet/best-practices/)**

## 👤 Next Steps

1. **✅ Complete the setup** following this guide
2. **✅ Run your first automation** to verify everything works
3. **✅ Explore the runbooks** in the repository
4. **✅ Customize configurations** for your environment
5. **✅ Set up monitoring** and alerts
6. **✅ Schedule regular operations** using Azure Automation

---

<div align="center">

**Ready to automate your Azure infrastructure?**

[🚀 Explore Runbooks](../runbooks/) • [📚 Read Full Docs](../README.md) • [📞 Get Support](https://github.com/a-ariff/azure-automation-hub-new/issues)

</div>
