# Secrétaire de Dhia & Mentor Scientifique

Application personnelle tout-en-un pour **Mohamed Dhia Bouchaala** (Sfax, Tunisie) — Chargé des opérations à l'Association Ifriqiya (initiative Baya Recyclage), étudiant en Master 2 de recherche Management et Prospectives (RV53, FSEG Sfax) et en formation Spectrum « Responsable Environnement, Énergie et Bilan Carbone ».

## Présentation des 5 Modules

1. **Accueil (`#accueil`)** : Tableau de bord quotidien (tâches urgentes, candidatures à relancer, nouvelles offres, progression des révisions, agenda du jour, compte à rebours du prochain examen).
2. **Postuler (`#offres` & `#candidatures`)** :
   - **Pilote automatique de candidature en 3 étapes** (*À préparer* → *À vérifier* → *Envoyées*).
   - Rédaction sur mesure de la lettre de motivation et génération automatique en PDF (`jsPDF`).
   - Gestion des pièces jointes (**CV** et **Diplômes**) et suivi des relances à 14 jours.
3. **Planning (`#taches`, `#semaine`, `#revisions`)** :
   - Gestionnaire de tâches par catégorie (*Master*, *Ifriqiya*, *Candidatures*, *Formation*, *Associations*, *Perso*).
   - Emploi du temps hebdomadaire combinant les cours du Master 2 RV53, la formation Spectrum et Google Agenda, avec détecteur automatique de conflits d'horaires.
   - Planificateur de séances de révision d'examens.
4. **Discussion (`#discussion`)** :
   - Secrétaire IA connectée à **Gmail**, **Google Calendar** et aux listes de l'application (18 outils intégrés + mode *« Faire sans moi »*).
5. **Mentor (`#mentor`)** :
   - Mentorat scientifique et révision espacée (système de Leitner à 5 boîtes : 1, 3, 7, 16, 35 jours) sur 8 domaines : **RSE, ESG, Bilan carbone, Normes ISO, Énergie, Économie circulaire, Gestion de projet, Management**.
   - Suivi du **Cap**, des **3 engagements actifs maximum**, et **Bilan hebdomadaire** sur 4 leviers (*Direction, Finition, Forme, Confiance*).

## Mode Hybride (Claude + PC Local)

- **Dans Claude (`claude.ai` / Claude Desktop)** : Utilise `window.claude.use("db")`, `use("mcp")` (Gmail, Google Calendar, navigateur intégré), `use("sample")` et `use("assets")`.
- **Sur PC (`http://localhost:8765` ou fichier local)** : Synchronisation automatique avec `data.json` sur le disque dur du PC, `localStorage` / `IndexedDB`, et boutons **Exporter / Importer JSON** dans la barre latérale.
