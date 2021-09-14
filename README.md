# SREHomeChalllenge
Evolution | SRE Home Challenge

## 1. Create kubernetes cluster using Vagrant in VirtualBox VM (or multiple VMs) using method you prefer 
Docuemntation used for the isntallationa and configuration for kubernates cluster :
Kubernates blog:
https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/

*Cloud provider Digital Ocean:
*Image: Ubuntu 20.01
*Files:
 * vagrant
 * master-playbook.yml
 * node-playbook.yml


## Task summary:
My first option for this taks was to use Oracle cloud Infraestrucure provider, Since I have many issues to use Vagrant and Virtual, the isue was realted to virtualization on the Oracle images, spend almost 2 days(5 hours) searching for a solution, the issue was on the amd virtualization and the workaround was to change son configs in the kernel, which is not allowed on the OCI image.I decide to move to another provider, I foudn digital Ocean give 100$ credit, I create a same ubuntu image and proceed to follow up the steps on the blog.

## Issues using OCI provider
On oracle provider I had issues using virtual box since on the boot step for the vagrant intance fails due to some issues on the virtualization on the ubuntu images which not was enabled. realize I was spending many days troubleshoting and move out to another option (ocean provider). 

## Issues to initiate K8 cluster with kubeadmin command
I had issues to execute kubeadmin to be able to create the kuberbate kluster, on line:
https://github.com/alejamig/SREHomeChalllenge/blob/main/miguelProjectK8s/kubernetes-setup/master-playbook.yml#L100
The command fails due to kubelet did not start, for more detials you can see error log attached:
https://github.com/alejamig/SREHomeChalllenge/blob/main/kubeadm_error_log

###### Added  remove swap on /etc/fstab
Searching on blogs for the erros on the logs I found a workaround to remove the swap on lines:
https://github.com/alejamig/SREHomeChalllenge/blob/main/miguelProjectK8s/kubernetes-setup/master-playbook.yml#L55
https://github.com/alejamig/SREHomeChalllenge/blob/main/miguelProjectK8s/kubernetes-setup/master-playbook.yml#L61

Those new additions did not resolve the issue.

###### ssh to k8s-master
I tried to excute manula the kube admin command:
```
kubeadm init --apiserver-advertise-address="192.168.50.10" --apiserver-cert-extra-sans="192.168.50.10"  --node-name k8s-master --pod-network-cidr=192.168.0.0/16 --v=5
```
And the command fails with this error:
> fail with connection refuse for Get http://localhost:10255/healthz

The solution was  to remove swap which I prevoiusly did it that solution. the main issue is kubelet did not initialize.

## Conclusion for task 1
I could not create the K8s cluster using ansible, vagrant and virtualbox due I could not find any soultion to resolve the kubelet issue. I will use the K8s feature on Digital Ocean to move this out since I take almost 4 days trying to create kubernates clusters.

Vagrant on creates the master but I failed to create the nodes:
> root@257k8s:~/SREHomeChalllenge/miguelProjectK8s# vagrant ssh k8s-master
>Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)
>
>* Documentation:  https://help.ubuntu.com
> * Management:     https://landscape.canonical.com
> * Support:        https://ubuntu.com/advantage
>
>  System information as of Mon 13 Sep 2021 03:03:32 AM UTC
>
>  System load:  0.32              Users logged in:          0
>  Usage of /:   5.7% of 61.31GB   IPv4 address for docker0: 172.17.0.1
>  Memory usage: 8%                IPv4 address for eth0:    10.0.2.15
>  Swap usage:   0%                IPv4 address for eth1:    192.168.50.10
>  Processes:    119
>
>
>This system is built by the Bento project by Chef Software
>More information can be found at https://github.com/chef/bento
>Last login: Mon Sep 13 02:06:00 2021 from 10.0.2.2
 
