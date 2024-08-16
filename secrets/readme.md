CREATING SECRETS 

1) using kubectl

kubectl create secret secretType secretName --from-file=file1 --from-file=file2

kubectl create secret generic mysecret --from-file=mysecretfile.txt --from-file=mysecretfile2.txt

2) or by yaml/manifest file. 