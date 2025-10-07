---
title: Acrobat Sign-texttaggar
description: Lär dig hur du skapar Acrobat Sign-formulärfält med texttaggar
feature: Workflow, Sign
role: User, Admin
level: Experienced
jira: KT-6059
thumbnail: KT-6402.jpg
exl-id: 3a54925d-b713-487b-92b7-ec7160513696,c981c640-e50a-4952-ac39-2f90d6d0cf08
source-git-commit: 656c87201aca58de947cb835f610f6c82a814d57
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Acrobat Sign-texttaggar

Lär dig skapa Acrobat Sign-formulärfält med texttaggar. Texttaggar kan läggas till direkt i redigeringsverktyg som Microsoft Word, Adobe InDesign eller om du har en PDF - i Acrobat. De kan avsevärt minska arbetet med att ta fram dokument som används i Acrobat Sign. När du har överfört ett taggat dokument i Acrobat Sign kan det konfigureras som en mall, vilket eliminerar behovet av att någon lägger till fält i sina dokument.

## Komma igång

Texttaggar är textstycken som har ett unikt format och som placeras var som helst i ett dokument och som automatiskt identifieras som fält när de överförs till Acrobat Sign.

![Syntax för texttagg](../assets/syntax.png)

Texttaggar kan läggas till direkt i redigeringsverktyg som Microsoft Word, Adobe InDesign eller om du har en PDF - Acrobat. Texttaggar gör det betydligt enklare att skapa dokument som används i Acrobat Sign.

### Lägga till taggar i Microsoft Word

Om du vill lägga till texttaggar i ett Microsoft Word-dokument kan du titta på den här [videosjälvstudiekursen](text-tagging-word.md).

### Lägga till taggar i Acrobat

Adobe Acrobat har en robust redigeringsmiljö för att dra och släppa formulär. Genom att använda texttaggar i Acrobat kan du utnyttja ytterligare funktioner som finns i Acrobat Sign.

1. Öppna formuläret i Acrobat.

1. Välj **[!UICONTROL Förbered ett formulär]** i panelen **[!UICONTROL Alla verktyg]**.

1. Välj **[!UICONTROL Skapa formulär]**.

1. Välj **[!UICONTROL Förbered formulär för e-signering]** i listrutan på panelen **[!UICONTROL Alternativ]**.

   ![Förbered formulär för e-signering](../assets/tag-prepare-e-signing.png)

1. Välj **[!UICONTROL Nästa]** för att bekräfta.

   ![Bekräfta konvertering av fält](../assets/tag-confirm.png)

1. Dubbelklicka på ett fält för att öppna dialogrutan **[!UICONTROL Egenskaper]**.

   Använd syntaxen som beskrivs i [Användarhandboken för Acrobat Sign-texttaggar](https://helpx.adobe.com/se/sign/using/text-tag.html) för att ändra formulärfältets namn.

1. Du kan till exempel skriva *OInt_es_:signer1:optinitials* i fältnamnet för att göra ett inledande fält valfritt.

   ![Ändra fältnamn](../assets/tag-opt-initials.png)

   Texttaggar läggs till i formulärfältets namn, och till skillnad från den syntax du skulle använda i Microsoft Word (eller andra redigeringsverktyg) tas inte klammerparenteserna med.

   Texttaggar kan också läggas till i panelen Fält genom att helt enkelt byta namn på formulärfältet.

   ![Byt namn i fältpanelen](../assets/tag-rename.png)

1. Spara och stäng filen.

1. Ladda upp filen i Acrobat Sign och skapa en återanvändbar mall enligt beskrivningen i nästa avsnitt.

### Skapa en återanvändbar mall

När du har skapat ett taggat dokument kan du konfigurera det som en återanvändbar mall, vilket gör att ingen behöver lägga till fält i dokumenten.

Om du vill skapa en mall som kan återanvändas kan du titta på den här [videosjälvstudiekursen](../sign-advanced-users/create-a-template.md).
