---
title: Skicka meddelanden med Adobe Sign för Microsoft Dynamics 365 och Marketo
description: Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande för att tala om för signeraren att ett avtal är på väg
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Skicka meddelanden med Adobe Sign för Microsoft Dynamics 365 och Marketo

Lär dig hur du skickar ett textmeddelande, ett e-postmeddelande eller ett push-meddelande så att signeraren vet att ett avtal är på väg med Adobe Sign, Adobe Sign för Microsoft Dynamic, Marketo och Marketo Microsoft Dynamics Sync. Om du vill skicka meddelanden från Marketo måste du först köpa eller konfigurera en SMS-hanteringsfunktion från Marketo. Vid genomgången används [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), men andra Marketo SMS-lösningar finns tillgängliga.

## Förutsättningar

1. Installera Marketo Microsoft Dynamics Sync.

   Information och det senaste plugin-programmet för Microsoft Dynamics Sync finns [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installera Adobe Sign för Microsoft Dynamics.

   Information om det här plugin-programmet finns [här.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Söka efter det anpassade objektet

När Marketo Microsoft Dynamics Sync- och Adobe Sign for Dynamics-konfigurationerna har slutförts visas två nya alternativ i Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

* Klicka på **[!UICONTROL Synkronisera Dynamics-enheter]**.

   Synkronisering måste inaktiveras innan du synkroniserar anpassade entiteter. Klicka på **[!UICONTROL Synkronisera schema]** om det är första gången. Annars klickar du på **[!UICONTROL Uppdatera schema]**.

   ![Uppdatera](assets/refreshSchema.png)

## Synkronisera det anpassade objektet

1. På höger sida letar du reda på [!UICONTROL Lead], [!UICONTROL Kontakt] och [!UICONTROL Konto]-baserade anpassade objekt.

   * **[!UICONTROL Aktivera]** Synkronisering för objekten under Lead om du vill utlösa när en lead läggs till i ett avtal i Dynamics.

   * **[!UICONTROL Aktivera]** Synkronisering för objekten under Kontakt om du vill utlösa när en kontakt läggs till i ett avtal i Dynamics.

   * **[!UICONTROL Aktivera]** Synkronisera för objekten under Konto om du vill utlösa när ett konto läggs till i ett avtal i Dynamics.

   * **Aktivera** synkronisering för avtalsobjektet under den önskade överordnade (lead, kontakt eller konto).

   ![Anpassade objekt](assets/enableSyncDynamics.png)

1. I det nya fönstret väljer du de egenskaper du vill ha under Avtal.

   Aktivera rutorna under **[!UICONTROL Begränsning]** och **[!UICONTROL Utlösare]** för att visa dem för dina marknadsföringsaktiviteter.

   ![Anpassad synkronisering 1](assets/entitySync1.png)

   ![Anpassad synkronisering 2](assets/entitySync2.png)

1. Återaktivera synkroniseringen när synkronisering har aktiverats för de anpassade objekten.

   Gå tillbaka till [!UICONTROL Admin Terminal], klicka på **[!UICONTROL Microsoft Dynamics]** och klicka sedan på **[!UICONTROL Aktivera synkronisering]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Aktivera global](assets/enableGlobalDynamics.png)

## Skapa programmet

1. I [!UICONTROL Marknadsföringsaktiviteter] högerklickar du på **[!UICONTROL Marknadsföringsaktiviteter]** till vänster, väljer **[!UICONTROL Ny kampanjmapp]** och ger den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen, välj **[!UICONTROL Nytt program]** och ge den ett namn.

   Lämna allt annat som standard och klicka sedan på **[!UICONTROL Skapa]**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

## Konfigurera [!DNL Twilio] SMS

Kontrollera först att du har ett aktivt [!DNL Twilio]-konto och har köpt de SMS-funktioner du behöver.

För att konfigurera Marketo - [!DNL Twilio] SMS-webkroken krävs tre [!DNL Twilio]-parametrar från ditt konto.

* Konto-SID
* Kontotoken
* Twilio-telefonnummer

Hämta de här parametrarna från ditt konto och öppna nu din Marketo-instans.

1. Klicka på **[!UICONTROL Admin]** överst till höger.

   ![Administratör](assets/adminTab.png)

1. Klicka på **[!UICONTROL Webhooks]** och klicka sedan på **[!UICONTROL Ny webkrok]**.

   ![Webhookar](assets/webhooks.png)

1. Ange ett **[!UICONTROL Webkroknamn]** och **[!UICONTROL Beskrivning]**.

1. Ange följande URL och se till att du ersätter `ACCOUNT_SID` och `AUTH_TOKEN` med dina [!DNL Twilio]-inloggningsuppgifter.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Välj **[!UICONTROL POST]** som frågetyp.

1. Ange följande **Mall** och se till att ersätta `MY_TWILIO_NUMBER` med ditt [!DNL Twilio] telefonnummer och `YOUR_MESSAGE` med ett meddelande som du väljer.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Ange **[!UICONTROL Begär tokenkodning]** till *Form/URL*.

1. Ställ in svarstypen på *JSON* och klicka sedan på **[!UICONTROL Spara]**.

## Konfigurera Smart Campaign Trigger

1. I avsnittet Marknadsföringsaktiviteter högerklickar du på det program du skapade och väljer sedan **[!UICONTROL Ny smart kampanj]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn och klicka sedan på **[!UICONTROL Skapa]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Du bör se flera utlösare som är tillgängliga för användning i mappen Microsoft.

1. Klicka och dra **[!UICONTROL Lägg till i avtal]** till **[!UICONTROL Smart lista]** och lägg sedan till eventuella begränsningar som du vill ha i utlösaren.

   ![Tillagt i avtal](assets/addedToAgreementDynamics.png)

## Ställ in smart kampanjflöde

1. Klicka på fliken **[!UICONTROL Flöde]** i [!UICONTROL Smart Campaign].

   Sök efter och dra **Anropa Webkrok**-flödet till arbetsytan och välj den webkrok du skapade i föregående avsnitt.

   ![Ring Webkrok](assets/callWebhook.png)

1. Din SMS-meddelandekampanj för leads som läggs till i ett avtal har nu konfigurerats.
>[!TIP]
>
>Den här självstudiekursen ingår i kursen [Snabba upp säljcyklerna med Adobe Sign för Microsoft Dynamics och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är kostnadsfri på Experience League!