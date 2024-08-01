install k8s metric server

https://github.com/kubernetes-sigs/metrics-server

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

-------------------

kubectl get pods 

kubectl top node nodename       -> shows cpu/memory utilization.

kubectl describe nodes nodename

check each pods and overall cpu/memeory utilization in that worker node.

and assign the containes cpu req /limits .