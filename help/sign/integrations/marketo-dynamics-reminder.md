---
title: Skicka påminnelser med Acrobat Sign för Microsoft Dynamics 365 och Marketo
description: Lär dig hur du skickar en e-postpåminnelse när ett avtal förblir osignerat efter en viss tid
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Skicka påminnelser med Acrobat Sign för Microsoft Dynamics 365 och Marketo

Lär dig hur du skickar en e-postpåminnelse när ett avtal förblir osignerat efter en viss tid. Den här integreringen använder Acrobat Sign, Acrobat Sign för Microsoft Dynamics, Marketo och Marketo Microsoft Dynamics Sync.

## Förutsättningar

1. Installera Marketo Microsoft Dynamics Sync.

   Information och det senaste plugin-programmet för Microsoft Dynamics Sync är tillgängligt [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installera [Acrobat Sign för Microsoft Dynamics](https://appsource.microsoft.com/sv-se/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Information om plugin-programmet finns tillgänglig [här.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Söka efter det anpassade objektet

När konfigurationerna för Marketo Microsoft Dynamics Sync och Acrobat Sign för Dynamics är klara visas två nya alternativ i Marketo Admin Terminal.

![Admin](assets/adminTerminal.png)

1. Klicka **[!UICONTROL Synkronisering av Dynamics-enheter]**.

   Synkronisering måste inaktiveras innan anpassade entiteter synkroniseras. Klicka **Synkroniseringsschema** om det är första gången. I annat fall klickar du på **Uppdatera schema**.

   ![Uppdatera](assets/refreshSchema.png)

## Synkronisera det anpassade objektet

1. Leta på höger sida [!UICONTROL Lead], [!UICONTROL Kontakt]och [!UICONTROL Konto]-baserade anpassade objekt.

   * **Aktivera synkronisering** för objekt under **[!UICONTROL Lead]** om du vill skicka en påminnelse när en [!UICONTROL Lead] har inte signerat ett avtal i Dynamics.

   * **Aktivera synkronisering** för objekt under **[!UICONTROL Kontakt]** om du vill skicka en påminnelse när en [!UICONTROL Kontakt] har inte signerat ett avtal i Dynamics.

   * **Aktivera synkronisering** för objekt under **[!UICONTROL Konto]** om du vill skicka en påminnelse när en [!UICONTROL Konto] har inte signerat ett avtal i Dynamics.

   * **Aktivera synkronisering** för avtalsobjektet under önskad **[!UICONTROL Överordnad]** ([!UICONTROL Lead], [!UICONTROL Kontakt]eller [!UICONTROL Konto]).

   ![Anpassade objekt](assets/enableSyncDynamics.png)

1. I det nya fönstret väljer du de egenskaper du vill använda under Avtal och aktiverar sedan rutorna under **Begränsning** och **Utlösare** för att exponera dem för era marknadsföringsaktiviteter.

   ![Anpassad synkronisering 1](assets/entitySync1.png)

   ![Anpassad synkronisering 2](assets/entitySync2.png)

1. Återaktivera synkningen efter att ha aktiverat synkning av de anpassade objekten.

   Gå tillbaka till Admin Terminal, klicka på **Microsoft Dynamics** och klicka sedan på **Aktivera synkronisering**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Aktivera global](assets/enableGlobalDynamics.png)

## Skapa programmet och token

1. I avsnittet Marknadsföringsaktiviteter i Marketo högerklickar du på **Marknadsföringsaktiviteter** i det vänstra fältet.

   Välj **Ny kampanjmapp** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen och välj **Nytt program** och ge den ett namn.

   Låt allt annat vara standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

1. Klicka på **Mina token** och dra sedan **E-postskript** till arbetsytan.

   ![E-postskript](assets/emailScript.png)

1. Ge den ett namn och klicka sedan på **Klicka för att redigera**.

   ![Namnge och redigera](assets/nameAndSave.png)

1. Expandera **[!UICONTROL Egna objekt]** till höger och sedan utöka **[!UICONTROL Avtal]** objekt.

   Söka och dra [!UICONTROL Namn], Avtalsstatus, Skickat och Aktuell signerar-URL på arbetsytan.

1. Skriv ett hastighetsskript med dessa token för att visa avtals-URL:en för ett avtal som förblir osignerat i en vecka. Här är ett exempel som jämför dagens datum med Skickat den:

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

Exempel på personalisering är: namnet på signeraren, namnet på avtalet, en länk till avtalet osv.

1. Högerklicka på programmet du skapade och klicka på **[!UICONTROL Ny lokal resurs]** och välj sedan **[!UICONTROL E-post]**.

   ![Ny e-postadress](assets/createNewEmail.png)

1. Ange en **[!UICONTROL Namn]** och **[!UICONTROL Beskrivning]** för e-postmeddelandet och välj en mall i mallväljaren.

   ![Mallväljare](assets/templatePicker.png)

1. Klicka på **[!UICONTROL Skapa]**.

1. Ange **[!UICONTROL Från namn]** och **[!UICONTROL Från adress]**.

   ![Påminnelsemeddelande](assets/reminderEmail.png)

1. Klicka på meddelandetexten för att aktivera redigeraren.

   Klicka på **[!UICONTROL Infoga token]** hittar du den anpassade avtals-URL-token som du skapade och klickar sedan på **[!UICONTROL Infoga]**. Slutför anpassningen av e-postmeddelandet och klicka på **[!UICONTROL Spara]**.

   ![Infoga token](assets/insertToken.png)

1. Förhandsgranska med en profil som har tilldelats ett avtal.

   Du bör se en länk till URL:en med avtalsnamnet som etikett.

   ![E-posta länk](assets/emailLink.png)

## Ställ in filtret Smart Campaign

1. Högerklicka på programmet du skapade och klicka sedan på **[!UICONTROL Ny smart kampanj]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn du väljer och klicka sedan på **[!UICONTROL Skapa]**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Sök efter och klicka och dra **[!UICONTROL Har avtal]** till den smarta listan.

   ![Har avtal](assets/hasAgreementDynamics1.png)

   Fälten som du exponerade för utlösaren ska vara tillgängliga i **[!UICONTROL Lägg till begränsning]**.

1. Välj **[!UICONTROL Avtalsstatus]** och andra fält som du vill filtrera efter.

   För varje fält som läggs till anger du de värden som ska filtreras efter. I detta fall utlöses den endast när **[!UICONTROL Avtalsstatus]** är *Skickat för signering* och **[!UICONTROL Skickat den]** är *senaste före 1 vecka*.

   ![Avtalsstatus](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Lägg till en unik identifierare till begränsningarna, till exempel **Namn**, om du vill att kampanjen endast ska köras för vissa avtal.

1. Bekräfta kampanjgruppen och se vem som kvalificerar sig på fliken Schema .

   ![Kvalificerare](assets/qualifiers.png)

## Ställ in smart kampanjflöde

Eftersom kampanjfiltret **Dagar tills förfallodatum** används kan du använda en schemalagd upprepning för kampanjen.

1. Klicka på **[!UICONTROL Flöde]** -fliken på [!UICONTROL Smart Campaign].

   Sök efter och dra **Skicka e-post** flöda till arbetsytan och välj påminnelsemeddelandet som du skapade i föregående avsnitt.

   ![Skicka e-post](assets/sendEmail.png)

1. Klicka på **[!UICONTROL Schemalägg]** i Smart Campaign. Se till att kampanjflödet begränsas till att köras endast en gång per person i **Inställningar för smart kampanj**. Klicka sedan på **Schemalägg upprepning** -fliken.

   ![Fliken Schemalägg](assets/scheduleTab.png)

1. Ange **Schemalägg** till _Dagligen_. Välj en startdag, starttid och slutdatum för kampanjen om det behövs.

   ![Schemainställningar](assets/scheduleSettings.png)

>[!TIP]
>
>Den här självstudiekursen är en del av kursen [Snabba upp säljcyklerna med Acrobat Sign för Microsoft Dynamics och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är tillgänglig gratis på Experience League!