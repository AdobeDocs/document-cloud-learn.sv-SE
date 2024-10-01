---
title: Skicka påminnelser med Acrobat Sign för Microsoft Dynamics 365 och Marketo
description: Lär dig skicka en e-postpåminnelse när ett avtal förblir osignerat efter en tid
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Skicka påminnelser med Acrobat Sign för Microsoft Dynamics 365 och Marketo

Lär dig skicka en e-postpåminnelse när ett avtal förblir osignerat efter en tid. Denna integrering använder Acrobat Sign, Acrobat Sign för Microsoft Dynamics, Marketo och Marketo Microsoft Dynamics Sync.

## Förutsättningar

1. Installera Marketo Microsoft Dynamics Sync.

   Information och det senaste plugin-programmet för Microsoft Dynamics Sync finns [här.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Installera [Acrobat Sign för Microsoft Dynamics](https://appsource.microsoft.com/sv-se/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Information om det här plugin-programmet finns [här.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Hitta det anpassade objektet

När konfigurationerna för Marketo Microsoft Dynamics Sync och Acrobat Sign för Dynamics är klara visas två nya alternativ i Marketo Admin Terminal.

![Administratör](assets/adminTerminal.png)

1. Klicka på **[!UICONTROL Dynamics Entities Sync]**.

   Synkronisering måste inaktiveras innan anpassade entiteter synkroniseras. Klicka på **Synkroniseringsschema** om det är första gången du gör det. Klicka annars på **Uppdatera schema**.

   ![Uppdatera](assets/refreshSchema.png)

## Synkronisera det anpassade objektet

1. Leta reda på [!UICONTROL Lead], [!UICONTROL Kontakt] och [!UICONTROL Konto]-baserade anpassade objekt på höger sida.

   * **Aktivera synkronisering** för objekten under **[!UICONTROL Lead]** om du vill skicka en påminnelse när en [!UICONTROL lead] inte har signerat ett avtal i Dynamics.

   * **Aktivera synkronisering** för objekt under **[!UICONTROL Kontakt]** om du vill skicka en påminnelse när en [!UICONTROL kontakt] inte har signerat ett avtal i Dynamics.

   * **Aktivera synkronisering** för objekten under **[!UICONTROL Konto]** om du vill skicka en påminnelse när ett [!UICONTROL konto] inte har signerat ett avtal i Dynamics.

   * **Aktivera synkronisering** för avtalsobjektet under önskad **[!UICONTROL överordnad]** ([!UICONTROL lead], [!UICONTROL kontakt] eller [!UICONTROL konto]).

   ![Anpassade objekt](assets/enableSyncDynamics.png)

1. Markera de egenskaper du vill använda under Avtal i det nya fönstret och aktivera sedan rutorna under **Begränsning** och **Utlösare** för att visa dem för dina marknadsföringsaktiviteter.

   ![Anpassad synkronisering 1](assets/entitySync1.png)

   ![Anpassad synkronisering 2](assets/entitySync2.png)

1. Återaktivera synkroniseringen när du har aktiverat synkronisering med de anpassade objekten.

   Gå tillbaka till Admin Terminal, klicka på **Microsoft Dynamics** och klicka sedan på **Aktivera synkronisering**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Aktivera global](assets/enableGlobalDynamics.png)

## Skapa programmet och token

1. Högerklicka på **Marknadsföringsaktiviteter** i det vänstra fältet i avsnittet Marknadsföringsaktiviteter i Marketo.

   Välj **Ny kampanjmapp** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på mappen som skapats, välj **Nytt program** och ge den ett namn.

   Låt allt annat vara standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

1. Klicka på **Mina token** och dra sedan **e-postskriptet** över till arbetsytan.

   ![E-postskript](assets/emailScript.png)

1. Ge den ett namn och klicka sedan på **Klicka för att redigera**.

   ![Namnge och redigera](assets/nameAndSave.png)

1. Expandera **[!UICONTROL Anpassade objekt]** till höger och expandera sedan objektet **[!UICONTROL Avtal]**.

   Hitta och dra [!UICONTROL Namn], Avtalsstatus, Skickat den och Aktuell signerings-URL till arbetsytan.

1. Skriv ett hastighetsskript med dessa token för att visa avtals-URL:en för ett avtal som förblir osignerat i en vecka. Här är ett exempel som jämför det aktuella datumet som ska skickas den:

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

## Skapa påminnelsen och lägg till anpassning

Exempel på anpassning är: signerarens namn, avtalsnamnet, en länk till avtalet osv.

1. Högerklicka på programmet du skapade och klicka på **[!UICONTROL Ny lokal resurs]**. Välj sedan **[!UICONTROL E-post]**.

   ![Ny e-postadress](assets/createNewEmail.png)

1. Ange ett **[!UICONTROL namn]** och en **[!UICONTROL beskrivning]** för e-postmeddelandet på den nya fliken och välj en mall i mallväljaren.

   ![Mallväljare](assets/templatePicker.png)

1. Klicka på **[!UICONTROL Skapa]**.

1. Ange **[!UICONTROL Från namn]** och **[!UICONTROL Från adress]**.

   ![Påminnelsemeddelande](assets/reminderEmail.png)

1. Klicka på meddelandetexten för att aktivera redigeraren.

   Klicka på knappen **[!UICONTROL Infoga token]**, leta reda på den anpassade token för avtals-URL som du skapade och klicka sedan på **[!UICONTROL Infoga]**. Slutför anpassningen av e-postadressen och klicka på **[!UICONTROL Spara]**.

   ![Infoga token](assets/insertToken.png)

1. Förhandsgranska med en profil som har tilldelats ett avtal.

   Du bör se en länk till URL:en med avtalsnamnet som etikett.

   ![E-postlänk](assets/emailLink.png)

## Ställ in filtret Smart Campaign

1. Högerklicka på programmet du skapade och klicka sedan på **[!UICONTROL Ny smart kampanj]**.

   ![Smart kampanj 1](assets/smartCampaign1.png)

1. Ge den ett namn du väljer och klicka sedan på **[!UICONTROL Skapa]**.

   ![Smart kampanj 2](assets/smartCampaign2.png)

1. Sök efter och klicka och dra **[!UICONTROL Har avtal]** till den smarta listan.

   ![Har avtal](assets/hasAgreementDynamics1.png)

   Fälten som du exponerade för utlösaren ska vara tillgängliga i **[!UICONTROL Lägg till begränsning]**.

1. Välj **[!UICONTROL Avtalsstatus]** och eventuella andra fält som du vill filtrera efter.

   För varje fält som läggs till anger du de värden som du vill filtrera efter. I detta fall utlöses det bara när **[!UICONTROL Avtalsstatus]** är *Skickat för signatur* och **[!UICONTROL Skickat den]** är *förflutet före 1 vecka*.

   ![Avtalsstatus](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Lägg till en unik identifierare i begränsningarna, t.ex. **Namn**, om du vill att den här kampanjen endast ska köras för vissa avtal.

1. Bekräfta kampanjgruppen och se vem som kvalificerar sig på fliken Schema.

   ![Kvalificerare](assets/qualifiers.png)

## Ställ in flödet Smart Campaign

Eftersom kampanjfiltret **Dagar tills förfallodatum** användes kan du använda en schemalagd upprepning för kampanjen.

1. Klicka på fliken **[!UICONTROL Flöde]** i [!UICONTROL Smart kampanj].

   Sök efter och dra flödet **Skicka e-post** till arbetsytan och välj e-postpåminnelsen som du skapade i föregående avsnitt.

   ![Skicka e-post](assets/sendEmail.png)

1. Klicka på fliken **[!UICONTROL Schemalägg]** i den smarta kampanjen. Se till att kampanjflödet begränsas till att endast köras en gång per person i inställningarna för **Smart kampanj**. Klicka sedan på fliken **Schemalägg upprepning**.

   ![Fliken Schemalägg](assets/scheduleTab.png)

1. Ställ in **Schema** på _Dagligen_. Välj en startdag, starttid och slutdatum för kampanjen om det behövs.

   ![Schemainställningar](assets/scheduleSettings.png)
