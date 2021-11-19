# Deploy Drupal/Wordpress application to the cluster

Now that we have our ingress controller running, we can deploy the application to the cluster and create an ingress resource to expose it.

Let’s start with a deployment:

Each deployment contain below kind

*  Namespace
*  Service
*  Deployment

## Deployment

### MySQL Deployment

```
kubectl apply -f deployment-mysql.yaml
```

### Drupal Deployment

```
kubectl apply -f deployment-drupal.yaml
```

### Wordpress Deployment

```
kubectl apply -f deployment-wordpress.yaml
```

## Ingress

Finally, let’s create our ingress resource:

### Drupal Ingress

```
kubectl apply -f ingress-drupal.yaml
```

### Wordpress Ingress

```
kubectl apply -f ingress-wordpress.yaml
```

Once everything is done, you will be able to get the ALB URL by running the following command:

### Drupal Ingress ALB

```
kubectl get ingress ingress-drupal
```

### Wordpress Ingress ALB

```
kubectl get ingress ingress-wordpress
```

The output of this command will be similar to this one:

```
NAME            HOSTS   ADDRESS                                                                 PORTS AGE
ingress-drupal    *     5e07dbe1-drupal-druingr-2e9-113757324.us-east-2.elb.amazonaws.com       80 20s
ingress-wordpress *     5e07dbe1-wordpress-wordingr-2e9-113757324.us-east-2.elb.amazonaws.com   80 40s
```# Sample Application deployment