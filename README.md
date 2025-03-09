

```markdown

Ce projet utilise Ansible pour automatiser l'installation et le déploiement de GitLab dans une infrastructure Docker.

## Étapes d'installation

1. Cloner le dépôt
    git clone https://github.com/azat44/tp-ansibleAH
    cd gitlab-ansible

2. Lancer les conteneurs Docker
    docker-compose up -d

3. Configurer l'authentification SSH
    docker exec -it node-manager ssh-keygen -t rsa -b 4096 -f /root/.ssh/id_rsa -N ""
    docker exec node-manager cat /root/.ssh/id_rsa.pub | docker exec -i target1 tee -a /home/ubuntu/.ssh/authorized_keys
    docker exec node-manager cat /root/.ssh/id_rsa.pub | docker exec -i target2 tee -a /home/ubuntu/.ssh/authorized_keys
    docker exec target1 chown -R ubuntu:ubuntu /home/ubuntu/.ssh
    docker exec target2 chown -R ubuntu:ubuntu /home/ubuntu/.ssh
    docker exec target1 chmod 600 /home/ubuntu/.ssh/authorized_keys
    docker exec target2 chmod 600 /home/ubuntu/.ssh/authorized_keys

4. Exécuter les playbooks Ansible
    docker exec node-manager ansible-playbook -i /inventory/inventory.ini /playbooks/infrastructure.yml
    docker exec node-manager ansible-playbook -i /inventory/inventory.ini /playbooks/deploy.yml

5. Vérifier l'installation
    docker exec target1 ls -la /etc/gitlab
