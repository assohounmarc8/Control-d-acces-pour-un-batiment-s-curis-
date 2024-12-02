### **Rapport de Projet : Système de Contrôle d'Accès**

#### **Introduction**

Le but de ce projet était de concevoir et développer un **système de contrôle d'accès** permettant de valider l'entrée d'un utilisateur à l'aide d'une **carte** et d'un **code secret**. Le système devait permettre de gérer plusieurs tentatives incorrectes, avec la possibilité d'ajouter des cartes et de modifier les codes associés. Ce rapport décrit les étapes du projet, de la conception initiale à la vérification du système, en passant par la gestion des états et des transitions dans l'automate de contrôle.

---

### **1. Spécifications Initiales**

Les spécifications initiales du projet étaient les suivantes :
- **Numéro de Carte et Code Secret** : Chaque utilisateur possède une carte avec un numéro unique et un code secret. L'utilisateur doit insérer la carte et saisir le bon code pour accéder à l'espace sécurisé.
- **Gestion des tentatives incorrectes** : L'utilisateur a droit à **trois tentatives** pour entrer le bon code. Après trois erreurs, l'accès est **bloqué**, et une **alarme** est déclenchée.
- **Ajout et Modification des Cartes** : Le système doit permettre d'ajouter de nouvelles cartes, ainsi que de modifier le code associé à une carte existante.
- **Automate de Contrôle** : Le système repose sur un automate qui passe par différentes étapes : attente de carte, vérification du code, accès accordé, accès refusé, et alarme après trois tentatives incorrectes.

---

### **2. Description du Modèle de l'Automate**

Le **modèle de l'automate** que nous avons utilisé se compose de plusieurs **états** :
1. **`ATTENTE_CARTE`** : L'utilisateur doit insérer une carte.
2. **`VERIFICATION_CODE`** : Une fois la carte insérée, le système vérifie si le code saisi est correct.
3. **`ACCES_ACCORDE`** : Si le code est correct, l'accès est accordé.
4. **`ACCES_REFUSE`** : Si le code est incorrect, l'accès est refusé et l'utilisateur peut essayer à nouveau.
5. **`ALARME`** : Après trois tentatives incorrectes, l'alarme se déclenche.

Chaque transition d'état dépend de l'entrée de l'utilisateur : insérer une carte, saisir un code correct ou incorrect, et retirer la carte.

---

### **3. Vérifications et Tests**

Lors de la réalisation de ce projet, plusieurs tests ont été effectués pour vérifier si le système répondait aux spécifications :
- **Tests d'accès accordé** : Lorsque l'utilisateur insère la bonne carte et le bon code, l'accès est accordé.
- **Tests de refus d'accès** : Lorsque le code saisi est incorrect, l'accès est refusé, et l'utilisateur a trois tentatives pour entrer le bon code.
- **Tests de l'alarme** : Si l'utilisateur entre trois fois un code incorrect, l'alarme se déclenche, et l'accès est définitivement refusé.
- **Ajout et modification des cartes** : Il est possible d'ajouter de nouvelles cartes et de modifier les codes des cartes existantes dans la base de données.

---

### **4. Défis Rencontrés et Solutions Apportées**

#### **Défis**
- **Gestion des tentatives incorrectes** : Un des défis majeurs était de gérer correctement les tentatives incorrectes. Il fallait veiller à ce que l'alarme se déclenche après trois tentatives infructueuses et que l'utilisateur ne puisse plus essayer après cela.
- **Ajout de cartes** : L'ajout et la modification des cartes nécessitaient un mécanisme pour vérifier que les cartes étaient uniques et que les codes associés étaient valides.

#### **Solutions**
- **Gestion des erreurs** : Le système a été conçu pour garder une trace des tentatives incorrectes et pour réinitialiser le compteur si l'utilisateur réussissait à entrer le bon code.
- **Base de données simple** : Une **`HashMap`** a été utilisée pour stocker les cartes et leurs codes. Cela permet d'ajouter, de modifier et de vérifier facilement les cartes.

---

### **5. Conclusion sur l'Efficacité et la Fiabilité du Système**

Ce projet a permis de créer un **système de contrôle d'accès simple et efficace**, qui permet de vérifier si un utilisateur a droit d'accès à un espace sécurisé. Le système répond aux spécifications de base et gère l'insertion de cartes, la vérification des codes, et l'ajout et modification des cartes.

#### **Points forts du système** :
- **Simplicité** : Le système est simple à comprendre et à utiliser grâce à son interface de commande.
- **Gestion des erreurs** : La gestion des tentatives incorrectes et de l'alarme permet de sécuriser l'accès.
- **Extensibilité** : Le système peut facilement être étendu pour intégrer de nouvelles fonctionnalités, comme la gestion des utilisateurs ou l'ajout d'une interface graphique.

#### **Améliorations possibles** :
- **Sécurité renforcée** : Bien que ce système soit simple et fonctionnel, il pourrait être amélioré avec des **mécanismes de sécurité** plus robustes, comme le cryptage des codes ou l'ajout d'une authentification multifactorielle.
- **Base de données** : Le stockage des cartes en mémoire est adapté pour un petit projet, mais il serait préférable d'utiliser une base de données pour des applications à grande échelle.

---

### **Synthèse**

En conclusion, ce projet a permis de concevoir un **système de contrôle d'accès fiable et sécurisé** qui répond aux besoins de base d'un environnement sécurisé. La gestion des cartes et des codes est claire et intuitive, et le système fonctionne comme prévu. Cependant, des améliorations et des optimisations sont possibles, notamment au niveau de la sécurité et de la gestion des données.

