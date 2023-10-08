# argocdkubernetes

First Setup kubernetes cluster

Next install Argo CD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

Download and install ArgoCD cli

Patch the service type as load balancer to expose argocd ui on the browser

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

Alternatively port forward Argocd service

kubectl port-forward svc/argocd-server -n argocd 8080:443

argocd default username is admin

And to get the password for login

argocd admin initial-password -n argocd

change the argocd password
argocd account update-password

Get the kubernetes cluster name using this command
kubectl config get-contexts -o name

Register the kubernetes cluster with argocd
argocd cluster add docker-desktop

Set the argocd namespace as current context
kubectl config set-context --current --namespace=argocd

Create a github repo with two brances main and development

create a sample application folder and put the kuberentes yamls of the respective application within it

Now raise a pr to main branch 

Now run this command to link a sample application to argo cd so that it can deploy the same in argo cd server

argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default