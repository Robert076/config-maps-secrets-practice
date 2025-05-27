# 🔐 config-maps-secrets-practice
Some of my notes while reading about **config maps** and **secrets** in Kubernetes.

> " Consider the following problem:
> 1. You deploy a Java application to the development environment for testing.
> 2. After the tests, the app is ready for production, and you need to deploy it. However, the MySQL
> endpoint for production is different from the one in development.
>
> There are two possibilities here:
> The configuration and application code are not decoupled, and the MySQL is hardcoded and bundled within the application code: you are stuck and need to rebuild the whole app after editing the application code.
> 
> The configuration and application code are decoupled. That’s good news for you as you can simply override the MySQL endpoint as you deploy to production.
> 
> That’s the key to the concept of portability: the application code should be independent of the infrastructure it is running on. The best way to achieve this is to decouple the application code from its configuration."
