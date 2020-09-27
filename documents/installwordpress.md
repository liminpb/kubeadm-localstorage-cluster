Install your Worpdress and Mysql service with PVC
===================================================


**step1**: Create secret 

    kubectl apply -f https://github.com/liminpb/kubeadm-localstorage-cluster/blob/master/yaml/secret.yaml

This will create the secret with all password details during the installation of wordpress.

**step2** : This step will create the mysql deployment along with mysql service and PVC for mysql.

        kubectl apply -f https://github.com/liminpb/kubeadm-localstorage-cluster/blob/master/yaml/wp-mysqldeploy.yaml
        
**step3** : This step will create the Wordpress deployment along with wordpress service and PVC for wordpress.

        kubectl apply -f https://github.com/liminpb/kubeadm-localstorage-cluster/blob/master/yaml/wordpressdeplo.yaml

