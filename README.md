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

