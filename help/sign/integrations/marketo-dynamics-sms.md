---
title: Skicka aviseringar med Acrobat Sign för Microsoft Dynamics 365 och Marketo
description: Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att informera signeraren om att ett avtal är på väg
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: a1e0b30321760c5e84fb40ac083183b98170d1e1
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Skicka aviseringar med Acrobat Sign för Microsoft Dynamics 365 och Marketo

Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att informera signeraren om att ett avtal är på väg med Acrobat Sign, Acrobat Sign för Microsoft Dynamic, Marketo och Marketo Microsoft Dynamics Sync. Om du vill skicka aviseringar från Marketo måste du först köpa eller konfigurera en Marketo SMS-hanteringsfunktion. Genomgången använder [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), men det finns andra Marketo SMS-lösningar.

## Förutsättningar

1. Installera Marketo Microsoft Dynamics Sync.

   Information och det senaste plugin-programmet för Microsoft Dynamics Sync är tillgängligt [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installera Acrobat Sign för Microsoft Dynamics.

   Information om plugin-programmet finns tillgänglig [här.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Söka efter det anpassade objektet

När konfigurationerna för Marketo Microsoft Dynamics Sync och Acrobat Sign för Dynamics är klara visas två nya alternativ i Marketo Admin Terminal.

![Administration](assets/adminTerminal.png)

* Klicka **[!UICONTROL Synkronisering av Dynamics-enheter]**.

   Synkronisering måste inaktiveras innan anpassade entiteter synkroniseras. Klicka **[!UICONTROL Synkroniseringsschema]** om det är första gången. I annat fall klickar du på **[!UICONTROL Uppdatera schema]**.

   ![Uppdatera](assets/refreshSchema.png)

## Synkronisera det anpassade objektet

1. Leta på höger sida [!UICONTROL Lead], [!UICONTROL Kontakt]och [!UICONTROL Konto]-baserade anpassade objekt.

   * **[!UICONTROL Aktivera synkronisering]** för objekten under Lead om du vill utlösa när ett lead läggs till i ett avtal i Dynamics.

   * **[!UICONTROL Aktivera synkronisering]** för objekten under Kontakt om du vill utlösa när en kontakt läggs till i ett avtal i Dynamics.

   * **[!UICONTROL Aktivera synkronisering]** för objekten under Konto om du vill utlösa när ett konto läggs till i ett avtal i Dynamics.

   * **Aktivera synkronisering** för avtalsobjektet under önskad överordnad (lead, kontakt eller konto).

   ![Anpassade objekt](assets/enableSyncDynamics.png)

1. Välj de egenskaper du vill använda under Avtal i det nya fönstret.

   Aktivera rutorna under **[!UICONTROL Begränsning]** och **[!UICONTROL Utlösare]** för att exponera dem för era marknadsföringsaktiviteter.

   ![Anpassad synkronisering 1](assets/entitySync1.png)

   ![Anpassad synkronisering 2](assets/entitySync2.png)

1. Återaktivera synkningen efter att ha aktiverat synkning av de anpassade objekten.

   Gå tillbaka till [!UICONTROL Admin Terminal]och klicka sedan på **[!UICONTROL Microsoft Dynamics]** och klicka sedan på **[!UICONTROL Aktivera synkronisering]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Aktivera global](assets/enableGlobalDynamics.png)

## Skapa programmet

1. I [!UICONTROL Marknadsföringsaktiviteter]högerklicka **[!UICONTROL Marknadsföringsaktiviteter]** i det vänstra fältet väljer du **[!UICONTROL Ny kampanjmapp]** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen och välj **[!UICONTROL Nytt program]** och ge den ett namn.

   Låt allt annat vara standard och klicka sedan på **[!UICONTROL Skapa]**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

## Konfigurera [!DNL Twilio] SMS

Se först till att du har en aktiv [!DNL Twilio] och har köpt de SMS-funktioner du behöver.

Konfigurera Marketo - [!DNL Twilio] SMS-webhook kräver tre [!DNL Twilio] parametrar från ditt konto.

* Konto-SID
* Kontotoken
* Twilio-telefonnummer

Hämta parametrarna från ditt konto och öppna nu Marketo-instansen.

1. Klicka **[!UICONTROL Administratör]** uppe till höger.

   ![Administration](assets/adminTab.png)

1. Klicka **[!UICONTROL Webhooks]** och klicka sedan på **[!UICONTROL Ny webhook]**.

   ![Webhookar](assets/webhooks.png)

1. Ange ett **[!UICONTROL Webhooknamn]** och **[!UICONTROL Beskrivning]**.

1. Ange följande URL och var noga med att ersätta `ACCOUNT_SID` och `AUTH_TOKEN` med [!DNL Twilio] autentiseringsuppgifter.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Välj **[!UICONTROL POST]** som typ av begäran.

1. Ange följande **Mall** och se till att ersätta `MY_TWILIO_NUMBER` med [!DNL Twilio] telefonnummer och `YOUR_MESSAGE` med ett meddelande som du själv väljer.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Ange **[!UICONTROL Begär tokenkodning]** till *Formulär/URL*.

1. Ställ in svarstypen på *JSON* klicka sedan på **[!UICONTROL Spara]**.

## Ställ in utlösaren för smarta kampanjer

1. I avsnittet Marknadsföringsaktiviteter högerklickar du på det program du skapade och väljer sedan **[!UICONTROL Ny smart kampanj]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn och klicka sedan på **[!UICONTROL Skapa]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Det bör finnas flera utlösare som kan användas i mappen Microsoft.

1. Klicka och dra **[!UICONTROL Lades till i avtal]** till **[!UICONTROL Smart lista]** och lägg sedan till eventuella begränsningar för utlösaren.

   ![Lades till i avtal](assets/addedToAgreementDynamics.png)

## Ställ in smart kampanjflöde

1. Klicka på **[!UICONTROL Flöde]** -fliken på [!UICONTROL Smart Campaign].

   Sök efter och dra **Anropa webhook** flöda till arbetsytan och välj den webhook som du skapade i föregående avsnitt.

   ![Anropa webhook](assets/callWebhook.png)

1. Din SMS-meddelandekampanj för leads som läggs till i ett avtal har nu konfigurerats.
>[!TIP]
>
>Den här självstudiekursen är en del av kursen [Snabba upp säljcyklerna med Acrobat Sign för Microsoft Dynamics och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är tillgänglig gratis på Experience League!