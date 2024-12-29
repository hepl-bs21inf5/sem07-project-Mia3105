# Journal de bord

## Semaine 1

| Tâche     | Temps estimé | Temps passé | Commentaires                      |
| --------- | ------------ | ----------- | --------------------------------- |
| Vue       | 15 minutes   | 10 minutes  |                                   |
| Bootstrap | 30 minutes   | 20 minutes  |                                   |
| Quiz      | 1h           | 2h20        | Pour lancer le lien : npm run dev |
| Rapport   | 20 minutes   | 25 minutes  |                                   |

### Difficultés :

Dans un premier temps, j'ai trouvé assez difficile de faire le compteur de score et de faire le bouton Réinitialiser. J'ai encore un problème, car si toutes les questions sont complétées, le bouton pour réinitialiser fonctionne une première fois comme le bouton Terminer et ensuite en appuyant une deuxième fois, il réinitialise.

### Explications et réflexions sur le code :

- **Questions :**

  1. Expliquer le rôle des fichiers suivants :

  - _main.ts :_
    Il permet d'appeler les modules dont nous aurons besoin dans tous les autres fichiers.
  - _main.css :_
    Il permet de définir le style de la page du quiz avec du css.
  - _App.vue :_
    Il permet de générer un lien URL en local pour visualiser la page.
  - _router/index.ts :_
    C'est un fichier TypeScript. Il permet de lier les chemins aux pages vue.
  - _AboutView.vue :_
    Il permet de définir l'onglet à propos qui donne les informations sur la page.
  - _HomeView.vue :_
    Il définit le titre de la page de quiz, le grand "Quiz" en haut de la page.
  - _QuizForm.vue :_
    Il permet d'écrire tout ce qui sera afficher dans le quiz.

  2. Dans le fichier QuizForm.vue :

  - _Quelles sont les similarités et les différences entre ref et computed ?_

    Les deux permettent de définir un objet.
    ref permet de définir un string, int, ...
    computed permet de définir une fonction, quelque chose qui va être lu et exécuté.

  - _Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?_

    Lorsque l'on clique sur le bouton Terminer, on rentre dans la fonction submit. Cette fonction va compter le nombre de points qui ont été faits et va ensuite ouvrir une fenêtre textuelle qui va afficher un récapitulatif des réponses données et qui va ensuite afficher le score.

  - _Qu'est-ce qu'un v-model ?_

    Cela permet de faire le lien entre la page et le code. S'il y a un changement dans le code, cela changera sur la page et inversement.

  - _À quoi sert le `:class="{ disabled: !filled }"` ?_

    Cela désactive le bouton Terminer tant que la fonction filled ne reçoit pas "True", c'est-à-dire tant que toutes les questions n'ont pas de réponses. Il faut répondre à toutes les questions pour pouvoir appuyer sur le bouton Terminer.

### Suite du projet :

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

### Difficultés :

Je n'ai pas eu de grandes difficultés cette semaine.
Peut-être une petite difficulté pour bien comprendre le fichier QuestionRadio pour être capable de reproduire et d'adapter dans le QuestionText.

### Explications et réflexions sur le code :

- **Questions :**

  - _Quelle est la différence entre un prop et un modèle (v-model) ?_

    Le modèle permet de définir les objets qui pourront être modifiés sur la page après, comme l'état des questions.
    Le prop permet de définir le squelette de la question, les choses qui ne seront jamais modifiées par la suite, comme l'id de la question, le texte, les options, la réponse correcte.

  - _Comment rendre la propriété placeholder optionnelle ?_

    Le placeholder ne serait pas nécessaire si, dans l'intitulé de la question, on écrivait directement que la réponse est un nombre à entrer.

### Suite du projet :

Est-ce que ce serait possible de rendre la création des questions encore plus simple ? D'avoir une sorte de formulaire général avec une boucle qui ferait qu'on n'a pas besoin de faire appel aux QuestionRadio et QuestionText à chaque fois que l'on veut créer une question.

