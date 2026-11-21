---
title: Les alternatives
lang: fr
permalink: /fr/alternatives/
description: Protéger un site contre les robots sans confier ses visiteurs à une autre entreprise, solutions comparées.
---

Les alternatives
===================================

{: .lead}
Protéger un site contre les robots est légitime. La question est de savoir *qui* examine les visiteurs : le site lui-même, ou une autre entreprise.

Cette page classe les solutions selon leur dépendance à un tiers, du « fait maison » aux grands services. Elle s'adresse à tout le monde ; les équipes techniques y trouveront de quoi comparer. Les informations viennent de la documentation des outils eux-mêmes, et ont été vérifiées le 21 novembre 2026.

Aucune solution n'est parfaite. L'OWASP rappelle que les captchas peuvent être cassés avec un taux de réussite assez élevé, et qu'exclure les navigateurs sans JavaScript nuit à l'accessibilité ([OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Credential_Stuffing_Prevention_Cheat_Sheet.html)). Une bonne protection combine souvent plusieurs techniques.


En un coup d'œil
---------------------------------------------------------

| Solution | Qui examine | JavaScript | Cookie | Code |
|---|---|---|---|---|
| Limitation des tentatives, champ piège (*rate limiting*, *honeypot*) | le site | non | non | — |
| Captcha simple fait maison (addition, image) | le site | selon la bibliothèque | selon la bibliothèque | libre, plusieurs langages |
| Double authentification (*2FA*), lien de connexion par email | le site | selon la méthode | non | — |
| Anubis | le site | oui, sauf mode sans JS | oui, du site | libre (MIT) |
| ALTCHA (version libre) | le site | oui | non par défaut | libre (MIT) |
| mCaptcha | le site | oui | non vérifié | libre (AGPL) |
| Friendly Captcha | entreprise allemande | oui | non | widget libre, service fermé |
| Cloudflare Turnstile | entreprise étatsunienne | oui | selon la configuration | fermé |
| hCaptcha | entreprise étatsunienne | oui | oui | fermé |
| Google reCAPTCHA | entreprise étatsunienne | oui | oui | fermé |
{: .table}


Sans tiers : le site se protège lui-même
---------------------------------------------------------

Le site garde la main : aucune autre entreprise n'examine ses visiteurs.

### Les techniques côté serveur

Elles ne demandent rien au navigateur des visiteurs :

- limiter le nombre de tentatives, par adresse IP ou par compte (*rate limiting*, *throttling*) ;
- ajouter un champ piège, caché aux humains, que seuls les robots remplissent (*honeypot*) ;
- filtrer le spam après coup, comme pour les emails (*spam filtering*).

Ces techniques sont décrites par l'[OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Credential_Stuffing_Prevention_Cheat_Sheet.html), le [NIST](https://pages.nist.gov/800-63-4/sp800-63b.html) et le [W3C](https://www.w3.org/TR/turingtest/), qui les présente comme des alternatives aux captchas, plus accessibles.

### Reconnaître la personne plutôt que traquer le robot

Pour les comptes, une autre approche consiste à vérifier que la personne est bien celle qu'elle prétend être, plutôt que de deviner si c'est un robot.

#### Double authentification (*2FA*)

