---
title: Automatisering av dokument med Adobe Sign för Microsoft Power Platform
description: Lär dig hur du aktiverar och använder Adobe Sign- och Adobe PDF-verktygsanslutningar för Microsoft Power Apps. Skapa arbetsflöden som automatiserar affärsprocesserna för godkännande och underskrift snabbt och säkert utan att koda
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 0%

---

# Automatisering av dokument med Adobe Sign för Microsoft Power Platform

Lär dig hur du aktiverar och använder Adobe Sign- och Adobe PDF-verktygsanslutningar för Microsoft Power Apps. Bygg arbetsflöden som automatiserar affärsprocesserna för godkännande och underskrift snabbt och säkert utan kod. Den här självstudiekursen består av fyra delar:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Del 1: Lagra signerade avtal i SharePoint med Adobe Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Del 1: Lagra signerade avtal i SharePoint med Adobe Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Del 2: Automatiserad godkännandeprocess för att få e-signatur med Adobe Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Del 2: Automatiserad godkännandeprocess för att få e-signatur med Adobe Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Del 3: Automatiserad OCR-dokumentgranskning med Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Del 3: Automatiserad OCR-dokumentgranskning med Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Del 4: Automatisk dokumentsammanställning med Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Del 4: Automatisk dokumentsammanställning med Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Förutsättningar

* Välbekant Microsoft 365 och Power Automate
* Adobe Sign Knowledge
* Microsoft 365-konto med tillgång till SharePoint och Power Automate (Basic for Adobe Sign, Premium for Adobe PDF Tools)
* Adobe Sign for enterprise- eller Adobe Sign-utvecklarkonto

**Utövningar 1 och 2**

* Adobe Sign-konto med tillgång till API:t. Ett utvecklarkonto eller ett Enterprise-konto.
* En SharePoint-webbplats som är tillgänglig för Power Automate och som du har redigeringsbehörighet till. Fullständig administratörsåtkomst rekommenderas.
* Exempeldokument för begäran om signaturgodkännande och signering.

**Utövningar 3 och 4**

