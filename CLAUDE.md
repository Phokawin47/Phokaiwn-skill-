# Working rules for this repository

This repo contains Agent Skills. Each skill lives at `skills/<category>/<name>/SKILL.md`.

## When adding or editing a skill

- `SKILL.md` must start with YAML frontmatter containing `name` and `description`. Without it the skill will not be discovered.
- `name` must match the directory name exactly.
- `description` is the only trigger mechanism. It must state what the skill does AND the contexts and user phrasings that should invoke it — including phrasings that do not mention the skill by name.
- Keep the body under ~500 lines. Split longer material into `references/` and point to it from SKILL.md.
- Write instructions in the imperative. Explain why a rule exists rather than stacking MUSTs.
- Do not add advice the model already follows by default. A skill earns its context budget by encoding what is specific: thresholds, project commands, stop conditions, prohibitions.

## Git

- Stage files by path. Do not use `git add -A`, `git add .`, or `git commit -a`.
- One skill change per commit.
- Conventional Commits: `feat(refactor): ...`, `docs(readme): ...`, `fix(skill): ...`

## Before committing a skill change

Verify the skill is discoverable:

```bash
npx skills add ./ --list
```

Then test triggering with a realistic user sentence that does not name the skill.
