# codex-skills

## Reference skills from another repository

Use a Git submodule to keep another developer's skills in `references/external-skills/`. The source repository stays separate, and this repo records the exact commit used as a reference.

Add a repository (replace `DEVELOPER/REPO` with its GitHub owner and name):

```bash
git submodule add https://github.com/DEVELOPER/REPO.git references/external-skills
git commit -m "Add external skills reference"
```

Update the reference to the latest upstream version:

```bash
git submodule update --remote references/external-skills
git add references/external-skills
git commit -m "Update external skills reference"
```

When cloning this repo, use `git clone --recurse-submodules <repo-url>`. For an existing clone, run `git submodule update --init --recursive` to download the referenced skills.
