# Helm deployments to openshift

Intro:

For the purposes of this post, I'm will often use kubernetes and openshift interchangabily. I understand that they are
different, however, they are so similar in many respects, especially with respect to helm, we can talk about them the
same way.


## Steps


* Start minishift

 minishift start --vm-driver xhyve
 
 Your mileage may vary, I'm working on a Mac, so I've chosen to use the xhyve provisioner
 
 Now that we finally have minishift running. 
 
 `oc status`
 
 https://192.168.64.4:8443/console/catalog
 
* setup helm in openshift cluster
    - install helm in your minishift cluster. 
        The current version of helm has a client and a server. Them `helm` client is the command running locally on your
        machine. The server is called `Tiller` which runs as a pod inside your openshift cluster.
        
        
        To setup helm, we will need to set the tiller namespace. By default, tiller wants to run in the `kube-system`
        namespace, this is one of those instances where openshift and kubernetes differ. We are able to install tiller
        in a specific namespace however. By setting the `TILLER_NAMESPACE` environment variable, we can tell helm to
        run all commands in a specific namespace
        
        `export TILLER_NAMESPACE=myproject`
        
        We can run a `helm version`, this will provide the local helm client version and it attempts to connect to the
        tiller service to provide the tiller service version. 
        
        In this case, we cannot connect to tiller as there is no tiller running. Lets install the tiller service
        
        `helm init` 
        
    - verify that helm is active.
        `helm version`
        `oc get all`: you should see the tiller service running.
        
    
    
   

* Write a helm chart. 
    - Lets choose an application. 
    https://github.com/jknight-liatrio/sample-app-api
    
    - Lets explore some of the components of the helm chart.
    
    - Lets discuss some changes that may need to be made to the helmchart to support openshift

* deploy the helm chart

* Tada! Magic. 
