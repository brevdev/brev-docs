# Hello fellow Brev dev :)

These are the brev docs. For any new page, please think hard about where it best fits. There are 4 options.

Tutorials:
    - Learning oriented.
    - Fucking bulletbroof guide, walking a user to an achievable goal.
    - Explain only whats absolutely necessary. Can you avoid the explanation for a later discussion? Do that.
    - Keep it short & sweet. The goal of this guide is to get em hooked. People get hooked when they can build something, are delighted, and are itching for more.

How-Tos:
    - Problem oriented.
    - If a brev user has a problem, they'll search for it, and they should stumble upon this.

Reference:
    - Information oriented.
    - This is a great place for stats, limitations, numbers, etc.

Discussions:
    - Understanding oriented.
    - Shed light on how and why.

## TO ADD A PAGE, FOLLOW THIS CHECKLIST
[ ] Create the md file for your page in whichever section folder it best fits.
[ ] Add the page to the sidebar in mkdocs.yml, otherwise no one will find it.
[ ] In the index.md for the section's folder, add a couple lines


# HOW TO RUN THIS LOCALLY

## Run locally
```
mkdocs serve -a localhost:3003
```

## Deploy

Make a branch with the latest changes

```
mkdocs gh-deploy
```

Push that branch and let github pages do the rest 🎉