Un second élément s'ajoute au mot de passe. L'OWASP distingue plusieurs méthodes ([OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html)) :

  - une application qui affiche un code temporaire (*TOTP*), simple, mais vulnérable à l'hameçonnage ;
  - une clé de sécurité ou une clé d'accès (*security key*, *passkey*), résistante à l'hameçonnage ; elle passe par JavaScript dans le navigateur ;
  - un code par SMS ou appel vocal : intéressant si le site travaille déjà avec un fournisseur d'envoi de SMS, sinon c'est un tiers de plus. C'est aussi la méthode la plus fragile : vol de numéro (*SIM swapping*), interception, hameçonnage. Le NIST le classe comme méthode « restreinte » et demande de toujours proposer une autre méthode ([NIST SP 800-63B-4, section 3.1.3](https://pages.nist.gov/800-63-4/sp800-63b.html)). Il suppose aussi un numéro de téléphone et passe par un opérateur ; le W3C note qu'un code uniquement vocal exclut les personnes sourdes ou malentendantes ([W3C, section 3.3](https://www.w3.org/TR/turingtest/)).

#### Lien de connexion par email (*magic link*)

La personne saisit son adresse email et reçoit un lien à usage unique qui la connecte, sans mot de passe ni captcha. C'est simple et sans tiers, mais la sécurité repose entièrement sur la boîte email : l'OWASP note qu'elle ne protège pas si la messagerie est compromise, et le NIST exclut l'email comme second facteur ([OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html), [NIST, section 3.1.3.1](https://pages.nist.gov/800-63-4/sp800-63b.html)). À réserver aux services où l'enjeu est modéré.

### Les outils à héberger soi-même

Ces outils font faire un petit calcul au navigateur du visiteur (une « preuve de travail », *proof of work*) : imperceptible pour une personne, coûteux pour un robot qui multiplie les visites. Ils demandent JavaScript, ce qui exclut les personnes qui naviguent sans.

#### Anubis

Un logiciel libre (MIT) qui se place devant le site, conçu contre les robots qui aspirent les pages. Il dépose un cookie propre au site après le calcul. Un mode sans JavaScript existe, désactivé par défaut, avec plus de faux positifs. Maintenu activement. ([Dépôt](https://github.com/TecharoHQ/anubis), [fonctionnement](https://github.com/TecharoHQ/anubis/blob/main/docs/docs/design/how-anubis-works.mdx), [mode sans JavaScript](https://github.com/TecharoHQ/anubis/blob/main/docs/docs/admin/configuration/challenges/metarefresh.mdx))

#### ALTCHA

Un widget libre (MIT) pour les formulaires, entièrement auto-hébergeable, sans cookie par défaut selon l'éditeur, une société tchèque. Des offres payantes existent à côté (service hébergé en Europe, serveur auto-hébergé sous licence). Maintenu activement. ([Dépôt](https://github.com/altcha-org/altcha), [site](https://altcha.org/))

#### mCaptcha

Un logiciel libre (AGPL) auto-hébergeable, financé en 2023 par le programme européen NGI0 via NLnet. Pas encore de version stable, et peu d'activité depuis octobre 2025. ([Dépôt](https://github.com/mCaptcha/mCaptcha))

### Les captchas simples, faits maison

Une question posée par le site lui-même : une addition, un mot à recopier depuis une image. C'est très basique, mais tout dépend de ce qu'on protège : pour un formulaire de contact peu visé, cela peut suffire. Des bibliothèques libres existent pour la plupart des langages, par exemple (le nom du langage lance une recherche pour en trouver d'autres) :

- [PHP](https://duckduckgo.com/?q=php+self+captcha+library) : [Gregwar/Captcha](https://github.com/Gregwar/Captcha) (image, MIT) ;
- [PHP, Laravel](https://duckduckgo.com/?q=laravel+self+captcha+library) : [mewebstudio/captcha](https://github.com/mewebstudio/captcha) (image ou calcul, MIT) ;
- [Python, Django](https://duckduckgo.com/?q=python+django+self+captcha+library) : [django-simple-captcha](https://github.com/mbi/django-simple-captcha) (image ou calcul, MIT) ;
- [Node.js](https://duckduckgo.com/?q=nodejs+self+captcha+library) : [captcha-canvas](https://github.com/Shashank3736/captcha-canvas) (image, Apache 2.0) ;
- [Java](https://duckduckgo.com/?q=java+self+captcha+library) : [Hutool Captcha](https://github.com/chinabugotech/hutool) (image ou calcul, MulanPSL 2.0) ;
- [Ruby, Rails](https://duckduckgo.com/?q=ruby+rails+self+captcha+library) : [rucaptcha](https://github.com/huacnlee/rucaptcha) (image, MIT) ;
- [Go](https://duckduckgo.com/?q=golang+self+captcha+library) : [base64Captcha](https://github.com/mojocn/base64Captcha) (image, calcul ou audio, Apache 2.0) ;
- [C#, .NET](https://duckduckgo.com/?q=dotnet+self+captcha+library) : [DNTCaptcha.Core](https://github.com/VahidN/DNTCaptcha.Core) (image ou somme, Apache 2.0) ;
- [Rust](https://duckduckgo.com/?q=rust+self+captcha+library) : [captcha](https://github.com/daniel-e/captcha) (image, MIT).

Leurs limites sont connues. Le W3C rappelle que les captchas à recopier sont « largement inaccessibles et peu sûrs », que même une addition simple peut gêner une personne dyscalculique, et que ces énigmes peuvent être résolues par des humains payés pour le faire. Il conseille de proposer plusieurs types de questions ([W3C, sections 2.1.1 et 2.1.3](https://www.w3.org/TR/turingtest/)).


Un tiers européen, sans traçage
---------------------------------------------------------

Le site confie la vérification à une autre entreprise, mais celle-ci s'engage à ne pas réutiliser les données.

### Friendly Captcha

Une société allemande. Preuve de travail et autres signaux de risque. Selon sa politique de confidentialité, elle agit comme sous-traitant, ne dépose pas de cookie, n'utilise pas les données à des fins marketing et hache les adresses IP. Un point d'accès hébergé en Allemagne et une option auto-hébergée existent dans les offres payantes supérieures. Le widget est libre (MPL 2.0), le service ne l'est pas. ([Politique de confidentialité](https://friendlycaptcha.com/legal/privacy-end-users/), [point d'accès européen](https://developer.friendlycaptcha.com/docs/v2/guides/eu-endpoint))

### ALTCHA

ALTCHA propose aussi un service hébergé en Europe, à côté de sa version libre.


Les grands tiers
---------------------------------------------------------

Le navigateur du visiteur se connecte à une grande entreprise, présente sur une grande partie du web, qui examine son navigateur et parfois son comportement.

### Cloudflare Turnstile

Gratuit, sans image à reconnaître : une série de tests en JavaScript sur le navigateur. Cloudflare se dit sous-traitant pour fournir le service, mais aussi responsable de traitement des signaux qu'il utilise pour améliorer sa détection des robots. ([Documentation](https://developers.cloudflare.com/turnstile/), [politique de confidentialité](https://www.cloudflare.com/turnstile-privacy-policy/))

### hCaptcha

Une société étatsunienne. Sa politique de confidentialité prévoit d'utiliser certaines données pour améliorer et développer ses services, et de fournir des données étiquetées à des clients qui souhaitent en acquérir. Elle dépose plusieurs cookies. ([Politique de confidentialité](https://www.hcaptcha.com/privacy))

### Google reCAPTCHA

La version 3 attribue un score à chaque visite, sans interaction. Depuis le 2 avril 2026, Google se présente comme sous-traitant, et non plus comme responsable de traitement ; reCAPTCHA dépose toujours un cookie. ([FAQ de Google](https://docs.cloud.google.com/recaptcha/docs/faq), [annonce](https://security.googlecloudcommunity.com/community-blog-42/switching-google-s-role-with-recaptcha-from-data-controller-to-data-processor-6646))


Adapter la protection à chaque activité
---------------------------------------------------------

Un forum, une boutique en ligne ou le service des impôts n'ont pas les mêmes enjeux, et un même site n'a pas besoin du même contrôle partout. Proposer plusieurs portes permet à chacun·e de passer : qui a activé la double authentification n'a pas à résoudre de captcha, et un captcha peut toujours être doublé d'un lien de connexion par email. Quelques pistes, à adapter au risque réel de chaque page :

| Activité | Pistes sans tiers |
|---|---|
| Parcourir le site, le catalogue | aucun contrôle ; contre l'aspiration massive des pages, limitation des requêtes ou Anubis |
| Créer un compte | champ piège, limitation des tentatives, confirmation par email |
| Se connecter | limitation des tentatives, double authentification, lien de connexion par email |
| Payer avec un compte | la personne est déjà connectée : pas de contrôle supplémentaire |
| Payer sans compte | limitation des tentatives, champ piège |
| Contacter le support | champ piège, filtrage du spam, captcha simple, une adresse email affichée |
| Poster un commentaire | champ piège, filtrage du spam, modération |
{: .table}


Ce que nous en pensons
---------------------------------------------------------

Protéger un site est légitime, et cette page le montre : les moyens existent, souvent simples, sans faire examiner chaque visiteur par une autre entreprise.

Nous pensons que :

- le contrôle doit rester à la mesure de ce qu'il protège : il n'y a pas besoin d'être fouillé par un vigile quand on veut regarder la vitrine ;
- le site doit garder la main sur sa porte d'entrée, de préférence avec des outils qu'il héberge lui-même ;
- une autre porte doit toujours exister pour les personnes qui refusent l'examen, ou qui ne peuvent pas le passer : handicap, navigation sans JavaScript, VPN ;
- si un tiers est vraiment nécessaire, il doit être choisi pour ne pas réutiliser les données, ni suivre les personnes d'un site à l'autre.

Se dire conforme au RGPD ne suffit pas. Le diable est dans les détails : ce que le service fait réellement des données, ce qu'il en fait sans le dire, et ce qui peut fuir. Un outil hébergé par le site lui-même réduit ces risques à la source : les données sont minimisées.

Aucune de ces solutions n'est magique. Mais entre « aucune protection » et « confier ses visiteurs à une grande entreprise », il y a beaucoup de place. Nous espérons que cette page vous aura fait découvrir des solutions plus acceptables, et que vous pourrez les mettre en place !


Proposer un outil, signaler une erreur
---------------------------------------------------------

Un projet libre ou un produit souhaite figurer sur cette page ? Il peut ouvrir une *issue* sur le [dépôt du site]({{ site.source_url }}) : la personne qui porte le projet évaluera la demande, selon les critères de cette page.

Une erreur dans notre analyse ? Signalez-la de la même façon, sources à l'appui : nous corrigerons volontiers.


Sources
---------------------------------------------------------

- OWASP, [Credential Stuffing Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Credential_Stuffing_Prevention_Cheat_Sheet.html).
- OWASP, [Multifactor Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html).
- NIST, [SP 800-63B-4, Digital Identity Guidelines: Authentication](https://pages.nist.gov/800-63-4/sp800-63b.html), juillet 2025.
- W3C, [Inaccessibility of CAPTCHA](https://www.w3.org/TR/turingtest/), note de groupe, 16 décembre 2021.
- Documentation, dépôts et politiques de confidentialité des outils, liés dans chaque section, consultés le 21 novembre 2026.
