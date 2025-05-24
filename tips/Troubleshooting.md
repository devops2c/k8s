sudo crictl ps -a
il faut lancer la cmd avec (root/sudo)
🛠️ Explication
Le socket /run/containerd/containerd.sock est possédé par root et lisible uniquement par le groupe root ou containerd.
Si tu exécutes crictl sans sudo, tu n’as pas le droit d’ouvrir ce fichier Unix socket → d’où l’erreur permission denied.

Puis
kubectl get pods -n kube-system
kubectl get nodes

![image](https://github.com/user-attachments/assets/b2d56192-ac2e-4bc9-9c25-585943c9d2ee)

🧩 crictl essaie par défaut plusieurs runtimes, dont dockershim, qui n’existe plus depuis Kubernetes 1.24.
Or tu utilises containerd, mais crictl n’a pas encore été configuré pour ça, donc il scanne tous les endpoints possibles et affiche des erreurs.

✅ Solution : configurer crictl pour containerd
Tu dois spécifier explicitement le socket containerd dans un fichier de configuration de crictl.

➤ Étapes :
bash
Copier
Modifier
# 1. Créer le fichier de config
sudo tee /etc/crictl.yaml <<EOF
runtime-endpoint: unix:///run/containerd/containerd.sock
image-endpoint: unix:///run/containerd/containerd.sock
timeout: 10
debug: false
EOF

![image](https://github.com/user-attachments/assets/9482eebb-8599-40bd-b6a7-4a463681786f)

