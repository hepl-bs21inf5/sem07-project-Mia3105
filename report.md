## Journal de bord

Semaine 1
Tache | Temps estimé | Temps passé | Commentaires
Vue | 15 minutes | 10 minutes |  
Bootstrap | 30 minutes | 20 minutes |
Quiz | 1h | 10h45 - 13h + ... |
Rapport | 20 minutes | |

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
        C'est un fichier TypeScript. Il permet de ...
    - AboutView.vue
        Il permet de définir la mise en page du quiz.
    - HomeView.vue

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
