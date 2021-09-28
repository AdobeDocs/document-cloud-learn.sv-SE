---
title: Skapa inbäddad e-signatur och dokumentupplevelser
description: Lär dig hur du använder Adobe Sign API:er för att bädda in e-signaturer och dokumentupplevelser på dina webbplattformar och i innehålls- och dokumenthanteringssystem
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: f015bd7ea1a25772a12cd0852d452d120f205a5c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Skapa inbäddade e-signaturer och dokumentupplevelser

Lär dig hur du använder Adobe Sign API:er för att bädda in e-signaturer och dokumentupplevelser på webbplattformar och i innehålls- och dokumenthanteringssystem. Den här självstudiekursen består av fyra delar:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Vad du kommer att behöva" src="assets/embeddedesignature/EmbedPart1_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Del 1: Vad du kommer att behöva</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Del 2: Låg/ingen kod — kraftfulla webbformulär" src="assets/embeddedesignature/EmbedPart2_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Del 2: Låg/ingen kod — kraftfulla webbformulär</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part3">
      <img alt="Del 3: Skicka avtal med ett formulär, sammanfoga data" src="assets/embeddedesignature/EmbedPart3_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part3"><strong>Del 3: Skicka avtal med ett formulär och slå samman data</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part4">
      <img alt="Del 4: Bädda in signeringsfunktion, omdirigering med mera" src="assets/embeddedesignature/EmbedPart4_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Del 4: Bädda in signeringsfunktion, omdirigering med mera</strong></a>
    </div>
  </td>
</tr>
</table>

## Del 1: Vad du kommer att behöva {#part1}

I del 1 får du lära dig att komma igång med allt du behöver för delar 2-4. Låt oss börja med att hämta API-autentiseringsuppgifter.

