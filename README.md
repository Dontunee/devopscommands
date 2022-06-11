# DOCKER
docker version.  
docker login    
docker images.  
docker rmi {{imageid}}. 
docker pull stacksimplify/dockerinto-springboot-helloworld-rest-api     
docker ps.   
docker run --name app1 -p 80:8080 stacksimplify/dockerintro-springboot-helloworld-rest-api:1.0.0-RELEASE.    
docker ps -a   
docker ps -a -q    
docker exec -it {{containename}} /bin/sh // connect to container terminal. 
ps ef
docker stop {{containername}}
docker start {{containename}}
docker rm {{containername}}.  
docker build -t afolabiba/mynginx_image:v1 .   
docker tag afolabiba/mynginx_image:v2 afolabiba/mynginx_image:v1-release     
 docker push afolabiba/mynginx_image:v1-release     
 docker pull image-info    
 docker port {{containedId}}.   
 docker stats    
 
 
** ELASTIC SEARCH **
 GET _cluster/health  
 GET _nodes/stats 

PUT favorite_candy

POST favorite_candy/_doc
{
  "firstName": "Tunde",
  "candy": "Bounty"
}    

PUT favorite_candy/_doc/3
{
  "firstName": "Kay",
  "candy": "skittles"
}   

GET favorite_candy/_doc/1   

PUT favorite_candy/_create/1
{
   "firstName": "Tunes",
  "candy": "coke"
}

POST favorite_candy/_update/1
{
  "doc": {
    "candy": "M&M's"
  }
}

DELETE favorite_candy/_doc/3.  

GET news_headlines/_search

**QUERY**
{
  "query": {
    "range": {
      "date": {
        "gte": "2015-06-20",
        "lte": "2015-06-20"
      }
    }
  }
}

{
  "query": {
    "match": {
      "headline": {
        "query": "khloe jennery kardashian",
        "operator": "and"
      }
    }
  }
}

**AGGREGATION**
{
  "aggs": {
    "by_category": {
      "terms": {
        "field": "category",
        "size": 100
      }
    }
  }
}

**query all documents that match the below criteris, bring all documetns that contain bla bla bla in headline field**
{
  "query": {
    "match": {
      "headline": {
        "query": "sdkjksjdsk dsjdsjsjsjkd"
      }
    }
  }
}
**QUERY AND AGGREGATION **
GET search results from the news_headlines index, first query all documents that match the entertainment category criteria ,
and run aggregations on the result and the report to be name popular_in_entertainment and run analysis on the significant text found 
in field HEADLINE
GET news_headlines/_search
{
  "query": {
    "match": { "category": "ENTERTAINMENT"}
  },
  "aggregations": {
    "popular_in_entertainment": {
      "significant_text": {"field": "headline"}
    }
  }
}

**Get search results from this index, query all documents that match this criteria below, 
grab all documents that include the dearch term in the field specified **
{
  "query":{
    "match": {
      "content": {
        "query": "python programming language"
      }
    }
  }
}

****ADVANCED SEARCH****
**exact match of words and must appear next to each other **
{
  "query": {
    "match_phrase": {
      "headline": {
        "query": "Shape of you"
      }
    }
  }
}

**MULITPLE FIELD QUERIES **
{
  "query": {
    "multi_match": {
      "query": "MICHELLE OBAMA",
      "fields": ["headline^2", "short_description","authors"]
    }
  }
}

{
  "query": {
    "multi_match": {
      "query": "MICHELLE OBAMA",
      "fields": ["headline^2", "short_description","authors"],
      "type": "phrase"
    }
  }
}


**COMBINED QUERIES **
{
  "query": {
    "bool": {
      "must": [{one or more queries}],
       "must_not": [{one or more queries}],
        "should": [{one or more queries}],
         "filter": [{one or more queries}],
    }
  }
}

 {
  "query": {
    "bool": {
      "must": [
        {
          "match_phrase": {
            "headline": "Michelle Obama"
          }
        },
        {
          "match": {
            "category": "Politics"
          }
        }
        ]
    }
  }
}

{
  "query": {
    "bool": {
      "must": [
        {
          "match_phrase": {
            "headline": "Michelle Obama"
          }
        }
        ],
        "filter":{
          "range": {
            "date": {
              "gte": "2014-03-25",
              "lte": "2016-03-25"
            }
          }
        }
    }
  }
}
 



# AWS DEVOPS COMMANDS 
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
   
  helm list -n ingress
   
  kubectl get svc -n ingress 
   
 kubectl port-forward svc/prometheus-operated 9090 -n monitoring
   
 kubectl get svc -n monitoring  
 
aws ec2 describe-vpcs.   
kubectl version --short --client.  
eksctl version.  

**CREATE CLUSTER STEPS **.   
eksctl create cluster --name=eksdemo1 --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup.   
kubectl get pods   
eksctl get clusters    

** CREATE & ASSOCIATE OIDC PROVIDER FOR OUR EKS CLUSTER **   
   eksctl utils associate-iam-oidc-provider --region us-east-1 --cluster eksdemo1 --approve
   
