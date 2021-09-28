---
title: Viktiga Acrobat DC-produktuppdateringar för ETLA-kunder
description: Läs om viktiga ändringar av Acrobat DC-berättiganden som ingår i ETLA (Enterprise Term License Agreement) från augusti 2020 till den 20 november 2020
role: Admin
product: adobe acrobat
level: Intermediate
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 018cbcfd1d1605a8ff175a0cda98f0bfb4d528a8
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 3%

---

# Viktiga Acrobat DC-produktuppdateringar för ETLA-kunder

[!DNL Adobe Sign Individual] (även kallat Adobe Sign Pro) kommer att tas bort från alla Acrobat DC-berättiganden som ingår i ETLA (Enterprise Term License Agreement) endast från och med augusti 2020 och fortsätter till och med 20 november 2020. [!DNL Adobe Sign Individual] har ingen funktionalitet i enterpriseklass och bör ersättas med Adobe Sign Enterprise for enterprise-kunder. Detta omfattar Acrobat DC som licensieras som en fristående app och Acrobat DC som licensieras som en del av Creative Cloud for enterprise - Alla program.

Du kan komma åt [!DNL Adobe Sign Individual] i Acrobat via verktyget **Adobe Sign** eller verktyget **Fill &amp; Sign** (Begär signaturer).

![[!DNL Adobe Sign Individual] behörighet i Acrobat DC](../assets/Deploy_SignEntitle1.png)

Om du inte har uppdaterat Acrobat DC till den senaste versionen kan verktyget ha etiketten&quot;Send for Signature&quot;.

## Varför avetablerar vi det här?

[I oktober 2018 släppte vi en helt ny Acrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC). Den senaste releasen innehåller nya verktyg och funktioner för att arbeta bättre med PDF:er på mobila enheter, på webben och datorer, plus helt nya samarbetsverktyg. Som prenumerant på Acrobat DC bör du redan ha tillgång till dessa fantastiska funktioner. En annan viktig uppdatering som vi har släppt var Adobe Sign lösning för elektroniska signaturer.

Före oktoberversionen 2018 har Acrobat DC-användare kunnat skicka ut dokument för e-signering med verktyg i Acrobat som är märkta &quot;Fill &amp; Sign&quot; (eller &quot;Adobe Sign&quot; eller &quot;Send for Signature&quot;) som var tilldelade [!DNL Adobe Sign Individual]-berättigande.

Även om det här alternativet har varit ett bra sätt att fånga in e-signaturer håller vi på att ta bort [!DNL Adobe Sign Individual] eftersom det inte har de funktioner för Enterprise-kvalitet som är tillgängliga via Adobe Sign Enterprise, till exempel:

* Möjlighet att centralt hantera användare som har behörighet att skicka avtal eller signera
* Tillåt administratörer att hantera avtal som skickas och används i hela organisationen
* Detaljerade kontroller för hantering av elektroniska signaturer i hela organisationen

Dessutom erbjuder Adobe Sign Enterprise fler funktioner jämfört med vad som var tillgängligt i [!DNL Adobe Sign Individual]-berättigandet, inklusive, men inte begränsat till:

* Administration
   * Enkel inloggning
   * Kontodelegering
* Integreringar
   * Färdiga företagsintegreringar med Dropbox, Salesforce, Workday osv.
   * Adobe Sign är den e-signaturlösning som [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html) rekommenderas i företagsportföljen, inklusive Office 365, SharePoint, Dynamics, Teams och Flow
* Anpassning och optimering
   * Förbättrad autentisering av e-signaturer, avancerad ID-baserad verifiering av signeraridentitet, arbetsflödesdesigner, avancerat språkstöd osv.

Adobe Sign är den branschledande globala lösningen för att hämta in juridiskt bindande signaturer. Adobe Sign är uppbyggt från grunden för att uppfylla alla era behov av e-signaturer, med IT-administratörsvänliga verktyg för att säkerställa att ni och era användare använder e-signaturer som till fullo uppfyller de olika regionala och branschmässiga reglerna för e-signaturer. Besök [här](https://helpx.adobe.com/se/enterprise/using/adobe-sign-for-enterprise.html) för mer information om hur du hanterar Sign via [Adobe Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).

Kontakta din kontaktperson på Adobe för att diskutera hur du kan fortsätta tillhandahålla organisationens e-signaturfunktioner via vår bredare plattform för digitala dokument som omfattar Acrobat DC och Adobe Sign Enterprise.

## Åtkomst till befintliga avtal

Användarna kan fortfarande komma åt avtal som skickats ut före den här åtgärden via Adobe Document Cloud genom att logga in med sin Adobe ID på https://documentcloud.adobe.com. Om den här användaren är schemalagd för migrering till Sign Enterprise måste de följa dessa [instruktioner](https://helpx.adobe.com/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Acrobat DC-upplevelse utan [!DNL Sign Individual]-berättigande

Användare som har Adobe Sign Enterprise-rättigheter kan skicka avtal inom Acrobat med antingen Adobe Sign eller [!UICONTROL Fill &amp; Sign] (Begär signaturer) verktyget.
Användare som inte har Adobe Sign Enterprise-rättigheter kommer inte att kunna skicka ut nya avtal och kommer att få ett felmeddelande. Bilden nedan visar möjliga utfall.

![Felmeddelande för Acrobat DC-upplevelsen](../assets/Deploy_SignEntitle2.png)

## Adobe Document Cloud Web experience without Sign Individual entitlement

Användarna kan logga in på https://documentcloud.adobe.com/ för att få åtkomst till och ladda ned avtal som har skickats ut innan Adobe Sign Individual-berättigandet upphör.

![Felmeddelande för webbupplevelsen i Document Cloud](../assets/Deploy_SignEntitle3.png)

## Mer information finns på följande sidor:

* [Logga in på Adobe Document Cloud](https://helpx.adobe.com/document-cloud/help/sign-in.html)
* [Hantera filer (Var är mina filer?)](https://helpx.adobe.com/document-cloud/help/manage-files.html)
* [Använda  [!UICONTROL Acrobat Customization ] Wizard för konfiguration](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [Översikt över  [!UICONTROL Admin Console]](https://helpx.adobe.com/enterprise/using/admin-console.html)
* [Hantera Adobe Sign på  [!UICONTROL Admin Console]](https://helpx.adobe.com/enterprise/using/adobe-sign-for-enterprise.html)

**20** maj 2020; ursprungligt inlägg - augusti 2019
