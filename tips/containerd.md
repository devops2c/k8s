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

# Configuration & install
# Installer containerd
sudo apt install -y containerd

# Générer sa config
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml

# Activer et démarrer
sudo systemctl restart containerd
sudo systemctl enable containerd

# Charger les modules
sudo modprobe overlay
sudo modprobe br_netfilter

# Appliquer les règles réseau
cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF

sudo sysctl --system
