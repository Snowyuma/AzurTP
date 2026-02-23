# AzurTP

# TP Noté — Déploiement de 2 VMs avec Load Balancer sur Azure via Terraform

##  Objectif

Déployer une infrastructure Azure complète avec Terraform comprenant :

- 2 machines virtuelles Ubuntu
- Installation automatique de Nginx
- Un Load Balancer public
- Distribution du trafic entre les 2 VMs
- Nettoyage complet de l’infrastructure

---

#  Etape 1 — Initialisation du projet

Création de la structure Terraform avec les fichiers :

- versions.tf
- provider.tf
- variables.tf
- main.tf
- outputs.tf

Initialisation du projet :

```bash
terraform init
```

###  Capture Etape 1
![Etape 1](preuves/etape1.png)

---

#  Etape 2 — Vérification avec Terraform Plan

Vérification de la configuration avant déploiement :

```bash
terraform plan
```

Cela permet de visualiser les ressources qui seront créées.

###  Capture Etape 2
![Etape 2](preuves/etape2.png)

---

#  Etape 3 et 4 — Configuration Réseau et Sécurité

Création des éléments suivants :

- Resource Group
- Virtual Network
- Subnet
- Network Security Group
- Règles :
  - Allow SSH (22)
  - Allow HTTP (80)
  - Deny All Inbound
- Association du NSG au Subnet

###  Capture Etape 3 et 4
![Etape 3 et 4](preuves/etape3-4.png)

---

#  Etape 5 — Déploiement des Machines Virtuelles

Création de :

- 2 Network Interfaces
- 2 Machines Virtuelles Ubuntu 22.04
- Authentification par clé SSH
- Installation automatique de Nginx via `custom_data`

Application de la configuration :

```bash
terraform apply
```

###  Capture Etape 5
![Etape 5](preuves/etape5.png)

---

#  Etape 6 — Mise en place du Load Balancer

Création de :

- IP publique statique
- Load Balancer (SKU Standard)
- Backend Address Pool
- Association des NIC au backend
- Health Probe HTTP
- Règle de Load Balancing sur le port 80

###  Capture Etape 6
![Etape 6](preuves/etape6.png)

---

#  Etape 7 — Test du Load Balancer

Récupération de l’IP publique :

```bash
terraform output
```

Test via navigateur ou curl :

```bash
curl http://IP_DU_LOAD_BALANCER
```

Résultat observé :
Alternance entre :

- Hello from tp-vm-1
- Hello from tp-vm-2

Preuve que le Load Balancer distribue correctement le trafic.

###  Capture Etape 7
![Etape 7](preuves/etape7.png)

---

#  Etape 8 — Nettoyage de l’infrastructure

Destruction complète des ressources :

```bash
terraform destroy
```

Confirmation de suppression de toutes les ressources.

###  Capture Etape 8 — Partie 1
![Etape 8 Part 1](preuves/etape8-1.png)

###  Capture Etape 8 — Partie 2
![Etape 8 Part 2](preuves/etape8-2.png)

---

#  Conclusion

L’infrastructure Azure a été déployée avec succès à l’aide de Terraform :

- 2 VMs Ubuntu fonctionnelles
- Installation automatique du serveur web Nginx
- Configuration réseau sécurisée
- Load Balancer public opérationnel
- Distribution du trafic validée
- Destruction complète effectuée pour éviter toute consommation de crédit Azure

Ce TP démontre la maîtrise des fondamentaux Terraform avec Azure ainsi que la gestion d’une infrastructure cloud reproductible.