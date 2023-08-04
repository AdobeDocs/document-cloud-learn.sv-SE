---
title: Skicka aviseringar med Acrobat Sign för Microsoft Dynamics 365 och Marketo
description: Lär dig hur du skickar ett textmeddelande, e-postmeddelande eller push-meddelande för att informera undertecknaren om att ett avtal är på väg
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Skicka aviseringar med Acrobat Sign för Microsoft Dynamics 365 och Marketo

Lär dig hur du skickar ett textmeddelande, e-postmeddelande eller push-meddelande för att informera undertecknaren om att ett avtal är på väg med hjälp av Acrobat Sign, Acrobat Sign för Microsoft Dynamic, Marketo och Marketo Microsoft Dynamics Sync. Om du vill skicka aviseringar från Marketo måste du först köpa eller konfigurera en Marketo SMS-hanteringsfunktion. Genomgången använder [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), men andra SMS-lösningar från Marketo är tillgängliga.

## Förutsättningar

1. Installera Marketo Microsoft Dynamics Sync.

   Information och det senaste plugin-programmet för Microsoft Dynamics Sync är tillgängliga [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installera Acrobat Sign för Microsoft Dynamics.

   Information om detta plugin-program är tillgänglig [här.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Hitta det anpassade objektet

När konfigurationerna för Marketo Microsoft Dynamics Sync och Acrobat Sign för Dynamics är klara visas två nya alternativ i Marketo Admin Terminal.

![Administration](assets/adminTerminal.png)

* Klicka **[!UICONTROL Dynamics - entitetssynkronisering]**.

  Synkronisering måste inaktiveras innan anpassade entiteter synkroniseras. Klicka **[!UICONTROL Synkroniseringsschema]** om det här är första gången du gör det. Klicka annars på **[!UICONTROL Uppdatera schema]**.

  ![Uppdatera](assets/refreshSchema.png)

## Synkronisera det anpassade objektet

1. Leta på höger sida [!UICONTROL Lead], [!UICONTROL Kontakt]och [!UICONTROL Konto]-baserade anpassade objekt.

   * **[!UICONTROL Aktivera synkronisering]** för objekten under Lead om du vill utlösa när en lead läggs till i ett avtal i Dynamics.

   * **[!UICONTROL Aktivera synkronisering]** för objekten under Kontakt om du vill utlösa när en kontakt läggs till i ett avtal i Dynamics.

   * **[!UICONTROL Aktivera synkronisering]** för objekten under Konto om du vill utlösas när ett konto läggs till i ett avtal i Dynamics.

   * **Aktivera synkronisering** för avtalsobjektet under den önskade mallen (lead, kontakt eller konto).

   ![Anpassade objekt](assets/enableSyncDynamics.png)

1. I det nya fönstret väljer du de egenskaper du vill ha under Avtal.

   Aktivera rutorna under **[!UICONTROL Begränsning]** och **[!UICONTROL Utlösare]** för att exponera dem för dina marknadsföringsaktiviteter.

   ![Anpassad synkronisering 1](assets/entitySync1.png)

   ![Anpassad synkronisering 2](assets/entitySync2.png)

1. Återaktivera synkroniseringen när du har aktiverat synkronisering med de anpassade objekten.

   Gå tillbaka till [!UICONTROL Administratörsterminal]och klicka sedan på **[!UICONTROL Microsoft Dynamics]** och klicka sedan på **[!UICONTROL Aktivera synkronisering]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Aktivera global](assets/enableGlobalDynamics.png)

## Skapa programmet

1. in [!UICONTROL Marknadsföringsaktiviteter], högerklicka **[!UICONTROL Marknadsföringsaktiviteter]** i det vänstra fältet väljer du **[!UICONTROL Ny kampanjmapp]** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen och välj **[!UICONTROL Nytt program]** och ge den ett namn.

   Låt allt annat vara standard och klicka sedan på **[!UICONTROL Skapa]**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

## Konfigurera [!DNL Twilio] SMS

Se först till att du har en aktiv [!DNL Twilio] och köpt de SMS-funktioner du behöver.

Konfigurera Marketo - [!DNL Twilio] För SMS-webhook krävs tre [!DNL Twilio] parametrar från ditt konto.

* Konto-SID
* Kontotoken
* Twilio-telefonnummer

Hämta parametrarna från ditt konto. Öppna nu Marketo-instansen.

1. Klicka **[!UICONTROL Administratör]** längst upp till höger.

   ![Administration](assets/adminTab.png)

1. Klicka **[!UICONTROL Webhooks]** och klicka sedan på **[!UICONTROL Ny webhook]**.

   ![Webhookar](assets/webhooks.png)

1. Ange ett **[!UICONTROL Namn på webhook]** och **[!UICONTROL Beskrivning]**.

1. Ange följande URL och var noga med att ersätta `ACCOUNT_SID` och `AUTH_TOKEN` med din [!DNL Twilio] autentiseringsuppgifter.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Välj **[!UICONTROL POST]** som typ av begäran.

1. Ange följande **Mall** och var noga med att ersätta `MY_TWILIO_NUMBER` med din [!DNL Twilio] telefonnummer och `YOUR_MESSAGE` med ett meddelande som du själv väljer.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Ange **[!UICONTROL Begär tokenkodning]** till *Formulär/URL*.

1. Ställ in svarstypen som *JSON* klicka sedan på **[!UICONTROL Spara]**.

## Ställ in utlösaren för smart kampanj

1. I avsnittet Marknadsföringsaktiviteter högerklickar du på det program du skapade och väljer sedan **[!UICONTROL Ny smart kampanj]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn och klicka sedan på **[!UICONTROL Skapa]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Du bör se flera utlösare som är tillgängliga för användning i Microsoft-mappen.

1. Klicka och dra **[!UICONTROL Tillagt i avtal]** till **[!UICONTROL Smart lista]** och lägg sedan till eventuella begränsningar för utlösaren.

   ![Tillagt i avtal](assets/addedToAgreementDynamics.png)

## Ställ in flödet Smart Campaign

1. Klicka på **[!UICONTROL Flöde]** fliken i [!UICONTROL Smart Campaign].

   Sök efter och dra **Anropa webhook** flöda till arbetsytan och välj den webhook som du skapade i föregående avsnitt.

   ![Anropa webhook](assets/callWebhook.png)

1. Din SMS-meddelandekampanj för leads som läggs till i ett avtal har nu konfigurerats.
>[!TIP]
>
>Den här självstudiekursen är en del av kursen [Påskynda försäljningscyklerna med Acrobat Sign för Microsoft Dynamics och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är tillgänglig gratis på Experience League!