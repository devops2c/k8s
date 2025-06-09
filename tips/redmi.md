#Probleme depot k8s sur node worker
message d'erreur :
Ign :7 https://packages.cloud.google.com/apt kubernetes-xenial InRelease
Err :9 https://packages.cloud.google.com/apt kubernetes-xenial Release
  404  Not Found [IP : 216.58.204.142 443]
Lecture des listes de paquets... Fait
E: Le dépôt https://apt.kubernetes.io kubernetes-xenial Release n'a pas de fichier Release.
N: Les mises à jour depuis un tel dépôt ne peuvent s'effectuer de manière sécurisée, et sont donc désactivées par défaut.
N: Voir les pages de manuel d'apt-secure(8) pour la création des dépôts et les détails de configuration d'un utilisateur.

#Etapes & commandes ✅ Étapes 100 % fiables pour Ubuntu 24.04 (mise à jour mai 2025)
🧹 1. Nettoie tout :
sudo rm -f /etc/apt/sources.list.d/kubernetes.list
sudo rm -f /etc/apt/keyrings/kubernetes-apt-keyring.gpg
🔐 2. Ajoute la clé GPG et le dépôt (v1.29 ou autre)

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key |
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

📦 3. Ajoute la source de paquets :
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

🔁 4. Recharge les sources :
sudo apt update
Si ici tu ne vois aucune erreur 404, c’est bon signe.

📥 5. Installe kubeadm, kubelet, kubectl
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

✅ 6. Vérifie :
kubeadm version
kubectl version --client

❌ Pourquoi pas Snap ?
Les paquets Snap ne sont pas compatibles avec le fonctionnement de kubeadm.

Snap isole trop les services pour permettre une bonne configuration du cluster Kubernetes.
sudo apt clean
sudo apt update  # Vérifiez qu'il n'y a plus d'erreur 404
