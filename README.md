# AI-Assisted CV Generation Workflow (personal)

A 6-step Claude prompt chain I built to rebuild **my own** CV from scratch — covering tool selection, recruiter-style audit, targeted rewrites, bilingual generation (EN/FR), ATS validation, and a final recap.

> ⚠️ **This is not a generic CV builder.** The prompts are tailored to my profile: junior software developer, Belgian tech market, targeting specific roles (software / fullstack / backend / analyst-developer / support-tester), with content rewrites built around my actual internship, my actual Anthropic Skilljar courses, and my actual French + English CV. If you want to reuse it, you'll need to adapt the prompts to your own background — see the **How to adapt it** section below.

> 🇬🇧 **English version below** · 🇫🇷 [Version française plus bas](#version-française)

---

## 🇬🇧 English version

### What this repo contains

The exact 6 prompts I used to rebuild my CV with Claude, plus a meta-review prompt I used to audit my own prompt engineering before running the chain. They are designed to be run **one at a time, each in a fresh chat with Claude**, with the output of one step pasted into the next.

I'm sharing this as a **case study** — a real example of how prompt chaining can be applied to a concrete personal project — not as a plug-and-play tool.

### How I used it

1. Opened a **new chat** with Claude (Sonnet/Opus) and attached my current CV.
2. Copy-pasted **Prompt 1**.
3. Read the answer, pushed back, asked follow-ups, approved.
4. At the end of each prompt, Claude produced a **Problem / Solution / Decisions** summary — I saved it.
5. Opened a **new chat** for the next prompt and pasted the previous summary into the relevant `<prompt_X_result>` tag.
6. Repeated for prompts 2 → 6.
7. The final prompt (Prompt 6) consolidated every summary into one clean recap.

> ⚠️ Each prompt **must** be run in its own chat. Don't chain them in a single conversation — context bleed degrades the output and the role-play (recruiter, ATS engine, CV writer…) gets diluted.

### What each prompt does (in my workflow)

| # | Role played by Claude | Goal |
|---|----------------------|------|
| **1** | Senior software developer | Pick the best tool to build an ATS-friendly, single-page CV (because my old one was in Canva — bad for ATS). |
| **2** | Belgian tech recruiter | 10-second recruiter pass + deep content audit of **my** current CV. Outputs Problem / Why it matters / Concrete fix triples. |
| **3a** | Tech CV writer | Decide how to position **my 9 Anthropic Skilljar courses** (list vs. summary block) and write the section. |
| **3b** | Belgian tech recruiter | Rewrite **my** profile summary, ATS-optimised, reflecting **my** interest in AI. |
| **3c** | Belgian tech recruiter | Rewrite **my** internship description with action verbs and measurable impact. |
| **4** | (Tool from Prompt 1) | Build the new CV from scratch in EN, then FR — applying every fix and rewrite from the previous steps, fitting one page, no fabricated facts (`[TO FILL]` markers when info is missing). |
| **5** | ATS engine + recruiter | Simulate ATS parsing on both EN and FR versions, flag parsing issues, check cross-version consistency. |
| **6** | Project reviewer | Consolidate all step summaries into a single Problem / Solution / Decisions table + a 5-sentence recap. |

### How to adapt it to your own CV

If you want to reuse this workflow, you'll need to edit the prompts before running them. The minimum changes:

- **Prompt 2, 3b, 3c**: replace "Belgian tech market" and the target roles with your own market and roles.
- **Prompt 3a**: replace the 9 Anthropic Skilljar courses with your own learning / certifications (or remove this prompt entirely if not relevant).
- **Prompt 4**: the personal data section, the language pair, and the "junior software developer interested in AI" framing all reflect me — adjust to your profile.
- **Prompt 5**: the cross-version comparison only makes sense if you're producing two language versions. Drop step 4 of that prompt if you only need one version.

The **structure** of the chain (audit → targeted rewrites → generation → validation → recap) is generic and reusable. The **content** of each prompt is mine.

### Why there are no `<output_format>` blocks in most prompts

This is the part of the workflow I want to be honest about, because in good prompt engineering practice **explicitly defining the output format is recommended** — it makes results predictable, reproducible, and easier to chain.

I deliberately did **not** specify rigid output formats here, because at the start of the project **I didn't yet know what I wanted my new CV to contain**. Locking the output too early would have pushed Claude into a shape I might have regretted. I wanted Claude's recommendations and rewrites to surprise me, not match a template I had imposed.

The trade-off: this workflow is **not fully automated**. Each step required me to read, push back, and approve before moving on. That was a conscious decision — I traded automation for discovery. If I were to rerun this workflow now that I know what I want, I'd add stricter `<output_format>` blocks to every prompt and run it end-to-end with much less manual intervention.

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

Les 6 prompts exacts que j'ai utilisés pour reconstruire **mon** CV avec Claude, plus un prompt méta que j'ai utilisé pour auditer ma propre ingénierie de prompts avant de lancer la chaîne. Ils sont conçus pour être lancés **un par un, chacun dans un nouveau chat Claude**, en collant la sortie d'une étape dans la suivante.

Je partage ça comme un **case study** — un exemple concret d'application du prompt chaining sur un projet personnel — pas comme un outil prêt à l'emploi.

### Comment je l'ai utilisé

1. J'ai ouvert un **nouveau chat** avec Claude (Sonnet/Opus) et joint mon CV actuel.
2. J'ai copié-collé le **Prompt 1**.
3. J'ai lu la réponse, challengé, posé des follow-ups, validé.
4. À la fin de chaque prompt, Claude a produit un résumé **Problème / Solution / Décisions** — je l'ai sauvegardé.
5. J'ai ouvert un **nouveau chat** pour le prompt suivant et collé le résumé précédent dans la balise `<prompt_X_result>` correspondante.
6. J'ai répété pour les prompts 2 → 6.
7. Le dernier prompt (Prompt 6) a consolidé tous les résumés en un seul récap propre.

> ⚠️ Chaque prompt **doit** être lancé dans son propre chat. Ne pas les enchaîner dans une seule conversation — le contexte qui déborde dégrade la sortie et le rôle joué (recruteur, moteur ATS, rédacteur CV…) se dilue.

### Ce que fait chaque prompt (dans mon workflow)

| # | Rôle joué par Claude | Objectif |
|---|---------------------|----------|
| **1** | Développeur senior | Choisir le meilleur outil pour construire un CV ATS-friendly une page (parce que mon ancien CV était sur Canva — mauvais pour les ATS). |
| **2** | Recruteur tech belge | Lecture recruteur 10 secondes + audit de contenu approfondi de **mon** CV actuel. Sortie en triplets Problème / Pourquoi ça compte / Correction concrète. |
| **3a** | Rédacteur de CV tech | Décider comment positionner **mes 9 cours Anthropic Skilljar** (liste vs. bloc résumé) et écrire la section. |
| **3b** | Recruteur tech belge | Réécrire **mon** résumé de profil, optimisé ATS, reflétant **mon** intérêt pour l'IA. |
| **3c** | Recruteur tech belge | Réécrire **ma** description de stage avec des verbes d'action et un impact mesurable. |
| **4** | (Outil choisi au Prompt 1) | Construire le nouveau CV from scratch en EN, puis FR — en appliquant toutes les corrections et réécritures précédentes, sur une page, sans inventer de faits (marqueurs `[TO FILL]` si une info manque). |
| **5** | Moteur ATS + recruteur | Simuler le parsing ATS sur les versions EN et FR, signaler les problèmes de parsing, vérifier la cohérence entre les deux versions. |
| **6** | Reviewer projet | Consolider tous les résumés d'étape dans un tableau unique Problème / Solution / Décisions + un récap en 5 phrases. |

### Comment l'adapter à ton propre CV

Si tu veux réutiliser ce workflow, tu devras éditer les prompts avant de les lancer. Le minimum à changer :

- **Prompts 2, 3b, 3c** : remplacer "marché tech belge" et les rôles ciblés par ton propre marché et tes rôles.
- **Prompt 3a** : remplacer les 9 cours Anthropic Skilljar par tes propres formations / certifications (ou supprimer ce prompt s'il n'est pas pertinent).
- **Prompt 4** : la section données personnelles, la paire de langues et le cadrage "junior dev intéressé par l'IA" reflètent mon profil — à adapter au tien.
- **Prompt 5** : la comparaison entre versions n'a de sens que si tu produis deux versions linguistiques. Supprimer l'étape 4 de ce prompt si tu n'as besoin que d'une version.

La **structure** de la chaîne (audit → réécritures ciblées → génération → validation → récap) est générique et réutilisable. Le **contenu** de chaque prompt est le mien.

### Pourquoi il n'y a pas de blocs `<output_format>` dans la plupart des prompts

C'est la partie du workflow sur laquelle je veux être honnête, parce qu'en bonne pratique d'ingénierie de prompts **définir explicitement le format de sortie est recommandé** — ça rend les résultats prévisibles, reproductibles et plus faciles à chaîner.

J'ai délibérément **choisi de ne pas** spécifier de formats rigides ici, parce qu'au démarrage du projet **je ne savais pas encore ce que je voulais dans mon nouveau CV**. Verrouiller le format trop tôt aurait poussé Claude vers une forme que j'aurais peut-être regrettée. Je voulais que les recommandations et réécritures de Claude me surprennent, pas qu'elles épousent un gabarit que je lui avais imposé.

Le trade-off : ce workflow **n'est pas totalement automatisé**. Chaque étape m'a demandé de lire, challenger et valider avant de passer à la suivante. C'était un choix conscient — j'ai troqué l'automatisation contre la découverte. Si je relançais ce workflow aujourd'hui en sachant ce que je veux, j'ajouterais des blocs `<output_format>` stricts à chaque prompt et je le ferais tourner de bout en bout avec beaucoup moins d'intervention manuelle.

### À propos du prompt méta

Le premier bloc dans [`prompts.md`](./prompts.md) est un **prompt qui review les 6 prompts eux-mêmes** — il ne fait pas partie de la chaîne. Je l'ai utilisé pour auditer ma propre ingénierie de prompts par rapport au cours Anthropic Skilljar sur le prompting avant de lancer le workflow. Utile comme pattern d'auto-check pour n'importe quelle chaîne de prompts.

### Stack technique

- **Claude** (Sonnet / Opus) via claude.ai
- **Typst** pour la mise en page finale du CV (recommandé par le Prompt 1)
- **XML structuré** à l'intérieur des prompts pour une séparation propre rôle / contexte / tâche
