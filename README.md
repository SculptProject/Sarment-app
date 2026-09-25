# Sarment-app
Développement de l'application Sarment. Un outil simple et intuitif pour les vignerons.

# Sarment

Application de gestion viticole simple et intuitive, pensée pour les petits et moyens vignobles (6 à 25 hectares) peu à l'aise avec le numérique.

> *"Un outil simple et intuitif fait par les vignerons, pour les vignerons qui libère la charge mentale"*

## Contexte du projet

- **Cible** : petits et moyens vignerons/viticulteurs, souvent freinés par le manque de temps et la complexité des outils numériques existants.
- **Promesse** : simplicité radicale, temps de saisie ultra restreint, interface épurée, tableau de bord centralisé, gamification légère.
- **Statut** : un prototype HTML (`sarment-prototype-V2.1.html`) existe et sert de **référence visuelle et fonctionnelle**. Le code de ce prototype n'est **pas repris** — le développement repart sur une stack propre.

## Stack technique

- **Frontend** : Next.js (React)
- **Style** : Tailwind CSS
- **Backend / Base de données** : Supabase (PostgreSQL + Auth + Storage)
- **Hébergement** : Hostinger (webapp + site vitrine)
- **Déploiement futur** : App Store (iOS) et Google Play (Android)

## Identité visuelle

| Élément | Couleur | Hex |
|---|---|---|
| Fond | Craie | `#EFE9DC` |
| Marque | Sarment | `#8B5E3C` |
| Module Vigne | Feuille | `#5B6B4D` |
| Module Vendanges | Ambre | `#C98A3B` |
| Module Cave | Raisin | `#5B3350` |
| Texte | Nuit | `#2A2420` |

Typographie : **Public Sans**
Logo : feuille de vigne à 5 lobes en contour, avec une coche de validation intégrée et un sarment en spirale traversant la feuille en diagonale.

## Fonctionnalités — feuille de route

### MVP
- Configuration du domaine (parcelles, cuves, hectares)
- Suivi des travaux et traitements de la vigne
- To-do list du patron vers les employés
- Tableau de bord simple

### V1.5
- Suivi de la sucrosité pendant les vendanges
- Gamification légère

### V2
- Suivi de la fermentation et de la filtration (module Cave)

## Navigation (écran d'accueil)

Deux entrées principales :
- **Gestion parcellaire** → liste des parcelles → fiche détaillée des tâches
- **Travaux en cave** → liste des cuves → fiche détaillée des tâches

## Exigences transverses

- **Sécurité** : protection anti-hacking et protection des données clients dès la conception (cible : entreprises manipulant des données confidentielles).
- **Comptes employés** : invitation via l'e-mail réel de l'employé (Supabase Auth), pas d'e-mail technique généré automatiquement.
- **Inscription patron** : email, mot de passe, et nom complet de l'exploitation (non unique en base).

## Structure du repo

```
/app            → pages et routes Next.js
/components     → composants React réutilisables
/lib            → logique métier, clients Supabase, utilitaires
/supabase
  /migrations   → migrations SQL (source de vérité, synchronisées avec Supabase)
/docs           → cahier des charges, moodboard, spécifications
```

## Base de données

Le schéma est géré via les migrations dans `supabase/migrations`, synchronisées avec le projet Supabase via l'intégration GitHub. Toute modification de schéma doit passer par une migration versionnée, jamais par une modification manuelle directe dans le dashboard Supabase en production.

## Variables d'environnement

Ne jamais committer de clés. Utiliser `.env.local` (ignoré par Git) en développement, et les GitHub Secrets pour la CI/CD :

```
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=   # jamais exposée côté client
```
