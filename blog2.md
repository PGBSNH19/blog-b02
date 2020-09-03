Bloginlägg för lektion 2:

För lektion fick vi tre övningar:

1. Installera Azure VM manuellt via Azures hemsida
2. Via Cli
3. Via Pulumi

Övning1:

För första övningen körde gruppen körde pairprogramming där en streamade och övriga hjälp. Då detta var ett något ovant sätt, hade vi en del tekniska problem, gällande bla säkerhetsnyckeln som laddades ner, som vi till slut fick hjälp med. Permissions för filen var tvungna att modifieras och det var inte helt lätt från början att förstå det av feltexten i windows powershell.

Sedan missuppfattade vi stegen vidare att installera Dotnet sdk och ubuntu, då vi följde artikeln: **[Hosting ASP.NET Core Web Application On Azure Linux VM]** i steg 1. Den stjälpte snare än hjälpte något alls. Samir och Piere hjälpte rätt vilka steg/länkar som skulle följas. ([[Install .NET Core SDK or .NET Core Runtime on Ubuntu v18.04]]()) Efter total ominstallation av VM (låg kvar gammal skit från ovanstående artikel), fungerade övning 1 för oss.

Övning 2:

Tack vare övning 1 var det rätt lätt att förstå övning 2 om man vid installation av SDK följde [**Install .NET Core SDK or .NET Core Runtime on Ubuntu v18.04**] som tidigare i övning 1, laddade ner lektionsrepo från git, öppnade port 5000 via cli för att sedan visa hemsidan.

Övning 3:

Det svåraste med denna övning är att koppla på pulumi på Cli. I artikeln som finns under övningsavsnittet finns det länkat att göra på flera sätt och det är inte heller tydligt vilket som fungerar bäst. Det verkar även extra omständigt att gå via Chocolatey package manager. Ytterligare en grej av en djungel av sidor man måste hålla reda på ännu en inloggning.

Än så länge har vi inte lyckats komma längre än att kunna visa versionsnumret av pulumi i cmd.