---

## Semaine 3

| Tâche    | Temps estimé | Temps passé | Commentaires |
| -------- | ------------ | ----------- | ------------ |
| Réponses | 1h           | 40 minutes  |              |
| Score    | 40 minutes   | 20 minutes  |              |
| Rapport  | 25 minutes   | 20 minutes  |              |

### Difficultés :

J'ai eu un peu de mal à bien comprendre le watch.

### Explications et réflexions sur le code :

- **Questions :**

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

    La première manière avec le filter fait un tri dans les questions et filtre uniquement les questions qui ont "Correct" comme satut et les met dans une liste. Le score est ensuite la longueur de la liste.
    La deuxième manière avec le for parcourt toutes les questions et quand elle rencontre une question dont le statut est "Correct", elle augmente le nombre "score" de 1.

### Suite du projet :

La suite directe serait de refaire fonctionner les deux boutons.

---

## Semaine 4

| Tâche              | Temps estimé | Temps passé | Commentaires |
| ------------------ | ------------ | ----------- | ------------ |
| État               | 40 minutes   | 30 minutes  |              |
| Boutons            | 50 minutes   | 45 minutes  |              |
| Réponses immuables | 5 minutes    | 5 minutes   |              |
| Rapport            | 25 minutes   | 20 minutes  |              |

### Difficultés :

J'ai de nouveau eu quelques problèmes pour bien saisir comment fonctionne le watch pour le retranscrire dans les autres questions.

### Explications et réflexions sur le code :

- **Questions :**

  - _Comment pourrait-on réécrire la ligne suivante sans l'opérateur ternaire (avec des if et else)_

    `model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;`

    Cette ligne va mettre dans model.value une valeur. Elle vérifie si value.value = props.anwer, si c'est vrai model.value = QuestionState.Correct et si l'égalité est fausse model.value = QuestionState.Wrong.

    Si on écrit cela en code, on obtient :

        if (value.value === props.answer){
          model.value = QuestionState.Correct ;
        }
        else {
          model.value = QuestionState.Wrong ;
        }

  - _Comment pourrait-on réécrire autrement la logique du watch sur value ?_

    La logique du watch sur value est comme cela :

        watch(value, (newValue) => {
          if (newValue === null) {
          model.value = QuestionState.Empty
          } else {
          model.value = QuestionState.Fill
          }
        },
        { immediate: true },
        )

    Elle attribue une valeur à model.valeur en fonction de ce que vaut newValue. On pourrait réécrire cette logique avec un opérateur ternaire :

        watch(value, (newValue) => {
          model.value = newValue === null ? QuestionState.Empty : QuestionState.Fill,
        }
        { immediate: true },
        )

### Suite du projet :

On pourrait vouloir introduire une explication si la réponse est fausse.

---

## Semaine 5

| Tâche             | Temps estimé | Temps passé | Commentaires |
| ----------------- | ------------ | ----------- | ------------ |
| Réponse détaillée | 20 minutes   | 20 minutes  |              |
| Style             | 20 minutes   | 10 minutes  |              |
| Améliorations     | 1h           | 1h30        |              |
| Rapport           | 30 minutes   | 25 minutes  |              |

### Difficultés :
Je n'ai pas rencontré de difficultés particulières cette semaine.

### Explications et réflexions sur le code :

