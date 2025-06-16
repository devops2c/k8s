# pods evicted status: 

Supprimer tous les Pods Evicted dans un namespace (ex : default)
kubectl get pods --field-selector=status.phase==Failed -n default | grep Evicted | awk '{print $1}' | xargs kubectl delete pod -n default


Alternative simple (namespace par défaut) :
kubectl delete pod $(kubectl get pod | grep Evicted | awk '{print $1}')


#supprimer tous les pods avec un status specifique : xxx
exemple: ContainerStatusUnknown

kubectl get pods --all-namespaces | grep ContainerStatusUnknown | awk '{print $1, $2}' | \
  while read namespace pod; do
    echo "Deleting $namespace/$pod"
    kubectl delete pod "$pod" -n "$namespace" --grace-period=0 --force
  done

# All Commands
Commande	                     Description
kubectl get pods	             Liste les pods dans le cluster
kubectl describe pod <pod>  	 Détaille tout : conteneurs, événements, volumes, etc.
kubectl logs <pod>	             Logs du conteneur principal d’un pod
kubectl exec -it <pod> -- bash	 Exécute une commande dans un conteneur du pod
kubectl delete pod <pod>	     Supprime un pod (Kubernetes recrée un nouveau si nécessaire)
