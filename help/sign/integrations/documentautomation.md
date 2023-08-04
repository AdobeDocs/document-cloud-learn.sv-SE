---
title: Dokumentautomatisering med Acrobat Sign för Microsoft Power Platform
description: Lär dig aktivera och använda Acrobat Sign- och Adobe PDF Tools-anslutningar för Microsoft Power-program. Skapa arbetsflöden som automatiserar affärsgodkännanden och signaturprocesser snabbt och säkert utan kodning
feature: Integrations, Workflow
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
jira: KT-7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 1%

---

# Dokumentautomatisering med Acrobat Sign för Microsoft Power Platform

Lär dig aktivera och använda Acrobat Sign- och Adobe PDF Tools-anslutningar för Microsoft Power-program. Skapa arbetsflöden som automatiserar affärsgodkännanden och signaturprocesser snabbt och säkert utan kodning. Den här praktiska självstudiekursen består av fyra delar, som beskrivs i länkarna nedan:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Del 1: Lagra signerat avtal i SharePoint med Acrobat Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Del 1: Lagra signerat avtal i SharePoint med Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Del 2: Automatisk godkännandeprocess för att få e-signatur med Acrobat Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Del 2: Automatisk godkännandeprocess för att få e-signatur med Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Del 3: Automatiserad dokument-OCR med Adobe PDF Tools" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Del 3: Automatiserad dokument-OCR med Adobe PDF Tools</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Del 4: Automatiserad dokumentsamling med Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Del 4: Automatiserad dokumentsamling med Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Förutsättningar

* Microsoft 365 och Power Automate-kännedom
* Acrobat Sign-kunskap
* Microsoft 365-konto med tillgång till SharePoint och Power Automate (grundläggande för Acrobat Sign, premium för Adobe PDF-verktyg)
* Utvecklarkonto för Acrobat Sign for enterprise eller Acrobat Sign

**Övningarna 1 och 2**

* Acrobat Sign-konto med åtkomst till API:et. Ett utvecklarkonto eller ett Enterprise-konto.
* En SharePoint-webbplats som är tillgänglig för Power Automate och som du har redigeringsbehörighet till. Fullständig administratörsåtkomst rekommenderas.
* Exempeldokument för begäran om godkännande av signatur och signering.

**Övningarna 3 och 4**

