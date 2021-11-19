---
description: Étude de la conformité RGAA des pages du site.
date: 2021-10-19
type: accessibility
kind: page
accessibility:
  website: "https://www.service-public.fr/compte/activer-un-espace-particulier?lienDemarche=https://psl.service-public.fr/mademarche/recensementCitoyen/demarche"
  audit:
    guidelines: "RGAA 4.1"
    condition: "Auto-évaluation"
    technologies: ["HTML", "CSS", "JavaScript"]
    tools:
      [
        "Inspecteur de code Chrome",
        "Inspecteur de code Safari",
        "Extension Chrome Assistant RGAA",
        "Extension Chrome HeadingsMap",
        "Extension Chrome Web Developer",
        "Extension Chrome Wave",
        "Color Contrast Analyser",
        "The W3C Markup Validation Service (validator.w3.org)",
      ]
    environment:
      [
        "MacOS Catalina 10.15.7",
        "Brave 1.30.89 Chromium: 94.0.4606.81",
        "Safari Version 14.1.2 (15611.3.10.1.5, 15611)",
      ]
  contact:
    email: __CONTACT_EMAIL__
    address: __CONTACT_ADDRESS__
---

Le rapport de conformité affiche un indicateur sur un « taux » d’accessibilité
d'une démarche correspondant au référentiel RGAA 4.1. Il permet d’estimer un
niveau global d’accessibilité des éléments présents sur le site en fonction de
[13 thématiques distinctes](/rgaa/4.1/criteres/).

En revanche, le rapport de conformité ne permet ni :

- de lister des erreurs de manière différenciée ;
- de spécifier le caractère bloquant d‘une erreur ;
- d’indiquer clairement une notion de complexité pour sa résolution.
