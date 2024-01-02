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
source-git-commit: 84aa3c18e0da0d4e5c83130c4e3303407ebf784a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# Samla dokument med stora volymer med GigaSign

Med GigaSign kan du skicka, samla in och spåra dokument för signering till tusentals personer samtidigt. Den är utformad för kommunikation med stora volymer med dina anställda och kunder, med stöd för upp till 2 500 mottagare vid varje massutskick. GigaSign använder Acrobat Sign API för att tillhandahålla samma funktioner som MegaSign, och inkluderar stöd för flera signerare, mottagargrupper, mottagarroller, avtalsnamn, karbonkopia med mera.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Hämta och installera GigaSign-appen

[Hämta zip-filen GigaSign](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:d1a3f4f2-0f7b-466f-9785-81dff2217776)

[Java 1.8 hämtningslänk (endast vid behov)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[IP-adresser till tillåtelselista (endast vid behov)](https://helpx.adobe.com/se/sign/system-requirements.html#IPs){target="_blank"}

## Grundläggande installationsanvisningar

1. Logga in på ditt Acrobat Sign-konto.

1. Klicka **[!UICONTROL Grupp]** eller **[!UICONTROL Konto]**, beroende på vad du ser högst upp.

1. Skriv &quot;Åtkomsttoken&quot; i sökfältet på vänster sida av skärmen.

1. Tryck på +-ikonen till höger.

1. Skapa en nyckel med de omfång som behövs (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Dubbelklicka på nyckeln du skapade och kopiera hela texten (den flyttas från skärmen till höger så se till att du får allt).

1. Öppna GigaSign.

1. Klicka på **[!UICONTROL Inställningar]** längst upp till höger.

1. Klistra in integreringsnyckeln på den första raden.

1. Ange e-postadressen till det konto som användes för att skapa nyckeln på den andra raden.

1. Klicka på **[!UICONTROL Skicka]**.
