## Samenvatting

<!-- Wat verandert er, en waarom? Een of twee zinnen. -->

## Type wijziging

<!-- De PR-titel moet met dit type beginnen, bijvoorbeeld `fix: kapotte link
     op de contactpagina`. De controle "Conventional commit title" kijkt daarop.
     Vink hieronder aan wat van toepassing is; de rest wordt automatisch
     opgeruimd zodra de checks klaar zijn. -->

- [ ] `feat` — nieuwe pagina, sectie of functionaliteit
- [ ] `fix` — bugfix: kapotte link, verkeerde configuratie, renderfout
- [ ] `content` — bestaande inhoud bijwerken of verbeteren
- [ ] `docs` — README, CONTRIBUTING of andere metabestanden
- [ ] `chore` — onderhoud: dependencies, CI/CD, configuratie
- [ ] `refactor` — herstructurering zonder gedragsverandering
- [ ] `style` — opmaak, witruimte, typefouten
- [ ] `revert` — een eerdere commit terugdraaien

## Checklist

- [ ] PR-titel volgt de commit-conventie (`type: korte omschrijving`)
- [ ] Geen secrets, tokens of persoonsgegevens in de diff
- [ ] `hugo server` lokaal gedraaid vanuit `src/` en de pagina bekeken
- [ ] Licht én donker thema gecontroleerd, en op een smal scherm
- [ ] Geen gebroken links of verwijzingen naar bestanden die niet bestaan
- [ ] Versiebump van Hugo, actionlint of lychee? De bijbehorende SHA-256 ook bijgewerkt