- **Questions :**

  - _Ajouter ce computed dans QuestionRadio.vue :_

        const answerText = computed<string>(() =>
        props.options.find((option) => option.value === props.answer)?.text ??
        props.answer,
        );

    _Remplacer {{ props.answer }} par {{ answerText }} dans le template._
    _Expliquer pourquoi on a fait ce changement ainsi que le code du computed._

    On fait cela pour éviter des fautes. 

    Le `props.otions.find` parcourt la liste des options et regarde si une des options (option.value) correspond à la réponse (props.answer). Si elle trouve une correspondance entre l'answer et une des options, elle utilise alors le texte de l'option comme réponse dans props.answer. Si elle ne trouve aucune option qui ne corresponde à l'answer, alors elle utilise le texte déjà présent dans props.answer. 

    Cela nous permet de faire afficher directement ce que nous avions décidé comme texte pour la réponse au lieu d'afficher ce qui se trouve dans la value. Cela nous permet aussi de nous rendre compte d'éventuelles fautes de frappe qui rendraient la réponse fausse, malgré qu'elle soit vraie.

  - _Que se passe-t-il lorsqu'on ne met pas de valeur à answer-detail ? Est-ce satisfaisant ? Si ce n'est pas le cas, proposer une amélioration._

    Lorsqu'on ne met pas de answer-detail, il y a quand même un tiret qui s'affiche. Ce n'est pas satisfaisant. Il faudrait que rien ne s'affiche s'il n'y a pas d'answer-detail.

    Pour faire cela, il suffit d'ajouter une condition à l'affichage du answerdetail. On veut qu'il s'affiche uniquement s'il y en a un, donc on ajoute un v-if devant son affichage :
    `<p v-if="props.answerDetail" class="blockquote-footer">{{ props.answerDetail }}</p>`
    Avec le 'v-if="props.answerDetail', on vérifie qu'il existe bien et qu'il n'est pas vide. S'il est vide, alors on n'affiche rien (pas de tiret).

### Suite du projet :
La suite du projet est de vraiment personnaliser ma page et d'ajouter différentes améliorations.

---

## Semaine 6

