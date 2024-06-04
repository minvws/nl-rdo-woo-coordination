# Voorbeeld release strategie van het WOO project (later vertalen naar Engels)

- Signaal: 'we willen releasen hoe het nu in main staat' (komt vanuit QA / PO)
- Aanmaken release branch: bijvoorbeeld `release/v1.4.58` (actie QA of in overleg met QA)
- Aanmaken Release issue in coordination repository met Release Notes en test cases (actie QA)
- Aanmaken rc tag van de release branch: bijvoorbeeld `v1.4.58-rc.1` (actie QA)
- Deploy naar de testomgeving aanvragen aan Operations van tag `v1.4.58-rc.1` (actie QA)

## Bugs in de release?

- Bij een bug bevinding (op bijvoorbeeld de testomgeving) volgt dit proces:
- aanmaken bug issue
- in het bug issue moet je aangeven naar welke branch de PR met een hotfix gedaan moet worden (dus naar `release/v1.4.58`) en dit is dus ook de branch waarvan de hotfix afgetakt zal worden. Het beginpunt.
- Een developer lost de bug zsm op indien het tijdkritisch is voor de release en anders wordt het in overleg met de PO ingepland
- er volgt een PR van de hotfix branch naar de `release/v1.4.58` branch.
- PR merged na reviewproces in de release branch
- Aanmaken rc tag om opnieuw naar test te deployen: `v1.4.58-rc.x` (x is een oplopend volgnummer)
- Bijwerken coordination release ticket Release Notes
- Deploy naar test aanvragen van tag `v1.4.58-rc.x`
- Testen of het opgelost is
- Release is klaar voor acceptatie

## Release is klaar voor acceptatie

- Als de laatste 'rc' versie klaar is (en akkoord getest dus op de TEST omgeving)
- dan maak je daarvan een nieuwe tag: `v1.4.58` (op dezelfde commit dus)
- Controleren Release Notes (in het coordination release ticket)
- release aanvragen naar de acceptatie omgeving van tag `v1.4.58`
- indien akkoord dan het productie release proces in

## Strategie van terug mergen (release branch naar `main`) tussentijds

- Het team heeft de vrijheid om een hotfix ook naar `main` klaar te zetten in een PR (want soms is het 'handig' om de fix direct in `main` te hebben).
- Let op: in sommige repositories is het verwijderen van branches automatisch aangezet bij een merge. Dus als je eventueel tussendoor terug merged, dan wordt de release branch weggegooid (door die rule). Je moet ervoor zorgen met de `restore branch` knop dat de release branch op dit moment niet wordt verwijderd, want die heb je nog nodig.

## Strategie van terug mergen (release branch naar `main`) na de productie release

- QA zet na de release naar productie een PR klaar om de release branch terug naar main te mergen
- Codeowner reviewed het en merged.
- Codeowner restored de release branch (dus die willen we op dit moment nog niet verwijderen)