**CREATE NODE GROUP WITH ADDITIONAL ADD-ONS IN PUBLIC SUBNETS **.    
   eksctl create nodegroup --cluster=eksdemo1  \
                           --region=us-east-1 \
                           --name=eksdemo1-ng-public1 \
                           --node-type=t3.medium \
                           --nodes=2   \
                           --nodes-min=2 \
                           --nodes-max=4 \
                           --node-volume-size=20 \
                           --ssh-access \
                           --ssh-public-key=kube-demo \
                           --managed \
                           --asg-access \
                           --external-dns-access \
                           --full-ecr-access \
                           --appmesh-access \
                           --alb-ingress-access
  
   eksctl get nodegroup --cluster=eksdemo1. 
   kubectl get nodes -o wide   
   kubectl config view --minify.   
   ssh -i kube-demo.cer ec2-user@3.80.138.17
   df -h    
   
   eksctl delete nodegroup --cluster={{clustername}} --name={{nodegroupname}}}.   
   eksctl delete cluster {{clustername}}.  
 kubectl get nodes -o wide.   
  kubectl run my-first-pod --image afolabiba/mynginx_image:1.0.0.  
  kubectl delete pod my-first-pod.  
 kubectl expose pod my-first-pod --type=NodePort --port=80 --name=my-first-service     
 kubectl get service.  
 kubectl get nodes -o wide.  
 kubectl expose pod my-first-pod --type=NodePort --port=81 --target-port=80 --name=my-first-service  
 kubectl logs my-first-pod.   
 kubectl logs -f my-first-pod.   
 
 **Get owner of pod** 
 kubectl get pods <pod-name> -o yaml 

 kubectl logs my-pod                                 # dump pod logs (stdout).   
kubectl logs -l name=myLabel                        # dump pod logs, with label name=myLabel (stdout).    
kubectl logs my-pod --previous                      # dump pod logs (stdout) for a previous instantiation of a container.   
kubectl logs my-pod -c my-container                 # dump pod container logs (stdout, multi-container case).   
kubectl logs -l name=myLabel -c my-container        # dump pod logs, with label name=myLabel (stdout).    
kubectl logs my-pod -c my-container --previous      # dump pod container logs (stdout, multi-container case) for a previous instantiation of a container.   
kubectl logs -f my-pod                              # stream pod logs (stdout).   
kubectl logs -f my-pod -c my-container              # stream pod container logs (stdout, multi-container case).   
kubectl logs -f -l name=myLabel --all-containers    # stream all pods logs with label name=myLabel (stdout).   
kubectl run -i --tty busybox --image=busybox:1.28 -- sh  # Run pod as interactive shell.    
kubectl run nginx --image=nginx -n mynamespace      # Start a single instance of nginx pod in the namespace of mynamespace.   
kubectl run nginx --image=nginx                     # Run pod nginx and write its spec into a file called pod.yaml.    
--dry-run=client -o yaml > pod.yaml.    

kubectl attach my-pod -i                            # Attach to Running Container.    
kubectl port-forward my-pod 5000:6000               # Listen on port 5000 on the local machine and forward to port 6000 on my-pod.   
kubectl exec my-pod -- ls /                         # Run command in existing pod (1 container case).   
kubectl exec --stdin --tty my-pod -- /bin/sh        # Interactive shell access to a running pod (1 container case).    
kubectl exec my-pod -c my-container -- ls /         # Run command in existing pod (multi-container case).    
kubectl top pod POD_NAME --containers               # Show metrics for a given pod and its containers.     
kubectl top pod POD_NAME --sort-by=cpu              # Show metrics for a given pod and sort it by 'cpu' or 'memory'.        
 
 
** create a pod    **
 kubectl run <desired-pod-name>. --image <container-image> --generator=run-pod/v1.  
 **e expose pod as a service **.  
 kubectl expose pod <pod-name> --type=NodePort --port=80 --name=<service-name>.      
 
 ** connect to a pod **.   
 kubectl exec -it <pod-name> -- /bin/bash.  
 
 ** Get environment variables in a container**.  
 kubectl exec -it <pod-name> env.   
 
 ** Get yaml ouput of pod and service **.   
 kubectl get pod <pod-name> -o yaml.   
 kubetcl get svc <service-name> -o yaml.     
 
 ** Get all objects in default namespace **
 kubectl get all
 
 **Deletion** 
 kubectl delete pod <pod-name>
 kubectl delete svc <service-name>

**create replicat set with yml**
kubectl create -f replicaset-demo.yml  
kubectl get replicaset 
kubectl descibe replicaset <replicasetname>

**expose replica set as a service**
kubectl expose rs <replicaset-name> --type=NodePort --port=80 --target-port=8080 --name=<service-name-to-be-created>

**replace existing yml**
kubectl replace -f replicaset-demo.yml

**creating a deployment**   
kubectl create deployment <deploymentname> --image<container-image>
kubect get deployments
kubectl descirbe deployment <deployment-name>
kubectl scale --replicas=<number-of-replicas> deployment <deployment-name>

**expose deployment as a service**
kubectl expose deployment <deployment-name> --type=NodePort --port=80 --target-port=80 --name=<deployment-service-name>
kubectl get svc 


**Update Deployment**
**Set Image**

**Get Container Name**
kubectl get deployment <deploymentName> -o yaml



  
 
 
 
 
 

   
   
   
   
   
   
   
   
 
