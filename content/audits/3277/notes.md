## Remarques générales et points bloquants

- Les boutons d'édition (bouton "crayon") ne sont pas accessibles au clavier
- Certains boutons n'ont pas d'intitulé, ou l'intitulé n'est pas explicite (par
  exemple : les boutons "éditer" et "supprimer")
- Les mises à jour de formulaire ne sont pas restituées par les lecteurs d'écran
  (il manque des attributs `aria-live` par exemple)
- Les messages de statuts ne sont pas restitués correctement
- Souvent des composants de formulaires désactivés (checkbox, boutons, champs de
  saisie) sont utilisés à la place de simples textes qui auraient été plus
  facilement accessible.

## Amélioration de l'accessibilité

- **Général**

  - Par critères :

    - **1.8** : "République Française" pourrait être écrit avec du texte (cf.
      DSFR)|L'image du label e-accessible est floue. Préférez l'utilisation de
      textes stylisés ou d'un SVG.

    - **6.1** (page "Type de travaux") : Le titre (`title`) "(Notice explicative
      pour les demandes de permis de construire, permis d’aménager, permis de
      démolir et déclaration préalable) - Nouvelle fenêtre" gagnerait à être
      affiché autrement que sur le `title`

    - **8.2** (pages à partir de "Type de travaux" jusqu'à la fin) : Supprimer
      un `aria-hidden` superflu dans la balise
      `<input aria-hidden="true" id="demarche-release" type="hidden" disabled="disabled" value="2.0.0-RELEASE">`

    - **8.6** (page "Type de travaux") : Plutôt que "Guidage", peut-être
      préciser : "Mode guidé: Maison neuve" ?

    - **8.9** : Dans le footer, les titres de listes de liens présentés sous
      forme de colonnes sont des éléments `<p>` alors qu'ils ne correspondent
      pas vraiment à des paragraphes.

    - **10.3** (page "Type de travaux") : Lorsque les styles sont désactivés, la
      carte pose des problèmes de compréhension et de défilement à la souris.

    - **10.7** : Attention le coutour du focus cache parfois légèrement le texte
      en dessous sur les bords extérieurs (gauche et droite)

    - **11.2** (page "Type de travaux") : Veuillez saisir le nom de la commune
      (exemple : Paris)" est peut-être incomplet car on peut aussi entrer un
      code postal|"N° de parcelle" est vocalisé "N degré de parcelle" au lieu de
      "Numéro de parcelle" (VoiceOver)

    - **11.11** (page "Lieu des travaux") : Les suggestions pour les champs
      obligatoires manquants pourraient être plus précises et indiquer le format
      attendu (par exemple : "Veuillez renseigner la section de la parcelle de
      travaux (2 caractères)" au lieu de "Veuillez renseigner la section de la
      parcelle de travaux."

  - Le lien d'évitement mène au contenu sous l'élément `<main>`, or il existe
    une navigation (`<nav>`) secondaire (la colonne accordéon de gauche) sous
    l'élément `<main>`. Il serait souhaitable que le lien d'évitement aille
    directement au contenu intéressant, c'est à dire en haut du panneau de
    droite, qui commence par le "cartouche", et même éventuellement après ce
    cartouche.
    - Il faudrait sortir la navigation secondaire du `<main>`. Comme sur
      l'article AcceDe Web
      [Structurer les menus de navigation principaux et secondaires…](https://www.accede-web.com/notices/html-et-css/structure-generale/structurer-les-menus-de-navigation-principaux-et-secondaires-avec-nav-rolenavigation/#:~:text=La%20balise%20%3Cnav%20role%3D%22,Le%20menu%20secondaire.)
    - Sûrement difficile à implémenter sur Service-Public.fr qui est un portail
      et qui doit avoir un modèle de page fixe pour toutes les démarches.
    - Solutions alternatives :
      - [_Action sur le portail_] améliorer le portail pour améliorer les liens
        d'évitement (en explicitant 1 premier lien vers la démarche, un 2e vers
        le contenu principal de la démarche)
      - [_Action sur la démarche_] ajouter un lien d'évitement sous le titre de
        niveau 1 "Assistance aux demandes d'autorisation d'urbanisme" pour
        "sauter" toute la navigation secondaire.

- **Le formulaire à étape (en général)**

  - **Amélioration de la navigation de gauche** Ajouter une indication pour
    l'étape courante. --> dans le code (`aria-current="step"`). Voir
    [MDN: aria-current](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-current)
    --> visuellement par l'ajout de style particulier pour l'étape courante
  - **Message d'attente "Merci de patienter…"** Cf. article
    [Accessible Loading Indicators—with No Extra Elements!](https://dockyard.com/blog/2020/03/02/accessible-loading-indicatorswith-no-extra-elements)

    Ajouter `aria-live="polite" aria-busy="true"` ainsi :

    ```html
    <div
      class="spinner-overlay"
      id="spinnerOverlay"
      aria-live="polite"
      aria-busy="true"
    >
      <div id="spinnerContainer" tabindex="-1">
        <span id="spinner"></span>
        <p id="spinnerTexte">
          Merci de patienter, votre page est en cours de traitement.
        </p>
      </div>
    </div>
    ```

  - **Imprécisions de textes**
    - **N°** N° est lu "N degré" par VoiceOver au lieu de "numéro"

- **2. Types de travaux** : le bouton **VALIDER** ne devrait pas être écrit en
  majuscule (utiliser CSS)

- **3. Dossier**

  - **Imprécisions de textes**

    - "**Étape 0/7**" : le "/" n'est pas vocalisé par VoiceOver. Proposition :

      ```html
      Étape 0<span aria-hidden="true">/</span><span class="sr-only">sur</span>7
      ```

    ```
        Ce problème est aussi présent à la page "Demande de validation" (Récapitulatif) => c'est encore plus gênant à cette page.
    ```

  - Le titre du cartouche, "Maison neuvecomplet Pièces à joindre : 0/7 23%", ne
    devrait peut-être pas être un élément `<hx>` (titre, en l'occurrence de
    niveau 2) car il perturbe la hiérarchie d'information, qui, en dehors de ce
    titre, est cohérente.
  - le bouton **RÉCAPITULATIF** ne devrait pas être écrit en majuscule (utiliser
    CSS)
  - dans la formulation "(A)+(B)+(C)-(D)-(E)" les "-" (moins) ne sont pas
    vocalisés. Remplacer "-" par "&#8722;" (voir
    [Minus Sign](https://www.toptal.com/designers/htmlarrows/math/minus-sign/))
  - "Tableau de surfaces de plancher avant 2016" : ajouter " (en m²)" à chaque
    intitulé de colonne
  - Les champs de saisie pour indiquer un pays sont parfois des recherches
    parfois des champs libres (par ex. sur la page "Codemandeurs")
  - Le groupe de champs "Adresse" de la page Codemandeurs n'est peut-être pas
    assez explicite. Faut-il préciser "Adresse à laquelle vous vivez
    actuellement" ?
  - Peut-être ajouter un message de statuts lorsqu'un codemandeur est ajouté ?

- **Demande de validation (récapitulatif)**
  - utilisation de de l'attribut `disabled` sous la forme `disabled="true"` puis
    `disabled="disabled"`. Utiliser simplement `disabled` partout.

## Typos

- **1. Lieu des travaux** : placeholder
  "`Rechercher votre saisissez l’adresse du lieu des travaux (numéro et voie ou lieu-dit)`"
  ("rechercher votre saisissez"…)
- **2. Types de travaux** :
  - "`un de types de travaux`"
  - "`La règle Silence vaut accord" s'applique`" : le guillemet semble mal placé
- **3.Dossier | Liste des pièces à joindre** :
  - "Vous êtes invité" au lieu de "Vous êtes invités"
  - Incohérence entre "si le poids total des pièces jointes ne dépasse pas la
    limite de 100 Mo" et en-dessous : "(20 Mo maxi)"
  - "Pour passer à l’étape suivante, vous devez choisir un `de` types de travaux
    parmi". Remplacer "`des`" par "`de`".
- **Fin de démarche**
  - "Informations sur `le consentements`" : . Remplacer "`consentements`" par"
    `consentement`".
  - Enlever la virgule dans la phrase "Ce numéro est généré à chaque demande de
    validation, (le numéro est identique pour tous les autres demandeurs et
    architecte)".

## UX / UI

- **Formulaire en général** :

  - Plutôt que d'afficher des boutons `(?)` permettant d'afficher une aide,
    écrire directement l'aide sous le libellé du champs, comme dans le système
    de design de l'État. Voir
    [DSFR | Champ avec texte d’aide](https://gouvfr.atlassian.net/wiki/spaces/DB/pages/217088099/Champs+de+saisie+-+Input#Champ-avec-texte-d%E2%80%99aide).
    Un exemple : "Surface taxable démolie de la (ou des) construction(s)".
    L'aide, cachée par défaut, donne une information importante : "Information à
    compléter uniquement si le projet de démolition s'accompagne d'un
    agrandissement"
  - Pourquoi conserver l'option manuelle alors que l'on a commencé la démarche
    de type "guidée" ?

- **1. Lieu des travaux** :

  - **L'icone "loupe"** est floue.
  - **Indications de format attendue pour les champs de formulaire** Par exemple
    :

    - Parcelle 1 Préfixe Le préfixe doit être composé de 3 chiffres.
    - Section La section doit être composée de 2 caractères.
    - N° de parcelle Le N° de parcelle doit être composé de 4 chiffres.
    - Surface ( m2) La surface de la parcelle doit être composé de 1 à 7
      chiffres.

    **--> indiquer les formats avant que l'erreur n'ait lieu.**

  - **Transmission automatique** La proposition de "transmettre la demande
    automatiquement" arrive à la fin du panneau listant les options "manuelles"
    (?) :
    - Site internet de la commune : <http://www.nantes.fr>
    - Adresse de la mairie : 29 rue de Strasbourg
    - Téléphone de la mairie : 02 40 41 90 00
    - Adresse électronique de la mairie : contact@mairie-nantes.fr
    - Réglementation applicable dans la commune : Plan local d'urbanisme ou
      autres documents d'urbanisme
    - Vous pouvez consulter ici les servitudes d'urbanisme et documents
      d'urbanisme de la commune le cas échéant – site en cours d'alimentation
      par la commune : Géoportail de l’Urbanisme
    - Vous pouvez télécharger ici les documents d’urbanisme Télécharger [zip]
    - Vous pouvez consulter ici une cartographie générale: Géoportail IGN

_La commune est raccordée à ce téléservice et votre dossier peut lui être
transmis automatiquement_

    **Proposition : placer le message avant le panneau**

- **2. Types de travaux** : pictos non visible au focus

  - sous "Travaux"
  - sous "Informations obligatoires"

- **3. Dossier** :

  - l'accès à un bouton RÉCAPITULATIF dès le départ est un peu étrange.
    Peut-être un problème de nommage ?
  - libellé "Date de naissance" OK. Pourquoi mettre des parenthèses aux libellés
    de champs suivants ? ("Pays (de naissance)", "Commune (de naissance)",…)
  - Étape "construction". Que faut-il mettre dans le champs "Nature des autres
    financements publics" ? Peut-être ajouter une aide ici ?

- **Demande de validation (récapitulatif)** :
  - les boutons "Modifier" ne seraient-ils pas mieux placés sous les
    informations correspondantes plutôt qu'au-dessus ?
  - dommage que le bouton "Reprendre plus tard" ne soit pas présent sur cette
    page (ou alors mieux, il faudrait que le formulaire soit enregistré
    automatiquement sans besoin de bouton)

## Bugs

- **Message de debug présent**

  - Vu dans le code : "`Une erreur juste pour tester`"
  - Vu dans le code :
    `<!-- TODO : Mettre en place un message d'avertissement cohérent si certains champs n'ont pas été enregistrés -->`

- **Définitions de symboles SVG manquantes** Les symboles SVG sont manquants.
  Par exemple, les icones du menu mobile. On les voit s'afficher si l'on
  reprenant ceux présents sur <https://www.service-public.fr/> (l'élément
  `<div class="svg-inline">` présent dans le code source de service-public.fr)

- **Le formulaire à étape (en général)** On de devrait pas avoir à remplir des
  champs pour revenir à une étape précédente dans le formulaire

- **1. Lieu des travaux** : erreur JavaScript **Étapes pour rerpoduire le bug**

  1. Saisissez l’adresse du lieu des travaux (numéro et voie ou lieu-dit) :
     taper une adresse et Valider
  2. Modifier ce même champ en tapant une nouvelle adresse, puis valider
  3. Une fenêtre de dialogue apparait "Attention"

  Attendu : que l'option OUI fonctionne et referme la fenêtre de dialogue.
  Actuellement : l'option OUI ne fonctionne pas, la fenêtre de dialogue reste
  affichée. Un erreur apparaît dans la console JavaScript :
  `"Error: Map container is being reused by another instance"`

- **3. Dossier** : le _tab_ "Dossier" dans la navigation en colonne de gauche
  mène vers "Type de travaux"

- **3. Dossier | Demandeur** : mauvaise classe CSS "`contaienr`" au lieu de
  "`container`" (sous le panneau `id="collapseCartouche"`)

- **3. Dossier | Codemandeurs** : bug de contrôle de saisie **Étapes pour
  rerpoduire le bug**

  1. Pour la question "Existe-t-il des Codemandeurs ?" sélectionner OUI
  2. Ajouter un Codemandeur vide
  3. Changer la réponse à la question "Existe-t-il des Codemandeurs ?" en
     sélectionnant NON
  4. Valider

  Attendu: possibilité de continuer le formulaire sans obtenir d'erreur
  Actuellement: une erreur apparait :
  "`Il y a 1 erreur(s) dans la page. Il y a une erreur de saisie.`"

  Suggestion pour résoudre le problème : si "Non" est coché, ignorer les
  éventuels codemandeurs renseignés.

- **3. Dossier | Démolitions :** _(note : je n'arrive pas à le reproduire)_ À
  l'étape "Démolitions", les champs obligatoires sont précédés d'un "_" mais la
  légende "Les champs marqués d'un_ sont obligatoires" n'est pas présente sur
  cette page (elle l'est pour d'autres pages).

- **Récapitulatif :** PRÉVISUALISER CERFA : mène vers une page "Un problème est
  survenu lors de votre navigation. Merci de réessayer ultérieurement."

## Éditorial

- **2. Types de travaux | Maison neuve**
  - _"Quel est le nombre de logement(s) créé(s) ?"_ Le verbe "créer" est-il
    adapté ici ? --> "combien de maisons prévoyez-vous de construire ?"
  - _"La donnée attendue doit être au format entier."_ --> forcer le format du
    champ comme par exemple : `<input type="number" min="1" max="9">` --> "Le
    nombre de maisons doit être un nombre compris entre 1 et 9" ou "Le nombre de
    maisons doit être un nombre supérieur à 0" ou …
- **3. Dossier**
  - Plutôt que "Autre personne que le(s) demandeur(s)", écrire "Autre personne
    que le demandeur ou les codemandeurs" (les parenthèses sont vocalisées
    telles quelles). Pareil pour "Codemandeur(s)" (on peut simplement supprimer
    les parenthèses)
  - "Numéro CEDEX" plutôt que "CEDEX numéro" ?
  - Vu à l'étape **Architecte** : "AD’AU" ("Dans AD’AU, l'architecte
    valide[…]"). Attention, le grand public ne connait pas l'acronyme AD'AU
  - Expliciter "PLU", "POS", "RNU"
  - "Tableau de surfaces de plancher avant 2016" : formulation qui prète à
    confusion (il s'agit d'un PLU antérieur au 1er janvier 2016 ou un POS – mais
    pas d'un plancher d'avant 2016…)
    - dans le tableau : "Destinations" est ambigu.
    - Page Codemandeurs : "J'accepte de recevoir par courrier électronique les
      documents transmis en cours d'instruction par l'administration à l'adresse
      suivante". Attention l'adresse est inscrite dans un champ situé avant
      cette explication, "suivante" est confusant dans ce cas.
    - Codemandeur est parfois écrit co-demandeur
    - "Adresse d’envoi des titres de perception (Si différente à échéance de vos
      taxes)." : compliqué
    - À l'étape "Liste des pièces à joindre", le passage suivant n'est pas
      clair : "La commune du lieu des travaux est raccordée au service AD’AU.
      Votre demande lui sera directement transmise par la voie électronique. Il
      vous reste à télécharger les pièces jointes attendues. La commune du lieu
      des travaux n’est pas raccordée au service AD’AU, vous ne pouvez pas lui
      télétransmettre votre dossier. Vous êtes invités à confirmer que vous
      disposez bien de l’ensemble des pièces jointes attendues afin de pouvoir
      compléter le bordereau de pièces jointes. Votre dossier devra être déposé
      au guichet de votre commune ou par voie électronique selon les modalités
      qu’elle aura définies." Est-ce qu'il manque un "si" ? Ou bien c'est un bug
      et seul un des deux paragraphes devrait être affiché ?
- **3. Dossier | Liste des pièces à joindre**
  - "pièces à joindre" plutôt que "pièces jointes" ?
  - Que veut dire "Bbio" ? (c'est un critère pour la pièce "Le projet est tenu
    de respecter la réglementation thermique ou la réglementation
    environnementale – (PC16-1/PCMI14-1/PA28-1)")
- **Demande de validation**
  - Titre manquant pour le message d'alerte en haut de la page :
    `daua.message.pageDemandeValidation`
  - "e—mail" au lieu de "e-mail"
  - "1°)" et "2°)" au lieu de "1)" et "2)"
  - "e/out architecte." au lieu de "et/ou architecte."
