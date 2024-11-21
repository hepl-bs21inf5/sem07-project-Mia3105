## Journal de bord

<Semaine 1>

| Tâche     | Temps estimé | Temps passé | Commentaires |
| --------- | ------------ | ----------- | ------------ |
| Vue       | 15 minutes   | 10 minutes  |
| Bootstrap | 30 minutes   | 20 minutes  |
| Quiz      | 1h           | 2h20        |
| Rapport   | 20 minutes   | 25 minutes  |

Difficultés :
Dans un premier temps, j'ai trouvé assez difficile de faire le compteur de score et de faire le bouton Réinitialiser. J'ai encore un problème, car si toutes les questions sont complétées, le bouton pour réinitialiser fonctionne une première fois comme le bouton Temriner et ensuite en appuyant une deuxième fois, il réinitialise.

Explications et réflexions sur le code :
Questions :

    1. Expliquer le rôle des fichiers suivants :
    - main.ts
        Il permet d'appeler les modules dont nous aurons besoin dans tous les autres fichiers.
    - main.css
        Il permet de définir le style de la page du quiz avec du css.
    - App.vue
        Il permet de générer un lien URL en local pour visualiser la page.
    - router/index.ts
        C'est un fichier TypeScript. Il permet de lier les chemins aux page vue.
    - AboutView.vue
        Il permet de définir l'onglet à propos qui donne les informations sur la page.
    - HomeView.vue
        ...
    - QuizForm.vue
        Il permet d'écrire tout ce qui sera afficher dans le quiz.


    2. Dans le fichier QuizForm.vue :
    - Quelles sont les similarités et les différences entre ref et computed ?
        Les deux permettent de définir un objet. ref permet de définir un string, int, ... et le computed permet de définir une fonction, quelque chose qui va être lu et executé.
    - Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?
        Lorsque l'on clique sur le bouton Terminer, on rentre dans la fonction submit. Cette fonction va compter le nombre de point qui ont été fait et va ensuite ouvrir une fenêtre textuelle qui va afficher un récapitulatif dans réponses données et qui va ensuite afficher le score.
    - Qu'est-ce qu'un v-model ?
        Cela permet de faire le lien entre la page et le code. S'il y a un changement dans le code, cela changera sur la page et inversément.

    - À quoi sert le :class="{ disabled: !filled }" ?
        Cela désactive le bouton Terminer tant que la fonction filled ne revoie pas vrai, c'est-à-dire tant que toutes les question n'ont pas de réponses. Il faut répondre à toutes les questions pour pouvoir appuyer sur le bouton Terminer.

Suite du projet :
Je trouve frustrant de devoir à chaque fois tout réécrire, autant pour créer les questions que dans la fonction filled. Il faudrait trouver un moyen d'écrire cela de façon plus concise.

---

<Semaine 2>

| Tâche            | Temps estimé | Temps passé | Commentaires |
| ---------------- | ------------ | ----------- | ------------ |
| QuestionRadio    | 40 minutes   | 25 minutes  |
| QuestionText     | 30 minutes   | 45 minutes  |
| API              | 40 minutes   | 20 minutes  |
| QuestionCheckbox | 40 minutes   | 35 minutes  |
| (BONUS)          |              | + ...       |
| Rapport          | 25 minutes   | 15 minutes  |

Difficultés :
Je n'as pas eu de grande difficultée cette semaine.
Peut-être une petite difficultée pour bien comprendre le fichier QuestionRadio pour être capable de re produire et addapter dans le QuestionText.

Explications et réflexions sur le code :
Questions :

    - Comment rendre la propriété placeholder optionnelle ?
        Le placeholder ne serait pas nécessaire si dans l'intitulé de la quesiton, on écrivait directement que la réponse est un nombre à entrer.

Suite du projet :
Est-ce que ce serait possible de rendre la création des questions encore plus simple ? D'avoir une sorte de formulaire général avec une boucle qui ferait qu'on n'a pas besoin de faire appel aux QuestionRadio et QuestionText à chaque fois que l'on veut crééer un question.

---

<Semaine 3>

| Tâche    | Temps estimé | Temps passé | Commentaires |
| -------- | ------------ | ----------- | ------------ |
| Réponses | 1h           | 40 minutes  |
| Score    | 40 minutes   | 20 minutes  |
| Rapport  | 25 minutes   |             |

Difficultés :

Explications et réflexions sur le code :
Questions : - À quoi sert l'option immediate: true dans le watch ? - Que se passe-t-il si on l'enlève ou si on met immediate: false ?

Proposer une autre manière de calculer le score et comparer les deux méthodes.

Suite du projet :

---

<Semaine 4>

| Tâche   | Temps estimé | Temps passé | Commentaires |
| ------- | ------------ | ----------- | ------------ |
|         |              |             |
|         |              |             |
|         |              |             |
|         |              |             |
| Rapport |              |             |

Difficultés :

Explications et réflexions sur le code :
Questions :

Suite du projet :

---

<Semaine 5>

| Tâche   | Temps estimé | Temps passé | Commentaires |
| ------- | ------------ | ----------- | ------------ |
|         |              |             |
|         |              |             |
|         |              |             |
|         |              |             |
| Rapport |              |             |

Difficultés :

Explications et réflexions sur le code :
Questions :

Suite du projet :

---

<Semaine 6>

| Tâche   | Temps estimé | Temps passé | Commentaires |
| ------- | ------------ | ----------- | ------------ |
|         |              |             |
|         |              |             |
|         |              |             |
|         |              |             |
| Rapport |              |             |

Difficultés :

Explications et réflexions sur le code :
Questions :

Suite du projet :
