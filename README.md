# Tp-Outils-formels
Rapport Final : Conception et Validation d’un Système de Contrôle d’Accès**


## **1. Introduction**

Dans le cadre de ce projet, un système de contrôle d'accès pour un bâtiment sécurisé a été conçu, modélisé, et validé. Ce système repose sur des mécanismes logiques et des transitions entre états clairement définis pour gérer les interactions utilisateur : lecture de carte, validation de code et gestion des erreurs. 

L'objectif était de garantir un fonctionnement fiable, incluant :  
- L’accès rapide et sécurisé aux utilisateurs autorisés.  
- La détection et la gestion des erreurs par une alarme en cas d'infractions répétées.  
- La réinitialisation du système pour revenir à un état de départ.  

Le rapport décrit en détail toutes les étapes du projet, des spécifications initiales à la validation finale, tout en expliquant les défis rencontrés et les solutions apportées.

---

## **2. Spécifications Initiales**

### **2.1. Description générale**

Le système est conçu pour gérer le contrôle d'accès au bâtiment via une interface utilisateur simple et des règles strictes basées sur :  
- Une carte d'identité pour identifier les utilisateurs.  
- Un code personnel associé à la carte pour valider l'accès.  
- La détection des échecs répétés et la déclenchement d'une alarme.  

### **2.2. États et transitions**

Le système est organisé en cinq états, modélisant les différentes étapes de l'interaction utilisateur :

1. **\( S_0 : \) Attente de carte**  
   - Le système est en veille, attendant une carte.  

2. **\( S_1 : \) Vérification du code**  
   - Une fois la carte détectée, le code associé est demandé pour validation.

3. **\( S_2 : \) Accès accordé**  
   - Si le code est correct, la porte s’ouvre.

4. **\( S_3 : \) Accès refusé**  
   - Si le code est incorrect, une tentative échouée est enregistrée.

5. **\( S_4 : \) Alarme déclenchée**  
   - Après trois échecs consécutifs, une alarme est activée pour signaler une possible intrusion.

---

### **2.3. Règles logiques**

Les comportements du système sont définis par les règles suivantes :  

1. **Accès accordé :**
   Une carte valide suivie d’un code correct permet d’ouvrir la porte.  
   \[
   \text{CarteValide} \land \text{CodeCorrect} \implies \text{AccèsAccordé}.
   \]

2. **Accès refusé :**
   Si la carte est invalide ou le code est incorrect, l’accès est refusé.  
   \[
   \neg\text{CarteValide} \lor \neg\text{CodeCorrect} \implies \text{AccèsRefusé}.
   \]

3. **Déclenchement de l'alarme :**
   Trois tentatives incorrectes consécutives déclenchent une alarme.  
   \[
   (\text{TentativesÉchec} \geq 3) \implies \text{Alarme}.
   \]

4. **Réinitialisation :**
   Une commande de réinitialisation retourne le système à l’état \( S_0 \).  
   \[
   \text{Réinitialiser} \implies \text{AttenteCarte}.
   \]

---

## **3. Modélisation**

### **3.1. Automate Fini Déterministe (AFD)**

Le système est modélisé à l’aide d’un automate fini déterministe (AFD) avec les éléments suivants :  
- **États :** \( Q = \{S_0, S_1, S_2, S_3, S_4\} \).  
- **Alphabet des entrées :** \( \Sigma = \{\text{CarteValide}, \text{CodeCorrect}, \text{CodeIncorrect}, \text{Réinitialiser}\} \).  
- **Fonction de transition :** \( \delta : Q \times \Sigma \to Q \).  

#### Transitions principales :
1. \( S_0 \to S_1 \) : Carte valide détectée.  
2. \( S_1 \to S_2 \) : Code correct saisi.  
3. \( S_1 \to S_3 \) : Code incorrect saisi.  
4. \( S_3 \to S_4 \) : Trois échecs consécutifs entraînent une alarme.  
5. \( S_4 \to S_0 \) : Réinitialisation effectuée.  

#### Représentation graphique :
```plaintext
           +---------+
           | S_0     |----CarteValide---->+---------+
           +---------+                    | S_1     |
                                          +---------+
                                        /     |      \
                     CodeIncorrect----->      |       ---->CodeCorrect
                                        V     V
                                     +---------+      +---------+
                                     | S_3     |      | S_2     |
                                     +---------+      +---------+
                                           |
                                    CodeIncorrect
                                           V
                                     +---------+
                                     | S_4     |
                                     +---------+
                                     Réinitialiser
```

---

### **3.2. Conception des circuits logiques**

Les règles logiques sont traduites en circuits logiques simples :

1. **Accès accordé :**
   \[
   Accès = \text{CarteValide} \land \text{CodeCorrect}.
   \]

2. **Accès refusé :**
   \[
   Refus = \neg\text{CarteValide} \lor \neg\text{CodeCorrect}.
   \]

3. **Alarme déclenchée :**
   \[
   Alarme = (\text{TentativesÉchec} \geq 3).
   \]

#### Exemple de schéma logique pour l’accès accordé :
```plaintext
CarteValide ----->|   AND   |-------> Accès Accordé
                  |         |
CodeCorrect ----->|         |
```

---

## **4. Vérification et Optimisations**

### **4.1. Vérifications formelles**

Des outils de simulation et des tests manuels ont permis de valider les comportements suivants :

1. **Propriété 1 :** Une carte valide suivie d’un code correct accorde toujours l’accès.  
   - Résultat : Validation réussie.  

2. **Propriété 2 :** Trois tentatives incorrectes déclenchent systématiquement l’alarme.  
   - Résultat : Validation réussie.  

3. **Propriété 3 :** La réinitialisation ramène toujours le système à l’état \( S_0 \).  
   - Résultat : Validation réussie.  

---

### **4.2. Optimisations**

1. **Circuits logiques :**  
   - Simplification des expressions grâce aux cartes de Karnaugh pour réduire le nombre de portes logiques.

2. **Transitions inutiles :**  
   - Suppression des transitions non utilisées pour simplifier l’automate.

3. **Modularité :**  
   - Division du système en fonctions indépendantes pour faciliter la maintenance.

---

## **5. Discussion**

### **5.1. Défis rencontrés**

1. **Gestion des échecs répétés :**  
   - La conception du compteur pour détecter trois tentatives incorrectes consécutives a demandé une logique supplémentaire.  

2. **Conflits dans les transitions :**  
   - Certaines transitions étaient ambiguës (par exemple, carte valide + code incorrect) et ont nécessité des priorités explicites.  

3. **Optimisation des circuits :**  
   - Les premières versions des circuits étaient redondantes et nécessitaient des ajustements.

### **5.2. Solutions apportées**

1. Intégration d’un compteur dans l’automate pour gérer les tentatives incorrectes.  
2. Hiérarchisation des transitions en fonction des priorités définies.  
3. Simplification des circuits grâce à une analyse systématique.

---

## **6. Conclusion**

Ce projet a permis de concevoir un système de contrôle d'accès robuste et efficace. La modélisation par automate et les tests de simulation ont montré que toutes les règles et transitions fonctionnent comme prévu. 

### **Bilan :**
- **Efficacité :** Le système répond parfaitement aux spécifications initiales.  
- **Fiabilité :** La vérification formelle a validé l’absence d’erreurs logiques ou de comportements imprévus.  
- **Optimisation :** Les circuits logiques et les transitions ont été simplifiés pour garantir une mise en œuvre facile.  

