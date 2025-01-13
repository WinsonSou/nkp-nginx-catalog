# nkp-nginx-catalog
catalog item for NGINX in NKP

1. Set the K8s context to the NKP Management Cluster.
2. Set the namespace to the relevant Workspace as an environmental variable:

```bash
export NAMESPACE=[your_namespace]
````

3. Apply the following manifest

```bash
kubectl apply -f - <<EOF
apiVersion: source.toolkit.fluxcd.io/v1beta1
kind: GitRepository
metadata:
  name: nginx-catalog
  namespace: ${NAMESPACE}
  labels:
    kommander.d2iq.io/gitapps-gitrepository-type: catalog
    kommander.d2iq.io/gitrepository-type: catalog
spec:
  interval: 1m0s
  ref:
    branch: main
  timeout: 1m0s
  url: https://github.com/WinsonSou/nkp-nginx-catalog
EOF
```