* [Utvecklarkonto för Adobe Sign](https://acrobat.adobe.com/se/sv/sign/developer-form.html)
* [Startkod](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [VS-kod (eller valfri redigerare)](https://code.visualstudio.com)
* Python 3.x
   * Mac — Hembreiska
   * Linux — Inbyggt installationsprogram
   * Windows — Chocolatey
   * Alla — https://www.python.org/downloads/

## Del 2: Låg/ingen kod — kraftfulla webbformulär {#part2}

I del 2 kommer du att undersöka alternativet för låg/ingen kod när du använder webbformulär. Det är alltid en bra idé att se om du kan undvika att skriva kod först.

1. Gå till Adobe Sign med ditt utvecklarkonto.
1. Klicka på **Publicera ett webbformulär** på startsidan.

   ![Skärmdump från Adobe Sign - startsida](assets/embeddedesignature/embed_1.png)

1. Skapa ditt avtal.

   ![Bild av hur du skapar ett webbformulär](assets/embeddedesignature/embed_2.png)

1. Bädda in avtalet på en platt HTML-sida.
1. Experimentera med att lägga till frågeparametrar dynamiskt.

   ![Bild av hur du lägger till frågeparametrar](assets/embeddedesignature/embed_3.png)

## Del 3: Skicka avtal med ett formulär och slå samman data {#part3}

I del 3 skapar du avtal dynamiskt.

Först måste du etablera åtkomst. Med Adobe Sign finns det två sätt att ansluta via API. OAuth-token och integreringsnycklar. Om du inte har en mycket specifik anledning att använda OAuth med ditt program vill du först utforska Integration Keys.

1. Välj **Integreringsnyckel** på menyn **API-information** på fliken **Konto** i Adobe Sign.

   ![Skärmbild som visar var integreringsnyckeln finns](assets/embeddedesignature/embed_4.png)

Nu när du har tillgång till och kan interagera med API:t kan du se vad du kan göra med API:t.

1. Navigera till [Adobe Sign REST API Version 6-metoder](http://adobesign.com/public/docs/restapi/v6).

   ![Skärmbild av navigering i Adobe Sign REST API Version 6-metoder](assets/embeddedesignature/embed_5.png)

1. Använd variabeln som ett&quot;innehavarvärde&quot;.

   ![Skärmbild av innehavarvärde](assets/embeddedesignature/embed_6.png)

Om du vill skicka ditt första avtal är det bäst att förstå hur du använder API:t.

1. Skapa ett övergående dokument och skicka det.

>[!NOTE]
>
>JSON-baserade begärandeanrop har alternativen &quot;Modell&quot; och &quot;Minimal Model Schema&quot;. Detta ger specifikationer och en lägsta nyttolast angiven.

![Bild av hur du skapar ett övergående dokument](assets/embeddedesignature/embed_7.png)

När du har skickat ett avtal för första gången är du redo att lägga till logiken. Det är alltid en bra idé att skapa några hjälpprogram för att minimera repetitioner. Här är några exempel:

**Validering**

![Skärmdump av valideringslogik](assets/embeddedesignature/embed_8.png)

**Rubriker/autenticering**

![Skärmdump av rubriker/auth-logik](assets/embeddedesignature/embed_9.png)

**Bas-URI**

![Skärmbild av bas-URI-logik](assets/embeddedesignature/embed_10.png)

Var uppmärksam på var Transient docs landar inom signaturekosystemets övergripande plan.
Transient -> Agreement
Övergående -> Mall -> Avtal
Transient -> Widget -> Agreement

I det här exemplet används en mall som dokumentkälla. Detta är vanligtvis den bästa vägen, såvida du inte har en solid anledning att dynamiskt generera dokument för signering (t.ex. äldre kod eller dokumentgenerering).

Koden är ganska okomplicerad. används ett biblioteksdokument (mall) för dokumentkällan. Den första och den andra signeraren tilldelas dynamiskt. Läget `IN_PROCESS` innebär att dokumentet skickas direkt. Dessutom används `mergeFieldInfo` för att fylla i fält dynamiskt.

![Skärmbild av kod för att lägga till signaturer dynamiskt](assets/embeddedesignature/embed_11.png)

## Del 4: Bädda in signeringsfunktion, omdirigering med mera {#part4}

I många fall kanske du vill att den utlösande deltagaren omedelbart ska kunna signera ett avtal. Detta är användbart för kundcentrerade program och kioskdatorer.

Om du inte vill att det första e-postmeddelandet ska utlösas är det enkelt att hantera beteendet genom att ändra API-anropet.

![Skärmbild av kod som inte utlöser sändning av e-post](assets/embeddedesignature/embed_12.png)

Så här styr du omdirigeringen efter signering:

![Skärmbild av kod som styr omdirigering efter signering](assets/embeddedesignature/embed_13.png)

När avtalet har uppdaterats genererar det sista steget signerings-URL:en. Det här samtalet är också ganska enkelt och genererar en URL som en signerare kan använda för att komma åt sin del av signeringsprocessen.

![Skärmbild av kod för att generera en signerares URL](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Observera att anropet för att skapa avtal är tekniskt asynkront. Det innebär att ett&quot;POST&quot;-avtalsanrop kan göras, men avtalet är inte klart än. Det bästa sättet är att skapa en upprepningsslinga. Använd ett nytt försök eller vad som helst som är den bästa metoden för din miljö.

![Skärmbild säger att det är bäst att skapa en upprepningsslinga](assets/embeddedesignature/embed_15.png)

När allt är samlat är lösningen ganska enkel. Du gör ett avtal och genererar sedan en signerings-URL som signeraren kan klicka på och påbörja signeringsritualen.

### Ytterligare ämnen

* [JS-händelser](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Webkrohändelser
   * [REST API](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks i Adobe Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Återaktivera e-postmeddelanden med begäranden (med händelser)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Ersätt timeout med ett nytt försök](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Anpassade påminnelser
   * Med det första skapandet

      ![Skärmbild av navigering till Power Automate](assets/embeddedesignature/embed_16.png)

   * Eller lägg till en [in-flight](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)

## Ytterligare resurser

http://bit.ly/Summit21-T126

Innehåller:
* Utvecklarkonto för Adobe Sign
* Adobe Sign API Docs
* Exempelkod
* Visual Studio Code
* Python
