### Rapport de TP : Système de Contrôle d'Accès

#### **Introduction**

Dans ce travail pratique, l'objectif était de créer un **système de contrôle d'accès** permettant à un utilisateur de valider son accès à l'aide d'une **carte** et d'un **code secret**. Nous avons utilisé plusieurs concepts, tels que la **logique formelle**, les **automates finis** et les **circuits logiques**, pour concevoir un système robuste et fonctionnel. Ce rapport résume les différentes étapes du projet, des spécifications à la vérification finale.

---

### **1. Spécifications Initiales**

Le système de contrôle d'accès devait permettre à un utilisateur de :
1. Insérer une carte d'accès.
2. Entrer un code secret associé à cette carte.
3. Valider ou refuser l'accès en fonction de la carte et du code.

Les spécifications du système sont les suivantes :
- Si la **carte** est valide et le **code** est correct, l'accès est **accordé**.
- Si la **carte** est valide mais le **code** est incorrect, l'accès est **refusé**.
- Le système devait aussi permettre de **retirer la carte** et de revenir à l'état initial.

Les règles de transition entre les états (attente de carte, vérification du code, accès accordé ou refusé) ont été définies.

---

### **2. Modélisation du Système avec un Automate**

Pour modéliser ce système, j'ai utilisé un **automate fini déterministe (AFD)** qui permet de représenter les **états** et **transitions** du système. Voici les états de l'automate :

1. **AttenteCarte** : L'utilisateur doit insérer une carte.
2. **VerificationCode** : Le système vérifie le code de la carte insérée.
3. **AccesAccorde** : Si la carte et le code sont corrects, l'accès est accordé.
4. **AccesRefuse** : Si le code est incorrect, l'accès est refusé.

Les transitions se font selon les actions de l'utilisateur (insertion de la carte, entrée du code). Si le code est incorrect, l'accès est refusé, et si le code est correct, l'accès est accordé.

---

### **3. Circuits Logiques**

Les règles du système ont été traduites en **expressions logiques** (algèbre de Boole) pour créer les circuits logiques nécessaires à l'implémentation :

- **Accès accordé** : Si la carte est valide et le code est correct, un **ET (AND)** est utilisé pour vérifier ces conditions.
- **Accès refusé** : Si la carte est valide mais le code est incorrect, un **ET (AND)** combiné avec un **NON (NOT)** est utilisé pour tester cette condition.

Les circuits ont été simplifiés à l'aide des **cartes de Karnaugh**, ce qui permet d'optimiser la logique et de réduire le nombre de portes logiques nécessaires.

---

### **4. Vérification du Système**

Après avoir conçu l'automate et les circuits, nous avons vérifié leur bon fonctionnement à l'aide de tests formels. Le but était de nous assurer que toutes les transitions d'état se produisent correctement et que le système respecte les règles de sécurité. 

La vérification a été effectuée à l'aide de la logique formelle pour simuler les différents scénarios (carte valide, code correct, carte invalide, tentatives incorrectes).

---

### **5. Défis Rencontrés et Solutions**

#### **Défis rencontrés** :
- **Gestion des erreurs** : Au début, la gestion des erreurs (tentatives incorrectes) était un peu complexe. Cependant, j'ai choisi de simplifier cette partie en supprimant la gestion des tentatives incorrectes et en me concentrant uniquement sur la validation du code une fois la carte insérée.
  
- **Validation des transitions d'état** : Assurer que les transitions d'un état à l'autre étaient bien définies et fonctionnaient comme prévu a pris un certain temps. Heureusement, l'utilisation d'un automate a facilité la gestion des transitions.

#### **Solutions apportées** :
- J'ai simplifié la gestion des erreurs en enlevant la gestion des tentatives incorrectes et en me concentrant sur l'accès accordé ou refusé uniquement en fonction du code.
  
- Pour les transitions d'état, j'ai utilisé des **outils de model checking** (en logique formelle) pour valider les règles du système et m'assurer que les transitions respectaient les spécifications.

---

### **6. Conclusion**

Le projet a permis de concevoir un **système de contrôle d'accès** simple mais efficace. En utilisant des automates et des circuits logiques, nous avons pu modéliser le système de manière formelle et optimiser les performances à l'aide de l'algèbre de Boole. Le système est désormais capable de vérifier l'accès en fonction de la carte et du code, et offre une gestion fluide des erreurs avec un accès accordé ou refusé.

Ce travail m'a permis de mieux comprendre comment utiliser les **automates finis**, la **logique formelle** et les **circuits logiques** pour modéliser des systèmes réels. Grâce à cette approche formelle, nous avons pu garantir que le système respecte les règles de sécurité tout en étant efficace.

---

### **Améliorations futures**

- Ajouter la gestion des **tentatives incorrectes** pour renforcer la sécurité.
- Permettre l'intégration de **cartes multiples** pour un même utilisateur.
- Intégrer un **système de stockage persistant** pour les cartes et les codes, afin de les enregistrer au-delà de la session.

En résumé, le système est fonctionnel et respecte les spécifications, mais il pourrait être amélioré en ajoutant des fonctionnalités supplémentaires pour le rendre plus robuste et sécurisé.
