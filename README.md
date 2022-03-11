# portworx_sandbox
portworx installation in sandbox env

0 - install PX-Central to generate spec
```bash
kubectl create -f https://install.portworx.com/?comp=pxoperator
```

1 - install portworx operator
```bash
kubectl apply -f 'https://install.portworx.com/2.8?comp=pxoperator'
```
```bash
kubectl apply -f 'https://install.portworx.com/2.8?operator=true&mc=false&kbver=1.22&k=etcd%3Ahttp%3A%2F%2Fportworx%3A5000&j=auto&c=px-cluster-2ed71f07-a441-4dce-bddf-00172cf63436&stork=true&csi=true&mon=true&tel=false&st=k8s&promop=true'
```

2 - apply the generated configuration:
```bash
git clone https://github.com/chapote/portworx_sandbox.git
```
```bash
kubectl create -f ./portworx_sandbox/central_portworx_result.yaml
```

3 - wait untill the portworx node is ready
```bash
kubectl -n kube-system get storagenodes -l name=portworx --watch
kubectl -n kube-system describe storagenode node01
```

4 - test portworx with a pod
```bash
kubectl create -f ./portworx_sandbox/portworx-sc.yaml
kubectl create -f ./portworx_sandbox/portworx-volume-pvcsc.yaml
kubectl create -f ./portworx_sandbox/portworx-volume-pvcscpod.yaml
```
