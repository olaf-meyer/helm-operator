# Tutorial to create an helmbased operator

## Prerequisite 

The following applications need to installed:

- helm
- operator-sdk
- git
- oc/kubectl tool
- Connection to running OpenShift/Kubernetes cluster

## Intialize the operator

``` bash
$>operator-sdk init --plugins=helm.sdk.operatorframework.io/v1 --group=demo --domain=consol.de --helm-chart=nginx-sts --project-name=nginx-sts
Created helm-charts/nginx-sts
Generating RBAC rules
I0315 16:08:14.986191  199443 request.go:655] Throttling request took 1.004878088s, request: GET:https://api.crc.testing:6443/apis/coordination.k8s.io/v1beta1?timeout=32s
WARN[0004] The RBAC rules generated in config/rbac/role.yaml are based on the chart's default manifest. Some rules may be missing for resources that are only enabled with custom values, and some existing rules may be overly broad. Double check the rules generated in config/rbac/role.yaml to ensure they meet the operator's permission requirements.
```

The operator sdk is expecting that the helm charts are located in a different where this operator files will be generated. Because of this we need to delete the original helmchart folder. A copy has been created in the folder helmcharts/nginx-sts.

The created file structure looks like this:

``` bash
$>tree
.
├── config
│   ├── crd
│   │   ├── bases
│   │   │   └── demo.consol.de_nginxsts.yaml
│   │   └── kustomization.yaml
│   ├── default
│   │   ├── kustomization.yaml
│   │   └── manager_auth_proxy_patch.yaml
│   ├── manager
│   │   ├── kustomization.yaml
│   │   └── manager.yaml
│   ├── prometheus
│   │   ├── kustomization.yaml
│   │   └── monitor.yaml
│   ├── rbac
│   │   ├── auth_proxy_client_clusterrole.yaml
│   │   ├── auth_proxy_role_binding.yaml
│   │   ├── auth_proxy_role.yaml
│   │   ├── auth_proxy_service.yaml
│   │   ├── kustomization.yaml
│   │   ├── leader_election_role_binding.yaml
│   │   ├── leader_election_role.yaml
│   │   ├── nginxsts_editor_role.yaml
│   │   ├── nginxsts_viewer_role.yaml
│   │   ├── role_binding.yaml
│   │   └── role.yaml
│   ├── samples
│   │   ├── demo_v1alpha1_nginxsts.yaml
│   │   └── kustomization.yaml
│   └── scorecard
│       ├── bases
│       │   └── config.yaml
│       ├── kustomization.yaml
│       └── patches
│           ├── basic.config.yaml
│           └── olm.config.yaml
├── Dockerfile
├── helm-charts
│   └── nginx-sts
│       ├── Chart.yaml
│       ├── templates
│       │   ├── configmap.yaml
│       │   ├── _helpers.tpl
│       │   ├── NOTES.txt
│       │   ├── route.yaml
│       │   ├── service.yaml
│       │   ├── stateful_sets.yaml
│       │   └── tests
│       │       └── test-connection.yaml
│       └── values.yaml
├── Makefile
├── PROJECT
├── README.md
└── watches.yaml

15 directories, 39 files
```
