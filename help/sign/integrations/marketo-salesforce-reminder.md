---
title: Skicka påminnelser med konfigurationshandboken för Acrobat Sign för Salesforce och Marketo
description: Lär dig hur du skickar en e-postpåminnelse från Marketo när ett avtal förblir osignerat efter en tidsperiod
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Skicka påminnelser med konfigurationshandboken för Acrobat Sign för Salesforce och Marketo

Lär dig skicka en e-postpåminnelse från Marketo när ett avtal fortfarande är osignerat efter en tid. Den här integreringen använder Acrobat Sign, Acrobat Sign för Salesforce, Marketo samt Marketo- och Salesforce-synkronisering.

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

## Synkronisera det anpassade objektet

Till höger finns information i Lead-, Contact- och Account-based custom objects.

**Aktivera synkronisering** för objekten under Lead om du vill skicka en påminnelse när en lead inte har signerat ett avtal i Salesforce.

**Aktivera synkronisering** för objekten under Kontakt om du vill skicka en påminnelse när en kontakt inte har signerat ett avtal i Salesforce.

**Aktivera synkronisering** för objekten under Konto om du vill skicka en påminnelse när ett konto inte har signerat ett avtal i Salesforce.

1. **Aktivera synkronisering** för **Avtal** objektet som visas under den önskade mallen (lead, kontakt eller konto). Gör detta för alla andra anpassade objekt som du vill synkronisera.

   ![Avtalsobjekt](assets/agreementObject.png)

1. Följande mediefiler visar hur du **Aktivera synkronisering**.

   ![Anpassad synkronisering 1](assets/customObjectSync1.png)

   ![Anpassad synkronisering 2](assets/customObjectSync2.png)

## Visa de anpassade objektfälten för utlösare

1. När Global Sync är inaktiverat väljer du objektet Anpassat avtal som du aktiverade synkronisering för och sedan **Redigera synliga fält**.

1. Markera fältet Avtalsnamn i utlösarkolumnen för att visa det för kampanjutlösarna. Markera eventuella andra fält som du vill filtrera efter och **Spara**.

   ![Redigera synliga fält 1](assets/editVisible1.png)

   ![Redigera synliga fält 2](assets/editVisible2.png)

1. När du är klar med att aktivera synkronisering för de anpassade objekten och visa utlösarvärdena, måste du aktivera synkroniseringen igen:

   ![Aktivera global](assets/enableGlobal.png)

## Skapa programmet och token

1. I avsnittet Marknadsföringsaktiviteter i Marketo högerklickar du på **Marknadsföringsaktiviteter** i det vänstra fältet väljer du **Ny kampanjmapp** och ge den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen och välj **Nytt program** och ge den ett namn. Låt allt annat vara standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

1. Klicka på **Mina tokens** och dra sedan  **E-postskript** över till arbetsytan.

   ![E-postskript](assets/emailScript.png)

1. Ge den ett namn och klicka sedan på **Klicka för att redigera**.

   ![Namnge och redigera](assets/nameAndSave.png)

1. Expandera **Anpassade objekt** till höger och sedan utöka **Avtal** objekt. Hitta och dra Avtalsnamn, Avtalsstatus, Signeringsdatum och Signerings-URL till arbetsytan.

1. Skriv ett hastighetsskript med dessa token för att visa avtals-URL:en för ett avtal som förblir osignerat i en vecka. Här är ett exempel som jämför dagens datum till Skickat den:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
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

1. Klicka på **Spara**.

## Skapa påminnelsen och lägg till anpassning

Exempel på anpassning är: signerarens namn, avtalsnamnet, en länk till avtalet osv.

1. Högerklicka på programmet du skapade och klicka på **Ny lokal resurs** och välj sedan **Mejl**.

   ![Ny e-postadress](assets/createNewEmail.png)

1. Ange ett värde på den nya fliken **Namn** och **Beskrivning** för e-postmeddelandet och välj en mall från mallväljaren. Klicka på **Skapa**.

   ![Mallväljare](assets/templatePicker.png)

1. Ange **Från namn** och **Från adress**.

   ![E-postpåminnelse](assets/reminderEmail.png)

1. Klicka på meddelandetexten för att aktivera redigeraren. Klicka på **Infoga token** hittar du den anpassade token för avtals-URL som du skapade och klickar sedan på **Infoga**. Slutför anpassningen av e-postadressen och klicka på **Spara**.

   ![Infoga token](assets/insertToken.png)

1. Förhandsgranska med en profil som har tilldelats ett avtal. Du bör se en länk till URL:en med avtalsnamnet som etikett.

   ![E-postlänk](assets/emailLink.png)

## Ställ in filtret Smart Campaign

1. Högerklicka på programmet du skapade och klicka sedan på **Ny smart kampanj**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn du väljer och klicka sedan på **Skapa**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Sök efter och klicka och dra **Har avtal** till den smarta listan.

   ![Har avtal](assets/hasAgreement.png)

1. Fälten som du exponerade för utlösaren ska nu vara tillgängliga i **Lägg till begränsning**. Välj **Avtalsstatus** och alla andra fält som du vill filtrera efter. För varje fält som läggs till anger du de värden som du vill filtrera efter. I så fall utlöses den först när **Avtalsstatus** har skickats för signatur och **Skickat den** har passerat innan 7 dagar.

   ![Avtalsstatus](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d en unik identifierare för begränsningarna, t.ex. **Avtalsnamn**, om du vill att den här kampanjen endast ska köras för vissa avtal.

1. Bekräfta kampanjgruppen och se vem som kvalificerar sig på fliken Schema.

   ![Kvalificerare](assets/qualifiers.png)

## Ställ in flödet Smart Campaign

Eftersom kampanjfiltret **Osignerade dagar** används kan du använda en schemalagd upprepning för kampanjen.

1. Klicka på **Flöde** i Smart Campaign. Sök efter och dra **Skicka mejl** flöda till arbetsytan och välj e-postpåminnelsen som du skapade i föregående avsnitt.

   ![Skicka mejl](assets/sendEmail.png)

1. Klicka på **Schemalägg** i Smart Campaign. Se till att kampanjflödet är begränsat till att endast köras en gång per person i **Inställningar för smart kampanj**. Klicka sedan på **Schemalägg upprepning** -fliken.

   ![Fliken Schemalägg](assets/scheduleTab.png)

1. Ange **Schemalägg** till Dagligen, välj en startdag och starttid och ett slutdatum för kampanjen om det behövs.

   ![Schemainställningar](assets/scheduleSettings.png)

>[!TIP]
>
>Den här självstudiekursen är en del av kursen [Påskynda försäljningscyklerna med Acrobat Sign för Salesforce och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är tillgänglig gratis på Experience League!
