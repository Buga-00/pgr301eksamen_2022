# DevOps med gode intensjoner

## Del 1 DevOps-prinsipper

* Hva er utfordringene med dagens systemutviklingsprosess - og hvordan vil innføring av DevOps kunne være med på å løse
  disse? Hvilke DevOps prinsipper blir brutt?

  Svar: Utfordringene med dagens systemutviklingsprosess er at det ikke er en kontinuerlig forbedring i kodestrukturen, oppdatering av applikasjonen med dette mener jeg release av ny funksjonalitet og dårlig kommunikasjon mellom organisasjonen og IT-teamet de har leid.
  Innføring av DevOps ville løst disse problemene ved å ha et DevOps IT team i organisasjonen som gjør koden automatisert ved bruk av pipeline.
  De har en kontinuerlig integrasjon og leveranse.
  Tester som gir dem feedback om koden kjører som den skal i tillegg til cloudwatch metrics og cloudwatch alarm som gir dem en ekstern overvåkning.
  DevOps prinsippene som blir brutt med dagens systemutvikling er Flyt og Feedback.
  Dette er fordi dagens systemutviklingsprosess har ikke en bra måte å få feedback på som for eksempel ved bruk av cloudwatch og micrometre.
  De har heller ikke n bra flyt hvor de kan automatisere prosessen ved bruk av for eksempel github actions med pipeline eller Docker i pipeline.

* En vanlig respons på mange feil under release av ny funksjonalitet er å gjøre det mindre hyppig, og samtidig forsøke å legge på mer kontroll og QA. Hva er problemet med dette ut ifra et DevOps perspektiv, og hva kan være en bedre tilnærming?

  Svar: 

* Teamet overleverer kode til en annen avdelng som har ansvar for drift - hva er utfordringen med dette ut ifra et DevOps perspektiv, og hvilke gevinster kan man få ved at team han ansvar for både drift- og utvikling?

  Svar: Utfordringene med at en annen avdeling har ansvar for drift av en kode de ikke har laget selv er at de for det første ikke erkjent med koden.
  Hvis det dukker opp en feil, så kan det hende de som drifter den ikke vet hvor denne feilen kommer fra og må enten da bruke lang tid på å debugge og finne feilen eller så må de kontakte den avdelingen de fikk den fra og få rettet den opp fra dem.
  Gevinstene med å både drifte og utvikle koden er at teamet har mye bedre kommunikasjon mellom hverandre.
  Teamet vet hvordan koden er strukturert som fører til at de alltid har en kontinuerlig forbedring og større sannsynlighet til å debugge.
  Flinkere til å få en kontinuerlig integrasjon og levering.

* Å release kode ofte kan også by på utfordringer. Beskriv hvilke- og hvordan vi kan bruke DevOps prinsipper til å redusere
  eller fjerne risiko ved hyppige leveraner.

  Svar: For å redusere eller fjerne risiko ved hyppige leveranser, så er det best å gjøre alt automatisk på grunn av oftest, så kommer feil ved hyppige leveranser gjennom manuelle prosesser.
  DevOpps prinsipper som burde bli brukt er flow med automation og continuous delivery hvor du har hyppige leveranser uten noen manuelle prosesser, men alt er i en automatisk prosess.


## Del 2 - CI

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

