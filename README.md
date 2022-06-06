# devopscommands
Just to make my devops commands available whenever i need them , i will do well to the command description from time to time but apologies if it isnt updated you can make also help out 

velero install --provider aws --plugins velero/velero-plugin-for-aws:v1.0.1 --bucket elero-backup --backup-location-config region=us-east-1 --snapshot-location-config region=us-east-1 --secret-file /Users/tundeafolabi/.aws/credentials

Instructions 

How to restore back up of an existing Cluster on a new Cluster Using Velero 

PreConditions 

2> Get Existing Cluster backup location on Object Storage (e.g S3)
   velero get backup-locations
   velero snapshot-location get -o yaml                             

3> Get location of your AWS credentials on your local system e.g (	/Users/tundeafolabi/.aws/credentials)

Create cluster 


eksctl create cluster --name prodreplica --node-type t3.medium --nodes 1 --nodes-min 1 --region us-east-1 --zones=us-east-1a,us-east-1b,us-east-1c --version 1.19 

Get user logged on 
aws sts get-caller-identity 

Connect to a cluster
aws eks update-kubeconfig --name replice

Get Current context 
kubectl config current-context

Create helm 
helm create helm

Install helm 
helm install helm .

Upgrade helm
helm upgrade helm .

Get pods
Kubectl get pods 


Kubectl get svc


aws eks list-clusters

error restoring ingresses.extensions/kube-system/kibana-ingress: Internal error occurred: failed calling webhook “validate.nginx.ingress.kubernetes.io" velar restore


velero restore describe velero-dailybackups-20220601214522-20220604111536

kubectl edit deploy/velero -n velero                                                                                                                                      

velero restore create --from-backup velero-dailybackups-20220601214522 

velero restore create --from-backup velero-dailybackups-20220601214522 --include-resources persistentvolumeclaims,persistentvolumes


Pod failure troubleshooting
1.  kubectl describe node <node-name>
2.  kubectl describe pod <pod-name>
3.  kubectl get —help

velero get backup-locations
velero snapshot-location get -o yaml   

  

velero install --provider aws --plugins velero/velero-plugin-for-aws:v1.0.1 --bucket stage-velero-backup --backup-location-config region=us-east-1,name=aws --snapshot-location-config region=us-east-1,name=aws --secret-file /Users/tundeafolabi/.aws/credentials

 kubectl apply -f  prometheus 
 
 kubectl get crds
  
kubectl get pods -n monitoring  
  
helm repo add ingress-nginx \https://kubernetes.github.io/ingress-nginx
  
helm template my-ing ingress-nginx/ingress-nginx \
--namespace ingress \
--version 4.1.3 \
--values values.yaml \
--output-dir my-ing
  
  helm install my-ing ingress-nginx/ingress-nginx \
--namespace ingress \
--version 4.1.3 \
--values values.yaml \
--create-namespace

  helm uninstall deployment01 -n opsb-helm --no-hooks
