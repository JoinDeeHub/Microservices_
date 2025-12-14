Kubernetes manifests generated.

To deploy to any k8s cluster you have kubectl access to:
1) Ensure images referenced in deployments exist in the cluster's accessible registry.
   - If you built images locally and your cluster can't access them, push to a registry and update image fields.
   - Example docker build & push:
     docker build -t <your-registry>/user-service:tag ./submission/user-service
     docker push <your-registry>/user-service:tag
     (then update deployments/*-service.yaml image fields)

2) Apply manifests:
   kubectl apply -f submission/deployments/
   kubectl apply -f submission/services/

3) (Optional) Enable ingress on your cluster (if using k8s provider's ingress) and apply:
   kubectl apply -f submission/ingress/ingress.yaml

4) Check:
   kubectl get pods -o wide
   kubectl get svc
   kubectl describe deploy gateway-service

Helpful: If you want to quickly test in a local single-node k8s like kind, create a kind cluster and load images:
  kind create cluster
  docker build -t user-service:latest ./submission/user-service
  kind load docker-image user-service:latest
  kubectl apply -f submission/deployments/
  kubectl apply -f submission/services/
