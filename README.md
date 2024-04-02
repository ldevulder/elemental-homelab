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
| `BACKUP_RESTORE_VERSION` | Version of the backup operator to used | latest |
| `PRIVATE_CA` | Create and use a private CA instead of the default selfsigned | empty(=false) |

Current default version of upstream K8s cluster:
- K3s: v1.26.10+k3s2

### Examples

- Install Elemental Stable on Rancher v2.7-head:
```bash
$ deploy-elemental stable devel-2.7
```

- Install Elemental Dev on Rancher v2.8-head:
```bash
$ deploy-elemental dev devel-2.8
```

- Install Elemental Dev on Rancher Latest (Dev version):
```bash
$ deploy-elemental dev latest
```

- Install Elemental Dev on Rancher Stable:
```bash
$ deploy-elemental dev stable
```

- Install Elemental Dev on Rancher Stable with RKE2 on the upstream cluster:
```bash
$ deploy-elemental dev stable v1.26.10+rke2r2
```

## Upgrade Rancher script

The `upgrade-rancher` script is used to upgrade (or reinstall) Rancher Manager to a specific version. The default values bump Rancher to version `v2.8-head`.

## Upgrade Elemental script

The `upgrade-elemental` script is used to upgrade (or reinstall) the Elemental operator to a specific version. The default values bump the operator to the Dev version.
