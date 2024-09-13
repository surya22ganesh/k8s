Step 1: Generating PRIVATE KEY for a particular user.

openssl genrsa -out keyname.key 2048

Step 2: ( Certificate Signing Request ) .Generate a certificate signing request for the user with the private key.

openssl req -new -key keyname.key -out username.csr -subj /CN=ganesh/O=dev/O=example.org

ls -ls . (Now you should have the privatekey and csr)

Step 3: Certificate Signing Authority

Go to /root/.kube/config

Select the certificate authority line.

NOTE:

1) If you are using Kops. In older versions of Kops the ca.key and ca.cert were created automatically in the AWS S3 bucket.
s3://<BUCKET_NAME>/<CLUSTER_NAME>/pki/private/ca/*.key
s3://<BUCKET_NAME>/<CLUSTER_NAME>/pki/issued/ca/*.crt

2) But now we have a folder called "kubernetes-ca" with inside a keyset.yaml.

In this yaml file you can find 2 keys such as,

privateMaterial -> base64encoded PRIVATE KEY. 

publicMaterial -> base64encoded CERTIFICATE.

We have to decode this using:

echo "bas64encodedValue" | base64 --decode

eg: echo "privateMaterialvalue" | base64 --decode 

-> by decoding you will get the RSA PRIVATE KEY save this as ca.key

eg: echo "publicMaterial" | base64 --decode 

-> by decoding you will get the CERTIFICATE save this as ca.crt

sudo openssl x509 -req -CA ca.crt -CAkey ca.key -CAcreateserial -days 730 -in username.csr -out username.crt

Step 4:  setting user in kube config file.

kubectl config set-credentials username --client-certificate=ca.crt --client-key=ca.key 

user has set message will appear.

Verify that is kube config file.

Step 5:  adding Context/user in kube config

kops get cluster -> to list clusters

kubectl config set-context contextName --cluster=clusterName --user=username --namespace=default

context created message will appear.

Verify that is kube config file. Or by

kubectl config get-contexts

Step 6: ( switching Contexts or user )

kubectl config use-context contextName
 
Check using :

kubectl config get-contexts . The * under CURRENT shows under which contexts/user you are currently working.

Now all the commands you give will be applied as A specific user/contexts instead of Default-admin-user 

Now try listing pods. kubectl get pods 

Which will not work since the user is authenticated but not authorized.

switch back to admin/default contexts to give permissions or roles.

kubectl config get-contexts
kubectl config use-context contextName

AUTHORIZATION.

Step 1: Create a role using role.yaml file for a specific NameSpace.

Step 2: Create a Rolebinding using yaml file. (Rolebinding will attach the Users/contexts with roles.) 

Under subjects -> name. Attach the users. 

Under roleRef -> name. Attach the roles.

Step3: Apply both os them.

Step 4: Switch to the context you have created and applied permissions.

kubectl config get-contexts
kubectl config use-context contextName

Step 5: now try listing pods,deploy in that NameSpace.

To Delete Contexts:

kubectl config delete-context contextName