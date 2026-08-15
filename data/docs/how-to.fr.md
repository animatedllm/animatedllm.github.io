# Comment utiliser l'application

Vous êtes enseignant, étudiant ou juste un curieux de passage ?

Bienvenue ! Dans ce bref aperçu, vous découvrirez ce que cette application peut faire et comment en tirer le meilleur parti.

## À quoi sert l'application ?

**Commençons par ce que AnimatedLLM n'est pas.**

AnimatedLLM n'est pas (du moins pour l'instant !) une application éducative complète qui vous guidera à travers le fonctionnement des grands modèles de langage de A à Z.

Pour bien comprendre le sujet, vous devrez également consulter d'autres ressources.

Pour commencer, essayez cette courte vidéo de la chaîne [3Blue1Brown](https://www.youtube.com/@3blue1brown/videos) (en anglais, avec des sous-titres dans de nombreuses langues) :

<iframe width="560" height="315" src="https://www.youtube.com/embed/LPZh9BOjkQs?si=Nogb8BgfP9kL1DIa" title="YouTube video player" frameborder="0" allow="clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Vous trouverez de nombreux autres supports sur Internet. Parmi les ressources de qualité, citons ces articles de blog illustrés de Jay Alammar :

- **[Illustrated GPT-2](https://jalammar.github.io/illustrated-gpt2/)**
- **[Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)**

Pour les étudiants tchèques, il existe des cours universitaires directement axés sur les grands modèles de langage :

- **MFF UK :** [Large Language Models (NPFL140)](https://ufal.mff.cuni.cz/courses/npfl140)
- **FIT ČVUT :** [Neural Language Models (NI-NLM)](https://bilakniha.cvut.cz/en/predmet8241006.html)
 
 
(Note : l'auteur de l'application participe au premier cours et dirige le second 😇)

**Alors, à quoi sert AnimatedLLM ?**

Les animations d'AnimatedLLM servent principalement d'outil pédagogique. Elles aident à expliquer les principes de fonctionnement des modèles de langage qui, autrement, nécessiteraient de longues explications gestuelles ou des schémas au tableau.

Par exemple :
- D'où vient le texte généré par le modèle ?
- Que signifie le fait qu'un modèle soit « entraîné sur des documents » ?
- D'où proviennent exactement les probabilités du prochain token ?
- etc.


Cependant, comprendre pourquoi nous abordons ces processus, comment les modèles de langage sont nés et quel est leur rôle dans des services complexes comme ChatGPT, Gemini ou Claude, est un sujet qu'il faudra étudier ailleurs.


**Dernier avertissement...**

Certains principes des modèles de langage sont simplifiés dans AnimatedLLM. Pas de manière excessive, mais certains détails techniques sont omis par souci de clarté.

Si ces détails techniques vous intéressent, les animations suivantes approfondissent davantage l'architecture des modèles :
- [llm-viz](https://bbycroft.net/llm)
- [Transformer Explainer](https://poloclub.github.io/transformer-explainer/)

## Comment l'application fonctionne-t-elle ?

Les animations de AnimatedLLM sont des **interactions enregistrées avec de réels modèles de langage**.

Cela signifie deux choses :
- Les animations montrent le comportement réaliste de véritables modèles de langage.
- Aucun modèle de langage ne tourne réellement pendant les animations ; il s'agit simplement d'un enregistrement lu dans le navigateur.

### Comment les enregistrements ont-ils été créés ?
Les enregistrements ont été générés à partir de modèles de langage open-source plus petits provenant du dépôt [Hugging Face](https://huggingface.co/models).

Les modèles ont tourné sur un cluster de calcul universitaire via le framework [vLLM](https://github.com/vllm-project/vllm). Ce framework permet de collecter des détails précis, tels que les probabilités des prochains tokens.

Les prompts et les documents ont été choisis pour démontrer divers phénomènes intéressants (par exemple, « pourquoi les modèles ne savent-ils pas bien compter les lettres ? »).

Les données sont disponibles pour différents :
- modèles,
- températures de décodage,
- langues.

Vous trouverez les scripts pour générer les enregistrements dans le [dépôt du projet](https://github.com/kasnerz/animated-llm/tree/main/scripts/data-generation).

Vous y trouverez également un script permettant de [télécharger et explorer](https://github.com/kasnerz/animated-llm/blob/main/scripts/download_data.py) tous les enregistrements actuels au format JSON.

### Quelles données sont présentes dans les enregistrements ?

⚠ Attention, ces informations ont pu partiellement changer depuis.

#### Modèle
L'application comprend les sorties des modèles suivants :
- [CohereForAI/aya-expanse-8b](https://huggingface.co/CohereForAI/aya-expanse-8b)
- [meta-llama/Llama-3.2-1B-Instruct](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct)
- [Qwen/Qwen3-4B-Instruct-2507](https://huggingface.co/Qwen/Qwen3-4B-Instruct-2507)
- [allenai/Olmo-3-7B-Think](https://huggingface.co/allenai/Olmo-3-7B-Think)
- [openai-community/gpt2-xl](https://huggingface.co/openai-community/gpt2-xl)

Pour l'entraînement, un enregistrement d'un « Transformer vanilla » est également disponible, c'est-à-dire un modèle avec des poids initialisés aléatoirement (il est basé sur l'architecture `Llama-3.2-1B-Instruct`, mais ce n'est qu'un détail technique).

#### Température de décodage
La température de décodage est un nombre compris entre 0 et ∞ qui détermine (pour simplifier) le degré de hasard dans la sélection des prochains tokens.

Alors qu'à une température proche de zéro, le token le plus probable est presque toujours choisi, à une température très élevée, les prédictions du modèle ne sont pratiquement plus prises en compte et le token est choisi de manière aléatoire.

Dans l'application, les enregistrements sont disponibles pour les valeurs de température suivantes :
- 🧊 **0.0** : le token le plus probable est toujours sélectionné,
- 🌡 **1.0** : le token est sélectionné aléatoirement sur la base des probabilités du modèle,
- 🔥 **5.0** : le token est sélectionné aléatoirement et les probabilités du modèle ne jouent qu'un rôle mineur.

#### Langue

Nous fournissons les enregistrements dans toutes les langues supportées par l'application. Celles-ci sont actuellement :

- 🇬🇧 Anglais
- 🇨🇿 Tchèque
- 🇫🇷 Français
- 🇺🇦 Ukrainien
- 🇨🇳 Chinois

Les langues ont été choisies pour couvrir un large éventail de familles de langues et d'écritures.

Vous souhaitez ajouter d'autres langues ou corriger des erreurs ? Rendez-vous dans la section « Comment donner mon avis sur l'application ? »

⚠ Attention : à l'exception de l'anglais et du tchèque, la traduction du site a été créée automatiquement à l'aide de grands modèles de langage.


## Comment contrôler l'application ?
### Comment choisir un enregistrement spécifique ?

1. Choisissez sur l'écran d'accueil l'aspect des modèles de langage qui vous intéresse.
2. Sélectionnez le **modèle et la température** dans les paramètres. Dans certaines animations, ce réglage est visible directement, ailleurs il est caché sous l'icône :

![settings](img/settings.png)

3. Choisissez la **langue** via l'icône du drapeau. (Actuellement, le changement de langue de l'enregistrement est lié au changement de langue de toute l'application) :

![language](img/languages.png)

4. Lancez l'animation en cliquant sur le bouton « Play ».

### Astuce pour les experts

L'animation peut également être contrôlée à l'aide de raccourcis clavier.

Au lieu du bouton « Play », vous pouvez par exemple faire défiler l'animation étape par étape avec la flèche droite, ou revenir en arrière avec la flèche gauche.

Et il y a bien d'autres raccourcis !

Vous trouverez tous les raccourcis sous l'icône du clavier :

![keyboard](img/keyboard.png)


## Comment donner mon avis sur l'application ?

Veuillez envoyer vos questions et idées d'amélioration sur le **[forum de discussion GitHub](https://github.com/kasnerz/animated-llm/discussions)**.

Si vous n'avez pas de compte GitHub, vous pouvez également écrire directement à l'auteur principal de l'application ([Zdeněk Kasner](https://kasnerz.github.io), vous trouverez son e-mail par exemple [ici](https://ufal.mff.cuni.cz/zdenek-kasner)).