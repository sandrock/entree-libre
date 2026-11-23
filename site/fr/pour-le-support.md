---
title: Une personne n'arrive pas à entrer sur votre site
lang: fr
permalink: /fr/pour-le-support/
description: Pour les équipes de support qui reçoivent le message d'une personne bloquée par une vérification anti-robots.
---

Une personne n'arrive pas à entrer sur votre site
================================

{: .lead}
Vous avez reçu un message parce qu'une personne est bloquée par une vérification. Vous pouvez sans doute l'aider : voici l'essentiel en deux minutes.


Ce qui se passe
----------------------------------------------------------------

Le site pour lequel vous apportez de l'aide confie une vérification (captcha, « Vérification que vous êtes humain »…) à une autre entreprise, qui examine le navigateur des personnes qui visitent le site. Certaines refusent cet examen, d'autres ne parviennent pas à le passer, d'autres encore tournent en rond : la vérification se répète sans fin, par défaut ou parce qu'elle est réglée trop sévèrement. Dans tous les cas, elles restent dehors et ne peuvent pas accéder aux services.


D'abord : existe-t-il déjà une autre porte ?
----------------------------------------------------------------

Il est normal qu'un site ait plusieurs accès, comme un magasin a une entrée principale, une entrée accessible et un guichet. En ligne, une autre porte peut être : 

- un lien de connexion envoyé par email
- un code de double authentification
- une validation par numéro de téléphone
- un autre formulaire sans vérification

Si une autre porte existe, indiquez-la à la personne : le problème est réglé pour elle.

> Désigner une autre porte : oui. Passer la vérification à sa place : non ; vous seriez examiné·e à votre tour, et ses données passeraient quand même par le service qu'elle refuse.


Sinon : quel souci voyez-vous ?
----------------------------------------------------------------

Le même problème peut se regarder de trois façons. Choisissez celle qui vous parle, selon le message reçu et ce que vous savez du site : [accessibilité](#accessibilite), [technique](#technique) ou [juridique](#juridique).

### Accessibilité {#accessibilite}

Les vérifications anti-robots sont un obstacle connu pour les personnes qui utilisent un lecteur d'écran, naviguent au clavier, voient mal ou ont du mal à résoudre des énigmes visuelles ou sonores. Le W3C, qui publie les règles d'accessibilité du web, y consacre une note entière ([*Inaccessibility of CAPTCHA*](https://www.w3.org/TR/turingtest/)).

> Avez-vous déjà reçu un message du type « je n'arrive pas à valider le captcha » ? Et la vérification de votre site, pouvez-vous la passer au clavier seul, sans souris ?

À faire remonter à la personne chargée de l'accessibilité, ou à l'équipe technique :

```
Un·e internaute signale ne pas pouvoir passer la vérification anti-robots de notre site (page : …).
Ce type de vérification pose des problèmes d'accessibilité connus : https://www.w3.org/TR/turingtest/
Existe-t-il un autre moyen d'accès ? Sinon, pouvons-nous en prévoir un ?
Pistes : {{ site.url }}{{ '/fr/alternatives/' | relative_url }}
```

### Technique {#technique}

La vérification ne bloque pas que des robots. Elle bloque aussi des internautes : celles et ceux dont le navigateur refuse les services d'autres entreprises (bloqueurs de publicité ou de pistage, réglages de confidentialité), ou utilise un navigateur peu courant. Elle peut aussi se tromper : une vérification réglée trop sévèrement, ou défaillante, renvoie certaines personnes à la même page, sans fin. Chaque blocage, c'est une personne qui renonce, ou un ticket de plus au support.

> Combien de tickets « je n'arrive pas à me connecter » ou « la page ne s'affiche pas » ce mois-ci ? Combien parlaient d'une vérification, ou d'une page qui se recharge sans fin ?

À faire remonter à l'équipe technique :

```
Un·e internaute est bloqué·e par la vérification anti-robots de notre site (page : …). Cette vérification est fournie par une autre entreprise que son navigateur refuse de charger.
Existe-t-il un autre moyen de passer ce contrôle ? Sinon, pouvons-nous en prévoir un ?
Des solutions sans service tiers existent : {{ site.url }}{{ '/fr/alternatives/' | relative_url }}
```

### Juridique {#juridique}

Pendant la vérification, le navigateur de la personne se connecte à une autre entreprise, qui lit des informations sur son appareil (l'examen). Selon la CNIL, quand le fournisseur réutilise ces données pour son propre compte, le consentement de la personne serait nécessaire ; et un dispositif soumis au consentement ne protège plus le site, puisqu'un refus suffit à le contourner. La CNIL recommande des solutions alternatives ([FAQ sur les cookies et autres traceurs](https://www.cnil.fr/fr/cookies-et-autres-traceurs/regles/cookies/FAQ), question 17, consultée le 23 novembre 2026).

> Savez-vous quelle entreprise reçoit les données des visiteurs pendant la vérification ? Est-elle citée dans la politique de confidentialité du site ? Le consentement cookie prévoit-il cet usage ?

À faire remonter à la personne déléguée à la protection des données (DPO), ou au service juridique :

```
Un·e internaute refuse la vérification anti-robots de notre site (page : …) car elle est fournie par une autre entreprise, et ne peut donc pas entrer.
La CNIL (FAQ cookies, question 17) indique que certains de ces services demandent le consentement, et recommande des alternatives : https://www.cnil.fr/fr/cookies-et-autres-traceurs/regles/cookies/FAQ
Pouvez-vous vérifier notre situation ?
```


Ce qu'il vaut mieux éviter
----------------------------------------------------------------

- Demander à la personne de changer de navigateur, de désactiver ses protections ou de vider son cache : si elle refuse la vérification, c'est un choix ; si la vérification boucle, le réglage se trouve du côté du site.
- Remplir la vérification à sa place.
- Renvoyer vers un forum de suggestions : c'est une question d'accès, pas une idée d'amélioration.


Pourquoi c'est important
----------------------------------------------------------------

Si vous hésitez encore : une vérification qu'on ne peut ni refuser ni contourner laisse dehors des personnes qui protègent leur vie privée ou qui ne peuvent pas la passer. [La démarche](../demarche/) explique pourquoi elles écrivent.


Merci
----------------------------------------------------------------

Vous êtes la première porte. Merci de faire passer le message.
