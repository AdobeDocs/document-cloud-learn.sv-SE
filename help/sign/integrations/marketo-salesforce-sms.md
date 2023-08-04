---
title: Skicka meddelanden med Acrobat Sign för Salesforce och Marketo
description: Lär dig hur du skickar ett textmeddelande, e-postmeddelande eller push-meddelande för att informera undertecknaren om att ett avtal är på väg
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Skicka aviseringar med Acrobat Sign för [!DNL Salesforce] och [!DNL Marketo]

Lär dig hur du skickar ett textmeddelande, e-postmeddelande eller push-meddelande för att informera undertecknaren om att ett avtal är på väg med hjälp av Acrobat Sign, Acrobat Sign för Salesforce, Marketo och Marketo Salesforce-synkronisering. Om du vill skicka aviseringar från Marketo måste du först köpa eller konfigurera en Marketo SMS-hanteringsfunktion. Genomgången använder [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), men andra SMS-lösningar från Marketo är tillgängliga.

## Förutsättningar

1. Installera Marketo Salesforce-synkroniseringen.

   Information och det senaste plugin-programmet för Salesforce Sync är tillgängligt [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installera Acrobat Sign för Salesforce.

   Information om detta plugin-program är tillgänglig [här.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Hitta det anpassade objektet

När konfigurationerna för Marketo Salesforce Sync och Acrobat Sign för Salesforce har slutförts visas flera nya alternativ i Marketo Admin Terminal.

![Administration](assets/adminTab.png)

![Objektsynkronisering](assets/salesforceAdmin.png)

1. Klicka **Synkroniseringsschema** om det här är första gången du gör det. Klicka annars på **Uppdatera schema**.

   ![Uppdatera](assets/refreshSchema1.png)

1. Om global synkronisering körs inaktiverar du den genom att klicka på **Inaktivera global synkronisering**.

   ![Inaktivera](assets/disableGlobal.png)

1. Klicka **Uppdatera schema**.

   ![Uppdatera 2](assets/refreshSchema2.png)

## Synkronisera anpassade objekt

Till höger finns information i Lead-, Contact- och Account-based custom objects.

**Aktivera synkronisering** för objekten under Lead om du vill utlösa när en lead läggs till i ett avtal i Salesforce.

**Aktivera synkronisering** för objekten under Kontakt om du vill utlösa när en kontakt läggs till i ett avtal i Salesforce.

**Aktivera synkronisering** för objekten under Konto om du vill utlösas när ett konto läggs till i ett avtal i Salesforce.

1. **Aktivera synkronisering** för de anpassade objekt som visas under den önskade mallen (lead, kontakt eller konto).

   ![Anpassade objekt](assets/customObjects.png)

1. Följande mediefiler visar hur du **Aktivera synkronisering**.

   ![Anpassad synkronisering 1](assets/customObjectSync1.png)

   ![Anpassad synkronisering 2](assets/customObjectSync2.png)

1. Återaktivera synkningen när du har aktiverat synkronisering av de anpassade objekten.

   ![Aktivera global](assets/enableGlobal.png)

## Skapa programmet

1. I avsnittet Marknadsföringsaktiviteter i Marketo högerklickar du på **Marknadsföringsaktiviteter** i det vänstra fältet väljer du **Ny kampanjmapp** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen och välj **Nytt program** och ge den ett namn. Låt allt annat vara standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

## Konfigurera Twilio SMS

Se först till att du har ett aktivt Twilio-konto och köpt SMS-funktionerna du behöver.

Konfigurera Marketo - Twilio SMS webhook kräver tre Twilio-parametrar från ditt konto.

- Konto-SID
- Kontotoken
- Twilio-telefonnummer

Hämta parametrarna från ditt konto. Öppna nu Marketo-instansen.

1. Klicka på **Administratör** längst upp till höger.

   ![Administration](assets/adminTab.png)

1. Klicka på **Webhooks**, sedan **Ny webhook**.

   ![Webhookar](assets/webhooks.png)

1. Ange ett **Namn på webhook** och **Beskrivning**.

1. Ange följande URL och var noga med att ersätta **[ACCOUNT_SID]** och **[AUTH_TOKEN]** med dina inloggningsuppgifter för Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Välj **POST** som typ av begäran.

1. Ange följande **Mall** och var noga med att ersätta **[MY_TWILIO_NUMBER]** med ditt Twilio telefonnummer och **[YOUR_MESSAGE]** med ett meddelande som du själv väljer.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Ställ in Begärandetokenkodning till Formulär/URL.

1. Ställ in svarstypen till JSON och klicka sedan på **Spara**.

## Ställ in utlösaren för smart kampanj

1. I avsnittet Marknadsföringsaktiviteter högerklickar du på det program du skapade och väljer sedan **Ny smart kampanj**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn och klicka sedan på **Skapa**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Om konfigurationen för den anpassade objektsynkroniseringen har gjorts korrekt bör du se följande utlösare tillgängliga för användning i mappen Salesforce.

1. Klicka och dra Tillagt till avtal i den smarta listan. Lägg till eventuella begränsningar för utlösaren.

   ![Lades till i avtal 2](assets/addedToAgreement2.png)

## Ställ in flödet Smart Campaign

1. Klicka på **Flöde** i Smart Campaign. Sök efter och dra **Anropa webhook** flöda till arbetsytan och välj den webhook som du skapade i föregående avsnitt.

   ![Anropa webhook](assets/callWebhook.png)

1. Din SMS-meddelandekampanj för leads som läggs till i ett avtal har nu konfigurerats.

>[!TIP]
>
>Den här självstudiekursen är en del av kursen [Påskynda försäljningscyklerna med Acrobat Sign för Salesforce och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är tillgänglig gratis på Experience League!