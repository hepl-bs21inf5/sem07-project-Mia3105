# Journal de bord

## Semaine 1

| Tâche     | Temps estimé | Temps passé | Commentaires                      |
| --------- | ------------ | ----------- | --------------------------------- |
| Vue       | 15 minutes   | 10 minutes  |                                   |
| Bootstrap | 30 minutes   | 20 minutes  |                                   |
| Quiz      | 1h           | 2h20        | Pour lancer le lien : npm run dev |
| Rapport   | 20 minutes   | 25 minutes  |                                   |

**Difficultés :**
Dans un premier temps, j'ai trouvé assez difficile de faire le compteur de score et de faire le bouton Réinitialiser. J'ai encore un problème, car si toutes les questions sont complétées, le bouton pour réinitialiser fonctionne une première fois comme le bouton Temriner et ensuite en appuyant une deuxième fois, il réinitialise.

**Explications et réflexions sur le code :**

- _Questions :_

  1. Expliquer le rôle des fichiers suivants :

  - _main.ts :_
    Il permet d'appeler les modules dont nous aurons besoin dans tous les autres fichiers.
  - _main.css :_
    Il permet de définir le style de la page du quiz avec du css.
  - _App.vue :_
    Il permet de générer un lien URL en local pour visualiser la page.
  - _router/index.ts :_
    C'est un fichier TypeScript. Il permet de lier les chemins aux page vue.
  - _AboutView.vue :_
    Il permet de définir l'onglet à propos qui donne les informations sur la page.
  - _HomeView.vue :_
    Il défini le titre de la page de quiz, le grand "Quiz" en haut de la page.
  - _QuizForm.vue :_
    Il permet d'écrire tout ce qui sera afficher dans le quiz.

  2. Dans le fichier QuizForm.vue :

  - _Quelles sont les similarités et les différences entre ref et computed ?_
    Les deux permettent de définir un objet.
    ref permet de définir un string, int, ...
    computed permet de définir une fonction, quelque chose qui va être lu et executé.
  - _Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?_
    Lorsque l'on clique sur le bouton Terminer, on rentre dans la fonction submit. Cette fonction va compter le nombre de point qui ont été fait et va ensuite ouvrir une fenêtre textuelle qui va afficher un récapitulatif des réponses données et qui va ensuite afficher le score.
  - _Qu'est-ce qu'un v-model ?_

    Cela permet de faire le lien entre la page et le code. S'il y a un changement dans le code, cela changera sur la page et inversément.

  - _À quoi sert le :class="{ disabled: !filled }" ?_

    Cela désactive le bouton Terminer tant que la fonction filled ne revoie pas vrai, c'est-à-dire tant que toutes les question n'ont pas de réponses. Il faut répondre à toutes les questions pour pouvoir appuyer sur le bouton Terminer.

**Suite du projet :**
Je trouve frustrant de devoir à chaque fois tout réécrire, autant pour créer les questions que dans la fonction filled. Il faudrait trouver un moyen d'écrire cela de façon plus concise.

---

## Semaine 2

