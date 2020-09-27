**Local Persistent Volumes – A Step-by-Step procedure**

"Local volumes" are similar to hostPath volumes, but they allow to pin-point PODs to a specific node, and thus making sure that a restarting POD always will find the data storage in the state it had left it before the reboot. They also make sure that other restrictions are met before the used persistent volume claim is bound to a volume.

**Prerequisites**
    
    Multi node Kubeadm Cluster 

**Step 1**: Create StorageClass with WaitForFirstConsumer Binding Mode

Persistent local volumes require to have a binding mode of WaitForFirstConsumer. the only way to assign the volumeBindingMode to a persistent volume seems to be to create a storageClass with the respective volumeBindingMode and to assign the storageClass to the persistent volume.

    kubectl apply -f https://github.com/liminpb/kubeadm-localstorage-cluster/blob/master/yaml/storageClass.yaml
    
The output should be: 
        
        storageclass.storage.k8s.io/my-local-storage created

**step2**: Create Local Persistent Volume

Since the storage class is available now, we can create local persistent volume with a reference to the storage class we have just created.

    Note: You might need to exchange the hostname value „node1“ in the nodeAffinity section by the name of the node that matches your environment.
    
    The „hostPath“ we had defined in our last blog post is replaced by the so-called „local path„.
    
    on the node, where the POD will be located (node1 in our case):
        DIRNAME="vol1"
        mkdir -p /mnt/disk/$DIRNAME 
        chmod 777 /mnt/disk/$DIRNAME

Then Run the apply command.
    
    kubectl apply -f https://github.com/liminpb/kubeadm-localstorage-cluster/blob/master/yaml/persistentVolume.yaml
        
The output should be: 
            
            persistentvolume/my-local-pv created

Now you can proceed with the your second PVC and so on. Also PVC creation you can include either seperatly or along with your applicaion yaml. 

Now proceed with wordpress creation.

