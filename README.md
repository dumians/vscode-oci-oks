# oci-oke Tools for VSCode

This `Visual Studio Code Kubernetes Tools` extension allows you to work with your oci-oke projects, shoots, plants and seeds.

## Features

- List
  - oci-oke projects
  -  clusters
  -  clusters
  -  clusters [*]
  - backup bucket resources [*]
  - backup entry resources [*]

- [Kubectl](https://github.com/oracle/oci) integration
  - Right click on shoot or seed to get a `Shell` to a node [*]
  - Right click on landscape, project, shoot or seed to `Target` with kubectl [*]
  - Right click on landscape, project, shoot or seed to `List` with kubectl `Ociokes`, `projects`, `seeds`, `shoots` or `issues`. [*]
  - Right click on landscape to `Register` / `Unregister` for the operator shift with kubectl [*]

[*] oci-oke operator only

## Requirements
- You have installed the [Kubernetes Tools](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools) extension from the marketplace
- Kubeconfig to (virtual) Ocioke cluster


### Install from VSIX

* In VSCode, open the [command palette](https://code.visualstudio.com/docs/getstarted/tips-and-tricks#_command-palette): `View` -> `Command Palette...` -> type in `Extensions: Install from VSIX...`
* Choose .vsix file downloaded in first step

## Extension Settings

This extension contributes the following settings:

* `vscode-oci-oke-tools.vscode-light-theme`: should match your configured theme style. Default: true
* `vscode-oci-oke-tools.landscapes`: Required configuration for Ocioke landscapes
* `vscode-oci-oke-tools.landscapes[].name`: Name of the Ocioke cluster
* `vscode-oci-oke-tools.landscapes[].OciokeName`: Optional name of the corresponding (kubectl) Ocioke. Default: Name of the landscape
* `vscode-oci-oke-tools.landscapes[].kubeconfigPath`: Path to the kubeconfig of the Ocioke cluster.
  * How to get the kubeconfig as regular project member: In the oci-oke dashboard, go to the `Members` section of your project and create a new service account. Afterwards you can download the kubeconfig of the service account.
* `vscode-oci-oke-tools.landscapes[].dashboardUrl`: oci-oke dashboard URL,
* `vscode-oci-oke-tools.landscapes[].projects[]`: Optional list of projects (names) to be shown. However, you should specify this list if you do not have operator rights on the Ocioke cluster or if you want to see only those projects.

Example config settings.json:
```js
    "vscode-oci-oke-tools": {
      "vscode-light-theme": false,
      "landscapes": [
        {
          "name": "landscape-dev",
          "OciokeName": "virtual-dev",
          "kubeconfigPath": "/kubeconfigpath/cluster-dev-virtual-Ocioke/kubeconfig.yaml",
          "dashboardUrl": "https://dashboard.Ocioke.dev.example.com",
          "projects": ["Ocioke", "myproject"]
        },
        {
          "name": "landscape-canary",
          "kubeconfigPath": "/kubeconfigpath/cluster-canary-virtual-Ocioke/kubeconfig.yaml",
          "dashboardUrl": "https://dashboard.Ocioke.canary.example.com"
        },
      ]
    }
```

To change the `oci-oke Kubernetes Tools` settings:
* On Windows/Linux - `File` > `Preferences` > `Settings`
* On macOS - `Code` > `Preferences` > `Settings`

Then search for `oci-oke Kubernetes Tools` or navigate to `User Settings` > `Extensions` > `oci-oke Kubernetes Tools`

## Known Issues
### No Projects are Listed
No projects are listed and you also see the entry `No permission to list projects. Specify the projects in the extension configuration.`

**Reason**: Most likely you have downloaded the kubeconfig of a service account in the `Members` section of your project in the oci-oke dashboard. This account does not have the permission to list projects.

**Solution**: Specify the list of projects that you want to see (and have access to) by setting the `projects` property of your landscape in the **Extension Settings**.
