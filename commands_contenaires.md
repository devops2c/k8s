# la cmd crictl ps -a
Elle liste tous les conteneurs gérés par le runtime CRI, y compris ceux qui ne sont plus en cours d’exécution.
ps : affiche les conteneurs en cours d'exécution par défaut.
-a (abréviation de --all) : inclut tous les conteneurs, même ceux :
qui sont arrêtés (Exited)
qui ont été terminés par le système (ex. : après un redémarrage de pod)
qui sont des init containers ou des jobs terminés

Quand l'utiliser ?
Pour déboguer un pod qui plante ou redémarre en boucle
Pour voir les anciens conteneurs liés à un pod
Pour vérifier l'état des conteneurs dans un cluster sans Docker (containerd, CRI-O)
Pour identifier les exit codes ou logs d’anciens conteneurs

# Status contenaire : Exited   
Quand un Pod est redémarré (manuellement, ou automatiquement suite à une panne ou à un kubelet restart), ses anciens conteneurs sont arrêtés et remplacés par de nouveaux conteneurs. Les anciens restent visibles avec le statut Exited.

Cela peut arriver si  :
tu as redémarré la machine ou le kubelet,
l’image a été re-pullée,
un kubectl rollout restart a été fait,
un problème de santé a déclenché un redéploiement.

# Remarque:
Certains conteneurs Exited sont init containers ou jobs one-shot

# Quand faut-il s’inquiéter des conteneurs Exited
Tu as des conteneurs qui sortent avec un code d’erreur (exit code != 0)
Ils redémarrent en boucle (CrashLoopBackOff)
Tu as une chaîne infinie de tentatives dans Attempt

# Pour verifier ca :
sudo crictl inspect <container_id> | grep -i exitcode

# Pour nettoyer (optionnel)
sudo crictl rm $(sudo crictl ps -a --state Exited -q)

# All Commands:
Commande	             Description
crictl ps	             Liste les conteneurs en cours d'exécution
crictl ps -a	         Liste tous les conteneurs (même arrêtés)
crictl inspect <id>	     Inspecte les détails d’un conteneur (exit code, runtime, etc.)
crictl logs <id>	     Affiche les logs d’un conteneur
crictl rm <id>	         Supprime un conteneur arrêté 