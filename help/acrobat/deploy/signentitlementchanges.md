---
title: Viktiga produktuppdateringar för Acrobat DC för ETLA-kunder
description: Läs mer om viktiga ändringar av Acrobat DC-berättiganden som ingår i ETLA (Enterprise Term License Agreement) som erbjuds från och med augusti 2020 till och med den 20 november 2020
feature: Deploy
role: Admin
level: Intermediate
jira: KT-7269
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 4e6fbf91e96d26f9ee8f1105ad68738b9450a32d
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 2%

---

# Viktiga produktuppdateringar för Acrobat DC för ETLA-kunder

[!DNL Adobe Sign Individual] (kallas även Adobe Sign Pro) kommer att avetableras från alla Acrobat DC-berättiganden som ingår i ETLA (Enterprise Term License Agreement) som erbjuds först från och med augusti 2020 och kommer att fortsätta till och med den 20 november 2020. [!DNL Adobe Sign Individual] tillhandahåller inte funktioner i företagsklass och bör ersättas med Adobe Sign Enterprise för företagskunder. Detta omfattar Acrobat DC som licensieras som en fristående app och Acrobat DC som licensieras som en del av Creative Cloud for enterprise - Alla program.

Åtkomst till [!DNL Adobe Sign Individual] är tillgänglig i Acrobat via verktyget **Adobe Sign** eller verktyget **Fill &amp; Sign** ([Begär signaturer](https://www.adobe.com/se/acrobat/online/request-signature.html){target="_blank"}).

![[!DNL Adobe Sign Individual] åtkomst i Acrobat DC](../assets/Deploy_SignEntitle1.png)

Om du inte har uppdaterat Acrobat DC till den senaste versionen kan verktyget vara märkt Send for Signature.

## Varför avetablerar vi detta?

[I oktober 2018 släppte vi ett helt nytt Acrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC). Den senaste versionen innehåller nya verktyg och funktioner som gör att du kan arbeta med PDF på mobila enheter, webben och datorn, plus helt nya samarbetsverktyg. Om du prenumererar på Acrobat DC bör du redan ha tillgång till de här fantastiska funktionerna. En annan stor uppdatering som vi släppte gällde vår lösning för elektroniska signaturer, Adobe Sign.

Före oktober 2018-versionen har Acrobat DC-användare kunnat skicka dokument för e-signering med verktyg i Acrobat som är märkta &quot;Fill &amp; Sign&quot; (eller &quot;Adobe Sign&quot; eller &quot;Send for Signature&quot;) och som har tilldelats [!DNL Adobe Sign Individual]-behörighet.

Det här alternativet är ett bra sätt att hämta e-signaturer, men vi avetablerar [!DNL Adobe Sign Individual] eftersom det inte ger den funktion på företagsnivå som är tillgänglig via Adobe Sign Enterprise, till exempel:

* Möjlighet att centralt hantera användare som har behörighet att skicka avtal eller signera
* Tillåt administratörer att hantera avtal som skickas och används i hela organisationen
* Ger detaljerade kontroller för att hantera elektroniska signaturer i hela organisationen

Dessutom har Adobe Sign Enterprise fler funktioner jämfört med vad som var tillgängligt i berättigandet till [!DNL Adobe Sign Individual], inklusive men inte begränsat till:

* Administration
   * Enkel inloggning
   * Kontodelegering
* Integreringar
   * Fördefinierade företagsintegrationer med Dropbox, Salesforce, Workday osv.
   * Adobe Sign är den föredragna e-signaturlösningen i hela företagsportföljen [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html), inklusive Office 365, SharePoint, Dynamics, Teams och Flow
* Anpassning och optimering
   * Förbättrad autentisering av e-signaturer, avancerad ID-baserad verifiering av signeraridentitet, arbetsflödesdesigner, avancerat språkstöd osv.

Adobe Sign är den branschledande globalt erkända lösningen för att hämta juridiskt bindande signaturer. Adobe Sign är byggt från grunden för att uppfylla ditt företags behov av e-signaturer med IT-administratörsvänliga verktyg för att säkerställa att du och dina användare använder e-signaturer som helt överensstämmer med olika regionala bestämmelser och branschbestämmelser om e-signaturer. Gå till [här](https://helpx.adobe.com/se/enterprise/using/adobe-sign-for-enterprise.html) om du vill ha mer information om hur du hanterar Sign via [Adobe Admin Console](https://helpx.adobe.com/se/enterprise/using/admin-console.html).

Kontakta din Adobe-kontakt för att diskutera hur du kan fortsätta att tillhandahålla e-signaturfunktioner för ditt företag via vår bredare plattform för digitala dokument som omfattar Acrobat DC och Adobe Sign Enterprise.

## Tillgång till befintliga avtal

Användare kan fortfarande komma åt alla avtal som skickas ut före den här åtgärden via Adobe Document Cloud genom att logga in med sitt Adobe ID på https://documentcloud.adobe.com. Om den här användaren har schemalagts för migrering till Sign Enterprise måste användaren följa de här [instruktionerna](https://helpx.adobe.com/se/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Acrobat DC-upplevelse utan [!DNL Sign Individual]-berättigande

Användare som har Adobe Sign Enterprise-berättiganden kan skicka avtal inom Acrobat med antingen Adobe Sign- eller [!UICONTROL Fill &amp; Sign]-verktyget (Begär signaturer).
Användare som inte har Adobe Sign Enterprise-berättiganden kan inte skicka ut nya avtal och får ett felmeddelande. Grafiken nedan visar möjliga resultat.

![Felmeddelande för Acrobat DC-upplevelsen](../assets/Deploy_SignEntitle2.png)

## Adobe Document Cloud-webbupplevelse utan individuell Sign-behörighet

Användare kan logga in på https://documentcloud.adobe.com/ för att komma åt och hämta alla avtal som har skickats ut innan Adobe Sign Individual-berättigandet inaktiveras.

![Felmeddelande för webbupplevelsen i Document Cloud](../assets/Deploy_SignEntitle3.png)

## Mer information finns på följande sidor:

* [Logga in på Adobe Document Cloud](https://helpx.adobe.com/se/document-cloud/help/sign-in.html)
* [Hantera filer (var är mina filer?)](https://helpx.adobe.com/se/document-cloud/help/manage-files.html)
* [Använder [!UICONTROL Acrobat Customization Wizard] för konfiguration](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [Översikt över [!UICONTROL Admin Console]](https://helpx.adobe.com/se/enterprise/using/admin-console.html)
* [Hantera Adobe Sign på [!UICONTROL Admin Console]](https://helpx.adobe.com/se/enterprise/using/adobe-sign-for-enterprise.html)

**Revisioner** 20 maj 2020; originalinlägg - augusti 2019
