# DevOps med gode intensjoner



## Del 1 DevOps-prinsipper

Beskriv med egne ord;

* Hva er utfordringene med dagens systemutviklingsprosess - og hvordan vil innføring av DevOps kunne være med på å løse
  disse? Hvilke DevOps prinsipper blir brutt?
* En vanlig respons på mange feil under release av ny funksjonalitet er å gjøre det mindre hyppig, og samtidig forsøke å legge på mer kontroll og QA. Hva er problemet med dette ut ifra et DevOps perspektiv, og hva kan være en bedre tilnærming?
* Teamet overleverer kode til en annen avdelng som har ansvar for drift - hva er utfordringen med dette ut ifra et DevOps perspektiv, og hvilke gevinster kan man få ved at team han ansvar for både drift- og utvikling? 
* Å release kode ofte kan også by på utfordringer. Beskriv hvilke- og hvordan vi kan bruke DevOps prinsipper til å redusere
  eller fjerne risiko ved hyppige leveraner.

## Del 2 - CI

Konsulentene som har jobbet med innføring av DevOps har startet på en GitHub actions workflow for kontinuerlig
integrasjon. GitHub actions workflow (yml) filen ligger i dette repositoryet og heter ````ci.yml````

Problemet er at utviklingsteamet må starte jobben manuelt fra GitHub actions brukergrensesnittet. Det er jo ikke bra!

Du kan gjerne teste dette selv ved å gå til "Actions" i ditt repository, du vil se teksten "This workflow has a workflow_dispatch event trigger." Og vil
ha et valg som heter "Run workflow"


### Oppgave 3 

For å implementere branch protection og status sjekker, så må man inn i github deretter gå inn på settings også branches som ligger under Code and automation. 
Når du er inne på branches trykker du på add rule for å legge til en ny regel. 
I Branch name pattern skriver du main eller master spørs hva du har som default. 
Deretter under protect matching branches, så velger du Require a pull request before merging. 
Når du velger dette så får du opp require approvals hvor du velger minst en gokjenning. 
Etter du har gjort dette, så velger du Require status checks to pass before merging og helt nederst velger du Do not allow bypassing the above settings. 
Når du har gjort alle disse stegene, så har du implementert branch protection og status sjekker.

## Del 3 - Docker

### Oppgave 1

Workflowen feiler på grunn av inn i github så var det ikke lagt til secrets som docker username og token, så når workflowen prøvde å kjøre, så spurte den om brukernavn og password for å logge inn på Dockerhub og laste inn image. 
For å få workflowen til å fungere så må du gå inn på setting deretter secrets under security også actions. 
Da dukker det opp et nytt vindu hvor du lager to repository secrets hvor den ene er DOCKER_HUB_USERNAME med brukernavnet og den andre er DOCKER_HUB_TOKEN med token du genererte fra Dockerhub.
Etter at man har gjort dette, så vil workflowen fungere og pushe et image til Dockerhub kontoen

### Oppave 3

Det sensor må gjør for å få sin fork til å laste opp container image til sitt eget ECR er repo er å først legge inn AWS_ACCES_KEY_ID og AWS_SECRET_ACCESS_KEY i secrets også bytte på der det står 1035 med navnet til sitt eget ECR repo i docker.yml filen. 
Etter dette når sensor har pushet endringene inn i sin fork så vil det bli lastet opp et container image i sensors ECR repo.


## Del 5 - Terraform og CloudWatch Dashboards

### Oppgave 1 

Årsaken til dette problemet er at du ikke har lagt en backend i s3 etter at du har gjort Terraform apply andre gangen.
Når du ikke har backend s3, så vil den prøve å opprette en ny bucket med samme navn som fører til at det ikke vil gå og du vil få error.
For å hindre dette trenger vi backend for state-filen i AWS s3 bucket.

