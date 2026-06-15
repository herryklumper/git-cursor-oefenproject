# Samenvatting: leeromgeving en leerdoelen

## Mijn infrastructuur

**MacBook Pro**
- Cursor (code-editor)
- Terminal

**TransIP VPS met Ubuntu**
- Portainer (Docker-beheer via webinterface)
- Docker (containers, o.a. een WordPress + MariaDB setup als experiment)

## Wat ik al heb gedaan (ervaring)

Ik heb een werkende feedback-app gebouwd in WordPress (PHP), draaiend in een Docker-container (`wordpress_lab`) op mijn TransIP VPS, beheerd via Portainer. Daarbij heb ik geleerd:

- Containers benaderen en bestanden kopiëren met `docker cp`, `docker exec`
- 'nano' geinstalleerd in Container
- Bestanden bewerken in een container met `nano`
- Rechten zetten met `chown` en `chmod`
- Hoe Docker volumes werken (`docker inspect`, data blijft bewaard buiten de container)
- SMTP/firewall troubleshooting (poorten, TransIP firewall, telnet-tests)
- Cyberduck/SFTP gebruiken om bestanden tussen Mac en server uit te wisselen

## Mijn leerdoelen

Ik wil groeien van "bewust onbekwaam" naar "bewust bekwaam" in:
- **Portainer**
- **Docker**
- **GitHub**
- **Terminal**
- **Cursor**

om kleine apps te ontwikkelen.

## Technologie-voorkeur

Mijn voorkeur gaat uit naar **Python / Django** in plaats van PHP/WordPress. De WordPress-oplossing was een nuttig experiment, maar ik wil nu toe naar een Python-gebaseerde workflow binnen dezelfde infrastructuur (Docker, Portainer, GitHub, Cursor).

## Wat ik wil bereiken

Een **solide, herhaalbare workflow** ontwikkelen waarbij ik:
- Code schrijf in Cursor
- Versiebeheer doe via GitHub
- Apps deploy via Docker/Portainer op mijn TransIP VPS
- Niet steeds handmatig bestanden hoef te kopiëren/plakken tussen Mac en server

## Voorgesteld vervolgproject

Dezelfde feedback-app (leden van een tennisvereniging kunnen opmerkingen/klachten/suggesties indienen via hun telefoon), maar dan opnieuw gebouwd in **Python/Django**, met een nette Docker + GitHub workflow als leertraject.

## Concrete eerste oefenstap: GitHub-workflow voor de bestaande WordPress-app

Voordat ik aan Django begin, wil ik eerst leren hoe ik mijn bestaande WordPress feedback-app (PHP) via Git/GitHub beheer, als oefening voor een betere workflow:

1. De bestanden (`tennis-feedback.php`, `feedback-handler.php`, `config.php`) in een GitHub-repository zetten
2. Op de Ubuntu server een `git clone` doen naar bijv. `~/tennis-feedback-repo/`
3. De `docker-compose.yml` van mijn `wordpress_lab` container aanpassen met een **bind mount**, zodat de gecloonde map direct gekoppeld is aan de juiste mappen in de container (in plaats van `docker cp`)
4. Workflow: bestand aanpassen in Cursor → committen → pushen naar GitHub → op server `git pull` → wijziging direct actief

Let op: dit raakt de huidige `docker-compose.yml` configuratie van de draaiende `wordpress_lab` container — dit wil ik rustig en stap voor stap aanpakken, niet "live" tussendoor.

Huidige situatie van de container (ter referentie):
```yaml
volumes:
    - wordpress_lab_data:/var/www/html
volumes:
  wordpress_lab_db:
  wordpress_lab_data:
```
Volume in werkelijkheid genaamd: `wordpress-lab_wordpress_lab_data`, te vinden op:
`/var/lib/docker/volumes/wordpress-lab_wordpress_lab_data/_data/`