Hämta material [här](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Del 1: Lagra signerade avtal i SharePoint med Adobe Sign {#part1}

I del ett använder du en Power Automate Flow-mall för att konfigurera ett automatiskt arbetsflöde som sparar alla signerade avtal på SharePoint-webbplatsen.

1. Navigera till Power Automate.
1. Sök efter Adobe Sign.

   ![Skärmbild av navigering till Power Automate](assets/documentautomation/automation_1.png)

1. Välj **Spara ett Adobe Sign-färdigt avtal i SharePoint-biblioteket**.

   ![Skärmbild av åtgärden Spara ett Adobe Sign-färdigt avtal till SharePoint-biblioteket](assets/documentautomation/automation_2.png)

1. Granska skärmen och konfigurera alla anslutningar som behövs. Aktivera Adobe Sign-anslutningen.
1. Klicka på den blå `+`-symbolen.

   ![Skärmbild av Adobe Sign- och SharePoint-flödesanslutning](assets/documentautomation/automation_3.png)

1. Ange e-postadressen till ditt Adobe Sign-konto och klicka på lösenordsfältet i det nya fönstret.

   ![Skärmbild av Adobe Sign inloggningsskärm](assets/documentautomation/automation_4.png)

   Vänta ett tag innan Adobe kan kontrollera ditt konto.

   >[!NOTE]
   >
   >Den här kontrollen dirigerar dig till lämplig inloggning om du använder en enkel inloggning från Adobe ID eller vårt företag.

1. Fullständig inloggning.
1. Klicka på **Fortsätt** för att gå till skärmen Flödesredigering.
1. Namnge utlösaren.

   ![Skärmbild som namnger utlösaren](assets/documentautomation/automation_5.png)

1. Konfigurera SharePoint-inställningarna.

   ![Skärmbild av hur du konfigurerar SharePoint-inställningarna](assets/documentautomation/automation_6.png)

   **Webbplatsadress:** din SharePoint-webbplats
   **Mappsökväg:** sökväg till de delade dokument som du vill använda
   **Filnamn:** Acceptera standard
   **Filinnehåll:** Acceptera standard

1. Spara flödet.

   ![Skärmbild av ikonen Spara](assets/documentautomation/automation_7.png)

1. Navigera till flödesöversiktsskärmen med den blå bakåtpilen. Du kommer att testa det här flödet i del 2.

   ![Skärmbild av fönstret Flödesöversikt](assets/documentautomation/automation_8.png)

Du kommer att testa det här flödet i nästa del.

## Del 2: Automatiserad godkännandeprocess för att få e-signatur med Adobe Sign {#part2}

I del två bygger vi av den första delen med ett stabilare flöde och testar båda flödena för att se dem i praktiken.

1. Välj **Mallar** till vänster i Power Automate-gränssnittet.

   ![Skärmbild av val av mallar](assets/documentautomation/automation_9.png)

1. Sök efter&quot;chefsgodkännande&quot;.
1. Välj **Begär godkännande för en vald fil**.

   ![Skärmbild som visar hur Request Manager godkänner en markerad fil](assets/documentautomation/automation_10.png)

   Granska anslutningarna och lägg till de som saknas.

   >[!NOTE]
   >
   >Om detta är det första flöde du gör med godkännanden kommer de att konfigureras fullständigt när flödet körs.

1. Klicka på **Fortsätt** för att gå till flödesredigeringsskärmen.

   Det här flödet har många förkonfigurerade steg, inklusive felkontroll och kapslade villkorliga steg.

1. Konfigurera **För en vald fil** enligt följande:
   **Webbplatsadress:** din SharePoint-webbplats
   **Biblioteksnamn:** din dokumentdatabas
1. Lägg till en inmatning enligt följande:
   **Typ**: E-post
   **Namn**: E-postadress till signerare

   ![Skärmbild av hur flödet konfigureras](assets/documentautomation/automation_11.png)

1. Konfigurera **Hämta filegenskaper:** enligt följande:
   **Webbplatsadress:** din SharePoint-webbplats
   **Biblioteksnamn:** din dokumentdatabas

1. Bläddra nedåt och sök efter **Om ja**.

   ![Skärmbild av konfiguration av Ja](assets/documentautomation/automation_12.png)

1. Klicka på **Lägg till en åtgärd** i rutan **Om ja** (inte längst ned) för att lägga till stegen som ska skickas för signatur.

   ![Bild av hur du lägger till en åtgärd i rutan Om ja](assets/documentautomation/automation_13.png)

1. Sök efter **SharePoint hämtar filinnehåll** och välj **Hämta filinnehåll**.

   ![Skärmbild av sökrutan](assets/documentautomation/automation_14.png)

1. Konfigurera **Hämta filinnehåll** enligt följande:

   ![Skärmbild av konfigurationen för Hämta filinnehåll](assets/documentautomation/automation_15.png)

   **Webbplatsadress:** din SharePoint-webbplats.
   **Fil-ID:** Sök efter&quot;identifierare&quot; och välj Identifierare i  **steget Hämta** filegenskaper.
1. Sök efter &quot;Adobe&quot; och välj **Adobe Sign** om du vill lägga till en annan åtgärd.

   ![Skärmbild av sökmeny](assets/documentautomation/automation_16.png)

1. Skriv&quot;upload&quot; i sökrutan för Adobe Sign och välj **Överför ett dokument och hämta ett dokument-ID**.
1. Sök efter den dynamiska variabeln **Namn** för att hämta namnet på objektet/dokumentet som valts i utlösaren under **Filnamn**.
1. Klicka på **Uttryck** i variabelassistenten under **Filinnehåll**.

   ![Bild av Överför ett dokument och få ett dokument-ID](assets/documentautomation/automation_17.png)

1. Lägg till en apostrof, klicka sedan tillbaka till **Dynamiskt innehåll**, ta bort din apostrof, välj **Filinnehåll** och klicka sedan på **OK**.

   Kontrollera att det inte finns några fler apostrofer och att det ser ut som exemplet nedan.

   ![Skärmbild av hur skärmen för dynamiskt innehåll ska se ut](assets/documentautomation/automation_18.png)

1. Sök efter&quot;skapa&quot; i Adobe Sign sökområde om du vill lägga till en till Adobe Sign-åtgärd.
1. Välj **Skapa och godkänn från ett överfört dokument och skicka för signatur**.

   ![Bild av sökning efter Skapa](assets/documentautomation/automation_19.png)

1. Konfigurera nödvändig information:
Välj **Namn** från den dynamiska variabelassistenten i **Avtalsnamn**.
Välj **Dokument-ID** från den dynamiska variabelassistenten i **Dokument-ID**.
Välj **E-postadress för signerare** från den dynamiska variabelassistenten i **Deltagarens e-postadress**.
Ange &quot;1&quot; i **Deltagarordning**.
Välj **Signerare** i listrutan i **Deltagarroll**.

   ![Skärmbild av den information som krävs](assets/documentautomation/automation_20.png)

1. **Spara** flödet.

### Testa flödet

Gå till SharePoint-webbplatsens dokumentarkiv och testa den.

1. Markera dokumentet och välj **Automate** och **Flöde** som du nyss skapade.

   ![Skärmbild som visar hur du väljer Automate-menyn och -flödet](assets/documentautomation/automation_21.png)

1. Starta flödet för att validera anslutningarna (endast första flödeskörningen).
1. Skriv ett fint meddelande till godkännaren i **Meddelande**.
1. Ange e-postadress för dokumentsigneraren i **e-postadress för signerare**.
1. Klicka på **Kör flöde**.

Den konfigurerade godkännaren för den användare som startar flödet får en godkännandebegäran. Du kan godkänna via e-post eller via Power Automate Action Items-menyn.
Signera dokumentet när det har godkänts. Beroende på din användare och om de är inloggade på Sign, kan du behöva öppna signeringsfönstren i ett privat webbläsarfönster.

![Skärmbild som öppnas i privata webbläsarfönster](assets/documentautomation/automation_22.png)

Slutför signeringen och titta sedan tillbaka i SharePoint-mappen.

![Skärmbild av SharePoint-mapp](assets/documentautomation/automation_23.png)

## Del 3: Automatiserad OCR-dokumentgranskning med Adobe PDF Tools {#part3}

I del tre får du lära dig att automatisera OCR i PDF-filer när de importeras till Microsoft SharePoint. Detta åtgärdar ett problem som inträffar med skannade PDF-dokument som inte är sökbara i SharePoint.

![Skärmbild av PDF-dokument i webbläsare](assets/documentautomation/automation_24.png)

### Konfigurera en mapp i SharePoint

Gå till Microsoft SharePoint där du vill lagra dokument.

1. Klicka på **+ Ny** för att skapa en ny mapp med namnet &quot;Bearbetade kontrakt&quot;.
1. Klicka på **+ Ny** för att skapa en ny mapp med namnet&quot;Gamla kontrakt&quot;.

   ![Bild av nya mappar](assets/documentautomation/automation_25.png)

Dessa mappar ingår nu i Power Automate-flödet.

### Skapa ett flöde från en mall

1. Logga in på https://flow.microsoft.com.
1. Klicka på **Mallar** i sidlisten.

   ![Bild av val av mallar](assets/documentautomation/automation_26.png)

1. Välj **Konvertera nytillagda filer till textsökbar PDF i SharePoint**.
1. Klicka på symbolen **+** bredvid Adobe PDF Tools.

   ![Skärmbild av symbolen +](assets/documentautomation/automation_27.png)

1. Gå till https://www.adobe.com/go/powerautomate_getstarted på en ny flik.
1. Klicka på **Kom igång**.

   ![Skärmbild på knappen Kom igång](assets/documentautomation/automation_28.png)

1. Logga in med din Adobe ID.

   ![Skärmbild av inloggningsskärmen](assets/documentautomation/automation_29.png)

1. Ange namn och beskrivning för autentiseringsuppgifter och klicka på **Skapa autentiseringsuppgifter**.

   ![Skärmbild av skärmen Skapa inloggningsuppgifter](assets/documentautomation/automation_30.png)

   Håll fönstret med inloggningsuppgifterna öppna. Du måste ange dem i Microsoft Power Automate.

   ![Skärmbild av webbläsarfliken för att hålla den öppen](assets/documentautomation/automation_31.png)

1. Ange inloggningsuppgifterna och klicka på **Skapa i Microsoft Power Automate**.

   ![Skärmbild av PDF-verktygets inloggningsuppgifter](assets/documentautomation/automation_32.png)

1. Klicka på **Fortsätt**.

   ![Skärmbild där du klickar på Fortsätt](assets/documentautomation/automation_33.png)

   Nu kan du se en vy över arbetsflödet och du måste konfigurera det för din miljö.

1. Välj fältet Webbplatsadress och välj vilken SharePoint-webbplats du använder under utlösaren med namnet **När en fil skapas i en mapp**.

   ![Skärmbild som visar när en fil skapas i en mapputlösare](assets/documentautomation/automation_34.png)

1. Klicka på mappikonen för att navigera till mappen Gammalt kontrakt under Mapp-ID.

   ![Skärmbild av hur du väljer mappen Gammalt kontrakt](assets/documentautomation/automation_35.png)

1. Redigera åtgärden **Skapa fil** längst ned i flödet:

   Ändra **Platsadress** till din platsadress.
Ange platsen för mappen Bearbetade kontrakt i mappsökvägen.

1. Klicka på **Spara** i det övre högra hörnet.
1. Klicka på **Testa**.
1. Välj **Manuellt**.
1. Klicka på **Testa**.

   ![Skärmbild av testflödet](assets/documentautomation/automation_36.png)

### Testa det nya flödet

1. Navigera till mappen Gammala kontrakt i SharePoint.
1. Navigera till E03/Old Contracts i övningsfilerna som du har laddat ned.
1. Kopiera filerna ReleaseFormXX.pdf till mappen Gammalt kontrakt i SharePoint.

   ![Skärmbild av kopiering av filer](assets/documentautomation/automation_37.png)

Om du nu navigerar till mappen Bearbetade kontrakt kan du se dina PDF-filer som är tillgängliga när flödet har hunnit köras. Om du öppnar PDF-filerna kan du se att texten är markeringsbar.
Dessutom indexerar SharePoint dokumentet så att du kan söka efter innehållet i dina dokument från sökfältet i SharePoint.

## Del 4: Automatisk dokumentsammanställning med Adobe PDF Tools {#part4}

I del fyra får du lära dig att sammanfoga många dokument baserat på den information som ges när du väljer och startar ett flöde från Microsoft SharePoint. I det här scenariot kommer flödet att:

* Be om information för att välja vad som ska ingå i ett paket för en kund.
* Baserat på den information som ges sammanfogas många dokument. Dessa dokument innehåller en försättsblad och informationsdokument (valfria).
* Det sammanfogade dokumentet sparas i SharePoint.

### Importera övningsfiler till SharePoint

1. Öppna E04-mappen i övningsfilerna.
1. Importera mapparna Förslag, Mallar och Genererade dokument till SharePoint.

   ![Bild av import av mappar](assets/documentautomation/automation_38.png)

De här mapparna kommer att användas som referens. Du kommer att använda filen Förslag.docx för ditt förslag.

I mappen Mallar finns mappen Omslag som innehåller omslagssidans design för olika städer. Det finns också en mapp för rapporter som innehåller ytterligare dokument som kan bifogas till slutet om du väljer det.

### Importera flödet till Microsoft Power Automate

1. Logga in på Microsoft Power Automate (https://flow.microsoft.com).
1. Klicka på **Mina flöden**.

   ![Skärmbild av var mina flöden ska markeras](assets/documentautomation/automation_39.png)

1. Klicka på **Importera**.

   ![Skärmbild av importskärm](assets/documentautomation/automation_40.png)

1. Klicka på **Överför** och välj mappen GenerateFörslag_20210311231623.zip i E04/Flows/.

   ![Skärmbild av val av mapp](assets/documentautomation/automation_41.png)

1. Klicka på **Importera**.

1. Klicka på ikonen för skiftnyckel under Åtgärd bredvid **Skicka förslag till kund**.

   ![Skärmbild av skiftnyckelsikonen](assets/documentautomation/automation_42.png)

1. Välj **Skapa som ny** under Konfigurera.
1. Ange flödets namn under Resursnamn.
1. Klicka på **Spara**.

   Upprepa detta för övriga relaterade resurser och välj anslutningen.

   ![Skärmbild som visar när filen sparades](assets/documentautomation/automation_43.png)

1. Klicka på **Importera** när du har gjort alla dina anslutningar.

### Ange för en markerad fil

Gör följande när flödet har skapats:

1. Klicka på **Redigera**.

   ![Skärmbild som visar var du kan välja redigering](assets/documentautomation/automation_44.png)

1. Välj utlösare **För en markerad fil**.

   Lägg till din SharePoint-webbplats i webbplatsadressen.
Lägg till ditt bibliotek i biblioteket.

   ![Skärmdump av slutförd utlösare](assets/documentautomation/automation_45.png)

### Ange templateFolderPath

1. Klicka på variabeln templateFolderPath.
1. Ange sökvägen till den plats där mappen Mallar finns på SharePoint-webbplatsen som du importerade.

### Ange innehåll för hämtning av omslagsfil

1. Klicka på **Omslagsåtgärden**, som utökar omfånget.
1. Expandera **Omslag: Hämta filinnehåll**.

   Ange webbplatsadressen till din SharePoint-webbplats.

   ![Skärmbild av expanderat omslag](assets/documentautomation/automation_46.png)



### Ange markerad fil

1. Expandera åtgärden **Markerad fil** omfång.

   Ändra webbplatsadressen och biblioteksnamnet till SharePoint-webbplatsen och biblioteket under **Hämta filegenskaper**.
Ändra webbplatsadressen till din SharePoint-webbplats under **Hämta filinnehåll**.

   ![Skärmbild av den utökade åtgärden Markerad fil](assets/documentautomation/automation_47.png)

### Ange rapporter

1. Klicka på **Åtgärd för informationsdokument**.
1. Expandera **villkor: Lägg till rapport**.

   ![Skärmbild av utökat villkor för Lägg till rapport](assets/documentautomation/automation_48.png)

1. Expandera **Informationsdokument 1: Hämta filinnehåll med sökvägen**.
Redigera platsadressen till den angivna SharePoint-webbplatsen.

Upprepa samma steg för **Villkor: Lägg till rapport 2**.

### Ange skapad fil

1. Expandera **Skapa fil**.

   Redigera platsadress och mappsökväg till SharePoint-webbplatsen och sökvägen till mappen Genererade dokument.

1. Klicka på **Spara**.

### Testa ditt flöde

1. Navigera till mappen Förslag i SharePoint.
1. Välj mappen Förslag.docx.

   ![Skärmbild av val av förslagsmapp](assets/documentautomation/automation_49.png)

1. Välj ditt flöde under menyn **Automate**.

   ![Skärmbild av Välja menyn Automatisera](assets/documentautomation/automation_50.png)

1. Klicka på **Fortsätt** för att påbörja flödet.

   ![Skärmbild av knappen Fortsätt](assets/documentautomation/automation_51.png)

1. Välj omslag och de informationsdokument du vill bifoga.
1. Klicka på **Kör flöde**.

   ![Skärmbild av knappen Kör flöde](assets/documentautomation/automation_52.png)

Navigera till mappen Generera dokument. Nu bör du se den genererade PDF-filen.

![Skärmdump av SharePoint-katalog med ny PDF-fil](assets/documentautomation/automation_53.png)

### Lägga till Protect och andra åtgärder i flödet

Nu när du har skapat ett flöde kommer du att redigera ditt flöde för att kryptera PDF-dokumentet med ett lösenord. Här beskrivs också hur du kan använda andra åtgärder.

1. Gå tillbaka till slutet av flödet.
1. Klicka på symbolen **+** mellan **Sammanfoga PDF-filer** och **Skapa fil**.

   ![Skärmbild av var symbolen + ska markeras](assets/documentautomation/automation_54.png)

1. Välj **Lägg till en åtgärd**.
1. Sök efter&quot;Adobe PDF Tools&quot;.

   ![Skärmdump från sökning efter Adobe PDF](assets/documentautomation/automation_55.png)

1. Välj **Protect PDF från Visa**.
1. Använd dynamiskt innehåll för att ställa in filnamnsfältet till **PDF-filnamn från Sammanfoga PDF**.

   ![Skärmdump av dynamiskt innehåll](assets/documentautomation/automation_56.png)

   I utlösaren finns det ett lösenordsfält som är en del av initieringsformuläret. Vi kan använda det här.

1. Sök efter **lösenordsfält** med dynamiskt innehåll och placera det i fältet Lösenord.

   ![Bild av sökning efter lösenord](assets/documentautomation/automation_57.png)

1. Använd dynamiskt innehåll för att ställa in det på **PDF-filinnehåll från sammanfoga PDF-filer** i fältet Filinnehåll.
1. Ändra **Skapa fil** för att hämta filinnehållet från Protect PDF i stället för att sammanfoga PDF-filer.
1. Expandera **Skapa fil**.
1. Rensa fältet Filinnehåll.
1. Använd dynamiskt innehåll om du vill montera **PDF-filinnehåll** från **Protect PDF från Viewing**.

### Testa ditt flöde

1. Navigera till mappen Förslag i SharePoint.
1. Välj Förslag.docx.

   ![Skärmbild av val av förslagsmapp](assets/documentautomation/automation_58.png)

1. Välj **Automatisera** för att välja ditt flöde.

   ![Skärmbild som visar hur du väljer Automate på menyn](assets/documentautomation/automation_59.png)

1. Klicka på **Fortsätt** för att påbörja flödet.

   ![Skärmbild av val av Fortsätt](assets/documentautomation/automation_60.png)

1. Välj det omslag och de informationsdokument som du vill lägga till.
1. Ställ in fältet Lösenord till det lösenord som du vill ange.
1. Klicka på **Kör flöde**.

   ![Skärmbild av markerade filer och knappen Kör flöde](assets/documentautomation/automation_61.png)

1. Navigera till mappen Generera dokument.
Du bör se den genererade PDF-filen. Öppna PDF-filen så uppmanas du att ange ditt PDF-lösenord.

   ![Skärmbild av genererad PDF i SharePoint-katalog](assets/documentautomation/automation_62.png)
