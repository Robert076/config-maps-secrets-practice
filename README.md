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
