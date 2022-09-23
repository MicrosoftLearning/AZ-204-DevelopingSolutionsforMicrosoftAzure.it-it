# <a name="lab-virtual-machine-setup"></a>Configurazione della macchina virtuale lab

## <a name="installed-software"></a>Software installato

| Software | Collegamento |
| --- | --- |
| Windows 10 (Build 2004) | <https://www.microsoft.com/software-download/windows10> |
| Visual Studio Code | <https://code.visualstudio.com> |
| Estensione Account di Azure per Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account> |
| Estensione Funzioni di Azure per Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions> |
| Estensione Azure Resource Manager Tools per Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools> |
| Estensione Azure CLI Tools per Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.azurecli> |
| Estensione di PowerShell per Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell> |
| Estensione C# per Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp> |
| PowerShell 7 | <https://github.com/PowerShell/PowerShell/releases/tag/v7.0.3> |
| .NET 6 SDK | <https://dotnet.microsoft.com/download/dotnet/6.0> |
| Azure PowerShell | <https://docs.microsoft.com/powershell/azure/install-az-ps> |
| Interfaccia della riga di comando di Azure | <https://docs.microsoft.com/cli/azure/install-azure-cli> |
| Esplora archivi Azure | <https://azure.microsoft.com/features/storage-explorer> |
| Strumento .NET - HttpRepl | <https://github.com/dotnet/HttpRepl> |
| Azure Functions Core Tools | <https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3> |
| Terminale Windows | <https://aka.ms/terminal> |
| Edge (Chromium) | <https://www.microsoft.com/edge> |

## <a name="additional-configuration"></a>Configurazione aggiuntiva

- Abilitare ClearType
  
- Configurare Microsoft Edge come browser predefinito

- Aggiornare la configurazione di VSCode

  ```json
  {
    "editor.fontFamily": "'Cascadia Code', Consolas, 'Courier New', monospace",
    "update.enableWindowsBackgroundUpdates": false,
    "update.mode": "manual",
    "terminal.integrated.shell.windows": "C:\\Program Files\\PowerShell\\7\\pwsh.exe",
    "workbench.startupEditor": "none",
    "terminal.integrated.rendererType": "dom",
    "csharp.suppressDotnetInstallWarning": true,
    "csharp.suppressDotnetRestoreNotification": true,
    "csharp.supressBuildAssetsNotification": true,
    "azureFunctions.showProjectWarning": false
  }
  ```

- Aggiornare la configurazione di Terminale Windows

  ```json
  {
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "profiles": [
      {
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
        "useAcrylic": true,
        "acrylicOpacity": 0.85,
        "colorScheme": "Campbell",
        "fontFace": "Cascadia Code",
        "hidden": false,
        "name": "PowerShell",
        "source": "Windows.Terminal.PowershellCore"
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": false,
        "name": "Azure Cloud Shell",
        "source": "Windows.Terminal.Azure"
      }
    ],
    "schemes": [],
    "keybindings": []
  }
  ```

- Configurare il menu Start e la barra delle applicazioni per includere solo le icone seguenti:
  - Esplora file
  - Microsoft Edge
  - Terminale Windows
  - Visual Studio Code
  - Esplora archivi Azure

- Disabilitare le notifiche di aggiornamento di PowerShell 7

  1. [Creare una variabile di ambiente](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_update_notifications?view=powershell-7) denominata ``POWERSHELL_UPDATECHECK``
  
  1. Impostare il valore della variabile di ambiente su ``Off`` (maiuscole/minuscole)

- Eseguire Azure Functions Core Tools almeno una volta per configurare Windows Firewall

  ```bash
  func init test --worker-runtime dotnet
  cd test
  func new --template 'HTTP trigger' --name web
  func start --build
  ```
