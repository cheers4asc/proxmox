# proxmox
## Nested Virtulization
In order to enable the Nested Virtulization
You will update the "/etc/pve/qemu-server/*.conf" file\
You will add a following line to the file \
`cpu: cputype=host` <br />
Please make sure the Host machine has virtulization enabled

reference:- https://pve.proxmox.com/wiki/Manual:_qm.conf <br />
            https://pve.proxmox.com/wiki/Nested_Virtualization


## Add local disk to VM via proxmox console 


##OpenShift local PV 

```cat localstorage.yaml 
apiVersion: "local.storage.openshift.io/v1"
kind: "LocalVolume"
metadata:
  name: "local-disks"
  namespace: "openshift-local-storage" 
spec:
  storageClassDevices:
    - storageClassName: "local"
      volumeMode: Filesystem 
      fsType: xfs 
      devicePaths: 
        - /dev/sdb 

 ```./oc create -f localstorage.yaml``` <br />
localvolume.local.storage.openshift.io/local-disks created


 ```oc get all -n openshift-local-storage``` <br />
```NAME                                          READY   STATUS    RESTARTS   AGE
pod/local-disks-local-diskmaker-8cc2b         1/1     Running   0          58s
pod/local-disks-local-diskmaker-9skdx         1/1     Running   0          57s
pod/local-disks-local-provisioner-9lwhn       1/1     Running   0          57s
pod/local-disks-local-provisioner-gfl9r       1/1     Running   0          58s
pod/local-local-diskmaker-gn5qs               1/1     Running   0          2d22h
pod/local-local-diskmaker-zp72n               1/1     Running   0          2d22h
pod/local-local-provisioner-9fmdz             1/1     Running   0          2d22h
pod/local-local-provisioner-j9h9d             1/1     Running   0          2d22h
pod/local-storage-operator-7fc7b6794f-2vv4z   1/1     Running   0          2d23h

NAME                                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
service/local-storage-operator-metrics   ClusterIP   172.30.110.18   <none>        8383/TCP,8686/TCP   2d23h

NAME                                           DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/local-disks-local-diskmaker     2         2         2       2            2           <none>          58s
daemonset.apps/local-disks-local-provisioner   2         2         2       2            2           <none>          58s
daemonset.apps/local-local-diskmaker           2         2         2       2            2           <none>          2d22h
daemonset.apps/local-local-provisioner         2         2         2       2            2           <none>          2d22h

NAME                                     READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/local-storage-operator   1/1     1            1           2d23h

NAME                                                DESIRED   CURRENT   READY   AGE
replicaset.apps/local-storage-operator-7fc7b6794f   1         1         1       2d23h

NAME                                                              AGE
vmimportconfig.v2v.kubevirt.io/vmimport-kubevirt-hyperconverged   13h ```

./oc get pv    --server=https://api.proxcluster.asciihome.net:6443
NAME                CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM                                                STORAGECLASS   REASON   AGE
local-pv-81622b7f   32Gi       RWO            Delete           Available                                                        local                   67s
local-pv-82909390   32Gi       RWO            Delete           Bound       openshift-machine-api/cirrosmin-rich-mite-rootdisk   local                   67s
