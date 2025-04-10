---
title: Skapa inbäddade e-signatur- och dokumentupplevelser
description: Lär dig hur du använder Acrobat Sign API:er för att bädda in e-signatur- och dokumentupplevelser i dina webbplattformar och system för innehålls- och dokumenthantering
feature: Integrations, Workflow
role: Developer
level: Intermediate
topic: Integrations
jira: KT-7489
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: 0a299592f0616988b6208fc98d3140f4ac22057e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Skapa inbäddade e-signaturer och dokumentupplevelser

Lär dig hur du använder Acrobat Sign API:er för att bädda in e-signaturer och dokumentupplevelser i dina webbplattformar och system för innehållshantering. Den här praktiska självstudiekursen består av fyra delar.

## Del 1: Vad du behöver

I del 1 lär du dig hur du kommer igång med allt du behöver för delarna 2-4. Vi börjar med att få API-inloggningsuppgifter.

+++Visa information om hur du hämtar API-uppgifter

* [Utvecklarkonto för Acrobat Sign](https://www.adobe.com/acrobat/business/developer-form.html)
* [Startkod](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS-kod (eller valfri editor)](https://code.visualstudio.com)
* Python 3.x
   * Mac - Homebrew
   * Linux - inbyggt installationsprogram
   * Windows - Chocolatey
   * All - https://www.python.org/downloads/

+++

## Del 2: Låg/ingen kod - kraften i webbformulär

I del 2 utforskar du alternativet låg/ingen kod för att använda webbformulär. Det är alltid en bra idé att se om du kan undvika att skriva kod i början.

+++Visa information om hur du skapar ett webbformulär

1. Kom åt Acrobat Sign med ditt utvecklarkonto.

1. Markera **Publish ett webbformulär** på startsidan.

   ![Startsida för skärmbilden i Acrobat Sign](assets/embeddedesignature/embed_1.png)

1. Skapa ett avtal.

   ![Skärmbild av hur du skapar ett webbformulär](assets/embeddedesignature/embed_2.png)

1. Bädda in ditt avtal på en platt HTML-sida.

1. Experimentera med att lägga till frågeparametrar dynamiskt.

   ![Skärmbild av tillägg av frågeparametrar](assets/embeddedesignature/embed_3.png)

+++

## Del 3: Skicka avtal med ett formulär och sammanfoga data

I del 3 skapar du avtal dynamiskt.

+++Visa information om hur du skapar avtal dynamiskt

Först måste du upprätta åtkomst. Med Acrobat Sign finns det två sätt att ansluta via API. OAuth-tokens och integrationsnycklar. Om du inte har ett mycket specifikt skäl till att använda OAuth med ditt program bör du utforska Integreringsnycklar först.

1. Välj **Integreringsnyckel** på menyn **API-information** på fliken **Konto** i Acrobat Sign.

   ![Skärmbild av var integreringsnyckeln finns](assets/embeddedesignature/embed_4.png)

Nu när du har åtkomst och kan interagera med API:et, se vad du kan göra med API:et.

1. Gå till [Acrobat Sign REST API Version 6-metoderna](http://adobesign.com/public/docs/restapi/v6).

   ![Skärmbild av navigering i Acrobat Sign REST API Version 6-metoder](assets/embeddedesignature/embed_5.png)

1. Använd token som ett bärarvärde.

   ![Skärmbild av bärarvärde](assets/embeddedesignature/embed_6.png)

När du vill skicka ditt första avtal är det bäst att förstå hur du använder API:et.

1. Skapa ett övergående dokument och skicka det.

>[!NOTE]
>
>JSON-baserade förfrågningsanrop har alternativen &quot;Model&quot; och &quot;Minimal Model Schema&quot;. Detta ger specifikationer och en lägsta nyttolast uppsättning.

![Skärmbild av hur ett övergående dokument skapas](assets/embeddedesignature/embed_7.png)

När du har skickat ett avtal för första gången är du redo att lägga till logiken. Det är alltid en bra idé att etablera vissa hjälpfunktioner för att minimera upprepning. Här är några exempel:

**Validering**

![Skärmbild av valideringslogik](assets/embeddedesignature/embed_8.png)

**Rubriker/autentisering**

![Skärmbild av rubriker/autentiseringslogik](assets/embeddedesignature/embed_9.png)

**Bas-URI**

![Skärmbild av bas-URI-logik](assets/embeddedesignature/embed_10.png)

Var medveten om var Övergående dokument hamnar i signeringsekosystemets stora schema.
Övergående -> Avtal
Övergående -> Mall -> Avtal
Övergående -> Widget -> Avtal

I det här exemplet används en mall som dokumentkälla. Detta är vanligtvis det bästa sättet om du inte har en solid anledning att dynamiskt generera dokument för signatur (t.ex. äldre kod eller dokumentgenerering).

Koden är ganska enkel. Den använder ett biblioteksdokument (mall) för dokumentkällan. Den första och andra undertecknaren tilldelas dynamiskt. Tillståndet `IN_PROCESS` innebär att dokumentet skickas omedelbart. Dessutom utnyttjas `mergeFieldInfo` för att fylla i fält dynamiskt.

![Skärmbild av kod för att lägga till signaturer dynamiskt](assets/embeddedesignature/embed_11.png)

+++

## Del 4: Bädda in signeringsupplevelse, omdirigeringar och annat

I många scenarier kanske du vill tillåta att den utlösande deltagaren omedelbart signerar ett avtal. Detta är användbart för kundvända applikationer och kiosker.

+++Visa information om hur du bäddar in signeringsfunktionen

Om du inte vill att det första e-postmeddelandet ska utlösas är det ett enkelt sätt att hantera beteendet genom att ändra API-anropet.

![Skärmbild av kod för att inte utlösa sändning av e-post](assets/embeddedesignature/embed_12.png)

Så här styr du omdirigering efter signering:

![Skärmbild av kod för att styra omdirigering efter signering](assets/embeddedesignature/embed_13.png)

När du har uppdaterat processen för att skapa avtal genereras signerings-URL:en i det sista steget. Det här anropet är också ganska enkelt och genererar en URL som en signerare kan använda för att komma åt sin del av signeringsprocessen.

![Skärmbild av kod för att generera en signerings-URL](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Observera att anropet för att skapa avtal är tekniskt asynkront. Det innebär att ett anrop till ett &quot;POST&quot;-avtal kan göras, men avtalet är inte klart än. Det bästa sättet är att skapa en upprepningsslinga. Använd ett nytt försök eller något som är det bästa tillvägagångssättet för din miljö.

![Skärmbild som visar att det är bäst att försöka igen](assets/embeddedesignature/embed_15.png)

När allt är sammansatt är lösningen ganska enkel. Du skapar ett avtal och sedan en signerings-URL som signeraren kan klicka på och påbörja signeringsritualen.

+++

## Ytterligare ämnen

* [JS-händelser](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webhook-händelser
   * [REST API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhookar i Acrobat Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Återaktivera e-postmeddelanden om förfrågningar (med händelser)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Ersätt timeout med ett nytt försök](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* Anpassade påminnelser
   * Med det första skapandet

     ![Skärmbild av navigering till Power Automate](assets/embeddedesignature/embed_16.png)

   * Eller lägg till en [pågående](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)
