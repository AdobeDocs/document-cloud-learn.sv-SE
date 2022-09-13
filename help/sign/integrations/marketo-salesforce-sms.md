---
title: Skicka aviseringar med Acrobat Sign för Salesforce och Marketo
description: Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att informera signeraren om att ett avtal är på väg
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 4827c827ee06c94c38290d5f0e716e8a8328bd48
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Skicka aviseringar med Acrobat Sign för [!DNL Salesforce] och [!DNL Marketo]

Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att informera signeraren om att ett avtal är på väg med Acrobat Sign, Acrobat Sign för Salesforce, Marketo och Marketo Salesforce Sync. Om du vill skicka aviseringar från Marketo måste du först köpa eller konfigurera en Marketo SMS-hanteringsfunktion. Genomgången använder [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), men det finns andra Marketo SMS-lösningar.

## Förutsättningar

1. Installera Marketo Salesforce Sync.

   Information och det senaste plugin-programmet för Salesforce Sync är tillgängligt [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installera Acrobat Sign för Salesforce.

   Information om plugin-programmet finns tillgänglig [här.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Söka efter det anpassade objektet

När konfigurationerna för Marketo Salesforce Sync och Acrobat Sign för Salesforce är klara visas flera nya alternativ i Marketo Admin Terminal.

![Admin](assets/adminTab.png)

![Objektsynkronisering](assets/salesforceAdmin.png)

1. Klicka **Synkroniseringsschema** om det är första gången. I annat fall klickar du på **Uppdatera schema**.

   ![Uppdatera](assets/refreshSchema1.png)

1. Om global synkronisering körs inaktiverar du genom att klicka på **Inaktivera global synkronisering**.

   ![Inaktivera](assets/disableGlobal.png)

1. Klicka **Uppdatera schema**.

   ![Uppdatera 2](assets/refreshSchema2.png)

## Synkronisera anpassade objekt

På höger sida finns mer information i Lead-, Contact- och Account-baserade anpassade objekt.

**Aktivera synkronisering** för objekten under Lead om du vill utlösa när ett lead läggs till i ett avtal i Salesforce.

**Aktivera synkronisering** för objekten under Kontakt om du vill utlösa när en kontakt läggs till i ett avtal i Salesforce.

**Aktivera synkronisering** för objekten under Konto om du vill utlösa när ett konto läggs till i ett avtal i Salesforce.

1. **Aktivera synkronisering** för de anpassade objekt som visas under önskad överordnad (lead, kontakt eller konto).

   ![Anpassade objekt](assets/customObjects.png)

1. Följande resurser visar hur du **Aktivera synkronisering**.

   ![Anpassad synkronisering 1](assets/customObjectSync1.png)

   ![Anpassad synkronisering 2](assets/customObjectSync2.png)

1. När du har aktiverat synkronisering på de anpassade objekten återaktiverar du synkroniseringen.

   ![Aktivera global](assets/enableGlobal.png)

## Skapa programmet

1. I avsnittet Marknadsföringsaktiviteter i Marketo högerklickar du på **Marknadsföringsaktiviteter** i det vänstra fältet väljer du **Ny kampanjmapp** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen och välj **Nytt program** och ge den ett namn. Låt allt annat vara standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

## Konfigurera Twilio SMS

Kontrollera först att du har ett aktivt Twilio-konto och köpt de SMS-funktioner du behöver.

Konfigurera Marketo - Twilio SMS-webhook kräver tre Twilio-parametrar från ditt konto.

- Konto-SID
- Kontotoken
- Twilio-telefonnummer

Hämta parametrarna från ditt konto och öppna nu Marketo-instansen.

1. Klicka på **Administratör** uppe till höger.

   ![Administratör](assets/adminTab.png)

1. Klicka på **Webhooks** sedan **Ny webhook**.

   ![Webhookar](assets/webhooks.png)

1. Ange ett **Webhooknamn** och **Beskrivning**.

1. Ange följande URL och var noga med att ersätta **[ACCOUNT_SID]** och **[AUTH_TOKEN]** med dina Twilio-inloggningsuppgifter.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Välj **POST** som typ av begäran.

1. Ange följande **Mall** och se till att ersätta **[MY_TWILIO_NUMBER]** med ditt Twilio-telefonnummer och **[YOUR_MESSAGE]** med ett meddelande som du själv väljer.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Ange Form/URL för Begär tokenkodning.

1. Ställ in svarstypen på JSON och klicka sedan på **Spara**.

## Ställ in utlösaren för smarta kampanjer

1. I avsnittet Marknadsföringsaktiviteter högerklickar du på det program du skapade och väljer sedan **Ny smart kampanj**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn och klicka sedan på **Skapa**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Om konfigurationen för anpassad objektsynkronisering var korrekt gjord bör du se följande utlösare tillgängliga för användning under Salesforce-mappen.

1. Klicka på och dra Lägg till i avtal till den smarta listan. Lägg till eventuella begränsningar för utlösaren.

   ![Lades till i avtal 2](assets/addedToAgreement2.png)

## Ställ in smart kampanjflöde

1. Klicka på **Flöde** i Smart Campaign. Sök efter och dra **Anropa webhook** flöda till arbetsytan och välj den webhook som du skapade i föregående avsnitt.

   ![Anropa webhook](assets/callWebhook.png)

1. Din SMS-meddelandekampanj för leads som läggs till i ett avtal har nu konfigurerats.

>[!TIP]
>
>Den här självstudiekursen är en del av kursen [Snabba upp säljcyklerna med Acrobat Sign för Salesforce och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är tillgänglig gratis på Experience League!