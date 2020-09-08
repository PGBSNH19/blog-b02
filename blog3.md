# Bloginlägg för lektion 3:

## Övergripande

Genom övning 1-3 har vi steg för steg, har vi haft en webapplikation, som vi gjort körbar genom att göra en image av den och stoppa i den i en körbar container, som gått att köra både lokalt, såväl som i Azure. För att detta skall fungera har vi använt oss utav Docker, där vi skapat en dockerfil innehållandes källor till runtime, sdk & hur imagen skall byggas. Dockerfilen har sedan skapat en imagefil som även fungerar som en körbar container lokalt.

## Ladda upp image till Azure Container Register

Efter att vi skapat vår image så skapade vi manuellt en containerregister i Azure, sedan gjorde vi försök att tagga den utefter tutorialen som länkades i uppgiften:
myappregistryzorkii.azurecr.io/myapp:v1
Dock fungerade det inte riktigt utan taggningen förblev "latest" och namnet blev endast myappregistryzorkii.azurecr.io, så fick göra det i två steg:
Först: docker tag myapp myappregistryzorkii.azurecr.io/myapp
Därefter: docker tag myapp myappregistryzorkii.azurecr.io/myapp:v1

I första uppladdningen råkade vi pusha upp fel image till ARC. Vi upptäckte detta genom att kontrollera att tag & image fanns i ACR repository:
az acr repository list --name myappregistryzorkii --output table
az acr repository show-tags --name myappregistryzorkii --repository myapp --output table

Vi tog bort repository och ladda upp rätt version. Borttagning skedde genom:
az acr repository delete --name myappregistryzorkii --repository myapp

Slutligen pushade vi upp den i vår ACR. Vi kontrollerade att image låg i registret & taggen var v1 genom följande kommandon: 
az acr repository list --name myappregistryzorkii --output table
az acr repository show-tags --name myappregistryzorkii --repository myapp --output table

## Koppla ACR mot ACI & kör containern

### Skaffa Credentials

Denna bit var lite svårare iom tutorialen använde bash-script & vi använde powershell, men med lite hjälp från några, kommer ej ihåg vilka tyvärr, så fick vi reda på vad vi skulle plocka ut för azurekommandon från "bash-scriptet".

Detta går att göra manuellt via Azure Portal (dvs skapa en manuell ACI, men vi använde script).

Följande kommando tog vi ut från bash-scriptet, använde vi och modifierade:

- **Service Principal Name:** ACR_REGISTRY_ID=$(az acr show --name $ACR_NAME --query id --output tsv)
- **Password:** SP_PASSWD=$(az ad sp create-for-rbac --name http://$SERVICE_PRINCIPAL_NAME --scopes $ACR_REGISTRY_ID --role acrpull --query password --output tsv)
- **ID:** SP_APP_ID=$(az ad sp show --id http://$SERVICE_PRINCIPAL_NAME --query appId --output tsv)

*Så genom att köra az acr show --name myappregistryzorkii --query id --output tsv fick vi ut ett name:*
/subscriptions/bc7d71cf-f924-4c98-ad75-eb683e9a794f/resourceGroups/myAppResourceGroup/providers/Microsoft.ContainerRegistry/registries/myappregistryzorkii

*Namet använde vi för att få ut vårt lösenord:*
az ad sp create-for-rbac --name myappregistryzorkii.azurecr.io --scopes /subscriptions/bc7d71cf-f924-4c98-ad75-eb683e9a794f/resourceGroups/myAppResourceGroup/providers/Microsoft.ContainerRegistry/registries/myappregistryzorkii --role acrpull --query password --output tsv

*För att få ut ID körde vi följande:*
az ad sp show --id http://myappregistryzorkii.azurecr.io --query appId --output tsv

### Skapa ACI & koppla Register

*Vi skapade upp ACI och kopplade registret + angav en egen dns via följande uppgifter(OBS ID & Lösenord gäller ej då ACI + register är borttagen från portalen):*
az container create --resource-group myAppResourceGroup --name myappcontainer --image myappregistryzorkii.azurecr.io/myapp:v1 --cpu 1 --memory 1 --registry-login-server myappregistryzorkii.azurecr.io --registry-username d6326c0d-e1a5-485b-a3cd-dbf09155cc2e --registry-password i~61zdd2-PpXXv7vl0rNWkpac2UBD4Pe6z --dns-name-label aci-myapp --ports 80

### Kör ACI

Öppna valfri webbläsare och skrev in aci-myapp.myappregistryzorkii.azurecr.io, så visades hemsidan

Uppgift3

https://docs.microsoft.com/en-us/azure/container-registry/container-registry-auth-aci



## Uppgift 4

Vi följde tutorialen och skapade upp en WebAPI och ett API som vi utefter tutorialen kopplade ihop mha Docker Compose där vi kunde visa websidan lokalt via webapplication + vädret som hamnade på samma sida (webapin).

När Yaml-filen i Composern körs, så skapas 2st images, en för varje projekt. Detta eftersom när man lägger till Docker support för resp. projekt skapas även en dockerfil. Yaml-filen hämtar genvägarna till dessa båda dockerfilerna och kör dem när yaml-filen körs. Väldigt smidigt. 

Tyvärr hann vi inte komma tillräckligt långt för att ladda upp det till Azure. Det långa steget är att troligen göra det manuellt, såsom vi gjort i tidigare övningar, men det borde finnas andra sätt att kunna ladda upp.
Vi har kollat en del på att lägga upp ContainerCluters, vilket borde fungera, men det kräver ytterligare konfiguration i yaml-filen som jag inte hann prova.

Rent generellt känns det aningen krångligt/tidskrävande att gå via Docker Composer och addera konfiguration, medan när man kikar på hur AKS fungerar (lektions, samt egen googling av exempel , så verkar det mycket lättare att få samma resultat mha där det skapas podar (containar) och kopplas till ett Container Cluster.

Dock när man har konfigurationen i yaml. filen på plats, så är det lätt att skapa flera instanser i Azure utspritt på flera olika servrar.

