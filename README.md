# SREHomeChalllenge
Evolution | SRE Home Challenge

1. Create kubernetes cluster using Vagrant in VirtualBox VM (or multiple VMs) using method you prefer 
Docuemntation used for the isntallationa and configuration for kubernates cluster :
Kubernates blog:
https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/

Cloud provider Digital Ocean:
Image: Ubuntu 20.01

Task summary:
My firdst option for this taks was to use Oracle cloud Infraestrucure provider, Since I have many issues to use Vagrant and Virtual, the iiseu was realted to virtualization on the Oracle images, spend almost 2 days(5 hours) searching for a solution, the issue was on the amd virtualization and the workaround was to change son configs in the kernel, which is not allowed on the OCI image.I decide to move to another provider, I foudn digital Ocean give 100$ credit, I create a same ubuntu image and proceed to follow up the steps on the blog.



