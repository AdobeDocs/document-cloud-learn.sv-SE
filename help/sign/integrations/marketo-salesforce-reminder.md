---
title: Skicka påminnelser med hjälp av Konfigurationshandboken för Adobe Sign för Salesforce och Marketo
description: Lär dig hur du skickar en e-postpåminnelse från Marketo när ett avtal förblir osignerat efter en viss tidsperiod
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Skicka påminnelser med hjälp av Konfigurationshandboken för Adobe Sign för Salesforce och Marketo

Lär dig hur du skickar en e-postpåminnelse från Marketo när ett avtal förblir osignerat efter en viss tidsperiod. Den här integreringen använder Adobe Sign, Adobe Sign för Salesforce, Marketo och Marketo och Salesforce Sync.

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

## Synkronisera det anpassade objektet

Till höger finns mer information i Lead-, Kontakt- och Kontobaserade anpassade objekt.

**Aktivera** Synkronisering för objekten under Lead om du vill skicka en påminnelse när en lead inte har signerat något avtal i Salesforce.

**Aktivera** Synkronisera för objekten under Kontakt om du vill skicka en påminnelse när en kontakt inte har signerat något avtal i Salesforce.

**Aktivera** Synkronisera för objekten under Konto om du vill skicka en påminnelse när ett konto inte har signerat något avtal i Salesforce.

1. **Aktivera** Synkronisera för  **** avtalsobjektet som visas under önskad överordnad (lead, kontakt eller konto). Gör detta för andra anpassade objekt som du vill synkronisera.

   ![Avtalsobjekt](assets/agreementObject.png)

1. Följande resurser visar hur du **aktiverar synkronisering**.

   ![Anpassad synkronisering 1](assets/customObjectSync1.png)

   ![Anpassad synkronisering 2](assets/customObjectSync2.png)

## Visa anpassade objektfält för utlösare

1. När den globala synkroniseringen är inaktiverad väljer du det anpassade avtalsobjekt som du aktiverade synkronisering för och sedan **Redigera synliga fält**.

1. Markera fältet Avtalsnamn i utlösarkolumnen för att visa det för dina utlösare av kampanjåtgärder. Markera andra fält som du vill filtrera efter och **Spara**.

   ![Redigera synliga fält 1](assets/editVisible1.png)

   ![Redigera synliga fält 2](assets/editVisible2.png)

1. När du har aktiverat synkronisering för de anpassade objekten och visar utlösarvärdena måste du komma ihåg att återaktivera synkroniseringen:

   ![Aktivera global](assets/enableGlobal.png)

## Skapa program och token

1. I avsnittet Marknadsföringsaktiviteter i Marketo högerklickar du på **Marknadsföringsaktiviteter** till vänster, väljer **Ny kampanjmapp** och ger den ett namn.

   ![Ny mapp](assets/newFolder.png)

1. Högerklicka på den skapade mappen, välj **Nytt program** och ge den ett namn. Lämna allt annat som standard och klicka sedan på **Skapa**.

   ![Nytt program 1](assets/newProgram1.png)

   ![Nytt program 2](assets/newProgram2.png)

1. Klicka på **Mina token** och dra sedan **E-postskript** till arbetsytan.

   ![E-postskript](assets/emailScript.png)

1. Ge den ett namn och klicka sedan på **Klicka för att redigera**.

   ![Namn och redigera](assets/nameAndSave.png)

1. Expandera **Egna objekt** till höger och expandera sedan objektet **Avtal**. Sök och dra avtalsnamn, avtalsstatus, datum för signering och signerings-URL till arbetsytan.

1. Skriv ett Velocity-skript med dessa token för att visa avtals-URL:en för ett avtal som inte signeras under en vecka. Här följer ett exempel som jämför aktuellt datum med Skickat den:

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

## Skapa påminnelsen och lägg till personalisering

Exempel på personalisering är: namnet på undertecknaren, namnet på avtalet, en länk till avtalet osv.

1. Högerklicka på det program du skapade och klicka på **Ny lokal resurs** och välj sedan **E-post**.

   ![Ny e-post](assets/createNewEmail.png)

1. På den nya fliken anger du ett **namn** och **Beskrivning** för e-postmeddelandet och väljer en mall i mallväljaren. Klicka på **Skapa**.

   ![Mallväljare](assets/templatePicker.png)

1. Ange **Från namn** och **Från adress**.

   ![Påminnelsemeddelande](assets/reminderEmail.png)

1. Klicka på meddelandetexten för att aktivera redigeraren. Klicka på knappen **Infoga token**, sök efter den anpassade avtals-URL-token som du skapade och klicka sedan på **Infoga**. Slutför anpassningen av e-postmeddelandet och klicka på **Spara**.

   ![Infoga token](assets/insertToken.png)

1. Förhandsgranska med en profil som har tilldelats ett avtal. Du bör se en länk till URL-adressen med avtalsnamnet som etikett.

   ![E-posta länk](assets/emailLink.png)

## Konfigurera filtret för smarta kampanjer

1. Högerklicka på det program du skapade och klicka sedan på **Ny smart kampanj**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Ge den ett namn du väljer och klicka sedan på **Skapa**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Sök efter, klicka och dra sedan **Har avtal** till den smarta listan.

   ![Har avtal](assets/hasAgreement.png)

1. Fälten som du exponerade för utlösaren ska nu vara tillgängliga i **Lägg till begränsning**. Välj **Avtalsstatus** och andra fält som du vill filtrera efter. För varje fält som läggs till definierar du de värden som ska filtreras efter. I det här fallet utlöses den endast när **avtalsstatus** är Skickat för signatur och **Skickat** är tidigare än 7 dagar.

   ![Avtalsstatus](assets/agreementStatus.png)

   >[!NOTE]
   >
   > Gör en unik identifierare för begränsningarna, t.ex. **Avtalsnamn**, om du vill att kampanjen endast ska köras för vissa avtal.

1. Bekräfta kampanjens målgrupp och se vem som är berättigad på fliken Schema.

   ![Kvalificerare](assets/qualifiers.png)

## Ställ in smart kampanjflöde

Eftersom kampanjfiltret **Dagar utan signatur** användes, kan du använda en schemalagd upprepning för kampanjen.

1. Klicka på fliken **Flöde** i Smart Campaign. Sök efter och dra flödet **Skicka e-post** till arbetsytan och välj påminnelsemeddelandet som du skapade i föregående avsnitt.

   ![Skicka e-post](assets/sendEmail.png)

1. Klicka på fliken **Schema** i Smart Campaign. Se till att kampanjflödet begränsas till att endast köras en gång per person i **inställningarna för Smart Campaign**. Klicka sedan på fliken **Schemalägg upprepning**.

   ![Fliken Schema](assets/scheduleTab.png)

1. Ställ in **Schedule** på Daily, välj startdag och -tid och ett slutdatum för kampanjen om det behövs.

   ![Schemainställningar](assets/scheduleSettings.png)

>[!TIP]
>
>Den här självstudiekursen ingår i kursen [Snabba upp säljcyklerna med Adobe Sign för Salesforce och Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) som är kostnadsfri på Experience League!
