## Create front-end ingress yaml

### Pre-requisite:

Be logged into your `IKS cluster` with correct context.

### Prepare yaml file

- Copy the frontend-ingress.yaml.tmpl file

- Export following ENVs for the above .yaml
Verify ENV substitution in template file
```
export SKPR_IKS_FRONTEND_SECRET=$(kubectl get cm ibm-cloud-cluster-ingress-info -n kube-system -o 'jsonpath={.data.ingress-secret}')
export SKPR_IKS_FRONTEND_SUBDOMAIN=$(kubectl get cm ibm-cloud-cluster-ingress-info -n kube-system -o 'jsonpath={.data.ingress-subdomain}')
export SKPR_IKS_FRONTEND_HOST=frontend.$MESH_IKS_FRONTEND_SUBDOMAIN
```
- Check set ENVs
```
env | grep MESH
```
- Create the .yaml file
```
envsubst < frontend-ingress.yaml.tmpl > frontend-ingress.yaml
