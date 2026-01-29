---
title: Arbeta med formulärfält
description: Lär dig lägga till olika typer av formulärfält, ange formulärfältegenskaper och lägga till säkerhet för att skapa professionella formulär av hög kvalitet
feature: Form, Edit PDF
role: User
level: Intermediate
jira: KT-9345
thumbnail: KT-9345.jpg
exl-id: b7dde660-846c-4875-b5a7-741ff087ccc9
source-git-commit: baf36807c1dcf2142d9a8a5502d8d10d5b8d6033
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Arbeta med formulärfält

I den här praktiska självstudiekursen lär du dig lägga till olika typer av formulärfält, ange formulärfältsegenskaper och lägga till säkerhet för att skapa professionella formulär av hög kvalitet.

<br> 

## Vad du behöver

[![Hämta fil](../assets/Getfiles.svg)](../assets/Questionnaire.pdf)
Exempelfil att öva med (PDF, 934 kB)

<br> 

## Lär dig arbeta med formulärfält

Använd Prepare Form-verktyget för att automatiskt lägga till formulärfält i en PDF.

>[!TIP]
>
>Aktivera enskilda tangenter i inställningarna i kategorin Allmänt.

<br> 

>[!VIDEO](https://video.tv.adobe.com/v/340084?quality=12&learn=on&hidetitle=true)

<br> 

## Vad du har lärt dig: arbeta med formulärfält

Så här lägger du till olika typer av formulärfält och anger deras egenskaper i ett befintligt PDF.

1. Hämta och öppna *Enkät.pdf*.
1. Markera **Prepare Form** i Verktygscentret.
1. Välj **Start**.
1. Välj **Redigera text och bilder** i verktygsfältet för att rätta till stavfelet.
1. Välj **Välj** i verktygsfältet för att avsluta redigeringsläget.
1. Markera och ta bort det övre formulärfältet.
1. Välj **Förhandsgranska** för att visa formuläret.
1. Välj **Redigera** för att avsluta förhandsgranskningsläget.

Om du lägger till ett listfält minskar risken för misstag i formulärdata.

1. Markera och ta bort textfältet *HQ-plats*.
1. Välj **Listruta** i verktygsfältet och placera ett nytt fält på platsen för det borttagna textfältet.
1. Skriv *HQ-plats* i **Fältnamn:**.
1. Välj **Alla egenskaper** och välj fliken **Alternativ**.
1. Lägg till tre olika platser i fältet **Objekt:**.
1. Välj standardplats i fältet **Objektlista:**.
1. Välj **Stäng**.
1. Håll ned Skift-tangenten och välj fältet nedan.
1. Välj **Matcha bredd och höjd** och **Vänsterjustera** i den högra rutan.

Datumväljarfält lägger till interaktivitet och eliminerar fel i ett formulär.

1. Markera och ta bort fälten *Projekttidslinje* och *SLUTDATUM*.
1. Välj **Datumfält** i verktygsfältet och placera det nya fältet på den borttagna platsen för fältet *Projekttidslinje*.
1. Skriv *Projektstart* i **Fältnamn:**.
1. Välj **Alla egenskaper** och välj fliken **Format**.
1. Välj ett datumformatalternativ och välj **Stäng**.
1. Håll ned Ctrl + Skift (Cmd + Skift på Mac) för att duplicera fältet.
1. Dubbelklicka på det nya fältet och välj fliken **Allmänt** och byt namn på fältet *Projektslut*.
1. Välj **Stäng**.
1. Håll ned Skift-tangenten och markera alla tre fälten.
1. Välj **Matcha bredd och höjd** i den högra rutan.
1. Använd piltangenterna för att justera varje fält om det behövs.

Kombinationsegenskaper används för att sprida text jämnt över ett textfälts bredd.

1. Dubbelklicka på fältet *Referenskod* och välj fliken **Alternativ**.
1. Avmarkera alla rutor utom **Kombinera av**.
1. Skriv *5* i rutan Tecken.
1. Välj fliken **Utseende** och välj en färg i rutan **Kantfärg**.
1. Välj **Stäng**.
1. Välj **Förhandsgranska** och ange några siffror för att testa kombinationsfältet.
1. Välj **Mer** > **Rensa formulär** för att ta bort data i den högra rutan.

## Lär dig ställa in egenskaper för flera fält samtidigt, tabbordning och skydda ett formulär

<br> 

>[!VIDEO](https://video.tv.adobe.com/v/340096?hidetitle=true)

<br> 

## Vad du har lärt dig: ställa in egenskaper för flera fält samtidigt, tabbordning och skydda ett formulär

Ange egenskaper för flera fält samtidigt genom att tabbordna och säkra ett formulär. Genom att ställa in textfältegenskaper en gång sparar du tid och ger ett formulär visuell konsekvens.

1. Håll ner skifttangenten och markera alla text - och listfält i det högra delfönstret.
1. Högerklicka och välj **Egenskaper...**.
1. Välj *12* i listrutan **Teckenstorlek:**.
1. Välj **Stäng**.

Om du anger tabbordningen kan formulärifyllaren lätt flytta från fält till fält när du fyller i ett formulär.

1. Skriv *Skift + N* för att visa tabbordningen.
1. Flytta fältet *HQ-plats* under fältet *Antal anställda* i den högra rutan.
1. Flytta fälten *Projektstart* och *Projektslut* under fältet *E-POSTADRESS* i den högra rutan.

Genom att skydda ett formulär försäkrar du dig om att dokumentets fält eller innehåll inte kan ändras.

1. Skriv *Ctrl + D (Cmd + D på Mac)* för att öppna dialogrutan **Dokumentegenskaper**.
1. Välj fliken **Säkerhet**.
1. Välj **Lösenordssäkerhet** under listrutan **Säkerhetsmetod:**.
1. Markera **Begränsa redigering och utskrift av dokumentet. Ett lösenord krävs för att ändra behörighetsinställningarna.**
1. Välj **Hög upplösning** i listrutan **Tillåten utskrift:**.
1. Välj **Fylla i formulärfält och signera befintliga signaturfält** i listrutan **Tillåtna ändringar:**.
1. Ange ett starkt lösenord i fältet **Ändra lösenord för behörighet:**.
1. Bekräfta lösenordet och välj **OK**.
1. Välj **OK** för att stänga dialogrutan.
