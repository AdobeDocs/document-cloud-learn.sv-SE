---
title: Samla dokument med stora volymer med GigaSign
description: Med GigaSign kan du skicka, samla in och spåra dokument för signering till tusentals personer samtidigt
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: ba9931920ab3bfb6ea38a92cac4a35da1d0295cd
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Samla dokument med stora volymer med GigaSign

Med GigaSign kan du skicka, samla in och spåra dokument för signering till tusentals personer samtidigt. Den är utformad för kommunikation med stora volymer med dina anställda och kunder, med stöd för upp till 2 500 mottagare vid varje massutskick. GigaSign använder Acrobat Sign API för att tillhandahålla samma funktioner som MegaSign, och inkluderar stöd för flera signerare, mottagargrupper, mottagarroller, avtalsnamn, karbonkopia med mera.

>[!IMPORTANT]
>
>GigaSign uppdateras inte längre till den senaste versionen av Java eller Acrobat Sign och kommer bara att ha begränsat stöd. Funktionerna i GigaSign läggs till i produkten under funktionen [Massutskick](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/getting-started-admin/megasign.html?). Använd Massutskick för alla användningsfall som inte uttryckligen kräver användning av GigaSign.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Hämta och installera GigaSign-appen

[Hämta zip-filen GigaSign](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Java 1.8-hämtningslänk (endast vid behov)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[IP-adresser till tillåtelselista (endast vid behov)](https://helpx.adobe.com/se/sign/system-requirements.html#IPs){target="_blank"}

## Grundläggande installationsanvisningar

1. Logga in på ditt Acrobat Sign-konto.

1. Klicka på **[!UICONTROL Grupp]** eller **[!UICONTROL Konto]**, beroende på vilket som visas högst upp.

1. Skriv &quot;Åtkomsttoken&quot; i sökfältet på vänster sida av skärmen.

1. Tryck på +-ikonen till höger.

1. Skapa en nyckel med de omfång som behövs (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Dubbelklicka på nyckeln du skapade och kopiera hela texten (den flyttas från skärmen till höger så se till att du får allt).

1. Öppna GigaSign.

1. Klicka på ikonen **[!UICONTROL Inställningar]** längst upp till höger.

1. Klistra in integreringsnyckeln på den första raden.

1. Ange e-postadressen till det konto som användes för att skapa nyckeln på den andra raden.

1. Klicka på **[!UICONTROL Skicka]**.
