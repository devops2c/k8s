#📌 containerd doit être installé sur tous les nœuds Kubernetes :
✅ Master (control-plane)
✅ Workers (nœuds de calcul)
🧠 Pourquoi ?
Kubernetes ne lance pas lui-même les conteneurs. Il délègue cette tâche à un runtime de conteneur via une API appelée CRI (Container Runtime Interface).

Le plus utilisé aujourd'hui est :

containerd (léger, stable, utilisé par Docker en interne)

Alternatives :

cri-o (autre runtime compatible CRI)

dockerd + cri-dockerd (deprecated, non recommandé)

📦 Donc, pour que kubelet fonctionne :
Il parle à containerd sur chaque nœud.

Sans containerd, kubelet échoue au démarrage (comme dans ton erreur).

✅ Résumé
Rôle du nœud	containerd requis ?	kubelet requis ?	kubeadm requis ?
Master	✅ Oui	✅ Oui	✅ Oui
Worker	✅ Oui	✅ Oui	✅ Oui
