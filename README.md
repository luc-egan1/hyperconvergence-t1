# VIRT-07 Projet HCI

Ce dépôt centralise la conception, la documentation et les futurs scripts du POC HCI réalisé à partir de composants open source assemblés séparément.

Le projet est en phase de conception. L'installation et les tests de fonctionnement restent à réaliser.

## Architecture proposée

| Couche | Composant envisagé |
| --- | --- |
| Système des nœuds | Debian GNU/Linux, version à confirmer |
| Orchestration | Kubernetes, méthode d'installation et versions à fixer |
| Virtualisation | KubeVirt avec QEMU/KVM |
| Stockage distribué | Longhorn sur des disques dédiés aux données |
| Import des images de VM | CDI, à intégrer au POC |
| Automatisation | Ansible, manifests YAML et templates de VM |
| Interface web des VM | À sélectionner et à valider |

Le POC cible trois nœuds qui exécutent les VM et hébergent leurs données répliquées. Les ressources matérielles, l'adressage et les interfaces réseau restent à renseigner.

L'accès distant à l'hôte Proxmox du laboratoire a été envisagé via Tailscale. La solution HCI du projet sera assemblée dans les nœuds Debian. Si ceux-ci sont virtualisés dans Proxmox, l'accès à la virtualisation imbriquée devra être vérifié.

## Fonctions à démontrer

- Créer une VM depuis un modèle.
- Démarrer et arrêter une VM.
- Consulter son état, son hôte et ses ressources.
- Répartir des VM sur plusieurs nœuds avec un stockage distribué.
- Migrer une VM à chaud entre deux nœuds du même cluster, périmètre à confirmer.
- Reproduire l'installation à partir de la documentation et des scripts.

KubeVirt fournit une API de gestion des VM. Le parcours web complet devra être validé avec l'interface retenue. Pour les disques Longhorn migratables, prévoir une StorageClass avec `migratable: "true"` et des PVC en `ReadWriteMany` avec `volumeMode: Block`, à vérifier avec les versions sélectionnées.

## Documents présents

- [Sujet du projet](VIRT-07%20%C2%B5projet%20HCI%20from%20scratch.pdf)
- [Fiche à compléter](VIRT-07%20%C2%B5projet%20HCI%20from%20scratch%20fiche%20info.docx)

Une fiche préremplie issue de la première proposition KVM/libvirt et Ceph existe dans le dossier de travail. Elle devra être actualisée si Kubernetes, KubeVirt et Longhorn sont retenus.

## Livrables prévus

- DAT avec les composants, leurs justifications, les schémas, le dimensionnement et le plan réseau.
- DEX avec l'installation du premier nœud, l'ajout des suivants, l'utilisation et le dépannage.
- Playbooks Ansible et inventaire exemple.
- Manifests et templates de VM, références et sommes de contrôle des images.
- Procédures et résultats des tests, dont la migration à chaud.

## Prochaines étapes

1. Confirmer les ressources des trois nœuds Debian et le périmètre de migration.
2. Choisir l'interface web de gestion des VM.
3. Figer les versions et le plan réseau.
4. Mettre à jour la fiche et le DAT.
5. Installer le premier nœud, puis étendre le cluster.
6. Automatiser et exécuter les scénarios de validation.

Les déploiements seront déclenchés explicitement depuis un poste d'administration. Les fichiers locaux de secrets, les kubeconfigs et les images de disques doivent être conservés hors du dépôt.

## Références techniques

- [Installation de KubeVirt](https://kubevirt.io/user-guide/cluster_admin/installation/)
- [Utilisation et interface de KubeVirt](https://kubevirt.io/user-guide/user_workloads/basic_use/)
- [Documentation Longhorn](https://longhorn.io/docs/)
- [Migration KubeVirt](https://kubevirt.io/user-guide/compute/live_migration/)
