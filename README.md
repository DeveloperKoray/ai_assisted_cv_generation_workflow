# AI-Assisted CV Generation Workflow

A 6-step Claude prompt chain to rebuild a junior developer CV from scratch — covering tool selection, recruiter-style audit, targeted rewrites, bilingual generation (EN/FR), ATS validation, and a final recap.

> 🇬🇧 **English version below** · 🇫🇷 [Version française plus bas](#version-française)

---

## 🇬🇧 English version

### What this repo contains

Six prompts (plus a meta-review prompt that critiques the chain itself) designed to be run **one at a time, each in a fresh chat with Claude**. The output of one step is pasted into the next.

### How to use it

1. Open a **new chat** with Claude (Sonnet or Opus).
2. Attach your current CV (PDF or text).
3. Copy-paste **Prompt 1** from this repo.
4. Read the answer, push back, ask follow-ups, approve.
5. At the end of each prompt, Claude will output a **Problem / Solution / Decisions** summary — save it.
6. Open a **new chat** for the next prompt and paste the previous summary into the relevant `<prompt_X_result>` tag.
7. Repeat for prompts 2 → 6.
8. The final prompt (Prompt 6) consolidates every summary into one clean recap.

> ⚠️ Each prompt **must** be run in its own chat. Don't chain them in a single conversation — context bleed degrades the output and the role-play (recruiter, ATS engine, CV writer…) gets diluted.

### What each prompt does

| # | Role played by Claude | Goal |
|---|----------------------|------|
| **1** | Senior software developer | Pick the best tool to build an ATS-friendly, single-page CV (Canva is bad for ATS). |
| **2** | Belgian tech recruiter | 10-second recruiter pass + deep content audit of the current CV. Outputs Problem / Why it matters / Concrete fix triples. |
| **3a** | Tech CV writer | Decide how to position the 9 Anthropic Skilljar courses (list vs. summary block) and write the section. |
| **3b** | Belgian tech recruiter | Rewrite the profile summary, ATS-optimised, reflecting interest in AI. |
| **3c** | Belgian tech recruiter | Rewrite the internship description with action verbs and measurable impact. |
| **4** | (Tool from Prompt 1) | Build the new CV from scratch in EN, then FR — applying every fix and rewrite from the previous steps, fitting one page, no fabricated facts (`[TO FILL]` markers when info is missing). |
| **5** | ATS engine + recruiter | Simulate ATS parsing on both EN and FR versions, flag parsing issues, check cross-version consistency. |
| **6** | Project reviewer | Consolidate all step summaries into a single Problem / Solution / Decisions table + a 5-sentence recap. |

### Why there are no `<output_format>` blocks in most prompts

This is the part of the workflow I want to be honest about, because in good prompt engineering practice **explicitly defining the output format is recommended** — it makes results predictable, reproducible, and easier to chain.

I deliberately did **not** specify rigid output formats here, because at the start of the project **I didn't yet know what I wanted my new CV to contain**. Locking the output too early would have pushed Claude into a shape I might have regretted. I wanted Claude's recommendations and rewrites to surprise me, not match a template I had imposed.

The trade-off: this workflow is **not fully automated**. Each step requires me to read, push back, and approve before moving on. That was a conscious decision — I traded automation for discovery. If I were to rerun this workflow now that I know what I want, I'd add stricter `<output_format>` blocks to every prompt and run it end-to-end with much less manual intervention.

### About the meta-review prompt

The first block in [`prompts.md`](./prompts.md) is a **prompt that reviews the 6 prompts themselves** — it's not part of the chain. I used it to audit my own prompt engineering against the Anthropic Skilljar prompting course before running the workflow. Useful as a self-check pattern for any prompt chain you build.

### Tech stack

- **Claude** (Sonnet / Opus) via claude.ai
- **Typst** for the final CV typesetting (recommended by Prompt 1)
- **Structured XML** inside prompts for clean role / context / task separation

---

<a id="version-française"></a>

## 🇫🇷 Version française

### Contenu du repo

Six prompts (plus un prompt méta qui critique la chaîne elle-même) conçus pour être lancés **un par un, chacun dans un nouveau chat Claude**. La sortie d'une étape est collée dans la suivante.

### Comment l'utiliser

1. Ouvrir un **nouveau chat** avec Claude (Sonnet ou Opus).
2. Joindre le CV actuel (PDF ou texte).
3. Copier-coller le **Prompt 1** depuis ce repo.
4. Lire la réponse, challenger, poser des follow-ups, valider.
5. À la fin de chaque prompt, Claude produira un résumé **Problème / Solution / Décisions** — le sauvegarder.
6. Ouvrir un **nouveau chat** pour le prompt suivant et coller le résumé précédent dans la balise `<prompt_X_result>` correspondante.
7. Répéter pour les prompts 2 → 6.
8. Le dernier prompt (Prompt 6) consolide tous les résumés en un seul récap propre.

> ⚠️ Chaque prompt **doit** être lancé dans son propre chat. Ne pas les enchaîner dans une seule conversation — le contexte qui déborde dégrade la sortie et le rôle joué (recruteur, moteur ATS, rédacteur CV…) se dilue.

### Ce que fait chaque prompt

| # | Rôle joué par Claude | Objectif |
|---|---------------------|----------|
| **1** | Développeur senior | Choisir le meilleur outil pour construire un CV ATS-friendly une page (Canva est mauvais pour les ATS). |
| **2** | Recruteur tech belge | Lecture recruteur 10 secondes + audit de contenu approfondi. Sortie en triplets Problème / Pourquoi ça compte / Correction concrète. |
| **3a** | Rédacteur de CV tech | Décider comment positionner les 9 cours Anthropic Skilljar (liste vs. bloc résumé) et écrire la section. |
| **3b** | Recruteur tech belge | Réécrire le résumé de profil, optimisé ATS, reflétant l'intérêt pour l'IA. |
| **3c** | Recruteur tech belge | Réécrire la description du stage avec des verbes d'action et un impact mesurable. |
| **4** | (Outil choisi au Prompt 1) | Construire le nouveau CV from scratch en EN, puis FR — en appliquant toutes les corrections et réécritures précédentes, sur une page, sans inventer de faits (marqueurs `[TO FILL]` si une info manque). |
| **5** | Moteur ATS + recruteur | Simuler le parsing ATS sur les versions EN et FR, signaler les problèmes de parsing, vérifier la cohérence entre les deux versions. |
| **6** | Reviewer projet | Consolider tous les résumés d'étape dans un tableau unique Problème / Solution / Décisions + un récap en 5 phrases. |

### Pourquoi il n'y a pas de blocs `<output_format>` dans la plupart des prompts

C'est la partie du workflow sur laquelle je veux être honnête, parce qu'en bonne pratique d'ingénierie de prompts **définir explicitement le format de sortie est recommandé** — ça rend les résultats prévisibles, reproductibles et plus faciles à chaîner.

J'ai délibérément **choisi de ne pas** spécifier de formats rigides ici, parce qu'au démarrage du projet **je ne savais pas encore ce que je voulais dans mon nouveau CV**. Verrouiller le format trop tôt aurait poussé Claude vers une forme que j'aurais peut-être regrettée. Je voulais que les recommandations et réécritures de Claude me surprennent, pas qu'elles épousent un gabarit que je lui avais imposé.

Le trade-off : ce workflow **n'est pas totalement automatisé**. Chaque étape me demande de lire, challenger et valider avant de passer à la suivante. C'était un choix conscient — j'ai troqué l'automatisation contre la découverte. Si je relançais ce workflow aujourd'hui en sachant ce que je veux, j'ajouterais des blocs `<output_format>` stricts à chaque prompt et je le ferais tourner de bout en bout avec beaucoup moins d'intervention manuelle.

### À propos du prompt méta

Le premier bloc dans [`prompts.md`](./prompts.md) est un **prompt qui review les 6 prompts eux-mêmes** — il ne fait pas partie de la chaîne. Je l'ai utilisé pour auditer ma propre ingénierie de prompts par rapport au cours Anthropic Skilljar sur le prompting avant de lancer le workflow. Utile comme pattern d'auto-check pour n'importe quelle chaîne de prompts.

### Stack technique

- **Claude** (Sonnet / Opus) via claude.ai
- **Typst** pour la mise en page finale du CV (recommandé par le Prompt 1)
- **XML structuré** à l'intérieur des prompts pour une séparation propre rôle / contexte / tâche
