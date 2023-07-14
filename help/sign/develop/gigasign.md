---
title: Samla in stora volymer dokument med GigaSign
description: Med Gigasign kan du skicka, samla in och spåra dokument för signering till tusentals personer samtidigt
role: User, Admin
product: adobe sign
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: aa8fd589d214879f2bfcb6bc54576c707532fd6f
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%

---

# Samla in stora volymer dokument med GigaSign

Med Gigasign kan du skicka, samla in och spåra dokument för signering till tusentals personer samtidigt. Den är utformad för kommunikation med stora volymer med dina anställda och kunder - med stöd för upp till 2 500 mottagare vid varje massutskick. GigaSign använder Acrobat Sign API för att tillhandahålla samma funktioner som MegaSign, och inkluderar stöd för flera signerare, mottagargrupper, mottagarroller, avtalsnamn, karbonkopia med mera.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Hämta och installera GigaSign-appen

[Hämta zip-filen GigaSign](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Hämtningslänk för Java 1.8 (endast vid behov)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[IP-adresser till vit lista (endast vid behov)](https://helpx.adobe.com/se/sign/system-requirements.html#IPs){target="_blank"}

## Grundläggande installationsanvisningar

1. Logga in på ditt Acrobat Sign-konto.

1. Klicka **[!UICONTROL Grupp]** eller **[!UICONTROL Konto]**, beroende på vad du ser högst upp.

1. Skriv &quot;Access tokens&quot; i sökfältet på vänster sida av skärmen.

1. Tryck på +-ikonen på höger sida.

1. Skapa en nyckel med de omfång som behövs (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Dubbelklicka på nyckeln du skapade och kopiera hela texten (den hamnar utanför skärmen till höger så se till att du får allt).

1. Öppna GigaSign.

1. Klicka på **[!UICONTROL Inställningar]** längst upp till höger.

1. Klistra in integreringsnyckeln på den första raden.

1. Ange e-postadressen till kontot som användes för att skapa nyckeln på den andra raden.

1. Klicka på **[!UICONTROL Skicka]**.
