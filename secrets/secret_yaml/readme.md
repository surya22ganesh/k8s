1) secret.yaml is the yaml/manifest file to create secret. 

2) here secret.yaml is an Opaque type secret resource.

3) normal string values are not accepted,base64 values are accepted as values.

4) echo -n "surya" | base64 -> converts to base64.which is assigned to a secret key.

5) kubectl -f secretfilename.yaml eg: kubectl -f secret.yaml

6) kubectl get secrets.

7) kubectl describe secrets

8) kubectl get secrets secretName -o jsonpath='{.data.secretKey}' | base64 --decode

#  secretName is mysecretname

# secretKey is MYSQL_ROOT_PASSWORD

9) kubectl exec -it podname -- /bin/bash 

# to enter into a pod 
# type env to check the env variables / Volumes Directories.

Decode

echo "bas64encodedValue" | base64 --decode