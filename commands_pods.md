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