| Tâche                     | Temps estimé | Temps passé | Commentaires                                |
| ------------------------- | ------------ | ----------- | ------------------------------------------- |
| Déploiement               | 10 minutes   | 30 minutes  | J'ai rencontré des problèmes avec le Trivia |
| Améliorations             | 2h           | 3h + ...    | (... = on n'a jamais vraiment fini)         |
| Nettoyage et vérification | 10 minutes   | 15 minutes  |                                             |
| Rapport                   | 40 minutes   | 55 minutes  |                                             |

### Lien : https://hepl-bs21inf5.github.io/sem07-project-Mia3105/#/

### Difficultés :

J'ai rencontré des problèmes avec le QuizTrivia. Il avait été fait en fonction de QuestionRadio et comme entre temps ce fichier a été modifié, il a fallu modifier QuizTrivia en conséquence.

### Explications et réflexions sur le code :

- _Améliorations :_

  - **Les options des QuestionRadio s'affichent de façon aléatoire :**

    J'ai choisi cette option, car je la trouve importante. Elle donne la possibilité de refaire le quiz en réfléchissant un minimum et de ne pas simplement reséléctionner les mêmes options aux mêmes endroits.

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

    Elle parcourt la liste avec un i depuis la fin en remontant et génère un nombre j aléatoire. Elle inverse ensuite la position des éléments i et de j.

    J'ai ensuite utilisé cette fonction sur le tableau de réponses des QuestionRadio.

    En voulant faire cela, j'ai d'abord rencontré un problème. J'ai d'abord fait le Shuffle directement dans le template de la question. En faisant cela, les options se mélangeaient à chaque fois qu'on en choisissait une. J'ai réfléchi au problème et je me suis rendu compte qu'en faisant de cette façon, le Shuffle était inscrit dans la boucle v-for et donc se faisait à chaque changement.
    J'ai été obligé de mettre le tableau mélangé dans un nouveau tableau _questionRadio_options_shuffleX_ dans la partie script. 
    
        const questionRadio_options_shuffle1 = ref(
        shuffleArray([
          { value: '3.1514131211', text: '3.1514131211' },
          { value: '3.1415926535', text: '3.1415926535' },
          { value: '3.1415996633', text: '3.1415996633' },
          { value: '1.1415926535', text: '1.1415926535' },
        ]),
        )

    Je fais ensuite référence à ce nouveau tableau dans les options de réponses: `:options="questionRadio_options_shuffle1"`

    Ainsi, le Shuflle ne se fait plus que quand on recharge la page ou quand on appuie sur le bouton "Réinitialiser" (car je l'ai ajouté dans la fonction reset).

  - **Un nouveau type de questions : QuestionSelect**

    J'ai créé une nouvelle catégorie de questions : les QuestionSelect. Les options de réponses sont contenues dans un menu déroulant. Je trouve intéressant de pouvoir proposer différentes formes de questions, cela permet de varier un peu et de tenir l'utilisateur en alerte.

    Pour faire cela, je me suis basée sur le code des QuestionRadio, parce que le principe est le même sauf que les options ne sont pas directement visibles, et j'ai fait quelques changements.

    J'ai commencé par changer le type et la classe de la question avec select. J'ai ensuite changé la balise input en balise select, car on ne veut pas que l'utilisateur saisisse une donnée (coche une option ou écrive un mot), on veut qu'il sélectionne une option. 

    À ce stade-là, la question s'affichait, mais les options se listaient toutes directement, chacune avec un menu déroulant propre. Il a donc fallu que je déplace la boucle v-for, car elle ne faisait pas au bon endroit. Je n'avais pas besoin que tout se répète, juste que les options soient lues par la boucle. J'ai donc déplacé la boucle qui affiche les options en dessous des informations de la question (après le < select >).
    
    J'ai ensuite dû mettre la balise < label > au-dessus de cette balise select pour props.id soit déclaré avant la définition de la question.

    Le dernier changement a été de changer la balise de la boucle v-for. Avec la balise < div >, le menu déroulant s'affichait autant de fois qu'il y avait d'options. J'ai donc changé la balise < div > en une balise < option >.

        {{ props.text }}
        <select
          :id="props.id"
          v-model="value"
          class="form-select"
          type="select"
          :name="props.id"
          :anwser="answerText"
          :disabled="
            model === QuestionState.Submit ||
            model === QuestionState.Correct ||
            model === QuestionState.Wrong
          "
        >
        <label class="from-select" :for="props.id"/>
          <option v-for="option in props.options" :key="option.value" class="form-select">
            {{ option.text }}
          </option>
        </select>

  - **Une petite box avec un aperçu du statut des questions**

    J'ai créé une petite box flottante qui affiche le statut des questions.

    Je suis partie du "Debug états" que nous avions fait. J'ai fait des modifications dans son style pour qu'il soit flottant et reste toujours en haut de la page. Je l'ai adapté par la suite aux petits écrans en faisait en sorte qu'il descende en bas de la fenêtre en dessous d'une certaine largeur d'écran.

    J'ai été ensuite dans le fichier models.ts et j'ai modifié les mots associés aux différents états. Dans un premier temps, j'ai simplement traduit en français les mots, mais cela faisait énormément "élément du débogage". Alors, je me suis dit que des petites pastilles seraient : ⚪ pour Empty, ⚫ pour Fill, 🟢 pour Correct, 🔴 pour Wrong.

    La dernière chose que j'ai changée est la façon dont les pastilles s'affichaient. Jusqu'ici, elles s'affichaient comme cela : [⚪,⚪], ce qui n'était pas très joli et ce qui ne permettait pas facilement de savoir de quelle question il s'agit. J'ai donc fait une boucle v-for qui parcourt questionStates et qui affiches l'état de chaque question avec son numéro : 1. ⚪ 2. ⚪.

        <div v-for="(state, index) in questionStates" :key="index">
          {{ index + 1 }}. {{ state }}
        </div>

    Je pense que cette façon de faire est bien pour des petits questionnaires, mais si les questionnaires deviennent assez longs, cette box flottante risque de prendre beaucoup de place. Il faudrait que je réfléchisse à une autre façon de la positionner pour être sûr qu'elle n'empiète pas sur le texte des questions quand le nombre de questions devient grand.

  - **Les questions avec Trivia**

    J'ai rendu le quiz Trivia jouable. J'aime bien le fait qu'il y ait un grand nombre de questions aléatoires qui soient générées, cela permet de jouer et de tester sa culture générale sur plein de sujets.

    Le document de base de QuizTrivia est le même que celui dans QuestionRadio. Il a juste fallu faire quelque petit ajustement pour le remettre à niveau, car le QuizRadio avait gagné des fonctionnalités entre temps (entre autres les watch). J'ai supprimé le watch sur model, car il générait une erreur de type et faisait, dans le QuizTrivia, la même chose que l'autre watch.
    J'ai aussi dû faire quelques changements dans les noms : modifier le `:anwser="answerText"` en `:answer="question.correct_answer"`, changer le `v-model="value"` en `v-model="questionStates[index]"`. Avant de changer cela, les boutons ne fonctionnaient pas, les états des questions n'étaient pas pris en compte. J'ai aussi changé le texte des questions pour que les questions soient numérotées.

    J'ai ensuite pris ce qui se trouvait dans le QuizForm et je l'ai adapté pour le QuizTrivia.
    J'ai copier-coller toutes les fonctions et déclarations se trouvant dans la partie script du QuizForm. 
    Je ne crois pas avoir dû faire des changements dans le script pour que le quiz fonctionne. 
    J'ai ajouté une fonction reset qui recharge la page et qui est associer à un bouton "Générer de nouvelles questions" pour que l'apparition de nouvelles questions soit plus intuitive.



  - **Plusieurs options possibles pour les QuestionText**

    Je trouve que cette amélioration est très importante pour les QuestionText. Si on demande un nombre à l'utilisateur, on ne sait pas s'il va le rentrer en chiffre, en lettre, avec une minuscule, avec une majuscule, .... Je trouve très bien de pouvoir accepter plusieurs réponses et ne pas devoir préciser à l'utilisateur qu'il doit obligatoirement entrer des chiffres par exemple.

    J'ai commencé par changer le type de answer, j'avais besoin que ce soit un array, un tableau de valeurs.

    J'ai ensuite dû changer la logique du watch sur réponse. Il a fallu que je l'adapte pour qu'il vérifie si l'option tapée par l'utilisateur se trouvait dans le tableau avec les réponses. Pour cela, j'ai utilisé la fonction `includes()`. J'ai vérifié que `value.value` soit bien dans le tableau `props.answer` et j'ai mis cette valeur dans `reponse.value`. Après avoir fait cela, j'ai eu une erreur, car value.value peut être null et le logiciel n'était pas content de vérifier si la valeur null était dans une liste. J'ai donc gérer l'erreur en lui asignant un string vide si elle était null.

        watch(reponse, (newModel) => {
        if (newModel === QuestionState.Submit) {
          if (value.value == null) {
            value.value = ''
          } else {
            reponse.value = props.answer.includes(value.value)
              ? QuestionState.Correct
              : QuestionState.Wrong
          }
        } else if (newModel === QuestionState.Empty) {
          value.value = null
        }
        })

    Cette amélioration est assez bonne, mais il faudrait essayer de gérer les cases avant de comparer les valeurs. Cela coûte beaucoup de devoir anticiper toutes les possibilités que pourrait rentrer l'utilisateur. Si on peut déjà en avoir un peu moins à gérer un mettant la réponse qu'on récupère toute en minuscule, cela est déjà un peu plus facile.



### Suite du projet :
La suite du projet serait d'améliorer encore le quiz au ajoutant par exemple les QuestionCheck avec les réponses multiples, proposer des questtions sous forme de texte à trous avec des QuestionSelect, .... On peut imaginer beaucoup de choses pour encore améliorer ce quiz. On peut aussi penser à des aspects plus techniques, comme la box à statuts de questions qui devrait être optimisée. 

Je pense que je vais encore pas mal m'amuser avec ce quiz, bien que le projet soit fini. Je vais continuer à essayer de l'améliorer. Je vais aussi pouvoir changer les questions pour me permettre de révisions mes cours et peut-être que je pourrais aussi en faire bon usage dans mon métier d'enseignant.
