Step:1
create a namespace
```
#kubectl create namespace ingress-internal
```
then run 
```
kubectl create -f *.yaml or *.yml
```
It will create an internal ELB which will be accessible only with in the VPC (you can test by curl from nodes of cluster)

After deployment, inorder to use this ingress-nginx controller add/replace your ingress.yaml with below entry under annotations:

Add this:
```
      "kubernetes.io/ingress.class": "nginx-internal",
```
Remove this: 
```
      "kubernetes.io/ingress.class": "nginx",
```      
If the ingress is with nginx it will add entries to public facing ingress-nginx controller, if you add it with nginx-internal it will create entries
on private facing ingress-nginx controller
