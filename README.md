# Deep Dive into Kustomize

First Tutorial taken from: https://antonputra.com/kubernetes/kubernetes-kustomize-tutorial/#convert-deployment-to-kustomize-base

# 1st Exmple

This example converts a deployment.yaml into a kustomization

## Applying Staging

From the root of this project
```
kubectl create namespace staging
kubectl config set-context --current --namespace=staging
kubectl apply -k environments/staging
```

## Applying production
From the root of this project
```
kubectl apply -k environments/production
```

## Deleting

From the root of this project
```
kubectl delete -k environments/production
```

# Example 2: Useing configMapGenerator

Apply using


```
kubectl apply -k staging
kubectl get pods
kubectl get cm
kubectl get cm config-<id> -o yaml
kubectl exec nginx-deployment-<id> -- cat /etc/config/credentials
```

# Example 4

Here we are providing a new version per environment. To replave in pipeline one can use (Where NEW_IMAGE is the new image version):

```
sed -i '0,/^\([[:space:]]*newTag: *\).*/s//\1NEW_IMAGE/' 4-exmple/staging/kustomization.yaml
```

Example:
```
sed -i '0,/^\([[:space:]]*newTag: *\).*/s//\11.21.7/' 4-exmple/staging/kustomization.yaml
```

Links:

* SpringBoot Example: [https://github.com/kubernetes-sigs/kustomize/tree/master/examples/springboot] (https://github.com/kubernetes-sigs/kustomize/tree/master/examples/springboot)