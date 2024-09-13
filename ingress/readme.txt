1) 1st we should download Ingress Controller link) https://github.com/kubernetes/ingress-nginx

2) git clone https://github.com/kubernetes/ingress-nginx.git

3) kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.1/deploy/static/provider/aws/deploy.yaml

-> This is a manifest file/ yaml file for NGINX Ingress Controller.Apply it to install.

-> Now new NameSpace ingress-nginx will be created.
 
4) kubectl get svc -A

5) Network Type Load balancer named ingress-nginx-controller will be created.

6)  kubectl get ingressclass -A 

7) ingress-nginx-controller gives us nginx. This should be used in ingress yaml/manifest file . spec : ingressClassName: nginx .

8) kubectl apply -f ingress.yaml . Apply the Ingress.yaml file.

9) Now check whether our Ingress file is read by our Ingress Controller using.

-> kubectl get pods -n ingress-nginx

->  kubectl logs ingress-nginx-controller-784997fdc7-7mcdl     (Ingress Controller Pod)

10)  kubectl get ing

