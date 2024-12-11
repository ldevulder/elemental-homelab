# Elemental Home Lab

This repository is only to host my personal tools to deploy my own Elemental home lab.
It can evolves on a daily basis and can be break at any time!

You can use/copy/modify it without any restriction, just respect the license!

**NO WARRANTY! THE PRODUCT AND THE THIRD-PARTY SOFTWARE ARE OFFERED ON AN
"AS-IS" BASIS AND NO WARRANTY, EITHER EXPRESS OR IMPLIED, IS GIVEN!
USE IT AT YOUR RISK!**

## Deploy Elemental script

The `deploy-elemental` script does the following steps:
- install Kubernetes (K3s or RKE2, defaulted to K3s)
- configure the Helm repositories 
- install certificates (selfsigned or private, defaulted to selsigned)
- install Rancher Manager
- install Elemental operator
- install Rancher Backup operator (only on K3s for now)

Some steps can be skipped depending on your needs:
| Variable | Description |
|:---:|:---:|
| `SKIP_BACKUP` | Skip installation of backup operator |
| `SKIP_CAPI` | Skip check of CAPI pod (needed for older Rancher versions) |
| `SKIP_CERT` | Skip installation of selfsigned/private CA |
| `SKIP_ELEMENTAL` | Skip installation of Elemental operator |
| `SKIP_HELM` | Skip Helm configuration |
| `SKIP_K8S` | Skip upstream cluster installation |
| `SKIP_RM` | Skip Rancher Manager installation |

There are also some variables that can be tuned:
| Variable | Description | Default value |
|:---:|:---:|:---:|
| `BACKUP_RESTORE_VERSION` | Version of the backup operator to use | latest |
| `ELEMENTAL_REPO` | Use a specific repository for the elemental operator | empty(=calculated) |
| `ELEMENTAL_VERSION` | Version of the elemental operator to use | dev |
| `K8S_VERSION` | Version of upstream K8s cluster to use | v1.28.10+k3s1 |
| `PRIVATE_CA` | Create and use a private CA instead of the default selfsigned | empty(=false) |
| `RM_SRV` | ServerName/HostName to use for Rancher Manager | empty(=calculated) |
| `RANCHER_VERSION` | Version of Rancher Manager to use | stable |

### Examples

- Deploy Elemental Stable with Rancher v2.7-head:
```bash
$ ELEMENTAL_VERSION=stable RANCHER_VERSION=devel-2.7 deploy-elemental
```

- Deploy Elemental Dev with Rancher v2.8-head:
```bash
$ ELEMENTAL_VERSION=dev RANCHER_VERSION=devel-2.8 deploy-elemental
```

- Deploy Elemental Stable with Rancher Latest (Dev version):
```bash
$ ELEMENTAL_VERSION=stable RANCHER_VERSION=latest deploy-elemental
```

- Deploy Elemental Dev with Rancher Stable:
```bash
$ ELEMENTAL_VERSION=dev RANCHER_VERSION=stable deploy-elemental dev stable
```

- Deploy Elemental Staging with Rancher Stable on RKE2 v1.26.10:
```bash
$ ELEMENTAL_VERSION=staging K8S_VERSION=v1.26.10+rke2r2 RANCHER_VERSION=stable deploy-elemental
```

- Deploy Elemental Dev with Rancher Stable on an already deployed K8s cluster:
```bash
$ SKIP_K8S=1 deploy-elemental
```

## Upgrade Rancher script

The `upgrade-rancher` script is used to upgrade (or reinstall) Rancher Manager to a specific version. The default values bump Rancher to `latest` version.

## Upgrade Elemental script

The `upgrade-elemental` script is used to upgrade (or reinstall) the Elemental operator to a specific version. The default values bump the operator to `dev` version.
