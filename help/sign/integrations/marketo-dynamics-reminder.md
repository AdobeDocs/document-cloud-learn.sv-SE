---
title: Skicka påminnelser med Adobe Sign för Microsoft Dynamics 365 och Marketo
description: Lär dig hur du skickar en e-postpåminnelse när ett avtal förblir osignerat efter en viss tidsperiod
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Skicka påminnelser med Adobe Sign för Microsoft Dynamics 365 och Marketo

Lär dig hur du skickar en e-postpåminnelse när ett avtal förblir osignerat efter en viss tidsperiod. Den här integreringen använder Adobe Sign, Adobe Sign för Microsoft Dynamics, Marketo och Marketo Microsoft Dynamics Sync.

## Förutsättningar

1. Installera Marketo Microsoft Dynamics Sync.

   Information och det senaste plugin-programmet för Microsoft Dynamics Sync finns [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installera [Adobe Sign för Microsoft Dynamics](https://appsource.microsoft.com/sv-se/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Information om det här plugin-programmet finns [här.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Söka efter det anpassade objektet

När Marketo Microsoft Dynamics Sync- och Adobe Sign for Dynamics-konfigurationerna har slutförts visas två nya alternativ i Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

1. Klicka på **[!UICONTROL Synkronisera Dynamics-enheter]**.

   Synkronisering måste inaktiveras innan du synkroniserar anpassade entiteter. Klicka på **Synkronisera schema** om det är första gången. Annars klickar du på **Uppdatera schema**.

   ![Uppdatera](assets/refreshSchema.png)

## Synkronisera det anpassade objektet

1. På höger sida letar du reda på [!UICONTROL Lead], [!UICONTROL Kontakt] och [!UICONTROL Konto]-baserade anpassade objekt.

   * **Aktivera** Synkronisering för de objekt under  **** Leadif som du vill skicka en påminnelse om när en   lead inte har signerat något avtal i Dynamics.

   * **Aktivera** synkronisering för objekten under  **** Kontakt om du vill skicka en påminnelse när en   kontaktperson inte har signerat ett avtal i Dynamics.

   * **Aktivera** Synkronisera för objekten under  **** Konto om du vill skicka en påminnelse när ett   konto inte har signerat ett avtal i Dynamics.

   * **Aktivera** Synkronisera för avtalsobjektet under önskat  **[!UICONTROL överordnat]**  objekt ([!UICONTROL Lead],  [!UICONTROL Kontakt] eller  [!UICONTROL Konto]).

   ![Anpassade objekt](assets/enableSyncDynamics.png)

1. I det nya fönstret väljer du de egenskaper du vill ha under Avtal och aktiverar sedan rutorna under **Begränsning** och **Utlösare** för att visa dem för dina marknadsföringsaktiviteter.

   ![Anpassad synkronisering 1](assets/entitySync1.png)

   ![Anpassad synkronisering 2](assets/entitySync2.png)

1. Återaktivera synkroniseringen när synkronisering har aktiverats för de anpassade objekten.

   Gå tillbaka till Admin Terminal, klicka på **Microsoft Dynamics** och klicka sedan på **Aktivera synkronisering**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Aktivera global](assets/enableGlobalDynamics.png)

## Skapa program och token

1. Högerklicka på **Marknadsföringsaktiviteter** på vänster fält i avsnittet Marknadsföringsaktiviteter i Marketo.

   Välj **Ny kampanjmapp** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen, välj **Nytt program** och ge den ett namn.

   Lämna allt annat som standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

1. Klicka på **Mina token** och dra sedan **E-postskript** till arbetsytan.

   ![E-postskript](assets/emailScript.png)

1. Ge den ett namn och klicka sedan på **Klicka för att redigera**.

   ![Namn och redigera](assets/nameAndSave.png)

1. Expandera **[!UICONTROL Egna objekt]** till höger och expandera sedan objektet **[!UICONTROL Avtal]**.

   Sök och dra [!UICONTROL Namn], Avtalsstatus, Skickat på och Aktuell URL för signerare till arbetsytan.

1. Skriv ett Velocity-skript med dessa token för att visa avtals-URL:en för ett avtal som inte signeras under en vecka. Här är ett exempel som jämför aktuellt datum med Skickat den:

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. Klicka på **[!UICONTROL Spara]**.

## Skapa påminnelsen och lägg till personalisering

Exempel på personalisering är: namnet på undertecknaren, namnet på avtalet, en länk till avtalet osv.

1. Högerklicka på det program du skapade och klicka på **[!UICONTROL Ny lokal resurs]** och välj sedan **[!UICONTROL E-post]**.

   ![Ny e-post](assets/createNewEmail.png)

1. På den nya fliken anger du ett **[!UICONTROL namn]** och **[!UICONTROL Beskrivning]** för e-postmeddelandet och väljer en mall i mallväljaren.

   ![Mallväljare](assets/templatePicker.png)

1. Klicka på **[!UICONTROL Skapa]**.

1. Ange **[!UICONTROL Från namn]** och **[!UICONTROL Från adress]**.

   ![Påminnelsemeddelande](assets/reminderEmail.png)

1. Klicka på meddelandetexten för att aktivera redigeraren.

   Klicka på knappen **[!UICONTROL Infoga token]**, sök efter den anpassade avtals-URL-token som du skapade och klicka sedan på **[!UICONTROL Infoga]**. Slutför anpassningen av e-postmeddelandet och klicka på **[!UICONTROL Spara]**.

   ![Infoga token](assets/insertToken.png)

1. Förhandsgranska med en profil som har tilldelats ett avtal.

   Du bör se en länk till URL-adressen med avtalsnamnet som etikett.

   ![E-posta länk](assets/emailLink.png)

## Konfigurera filtret för smarta kampanjer

1. Högerklicka på det program du skapade och klicka sedan på **[!UICONTROL Ny smart kampanj]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn du väljer och klicka sedan på **[!UICONTROL Skapa]**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Sök efter, klicka och dra sedan **[!UICONTROL Har avtal]** till den smarta listan.

   ![Har avtal](assets/hasAgreementDynamics1.png)

   Fälten som du exponerade för utlösaren ska vara tillgängliga i **[!UICONTROL Lägg till begränsning]**.

1. Välj **[!UICONTROL Avtalsstatus]** och andra fält som du vill filtrera efter.

   För varje fält som läggs till definierar du de värden som ska filtreras efter. I det här fallet utlöses den endast när **[!UICONTROL avtalsstatus]** är *Skickat för signatur* och **[!UICONTROL Skickat den]** är *tidigare än en vecka*.

   ![Avtalsstatus](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Lägg till en unik identifierare till begränsningarna, t.ex. **Namn**, om du vill att kampanjen endast ska köras för vissa avtal.

1. Bekräfta kampanjens målgrupp och se vem som är berättigad på fliken Schema.

   ![Kvalificerare](assets/qualifiers.png)

## Ställ in smart kampanjflöde

Eftersom kampanjfiltret **Dagar till förfallodatum** användes, kan du använda en schemalagd upprepning för kampanjen.

1. Klicka på fliken **[!UICONTROL Flöde]** i [!UICONTROL Smart Campaign].

   Sök efter och dra flödet **Skicka e-post** till arbetsytan och välj påminnelsemeddelandet som du skapade i föregående avsnitt.

   ![Skicka e-post](assets/sendEmail.png)

1. Klicka på fliken **[!UICONTROL Schema]** i Smart Campaign. Se till att kampanjflödet begränsas till att endast köras en gång per person i **inställningarna för Smart Campaign**. Klicka sedan på fliken **Schemalägg upprepning**.

   ![Fliken Schema](assets/scheduleTab.png)

1. Ställ in **Schedule** på _Daily_. Välj startdag och slutdatum för kampanjen om det behövs.

   ![Schemainställningar](assets/scheduleSettings.png)

>[!TIP]
>
>Den här självstudiekursen ingår i kursen [Snabba upp säljcyklerna med Adobe Sign för Microsoft Dynamics och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är kostnadsfri på Experience League!