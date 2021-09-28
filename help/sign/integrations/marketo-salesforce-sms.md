---
title: Skicka meddelanden med Adobe Sign för Salesforce och Marketo
description: Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att tala om för signeraren att ett avtal är på väg
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Skicka meddelanden med Adobe Sign för Salesforce och Marketo

Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att tala om för signeraren att ett avtal är på väg att användas med Adobe Sign, Adobe Sign för Salesforce, Marketo och Marketo Salesforce Sync. Om du vill skicka meddelanden från Marketo måste du först köpa eller konfigurera en SMS-hanteringsfunktion från Marketo. Vid genomgången används [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), men andra Marketo SMS-lösningar finns tillgängliga.

## Förutsättningar

1. Installera Marketo Salesforce Sync.

   Information och det senaste plugin-programmet för Salesforce Sync finns [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Installera Adobe Sign för Salesforce.

   Information om det här plugin-programmet finns [här.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Söka efter det anpassade objektet

När konfigurationerna för Marketo Salesforce Sync och Adobe Sign för Salesforce har slutförts visas flera nya alternativ i Marketo Admin Terminal.

![Admin](assets/adminTab.png)

![Objektsynkronisering](assets/salesforceAdmin.png)

1. Klicka på **Synkronisera schema** om det är första gången. Annars klickar du på **Uppdatera schema**.

   ![Uppdatera](assets/refreshSchema1.png)

1. Om global synkronisering körs inaktiverar du genom att klicka på **Inaktivera global synkronisering**.

   ![Inaktivera](assets/disableGlobal.png)

1. Klicka på **Uppdatera schema**.

   ![Uppdatera 2](assets/refreshSchema2.png)

## Synkronisera anpassade objekt

Till höger finns mer information i Lead-, Kontakt- och Kontobaserade anpassade objekt.

**Aktivera** Synkronisering för objekten under Lead om du vill aktivera när en lead läggs till i ett avtal i Salesforce.

**Aktivera** Synkronisering för objekten under Kontakt om du vill utlösa när en kontakt läggs till i ett avtal i Salesforce.

**Aktivera** Synkronisera för objekten under Konto om du vill aktivera när ett konto läggs till i ett avtal i Salesforce.

1. **Aktivera** synkronisering för de anpassade objekt som visas under den överordnade (lead, kontakt eller konto) som du vill använda.

   ![Anpassade objekt](assets/customObjects.png)

1. Följande resurser visar hur du **aktiverar synkronisering**.

   ![Anpassad synkronisering 1](assets/customObjectSync1.png)

   ![Anpassad synkronisering 2](assets/customObjectSync2.png)

1. När synkroniseringen av anpassade objekt har aktiverats återaktiveras synkroniseringen.

   ![Aktivera global](assets/enableGlobal.png)

## Skapa programmet

1. I avsnittet Marknadsföringsaktiviteter i Marketo högerklickar du på **Marknadsföringsaktiviteter** till vänster, väljer **Ny kampanjmapp** och ger den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen, välj **Nytt program** och ge den ett namn. Lämna allt annat som standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

## Konfigurera Twilio SMS

Kontrollera först att du har ett aktivt Twilio-konto och har köpt de SMS-funktioner du behöver.

För att konfigurera Marketo - Twilio SMS-webkroken krävs tre Twilio-parametrar från ditt konto.

- Konto-SID
- Kontotoken
- Twilio-telefonnummer

Hämta de här parametrarna från ditt konto och öppna nu din Marketo-instans.

1. Klicka på **Admin** överst till höger.

   ![Administratör](assets/adminTab.png)

1. Klicka på **Webhooks** och **Ny Webkrok**.

   ![Webhookar](assets/webhooks.png)

1. Ange ett **Webkroknamn** och **Beskrivning**.

1. Ange följande URL och se till att ersätta **[ACCOUNT_SID]** och **[AUTH_TOKEN]** med dina Twilio-autentiseringsuppgifter.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Välj **POST** som frågetyp.

1. Ange följande **Mall** och se till att **[MY_TWILIO_NUMBER]** ersätts med ditt Twilio-telefonnummer och **[DITT_MEDDELANDE]** med ett meddelande som du väljer.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Ställ in formuläret/URL för Begär tokenkodning.

1. Ställ in svarstypen på JSON och klicka sedan på **Spara**.

## Konfigurera Smart Campaign Trigger

1. I avsnittet Marknadsföringsaktiviteter högerklickar du på det program du skapade och väljer sedan **Ny smart kampanj**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn och klicka sedan på **Skapa**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Om konfigurationen för den anpassade objektsynkroniseringen har utförts på rätt sätt bör du se följande utlösare som är tillgängliga för användning i Salesforce-mappen.

1. Klicka på och dra Lägg till i avtal till den smarta listan. Lägg till eventuella begränsningar som du vill ha på utlösaren.

   ![Tillagt i avtal 2](assets/addedToAgreement2.png)

## Ställ in smart kampanjflöde

1. Klicka på fliken **Flöde** i Smart Campaign. Sök efter och dra **Anropa Webkrok**-flödet till arbetsytan och välj den webkrok du skapade i föregående avsnitt.

   ![Ring Webkrok](assets/callWebhook.png)

1. Din SMS-meddelandekampanj för leads som läggs till i ett avtal har nu konfigurerats.

>[!TIP]
>
>Den här självstudiekursen ingår i kursen [Snabba upp säljcyklerna med Adobe Sign för Salesforce och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är kostnadsfri på Experience League!