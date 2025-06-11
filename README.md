# 🔐 config-maps-secrets-practice
Some of my notes while reading about **config maps** and **secrets** in Kubernetes.

### 🌎 Purpose of decoupling configuration from the application, hence the existence of ConfigMaps and Secrets:
> **Consider the following scenario:**  
> 1. You deploy a Go application to a staging environment for internal review.  
> 2. When moving to production, the PostgreSQL connection string is different.  
>  
> If the database URL is hardcoded in the Go app, you’ll need to rebuild it for production.  
>  
> But if the app reads its config from the environment or a file, you can swap in the new database URL without touching the code.  

❗️ The application code should be ***independent*** of the infrastructure it is running on.

---

### ⚙️  How to think about ConfigMaps and Secrets:
Think of them as repositories for key-value pairs.

---

### 🚀 Useful commands:
1. Get configmaps in your cluster:
```bash
kubectl get configmaps
```

2. Same thing but shorter:
```bash
kubectl get cm
```

3. Creating an empty configmap imperatively:
```bash
kubectl create cm my-first-configmap
```

4. Creating a configmap from literal values imperatively:
```bash
# creates a key named "color" and its value is set to "blue"
kubectl create cm my-second-configmap --from-literal=color=blue
```

5. Creating a configmap from an env file:
```bash
kubectl create cm anotherconfigmap --from-env-file=my-env-file.txt
```

6. View the data inside the configmap:
```bash
# data in configmaps is not encrypted so use secrets for stuff you don't want public
kubectl describe cm/anotherconfigmap
```

7. Launch a pod with an env variable taken from config map:
```bash
kubectl apply -f nginx-pod-with-configmap.yml
```

8. See that variable for yourself:
```bash
kubectl exec pods/nginx-pod-with-configmap -- env
```

9. In the case of a configmap mounted as a volume:
```bash
echo “I’m just a dummy config file” >> $HOME/configfile.txt

kubectl create cm my-sixth-configmap --from-literal=color=yellow --from-file=$HOME/configfile.txt

kubectl apply -f pod-with-volume-cm.yml

kubectl exec pods/nginx-pod-cm -- ls /etc/conf
```

10. Creating a secret imperatively:
```bash
kubectl create secret generic my-first-secret --from-literal='db_pass=my_db_pass'
```

11. Creating a secret from a file:
```bash
kubectl create secret generic mypassword --from-file=./password.txt
```

12. Creating a pod using the secret from a file we just made:
```bash
kubectl create -f nginx-pod-with-secret-env-var.yml
```

13. Creating a pod with envFrom secret:
```bash
kubectl create -f nginx-secret-envfrom.yml
```

14. Seeing those env vars in person:
```bash
kubectl exec -it pod/nginx-secret-envfrom --container nginx-container -- /bin/bash

env
```

> Lastly, note that there is no clean and consistent way to modify a secret once it has been created through kubectl. <br>
> To update a secret, you will need to delete it and then recreate it with the new values you need by following the examples given previously.