| Tâche                    | Temps estimé | Temps passé | Commentaires                                                                                                                      |
| ------------------------ | ------------ | ----------- | --------------------------------------------------------------------------------------------------------------------------------- |
| QuestionRadio            | 40 minutes   | 25 minutes  |                                                                                                                                   |
| QuestionText             | 30 minutes   | 45 minutes  |                                                                                                                                   |
| API                      | 40 minutes   | 20 minutes  |                                                                                                                                   |
| QuestionCheckbox (BONUS) | 40 minutes   | 35 minutes  | Le bouton Terminer et Réinitialiser ne fonctionnent pas (mais comme ils sont modifiés dans le semaine 3, je n'ai pas plus essayé) |
| Rapport                  | 25 minutes   | 15 minutes  |                                                                                                                                   |

**Difficultés :**
Je n'ai pas eu de grande difficultée cette semaine.
Peut-être une petite difficultée pour bien comprendre le fichier QuestionRadio pour être capable de reproduire et adapter dans le QuestionText.

**Explications et réflexions sur le code :**

- _Questions :_

  - _Quelle est la différence entre un prop et un modèle (v-model) ?_

    Le modèle permet de définir les objets qui pourront être modifiés sur la page après, comme l'état des questions.
    Le prop permet de définir le squelette de la question, les choses qui ne seront jamais modifiée par la suite, comme l'id de la question, le texte, les options, la réponse correcte.

  - _Comment rendre la propriété placeholder optionnelle ?_

    Le placeholder ne serait pas nécessaire si, dans l'intitulé de la quesiton, on écrivait directement que la réponse est un nombre à entrer.

**Suite du projet :**
Est-ce que ce serait possible de rendre la création des questions encore plus simple ? D'avoir une sorte de formulaire général avec une boucle qui ferait qu'on n'a pas besoin de faire appel aux QuestionRadio et QuestionText à chaque fois que l'on veut crééer un question.

---

## Semaine 3

| Tâche    | Temps estimé | Temps passé | Commentaires |
| -------- | ------------ | ----------- | ------------ |
| Réponses | 1h           | 40 minutes  |              |
| Score    | 40 minutes   | 20 minutes  |              |
| Rapport  | 25 minutes   | 20 minutes  |              |

**Difficultés :**
J'ai eu un peu de mal à bien comprendre le watch.

**Explications et réflexions sur le code :**

- _Questions :_

  - _À quoi sert l'option immediate: true dans le watch ?_

    Un watch permet de récupérer les données à chaque fois qu'il y a un changement. Avec l'option immediate:true, le watch récupère une première fois les données lorsqu'il est créé, sans attendre qu'il y ait de changements. Il fonctionne ensuite normalement en récupérant les données à chaque prochain changement.

  - _Que se passe-t-il si on l'enlève ou si on met immediate: false ?_

    Si on ne met pas l'option, alors la première fois que les données seront récupérées sera au premier changement et pas avant.

  - _Proposer une autre manière de calculer le score et comparer les deux méthodes._$

    Manière du cours : avec un filter

          const score = computed<number>(
              () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
          )

    Autre manière : avec une boucle for

          const score = computed<number>(() => {
          let score = 0;
          for (let i = 0; i < questionStates.value.length; i++) {
              if (questionStates.value[i] === QuestionState.Correct) {
              score = score + 1;
              }
          }
          return score;
          })

    La première manière avec le filter fait un tri dans les questions et filtre uniquement les questions qui ont "Correct" comme satus et les met dans une liste. Le score est ensuite la longueur de la liste.
    La deuxième manière avec le for parcourt toutes les questions et quand elle rencontre une question dont le statut est "Correct", elle augmente le nombre "score" de 1.

**Suite du projet :**
La suite directe serait de refaire fonctionner les deux boutons.

---

## Semaine 4

| Tâche              | Temps estimé | Temps passé | Commentaires |
| ------------------ | ------------ | ----------- | ------------ |
| État               | 40 minutes   | 30 minutes  |              |
| Boutons            | 50 minutes   | 45 minutes  |              |
| Réponses immuables | 5 minutes    | 5 minutes   |              |
| Rapport            | 25 minutes   | 20 minutes  |              |

**Difficultés :**

**Explications et réflexions sur le code :**

- _Questions :_

  - _Comment pourrait-on réécrire la ligne suivante sans l'opérateur ternaire (avec des if et else)_
  
    `model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;`

    Cette ligne va mettre dans model.value une valeur. Elle vérifie si value.value = props.anwer, si c'est vrai model.value = QuestionState.Correct et si l'égalité est fausse model.value = QuestionState.Wrong. 

    Si on écrit cela en code on obtient :

        if (value.value === props.answer){
          model.value = QuestionState.Correct ;
        } 
        else {
          model.value = QuestionState.Wrong ;
        } 

  - _Comment pourrait-on réécrire autrement la logique du watch sur value ?_

    ...... (à répondre)

**Suite du projet :**
...... (à répondre)

---

## Semaine 5

| Tâche             | Temps estimé | Temps passé | Commentaires |
| ----------------- | ------------ | ----------- | ------------ |
| Réponse détaillée | 20 minutes   | 20 minutes  |              |
| Style             | 20 minutes   | 10 minutes  |              |
| Amélioration      | ...          |             |              |
|                   |              |             |              |
| Rapport           | 30 minutes   | 25 minutes  |              |

**Difficultés :**

**Explications et réflexions sur le code :**

- _Questions :_

  - _Ajouter ce computed dans QuestionRadio.vue :_

        `const answerText = computed<string>(() =>

    props.options.find((option) => option.value === props.answer)?.text ??
    props.answer,
    ); `

        _Remplacer {{ props.answer }} par {{ answerText }} dans le template._
        _Expliquer pourquoi on a fait ce changement ainsi que le code du computed._

        ....

  - _Que se passe-t-il lorsqu'on ne met pas de valeur à answer-detail ? Est-ce satisfaisant ? Si ce n'est pas le cas, proposer une amélioration._

    ...

**Suite du projet :**

---

## Semaine 6

| Tâche                     | Temps estimé | Temps passé | Commentaires                                |
| ------------------------- | ------------ | ----------- | ------------------------------------------- |
| Déploiement               | 10 minutes   | 30 minutes  | J'ai rencontré des problèmes avec le Trivia |
| Améliorations             | 2h           | 3h          |                                             |
| Nettoyage et vérification | 10 minutes   | 15 minutes  |                                             |
| Rapport                   | 40 minutes   | 55 minutes  |                                             |

**Lien :** https://hepl-bs21inf5.github.io/sem07-project-Mia3105/

**Difficultés :**
J'ai rencontré des problèmes avec le QuizTrivia. Il avait été fait en fonction de QuestionRadio et comme entre temps ce fichier a été modifié, il a fallu modifier QuizTrivia en conséquence.

**Explications et réflexions sur le code :**

- _Améliorations :_

  - **Les options des QuestionRadio s'affichent de façon aléatoire :**

    J'ai choisi cette option car je la trouve importante. Elle donne la possibilité de refaire le quiz en réfléchissant un minimum et de ne pas simplement reséléctionner les mêmes options aux mêmes endroits.

    J'ai implémenté cette option dans le QuizForm. 
    J'ai pris une fonction ShuffleArray qui j'ai trouvé sur un forum :

          function shuffleArray<T>(array: T[]): T[] {
            const shuffled = [...array]
            for (let i = shuffled.length - 1; i > 0; i--) {
              const j = Math.floor(Math.random() * (i + 1));
              [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]]
            }
            return shuffled
          }

    Elle parcours la liste avec un i depuis la fin en remontant et génère un nombre j aléatoire. Elle inverse ensuite la position des éléments i et de j.

    J'ai ensuite utilisé cette fonction sur le tableau de réponses des QuestionRadio. 
    
    En voulant faire cela, j'ai d'abord rencontré un problème. J'ai d'abord fait le Shuffle directement dans le template de la question. En faisant cela, les options se mélangeaient à chaque fois qu'on en choisissait une. J'ai réfléchi au problème et je me suis rendu compte qu'en faisant de cette façon, le Shuffle était inscrit dans la boucle v-for et donc se faisait à chaque changement. 
    J'ai été obligé de mettre le tableau mélangé dans un nouveau tableau *questionRadiooptionsshuffleX* dans la partie script. Je fais ensuite référence à ce nouveau tableau dans les options de réponses. Ainsi le Shuflle ne se fait plus que quand on recharge la page ou quand on appuie sur le bouton "Réinitialiser" (car je l'ai ajouté dans la fonction reset).



  - **Un nouveau type de questions : QuestionSelect**

    L


  - **Une petite box avec un aperçu du statut des questions**

    L

  - **Les questions avec Trivia**

    L

  - **Plusieurs options possibles pour les QuestionText**

    L

**Suite du projet :**
