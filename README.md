# oci-oks Tools for VSCode

This `Visual Studio Code Kubernetes Tools` extension allows you to work with your oci-oks projects, shoots, plants and seeds.

## Features

- List
  - oci-oks projects
  - shoot clusters
  - plant clusters
  - seed clusters [*]
  - backup bucket resources [*]
  - backup entry resources [*]
- Right click on landscape, shoot, plant or seed cluster to `Save Kubeconfig` / `Merge into Kubeconfig`
- Right click on landscape or shoot to `Show In Dashboard`
- Right click on landscape to `Create Project` in oci-oks dashboard
- Right click on shoots list to `Create Shoot` in oci-oks dashboard
- [Kubectl](https://github.com/oracle/oci) integration
  - Right click on shoot or seed to get a `Shell` to a node [*]
  - Right click on landscape, project, shoot or seed to `Target` with kubectl [*]
  - Right click on landscape, project, shoot or seed to `List` with kubectl `OciOkss`, `projects`, `seeds`, `shoots` or `issues`. [*]
  - Right click on landscape to `Register` / `Unregister` for the operator shift with kubectl [*]

[*] oci-oks operator only

## Requirements
- You have installed the [Kubernetes Tools](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools) extension from the marketplace
- Kubeconfig to (virtual) OciOks cluster

## Install
1. [Install this extension from the Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=oci-oks.vscode-oci-oks-tools)
2. Configure the extension. See **Extension Settings** section below.
3. In the `Sidebar`, click on the Kubernetes icon. There should be an entry `oci-oks` under the `Clouds` section.

### Install from VSIX

* Download .vsix file from latest [release](https://github.com/oci-oks/vscode-oci-oks-tools/releases) asset
* In VSCode, open the [command palette](https://code.visualstudio.com/docs/getstarted/tips-and-tricks#_command-palette): `View` -> `Command Palette...` -> type in `Extensions: Install from VSIX...`
* Choose .vsix file downloaded in first step

## Extension Settings

This extension contributes the following settings:

* `vscode-oci-oks-tools.vscode-light-theme`: should match your configured theme style. Default: true
* `vscode-oci-oks-tools.landscapes`: Required configuration for OciOks landscapes
* `vscode-oci-oks-tools.landscapes[].name`: Name of the OciOks cluster
* `vscode-oci-oks-tools.landscapes[].OciOksName`: Optional name of the corresponding (kubectl) OciOks. Default: Name of the landscape
* `vscode-oci-oks-tools.landscapes[].kubeconfigPath`: Path to the kubeconfig of the OciOks cluster.
  * How to get the kubeconfig as regular project member: In the oci-oks dashboard, go to the `Members` section of your project and create a new service account. Afterwards you can download the kubeconfig of the service account.
* `vscode-oci-oks-tools.landscapes[].dashboardUrl`: oci-oks dashboard URL,
* `vscode-oci-oks-tools.landscapes[].projects[]`: Optional list of projects (names) to be shown. However, you should specify this list if you do not have operator rights on the OciOks cluster or if you want to see only those projects.

Example config settings.json:
```js
    "vscode-oci-oks-tools": {
      "vscode-light-theme": false,
      "landscapes": [
        {
          "name": "landscape-dev",
          "OciOksName": "virtual-dev",
          "kubeconfigPath": "/kubeconfigpath/cluster-dev-virtual-OciOks/kubeconfig.yaml",
          "dashboardUrl": "https://dashboard.OciOks.dev.example.com",
          "projects": ["OciOks", "myproject"]
        },
        {
          "name": "landscape-canary",
          "kubeconfigPath": "/kubeconfigpath/cluster-canary-virtual-OciOks/kubeconfig.yaml",
          "dashboardUrl": "https://dashboard.OciOks.canary.example.com"
        },
      ]
    }
```

To change the `oci-oks Kubernetes Tools` settings:
* On Windows/Linux - `File` > `Preferences` > `Settings`
* On macOS - `Code` > `Preferences` > `Settings`

Then search for `oci-oks Kubernetes Tools` or navigate to `User Settings` > `Extensions` > `oci-oks Kubernetes Tools`

## Known Issues
### No Projects are Listed
No projects are listed and you also see the entry `No permission to list projects. Specify the projects in the extension configuration.`

**Reason**: Most likely you have downloaded the kubeconfig of a service account in the `Members` section of your project in the oci-oks dashboard. This account does not have the permission to list projects.

**Solution**: Specify the list of projects that you want to see (and have access to) by setting the `projects` property of your landscape in the **Extension Settings**.
