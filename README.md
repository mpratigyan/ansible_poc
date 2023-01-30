1.) install python 3 if not installed.

2.) install ansible if not installed.

3.) copy the host details to /etc/ansible/hosts file. (change the host names and ip's accordingly)

[kubernetes_master_node]
192.168.56.105

[poc_hosts]
192.168.56.105

4.) login to register server on known hosts and add fingerprints .
5.) replace the user in the code to your current user.
6.) add entry for all the ports which are needed to open in env_variable file.

7.) if you have more than one node Uncomment below tasks - 
    configure_master_node.yaml - 
       * Get the join command to be used by the worker
       * Save the join command to a local file
    add_worker_nodes.yaml
       uncomment the firs line and run below command

8.) if you have more than one node comment below tasks - - 
    configure_master_node.yaml - 
       * Allow Kubernetes controle-plane to schedule pods on itself

9.) run below command to install ansible core in ansible-
    $ ansible-galaxy collection install kubernetes.core

10.) try to ping all using ansible ping command -
    $ ansible all -m ping --user username --ask-pass --ask-become-pass

11.) run below command to create the kubernetes cluster using ansible -
    $ ansible-playbook -v build_k8s_cluster.yaml --user username --ask-pass --ask-become-pass

12.) ** run below command if you have more than one node to join the worker nodes - **
    $ ansible-playbook -v add_worker_nodes.yaml --user username --ask-pass --ask-become-pass

13.) run below command to install argocd in	 the kubernetes cluster using ansible -
    $ ansible-playbook -v install_argocd_and_nginx_ingress_controller.yaml --user username --ask-pass --ask-become-pas

14). get argocd credential using below command -
    $ kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
    - login using the password and change the password.

15.) copy kubernetes cluster config file to run the kubernetes commands using local terminal.
    $ cd ~
    $ scp -r username@192.168.56.101:/home/username/.kube .

16.) download application.yaml file from kubernetes apps repository and run below command, it will deploy all the app in the cluster -
    $ kubectl -f application.yaml -n argocd


17.) get token for kubernetes dashboard using below command - 
    $ kubectl -n kubernetes-dashboard create token kubernetes-dashboard --duration=2628000s
    - use this token to login to kubernetes dashboard and see the cluster state.


14.) install mysql workbench to use mysql using nodeport 30006 (configure using env_variable file)

extra - 

- install nginx-ingress controller for ingress
- install helm 
- install prometheus using helm
- install grafana using kubectl