Hämta material [här](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Del 1: Lagra signerat avtal i SharePoint med Acrobat Sign {#part1}

I del ett kommer du att använda en Power Automate-flödesmall för att konfigurera ett automatiskt arbetsflöde som sparar alla signerade avtal på din SharePoint-webbplats.

1. Gå till Power Automate.
1. Sök efter Acrobat Sign.

   ![Skärmbild av navigering till Power Automate](assets/documentautomation/automation_1.png)

1. Välj **Spara ett slutfört Acrobat Sign-avtal i SharePoint-biblioteket**.

   ![Skärmbild av åtgärden Spara ett slutfört Acrobat Sign-avtal till SharePoint-biblioteket](assets/documentautomation/automation_2.png)

1. Granska skärmen och konfigurera eventuella anslutningar. Aktivera Acrobat Sign-anslutningen.
1. Klicka på den blå knappen `+` -symbolen.

   ![Skärmbild av Acrobat Sign- och SharePoint-flödesanslutning](assets/documentautomation/automation_3.png)

1. Ange e-postadressen för ditt Acrobat Sign-konto och klicka på lösenordsfältet i det nya fönstret.

   ![Skärmbild av Acrobat Sign inloggningsskärm](assets/documentautomation/automation_4.png)

   Vänta en stund tills Adobe har kontrollerat ditt konto.

   >[!NOTE]
   >
   >Den här kontrollen dirigerar dig till lämplig inloggning om du använder ett Adobe ID eller vår SSO för företaget.

1. Slutför inloggningen.
1. Klicka **Fortsätt** om du vill gå till skärmen Flödesredigering.
1. Ge utlösaren ett namn.

   ![Skärmbild där utlösaren namnges](assets/documentautomation/automation_5.png)

1. Konfigurera SharePoint-inställningarna.

   ![Skärmbild av hur du konfigurerar SharePoint-inställningar](assets/documentautomation/automation_6.png)

   **Webbplatsadress:** Din SharePoint-webbplats
   **Mappsökväg:** Sökväg till de delade dokument du vill använda
   **Filnamn:** Acceptera standardvärdet
   **Filinnehåll:** Acceptera standardvärdet

1. Spara flödet.

   ![Skärmbild av ikonen Spara](assets/documentautomation/automation_7.png)

1. Gå till skärmen Flödesöversikt med den blå bakåtpilen. Du kommer att testa detta flöde i del 2.

   ![Skärmbild av skärmen Flödesöversikt](assets/documentautomation/automation_8.png)

Du kommer att testa detta flöde i nästa del.

## Del 2: Automatisk godkännandeprocess för att få e-signatur med Acrobat Sign {#part2}

I del två bygger vi ut den första delen med ett mer robust flöde och testar båda flödena för att se dem i aktion.

1. Välj **Mallar** till vänster från Power Automate-gränssnittet.

   ![Skärmbild av val av mallar](assets/documentautomation/automation_9.png)

1. Sök efter &quot;chefsgodkännande&quot;.
1. Välj **Begär godkännande av hanterare för en vald fil**.

   ![Skärmbild av val av Request Manager-godkännande för en vald fil](assets/documentautomation/automation_10.png)

   Granska anslutningarna och lägg till de anslutningar du saknar.

   >[!NOTE]
   >
   >Om det här är det första flödet du gör med godkännanden kommer de att vara helt konfigurerade när flödet körs.

1. Klicka **Fortsätt** om du vill gå till skärmen för flödesredigering.

   Det här flödet har många förkonfigurerade steg, inklusive felkontroll och kapslade villkorliga steg.

1. Konfigurera **För en markerad fil** enligt följande:
   **Webbplatsadress:** Din SharePoint-webbplats
   **Biblioteksnamn:** Din dokumentdatabas
1. Lägg till indata enligt följande:
   **Typ**: E-post
   **Namn**: Signerarens e-postadress

   ![Skärmbild av konfiguration av flödet](assets/documentautomation/automation_11.png)

1. Konfigurera **Hämta filegenskaper:** enligt följande:
   **Webbplatsadress:** Din SharePoint-webbplats
   **Biblioteksnamn:** Din dokumentdatabas

1. Bläddra nedåt och leta efter **Om ja**.

   ![Skärmbild av konfiguration av Om ja](assets/documentautomation/automation_12.png)

1. Klicka **Lägg till en åtgärd** i **Om ja** (inte den nedersta) för att lägga till stegen som ska skickas för signering.

   ![Skärmbild av hur du lägger till en åtgärd i rutan Om ja](assets/documentautomation/automation_13.png)

1. Sök efter **Hämta filinnehåll i SharePoint** och välja **Hämta filinnehåll**.

   ![Skärmbild av sökrutan](assets/documentautomation/automation_14.png)

1. Konfigurera **Hämta filinnehåll** enligt följande:

   ![Skärmbild av konfigurationen Hämta filinnehåll](assets/documentautomation/automation_15.png)

   **Webbplatsadress:** Din SharePoint-webbplats.
   **Filidentifierare:** Sök efter &quot;identifier&quot; (identifierare) och välj Identifier från **Hämta filegenskaper** steg.
1. Sök efter &quot;Adobe&quot; och välj **Acrobat Sign** för att lägga till en annan åtgärd.

   ![Skärmbild av sökmeny](assets/documentautomation/automation_16.png)

1. Ange &quot;ladda upp&quot; i sökrutan för Acrobat Sign och välj **Ladda upp ett dokument och hämta ett dokument-ID**.
1. Sök efter den dynamiska variabeln **Namn** för att hämta namnet på objektet/dokumentet som markerats i utlösaren under **Filnamn**.
1. Klicka **Uttryck** i variabelassistenten under **Filinnehåll**.

   ![Skärmbild av Ladda upp ett dokument och få ett dokument-ID](assets/documentautomation/automation_17.png)

1. Lägg till en enstaka apostrof och klicka sedan tillbaka till **Dynamiskt innehåll**, ta bort apostrofen, välj **Filinnehåll** och klicka sedan på **OK**.

   Se till att det inte finns några ytterligare apostrofer och det ser ut som provet nedan.

   ![Skärmbild av hur skärmen Dynamiskt innehåll ska se ut](assets/documentautomation/automation_18.png)

1. Sök efter &quot;skapa&quot; i Acrobat Sign sökområde för att lägga till en annan Acrobat Sign-åtgärd.
1. Välj **Skapa och godkänn från ett uppladdat dokument och skicka för signering**.

   ![Skärmbild av sökning efter skapa](assets/documentautomation/automation_19.png)

1. Konfigurera nödvändig information: Välj **Namn** från den dynamiska variabelassistenten i **Avtalsnamn**.
Välj **Dokument-ID** från den dynamiska variabelassistenten i **Dokument-ID**.
Välj **Signerarens e-postadress** från den dynamiska variabelassistenten i **Deltagarens e-postadress**.
Ange &quot;1&quot; i **Deltagarordning**.
Välj **Undertecknare** från listruta i **Deltagarroll**.

   ![Skärmbild av den information som krävs](assets/documentautomation/automation_20.png)

1. **Spara** Flöde.

### Testa flödet

Testa den i dokumentarkivet på SharePoint-webbplatsen.

1. Markera dokumentet och välj **Automatisera** och **Flöde** du just skapade.

   ![Skärmbild av val av automatiseringsmeny och flöde](assets/documentautomation/automation_21.png)

1. Starta flödet för att validera anslutningarna (endast den första körningen av flödet).
1. Skriv ett meddelande till godkännaren i **Meddelande**.
1. Ange e-postadress för dokumentsigneraren i **Signerarens e-postadress**.
1. Klicka **Kör flöde**.

Den konfigurerade godkännaren för användaren som startar flödet får en begäran om godkännande. Du kan godkänna via e-post eller genom Power Automate-åtgärdsobjektmenyn.
Signera dokumentet när det har godkänts. Beroende på din användare och om de är inloggade på Sign kan du behöva öppna signeringsfönstren i ett privat webbläsarfönster.

![Skärmbild av öppning i privat webbläsarfönster](assets/documentautomation/automation_22.png)

Slutför signeringen och titta sedan tillbaka i SharePoint-mappen.

![Skärmbild av SharePoint-mappen](assets/documentautomation/automation_23.png)

## Del 3: Automatiserad dokument-OCR med Adobe PDF Tools {#part3}

I del tre får du lära dig hur du automatiserar OCR i PDF när de importeras till Microsoft SharePoint. Detta åtgärdar ett problem som uppstår med skannade PDF-dokument som inte är sökbara i SharePoint.

![Skärmbild av PDF-dokument i webbläsare](assets/documentautomation/automation_24.png)

### Konfigurera en mapp i SharePoint

Gå till Microsoft SharePoint där du vill lagra dokument.

1. Klicka **+ Nytt** för att skapa en ny mapp med namnet Bearbetade avtal.
1. Klicka **+ Nytt** för att skapa en ny mapp med namnet &quot;Gamla kontrakt&quot;.

   ![Skärmbild av nya mappar](assets/documentautomation/automation_25.png)

Dessa mappar refereras nu som en del av ditt Power Automate-flöde.

### Skapa ett flöde från en mall

1. Logga in på https://flow.microsoft.com.
1. Klicka **Mallar** i sidofältet.

   ![Skärmbild av val av mallar](assets/documentautomation/automation_26.png)

1. Välj **Konvertera nyligen tillagda filer till PDF för textsökning i SharePoint**.
1. Klicka på **+** bredvid Adobe PDF Tools.

   ![Skärmbild av valet +](assets/documentautomation/automation_27.png)

1. Gå till https://www.adobe.com/go/powerautomate_getstarted på en ny flik.
1. Klicka på **Kom igång**.

   ![Skärmbild av knappen Kom igång](assets/documentautomation/automation_28.png)

1. Logga in med ditt Adobe ID.

   ![Skärmbild av inloggningsskärmen](assets/documentautomation/automation_29.png)

1. Ange inloggningsnamn och inloggningsbeskrivning och klicka på **Skapa autentiseringsuppgifter**.

   ![Skärmbild på skärmen Skapa autentiseringsuppgifter](assets/documentautomation/automation_30.png)

   Håll fönstret med autentiseringsuppgifterna öppna. Du måste ange dem i Microsoft Power Automate.

   ![Skärmbild av webbläsarfliken för att hålla den öppen](assets/documentautomation/automation_31.png)

1. Ange autentiseringsuppgifterna och klicka på **Skapa i Microsoft Power Automate**.

   ![Skärmbild av inloggningsuppgifter för PDF Tools](assets/documentautomation/automation_32.png)

1. Klicka på **Fortsätt**.

   ![Skärmbild av var du kan klicka på Fortsätt](assets/documentautomation/automation_33.png)

   Nu kan du se en vy över arbetsflödet och du måste konfigurera den för din miljö.

1. Markera fältet Webbplatsadress och välj vilken SharePoint-webbplats du använder under utlösaren som heter **När en fil skapas i en mapp**.

   ![Skärmbild av val när en fil skapas i en mapputlösare](assets/documentautomation/automation_34.png)

1. Klicka på mappikonen och gå till mappen Gamla kontrakt som finns under Mapp-ID.

   ![Skärmbild av val av mapp med gamla avtal](assets/documentautomation/automation_35.png)

1. Redigera **Skapa fil** Åtgärd längst ned i flödet:

   Ändra **Webbplatsadress** till din webbplatsadress.
Ange platsen för den bearbetade avtalsmappen i mappsökvägen.

1. Klicka **Spara** i det övre högra hörnet.
1. Klicka **Testa**.
1. Välj **Manuellt**.
1. Klicka **Testa**.

   ![Skärmbild av testflödet](assets/documentautomation/automation_36.png)

### Prova ditt nya flöde

1. Gå till mappen Gamla avtal i SharePoint.
1. Gå till E03/Old Contracts i övningsfilerna du hämtade.
1. Kopiera filerna ReleaseFormXX.pdf till mappen Old Contracts i SharePoint.

   ![Skärmbild av kopiering av filerna](assets/documentautomation/automation_37.png)

Om du nu går till mappen Bearbetade avtal kan du se PDF tillgängligt efter att flödet har beviljats några minuter. Om du öppnar PDF kan du se att texten går att markera.
Dessutom indexerar SharePoint dokumentet så att du kan söka i dokumentens innehåll från sökfältet i SharePoint.

## Del 4: Automatiserad dokumentsamling med Adobe PDF Tools {#part4}

I del fyra får du lära dig hur du slår samman många dokument utifrån den information som ges när du väljer och startar ett flöde från Microsoft SharePoint. I detta scenario kommer flödet att

* Be om information för att välja vad som ska ingå i ett paket för en kund.
* Baserat på den information som ges sammanfogas många dokument. Dokumenten innehåller ett försättsblad och valfria informationsdokument.
* Det sammanfogade dokumentet sparas i SharePoint.

### Importera övningsfiler till SharePoint

1. Öppna mappen E04 i övningsfilerna.
1. Importera mapparna Förslag, Mallar och Genererade dokument till SharePoint.

   ![Skärmbild av import av mappar](assets/documentautomation/automation_38.png)

Mapparna används som referens. Du kommer särskilt att använda filen proposal.docx för ditt förslag.

I mappen Mallar finns mappen Omslag som innehåller försättsblad för olika städer. Det finns även en mapp med informationsdokument som innehåller ytterligare informationsdokument som bifogas till slutet om det här alternativet väljs.

### Importera flödet till Microsoft Power Automate

1. Logga in på Microsoft Power Automate (https://flow.microsoft.com).
1. Klicka **Mina flöden**.

   ![Skärmbild av var du kan välja Mina flöden](assets/documentautomation/automation_39.png)

1. Klicka på **Importera**.

   ![Skärmbild av importskärmen](assets/documentautomation/automation_40.png)

1. Klicka **Överför** och välj mappen Generateproposal_20210311231623.zip i E04/Flow/.

   ![Skärmbild av val av mapp](assets/documentautomation/automation_41.png)

1. Klicka på **Importera**.

1. Klicka på skiftnyckeln under Åtgärd bredvid **Skicka förslag till kund**.

   ![Skärmbild av skiftnyckeln ikon](assets/documentautomation/automation_42.png)

1. Välj **Skapa som ny** under Inställningar.
1. Ange flödets namn under Resursnamn.
1. Klicka på **Spara**.

   Upprepa detta för andra relaterade resurser och välj din anslutning.

   ![Skärmbild av hur filen sparas](assets/documentautomation/automation_43.png)

1. Klicka **Importera** när du har gjort alla anslutningar.

### Ange för en markerad fil

Gör följande nu när flödet har skapats:

1. Klicka på **Redigera**.

   ![Skärmbild av var du kan redigera](assets/documentautomation/automation_44.png)

1. Välj utlösare **För en markerad fil**.

   Lägg till SharePoint-webbplatsen i webbplatsadressen.
Lägg till ditt bibliotek i biblioteket.

   ![Skärmbild av slutförd utlösare](assets/documentautomation/automation_45.png)

### Ange templateFolderPath

1. Klicka på variabeln templateFolderPath.
1. Ange sökvägen till den plats där mappen Mallar finns på SharePoint-webbplatsen som du importerade.

### Ställ in omslagsbild för att hämta filinnehåll

1. Klicka **Omslag** som utvidgar räckvidden.
1. Expandera **Omslag: Hämta filinnehåll**.

   Ange webbplatsadressen till din SharePoint-webbplats.

   ![Skärmbild av expanderat omslag](assets/documentautomation/automation_46.png)



### Ställ in vald fil

1. Utöka **Vald fil** omfångsåtgärd.

   Ändra webbplatsadressen och biblioteksnamnet till din SharePoint-webbplats respektive ditt bibliotek under **Hämta filegenskaper**.
Ändra webbplatsadressen till din SharePoint-webbplats under **Hämta filinnehåll**.

   ![Skärmbild av expanderad vald fil](assets/documentautomation/automation_47.png)

### Ange informationsdokument

1. Klicka **Informationsdokument** åtgärder.
1. Expandera **Villkor: Lägg till informationsdokument**.

   ![Skärmbild av utökat villkor för Lägg till informationsdokument](assets/documentautomation/automation_48.png)

1. Expandera **Informationsdokument 1: Hämta filinnehåll med sökväg**.
Redigera webbplatsadressen till den angivna SharePoint-webbplatsen.

Upprepa samma steg för **Villkor: Lägg till informationsdokument 2**.

### Ställ in Skapa fil

1. Expandera **Skapa fil**.

   Redigera webbplatsadress och mappsökväg till den SharePoint-webbplats och sökväg där den genererade dokumentmappen finns.

1. Klicka på **Spara**.

### Testa flödet

1. Gå till mappen Förslag i SharePoint.
1. Välj mappen Förslag.docx.

   ![Skärmbild av val av förslagsmapp](assets/documentautomation/automation_49.png)

1. Välj ditt flöde under **Automatisera** -menyn.

   ![Skärmbild av valet av automatiseringsmenyn](assets/documentautomation/automation_50.png)

1. Klicka **Fortsätt** för att påbörja flödet.

   ![Skärmbild av val av knappen Fortsätt](assets/documentautomation/automation_51.png)

1. Välj omslag och de informationsdokument du vill bifoga.
1. Klicka **Kör flöde**.

   ![Skärmbild av knappen Kör flöde](assets/documentautomation/automation_52.png)

Gå till mappen Generera dokument. Du bör nu se din genererade PDF-fil.

![Skärmbild av SharePoint-katalogen med en ny PDF-fil](assets/documentautomation/automation_53.png)

### Lägga till Protect och andra åtgärder i Flow

Nu när du har skapat ett flöde kommer du att redigera det för att kryptera PDF-dokumentet med ett lösenord. Detta går också igenom hur du kan utnyttja andra åtgärder.

1. Gå tillbaka till slutet av flödet.
1. Klicka på **+** symbol mellan **Sammanfoga PDF** och **Skapa fil**.

   ![Skärmbild av var du ska välja + symbol](assets/documentautomation/automation_54.png)

1. Välj **Lägg till en åtgärd**.
1. Sök efter &quot;Adobe PDF Tools&quot;.

   ![Skärmbild av sökning efter Adobe PDF](assets/documentautomation/automation_55.png)

1. Välj **Protect PDF från visning**.
1. Använd Dynamiskt innehåll för att ställa in fältet Filnamn på **PDF-filnamn från Slå samman PDF**.

   ![Skärmbild av dynamiskt innehåll](assets/documentautomation/automation_56.png)

   I utlösaren finns det ett lösenordsfält som ingår i initieringsformuläret. Det kan vi använda här.

1. Sök efter **Lösenordsfält** använda dynamiskt innehåll och placera det i fältet Lösenord.

   ![Skärmbild av sökning efter lösenord](assets/documentautomation/automation_57.png)

1. Använd dynamiskt innehåll för att ställa in det på **PDF-filinnehåll från Slå samman PDF** i fältet Filinnehåll.
1. Ändra **Skapa fil** om du vill hämta filinnehållet från Protect PDF i stället för att sammanfoga PDF.
1. Expandera **Skapa fil**.
1. Rensa fältet Filinnehåll.
1. Använda dynamiskt innehåll för montering **PDF-filinnehåll** från **Protect PDF från visning**.

### Testa flödet

1. Gå till mappen Förslag i SharePoint.
1. Välj förslag.docx.

   ![Skärmbild av val av förslagsmapp](assets/documentautomation/automation_58.png)

1. Välj **Automatisera** för att välja flöde.

   ![Skärmbild av att välja Automatisera i menyn](assets/documentautomation/automation_59.png)

1. Klicka **Fortsätt** för att påbörja flödet.

   ![Skärmbild av att välja Fortsätt](assets/documentautomation/automation_60.png)

1. Välj omslaget och de informationsdokument du vill bifoga.
1. Ställ in fältet Lösenord till det Lösenord som du vill ställa in.
1. Klicka **Kör flöde**.

   ![Skärmbild av valda filer och knappen Kör flöde](assets/documentautomation/automation_61.png)

1. Gå till mappen Generera dokument.
Du bör se din genererade PDF-fil. Öppna filen PDF och du ombeds att ange ditt PDF-lösenord.

   ![Skärmbild av genererat PDF i SharePoint-katalog](assets/documentautomation/automation_62.png)
