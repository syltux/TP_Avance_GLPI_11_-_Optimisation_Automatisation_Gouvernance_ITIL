# Rapport de TP SLA EXEC AUTO - Syltux

![Capture d'écran](/medias/Capture%20d’écran%20(1579).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1580).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1581).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1582).png)


# Rapport de TP Avancé GLPI 11 : Optimisation, Automatisation et Gouvernance ITIL sur GLPI 11 - Syltux

**Environnement de déploiement :** Debian 13 (Client / Server) sur VMware Workstation.

**Prérequis:** Création des utilisateurs pour le TP

![Capture d'écran](/medias/Capture%20d’écran%20(1587).png)

---

## Partie 1 : Structuration Multi-Entités et Profils (Gouvernance)

### 1. Arborescence des Entités
Afin de répondre aux besoins de cloisonnement de l'entreprise "CleanHouse Robotics", une sous-entité dédiée a été créée :
* **Structure :** `Entité Racine (CleanHouse Robotics)` -> `Département R&D`. L'entité racine a été renommée en `CleanHouse Robotics`


![Capture d'écran](/medias/Capture%20d’écran%20(1592).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1593).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1594).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1595).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1596).png)

* **Configuration :** La sous-entité `Département R&D` a été configurée avec des paramètres personnalisés pour ne pas hériter des notifications de l'entité racine, garantissant l'isolation complète des alertes opérationnelles.

### 2. Profil personnalisé "Technicien Niveau 2"
Un profil sur-mesure a été configuré pour l'équipe technique de support avancé. 
![Capture d'écran](/medias/Capture%20d’écran%20(1597).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1598).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1599).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1600).png)


* **Habilitations accordées :** Droits explicites pour valider des demandes de changement et créer/gérer des Problèmes.
![Capture d'écran](/medias/Capture%20d’écran%20(1605).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1608).png)
* **Restrictions de sécurité :** Interdiction stricte de supprimer des composants au niveau de l'inventaire général (CMDB).
![Capture d'écran](/medias/Capture%20d’écran%20(1607).png)

* **Affectation :** L'utilisateur `tech.support` a été associé à ce profil spécifique de manière récursive depuis l'entité racine.
![Capture d'écran](/medias/Capture%20d’écran%20(1611).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1613).png)

---

## Partie 2 : Automatisation & Moteur de Règles

### 1. Règle métier pour l'aiguillage des incidents d'impression
Pour automatiser le traitement et le dispatching des requêtes de premier niveau, une règle métier a été implémentée :
* **Critères :** Analyse automatisée du titre ou de la description pour intercepter les mots-clés "Imprimante" ou "Copieur".
* **Actions appliquées :** 
  * Assignation automatique du ticket au groupe d'experts : `Support Infrastructures`.
  ![Capture d'écran](/medias/Capture%20d’écran%20(1614).png)
  ![Capture d'écran](/medias/Capture%20d’écran%20(1616).png)
  Création du groupe `Support Infrastructures`
    ![Capture d'écran](/medias/Capture%20d’écran%20(1617).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1614).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1615).png) 
    ![Capture d'écran](/medias/Capture%20d’écran%20(1617).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1621).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1632).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1633).png)
    Assignation.
  * Catégorisation ITIL automatique : `Matériel -> Impression` (création de la catégorie ITIL `Impression`).
    ![Capture d'écran](/medias/Capture%20d’écran%20(1634).png)
  * Définition d'un niveau d'impact : `Moyen`.
  * Test de la règle.
    ![Capture d'écran](/medias/Capture%20d’écran%20(1643).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1645).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1649).png)
    ![Capture d'écran](/medias/Capture%20d’écran%20(1650).png)
### 2. Collecteur de mails automatique
Cette partie a été laissée pour plus tard et n'a donc pas été traitée.

---

## Partie 3 : Gestion des Engagements (SLA / OLA)

Afin de garantir la résolution des incidents critiques selon les exigences métier :
* **Contrat SLA :** Création du `SLA _ Incidents Critiques` configuré avec un temps de résolution (TTR) de 2 heures, actif en calendrier 24h/24 et 7j/7.

![Capture d'écran](/medias/Capture%20d’écran%20(1651).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1652).png)

* **Niveaux d'escalade automatique :**
  * **À T - 30 min avant l'échéance :** Envoi d'un courriel de rappel de vigilance automatique au technicien en charge.
  * **À T + 1 min (Dépassement) :** Changement automatique du groupe assigné vers `Responsables IT` et bascule immédiate du statut du ticket en `Urgent`.

![Capture d'écran](/medias/Capture%20d’écran%20(1653).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1654).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1655).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1656).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1657).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1658).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1659).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1660).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1661).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1662).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1663).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1664).png)

---

## Partie 4 : Workflow ITIL Avancé (Gestion des Incidents, Problèmes et Changements)

### 1. Cycle de l'Incident majeur au Problème
Suite à une indisponibilité totale du serveur de production hébergeant l'ERP, le workflow de gestion des incidents majeurs a été mené :
* Réception et centralisation de 3 tickets d'incidents distincts signalant la panne ERP.

![Capture d'écran](/medias/Capture%20d’écran%20(1667).png)

* Création d'un ticket **Problème** transverse nommé : `Panne récurrente Base de données ERP`.

![Capture d'écran](/medias/Capture%20d’écran%20(1667).png)

* Liaison des 3 incidents au Problème pour centraliser l'analyse de cause racine.


### 2. Initialisation et Approbation du Changement
L'analyse technique ayant conclu à la nécessité de remplacer le stockage, un changement de l'infrastructure a été planifié :
* Génération d'un ticket de **Changement** lié au Problème : `Migration des disques de l'ERP vers un stockage SSD`.
* Documentation d'un plan de repli (Rollback) dans l'onglet dédié.
![Capture d'écran](/medias/Capture%20d’écran%20(1745).png)
* Soumission d'une demande de validation obligatoire affectée au responsable `manager.it`.

![Capture d'écran](/medias/Capture%20d’écran%20(1668).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1669).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1670).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1671).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1672).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1673).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1674).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1675).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1676).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1677).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1678).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1679).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1680).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1683).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1684).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1685).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1686).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1687).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1688).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1689).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1690).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1691).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1692).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1693).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1694).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1695).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1696).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1697).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1698).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1699).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1700).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1701).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1702).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1703).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1704).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1705).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1706).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1707).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1708).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1709).png)

### 3. Application de la Solution et Clôture
* La demande de validation a été approuvée par le gestionnaire.
* Le statut du Changement a été passé à **Appliqué** suite à l'intervention technique.
* Le Changement a été définitivement basculé à l'état **Clos** après enregistrement de la solution.
![Capture d'écran](/medias/Capture%20d’écran%20(1710).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1711).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1712).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1713).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1714).png)

Dans l'état actuel de GLPI v11, la cascade ne remonte pas au statut du problème et des tickets d'incident.

---

## Partie 5 : Sécurisation & Maintenance de la Plateforme (Hardening)

### 1. Sécurisation du Webroot (Dossier Public)
Afin de se conformer aux exigences de durcissement (hardening) de GLPI 11 et d'isoler les dossiers sensibles (`/config`, `/files`), le point d'entrée du serveur Web Apache a été restreint au seul répertoire public.

La directive `DocumentRoot` au sein du fichier `/etc/apache2/sites-available/000-default.conf` a été modifiée :
```apache
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/glpi/public

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
![Capture d'écran](/medias/Capture%20d’écran%20(1715).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1716).png)

Le service a ensuite été redémarré pour appliquer les restrictions :

```Bash
sudo systemctl restart apache2
```

### 2. Sécurisation des scripts d'installation

Conformément aux bonnes pratiques de mise en production, le script d'installation a été complètement purgé de l'arborescence pour empêcher toute réinitialisation malveillante de la base de données :

```Bash
sudo rm -rf /var/www/html/glpi/install/install.php
```
Cette commande avait été appliquée lors de la finalisation de l'installation de GLPI et a donc été ignorée ici.

### 3. Externalisation des Tâches Planifiées (Mode CLI / Cron système)
Afin de libérer GLPI du mode Ajax (qui nécessite qu'un utilisateur navigue sur le site pour déclencher les tâches en arrière-plan), l'ensemble des actions automatiques a été délégué au démon Cron de l'OS Debian.

La crontab de l'utilisateur de l'application Web (www-data) a été ouverte pour édition :

```Bash
sudo crontab -u www-data -e
```
![Capture d'écran](/medias/Capture%20d’écran%20(1717).png)

Ouverture de la table crontab système.

La tâche planifiée suivante a été ajoutée pour exécuter le moteur GLPI toutes les minutes :

```Nano
* * * * * /usr/bin/php /var/www/html/glpi/front/cron.php &>/dev/null
```

![Capture d'écran](/medias/Capture%20d’écran%20(1718).png)

Configuration de la ligne cron dans l'éditeur.

![Capture d'écran](/medias/Capture%20d’écran%20(1719).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1720).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1721).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1722).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1723).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1724).png)
![Capture d'écran](/medias/Capture%20d’écran%20(1725).png)

Validation finale sur l'interface graphique.

L'intégralité des actions de maintenance et de synchronisation (notamment mailgate, closeticket, logs, cartridge, etc.) ont été basculées en masse du mode GLPI vers le mode d'exécution CLI via les Actions.

Modification groupée du mode d'exécution et vue d'ensemble finale des tâches migrées en mode CLI.