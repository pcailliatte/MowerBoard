# Guide de Contribution

Merci de votre intérêt pour le projet **MowerBoard** ! Ce guide explique comment contribuer efficacement au projet.

## 📋 Table des matières

- [Code de conduite](#-code-de-conduite)
- [Avant de commencer](#-avant-de-commencer)
- [Comment contribuer](#-comment-contribuer)
- [Processus de Pull Request](#-processus-de-pull-request)
- [Directives de code](#-directives-de-code)
- [Directives de documentation](#-directives-de-documentation)
- [Signalement de bugs](#-signalement-de-bugs)
- [Suggestions d'améliorations](#-suggestions-daméliorations)
- [Questions & Support](#-questions--support)

---

## 🤝 Code de conduite

Ce projet adhère à un code de conduite inclusif. En participant, vous vous engagez à :

*   Traiter tous les contributeurs avec respect et bienveillance
*   Accepter les critiques constructives
*   Vous concentrer sur ce qui est meilleur pour la communauté
*   Respecter les différents points de vue et expériences

**Les comportements inacceptables incluent :** le harcèlement, les discriminations, les insultes, les attaques personnelles.

---

## ⚠️ Avant de commencer

### Important : Sécurité d'abord

**MowerBoard contrôle une machine dangereuse.** Avant toute contribution matérielle ou firmware :

1. ✅ Vous acceptez la clause de non-responsabilité du projet
2. ✅ Vous comprenez les risques de sécurité associés
3. ✅ Vous testez vos changements dans un environnement **isolé et sécurisé**
4. ✅ Vous documentez les implications de sécurité de vos modifications

Tout code ou schéma contribué doit **maintenir ou améliorer** les normes de sécurité existantes.

### Vérifier les ressources existantes

*   Consultez la documentation dans `/Doc`
*   Parcourez les Issues ouvertes pour voir si votre idée est déjà discutée
*   Regardez les Pull Requests en cours
*   Lisez le README.md et la LICENCE.MD

---

## 🚀 Comment contribuer

### 1. Fork le projet

Cliquez sur le bouton **Fork** en haut à droite du dépôt.

```bash
git clone https://github.com/pcailliatte/MowerBoard.git
cd MowerBoard
```

### 2. Créer une branche

Utilisez un nom de branche descriptif :

```bash
git checkout -b feature/description-courte
```

**Conventions de nommage :**
*   `feature/` – Nouvelle fonctionnalité
*   `bugfix/` – Correction de bug
*   `docs/` – Mise à jour de documentation
*   `refactor/` – Refonte de code existant
*   `test/` – Ajout de tests

Exemples valides :
```
feature/securite-arret-urgence
bugfix/watchdog-timeout
docs/guide-assemblage
refactor/optimisation-interruptions
```

### 3. Effectuer vos modifications

*   Suivez les directives de code (voir ci-dessous)
*   Committez régulièrement avec des messages clairs
*   Testez vos changements avant de pousser

### 4. Pousser vers votre fork

```bash
git push origin feature/description-courte
```

### 5. Créer une Pull Request

Allez sur le dépôt original et cliquez sur **New Pull Request**.

---

## 🔄 Processus de Pull Request

### Template de PR (à remplir)

```
## Description
Décrivez clairement ce que change cette PR et pourquoi.

## Type de changement
- [ ] Nouvelle fonctionnalité
- [ ] Correction de bug
- [ ] Mise à jour de documentation
- [ ] Refonte de code
- [ ] Autre : ...

## Changements apportés
- Point 1
- Point 2
- Point 3

## Tests effectués
Décrivez les tests menés pour valider ces changements.

## Implications de sécurité
- [ ] Aucune implication de sécurité
- [ ] Voir détails ci-dessous

[Détails si applicable]

## Checklist
- [ ] Mon code suit les directives du projet
- [ ] J'ai testé mes changements
- [ ] J'ai mis à jour la documentation
- [ ] Je n'ai pas d'avertissements de compilation
- [ ] Mes commits ont des messages clairs
```

### Ce qu'on recherche dans une bonne PR

✅ **Scope limité** – Une PR = un changement logique  
✅ **Tests validants** – Prouvez que ça fonctionne  
✅ **Documentation** – Expliquez vos changements  
✅ **Messages de commit clairs** – Utilisez l'impératif présent  
✅ **Pas de conflits** – Rebasez sur `main` si nécessaire  

### Processus de review

1. Au moins un mainteneur review la PR
2. Les changements demandés sont signalés
3. Vous avez une semaine pour répondre
4. Une fois approuvée, la PR est mergée

---

## 💻 Directives de code

### Firmware (C)

#### Style général

*   **Indentation :** 4 espaces (pas de tabs)
*   **Longueur des lignes :** Max 100 caractères
*   **Commentaires :** En français ou anglais, clairs et utiles

```c
// Mauvais
int x = 5;

// Bon
// Délai d'attente pour le watchdog en millisecondes
int watchdog_timeout_ms = 5;
```

#### Nommage

```c
// Variables & fonctions : snake_case
int motor_speed = 100;
void enable_blade_clutch(void);

// Constantes : UPPER_SNAKE_CASE
#define MAX_MOTOR_SPEED 255
#define SAFETY_TIMEOUT_MS 1000
```

#### Sécurité

*   **Pas de magic numbers** – Utilisez des `#define`
*   **Vérifications de limites** – Validez les entrées
*   **Gestion d'erreurs** – Retournez des codes d'erreur explicites
*   **Watchdog** – Incluez des points de contrôle réguliers

```c
// Mauvais
void set_speed(int speed) {
    motor_speed = speed;
}

// Bon
int set_speed(int requested_speed) {
    if (requested_speed < 0 || requested_speed > MAX_MOTOR_SPEED) {
        return ERROR_INVALID_SPEED;
    }
    motor_speed = requested_speed;
    return SUCCESS;
}
```

#### Documentation de fonction

```c
/**
 * Configure la vitesse du moteur
 * 
 * @param speed : Vitesse cible (0-255)
 * @return : 0 si succès, code d'erreur sinon
 * @note : Cette fonction met à jour le watchdog
 */
int set_motor_speed(int speed);
```

### Hardware (KiCad)

#### Conventions d'étiquetage

*   **Références** : U1, R1, C1 (standard KiCad)
*   **Valeurs** : Claires et lisibles
*   **Noms de nets** : Descriptifs
    - PWR_12V, GND, BLADE_CMD
    - Pas de numéros génériques comme N1, N2

#### Bonne pratique

*   Utilisez des symboles KiCad standard
*   Regroupez les fonctions logiques sur des pages séparées
*   Documentez les choix critiques dans le schéma
*   Incluez les feuilles de données des composants clés

---

## 📖 Directives de documentation

*   **Langage :** Français de préférence, anglais acceptable
*   **Format :** Markdown (.md)
*   **Structure :** Titres, listes, code blocks
*   **Liens :** Vérifiez que les liens fonctionnent
*   **Images :** Optimisées et sous /Doc/assets

### Template de nouvelle doc

```markdown
# Titre Clair et Descriptif

## Introduction
Contexte et objectif.

## Étapes / Sections
...

## Dépannage
Problèmes courants et solutions.

## Ressources
Liens et références utiles.
```

---

## 🐛 Signalement de bugs

### Avant de signaler

1. Vérifiez que le bug n'est pas déjà signalé
2. Testez avec la version la plus récente
3. Isolez le problème au maximum

### Comment signaler

Cliquez sur Issues et remplissez :

```
## Description du bug
Décrivez le problème clairement et concisément.

## Étapes pour reproduire
1. Étape 1
2. Étape 2
3. ...

## Comportement attendu
Ce qui devrait se passer.

## Comportement observé
Ce qui s'est réellement passé.

## Environnement
- Hardware : [ex: AVR ATmega328P]
- Compilateur : [ex: MPLAB X v6.15, XC8]
- OS : [ex: Windows 10, Linux]

## Logs / Captures d'écran
[Si applicable]

## Contexte supplémentaire
Toute autre information utile.
```

---

## 💡 Suggestions d'améliorations

Vous avez une idée pour améliorer le projet ? Ouvrez une Discussion ou une Issue avec le label `enhancement`.

**Décrivez :**
*   Le problème que ça résout
*   La solution proposée
*   Les avantages et inconvénients
*   Les impacts potentiels

---

## ❓ Questions & Support

*   **Questions techniques :** Ouvrez une Discussion
*   **Bugs :** Créez une Issue
*   **Chats informels :** Utilisez les Discussions

---

## 📜 Licence

En contribuant à ce projet, vous acceptez que vos contributions soient licenciées sous la **CERN Open Hardware Licence - Strong Reciprocal v2 (CERN-OHL-S v2)**.

Cela signifie que votre code/schéma peut être utilisé, modifié et distribué sous les mêmes conditions ouvertes.

---

## 🙏 Remerciements

Merci de votre contribution à MowerBoard ! Chaque amélioration rapproche le projet d'une solution de contrôle ouverte et sûre pour les tracteurs tondeuses.

---

**Questions sur ce guide ?** Ouvrez une Discussion !
