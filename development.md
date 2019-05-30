## Git

(diky patri Honzovi Holubcovi)

- Jak commitovat soubor s vice nezavislymi zmenami? (napr. jsem zapomnel provest mezi zmenami commity)
    - `git add -i`, pak treba status, patch a projit jednotlive zmeny v souboru a vybrat, co s danym radkem udelat

- Chci se na nejaky predchozi commit, co uz je pushnuty v repu, ke kteremu ma pristup vice lidi.
    - `git revert`

- Chci sloucit commity.
    - `git rebase` interactive mode (https://git-scm.com/docs/git-rebase#_interactive_mode)