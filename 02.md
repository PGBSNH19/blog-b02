# Bloginlägg för lektion 2:

För lektion 2 fick vi 4 (1+3) övningar.

## Övning 1 - Lokal Virtuell Maskin

1. Skapa en Lokal Virtuell Maskin.

Detta lyckades vi tyvärr inte helt ut med då det var mycket strul, utan fokus blev att få igång virtuella maskiner med Azure. Således kunde vi inte heller göra en korrekt SWAT-analys.

**Men lite kort om fördelar/nackdelar med lokal virtuell maskin:**
*Fördelar:*
Kan installera andra operativsystem för att lära dig
Kan köra program som kräver vissa operativsystem
Behöver därmed inte ha flera olika datorer
Billigt om det gäller privat bruk

*Nackdelar:*
Minne allokeras för varje Virtuell Maskin
Filerna som läses in är stora och resurskrävande
Begränsningar i hårdvara + stora filer, för att alla program kanske inte går att köra, eller att de är sega när man kör dem.
Måste köpa hårdvara för att få den snabbare.

Fördelar/nackdelar Cloud Virtuell maskin:
*Fördelar:*
Alla kan komma åt maskinen om de har inloggning
Inga begränsningar i prestanda eller trafik, endast en ekonomisk fråga
Uppskalning/nerskalning av trafik och prestanda; antingen genom att sätta olika parmetrar och regler, eller kunna ha det automatiskt.
Slippa stå för hårdvara inkl. utrymme för ev. servar, samt ha personal som sköter om det.
Lätt att skapa nya instanser av olika konfigurationer
Lätt att ta bort instanser

*Nackdelar:*
Kan bli dyrt om man inte monitorerar, eller sätter begränsningar.
Kräver kunskap hur man skapar upp de virtuella maskinerna samt om GDPR
Data går att komma åt för den som får tag i inloggningsuppgifter eller annan hacking

## Övning 2-3-4 - Azure

2. Installera Azure VM manuellt via Azures hemsida

3. Via Cli

4. Via Pulumi

### Övning2:

För första övningen körde gruppen körde pairprogramming där en streamade och övriga hjälp. Då detta var ett något ovant sätt, hade vi en del tekniska problem, gällande bla säkerhetsnyckeln som laddades ner, som vi till slut fick hjälp med. Permissions för filen var tvungna att modifieras och det var inte helt lätt från början att förstå det av feltexten i windows powershell.

Sedan missuppfattade vi stegen vidare att installera Dotnet sdk och ubuntu, då vi följde artikeln: **[Hosting ASP.NET Core Web Application On Azure Linux VM]** i steg 1. Den stjälpte snare än hjälpte något alls. Samir och Piere hjälpte rätt vilka steg/länkar som skulle följas. ([[Install .NET Core SDK or .NET Core Runtime on Ubuntu v18.04]]()) Efter total ominstallation av VM (låg kvar gammal skit från ovanstående artikel), fungerade övning 1 för oss.

### Övning 3:

Tack vare övning 1 var det rätt lätt att förstå övning 2 om man vid installation av SDK följde [**Install .NET Core SDK or .NET Core Runtime on Ubuntu v18.04**] som tidigare i övning 1, laddade ner lektionsrepo från git, öppnade port 5000 via cli för att sedan visa hemsidan.

Pga olika tider då vi kunnat sitta online, har vi ej kunnat köra pairprogramming utan fått försöka var och en för sig. På fredagen gick jag (Micael) igenom CLI med Anders, som i sin tur gick igenom CLI med Irvin.

### Övning 4:

Från början följde jag Get started av Pulumi via Pulumis hemsida, och lyckades skapa upp ett nytt repo med en Storage, men inte så mycket mer.

Därefter följde vi tillsammans via pairprogrammering Uppgifts4 Github-länk för Pulumi och forkade ut en egen instans till mitt konto. Vi gick sedan in i katalogen azure-cs-webserver och följde instruktionerna från github-sidan.

Därefter följde vi stegen i CLI (**Install .NET Core SDK or .NET Core Runtime on Ubuntu v18.04**) för att installera Ubuntu, .Net SDK & Runtime.

För att lägga port till 5000, gick vi in i Virtual Machines i Azure för att hitta det autogenererade namnet och resursen.

Sedan var det precis som i uppgift 2 dra ner Github-repo, öppna en SSH-connection. Men där behövde vi skriva in användarnamn och lösenord som vi hittade i exempelrepot.

Slutligen startade vi SimpleWebHalloWorld och kom åt den via webläsaren. 



## Resurser som skapas i Azure för Virtuell Maskin

När en virtuell maskin skapas, så skapas en resursgrupp och ett namn för den virtuella maskinen. Någon sorts virtuell storage skapas också där man kan lägga program när man loggat in.

I samband med skapande av VM, läggs det även till nätverks- och acessresurser. Annars skulle det inte gå att få åtkomst.

Server resurs; tex USWest, för att inte glömma att du provisionerar upp olika hårdvaruresurser, såväl som kapacitesresruser.

Skillnaden mellan de olika resurserna som går att välja mellan (hårdvara, lagring, prestanda mfl), har direkt att göra med svarstider på servern, lagringsutrymme, prestanda, vilka i slutändan på beroende av företagets ekonomi.

