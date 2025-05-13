# k8s
Installation un environnement de test KubeADM avec containerd

doc utiles:
- https://blog.stephane-robert.info/docs/conteneurs/orchestrateurs/kubernetes/kubeadm/
- xxxxxx


# pourquoi kubeadm
Kubeadm offre plusieurs fonctionnalités clés qui simplifient le déploiement et la gestion des clusters Kubernetes :

Initialisation du cluster : Configure automatiquement les composants critiques du plan de contrôle.
Ajout de nœuds : Génère des jetons d’adhésion sécurisés pour intégrer de nouveaux nœuds au cluster.
Gestion des mises à jour : Simplifie la mise à jour des composants du plan de contrôle et des nœuds de travail.
Gestion des certificats : Génère, renouvelle et distribue les certificats de sécurité nécessaires.
Configuration du réseau de pods : Supporte plusieurs plugins de réseau comme Calico et Flannel.
Support multi-plateforme : Compatible avec plusieurs systèmes d’exploitation et architectures matérielles.
Automatisation : S’intègre avec des outils comme Ansible, Terraform et des bash script pour automatiser les tâches d’administration.
Vérification de l’état du cluster : Fournit des outils pour diagnostiquer et vérifier l’état du cluster.

# Preparation environnement & prérequis

# Installation control node

# Installation worker node

# Commandes utiles
- https://hackernoon.com/lang/fr/configurer-et-g%C3%A9rer-un-cluster-kubernetes-avec-kubeadm
-  https://www.server-world.info/en/
# Tips
- changer vers root : # sudo -s (sans changement ~ ) ou # su -  (avec changement ~)
- changer mot de passe root : # sudo passwd root
