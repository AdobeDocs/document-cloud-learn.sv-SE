---
title: Arbeta med formulärfält
description: Lär dig lägga till olika typer av formulärfält, ange formulärfältegenskaper och lägga till säkerhet för att skapa professionella formulär av hög kvalitet
feature: Form, Edit PDF
role: User
level: Intermediate
jira: KT-9345
thumbnail: KT-9345.jpg
exl-id: b7dde660-846c-4875-b5a7-741ff087ccc9
source-git-commit: 4e6fbf91e96d26f9ee8f1105ad68738b9450a32d
workflow-type: tm+mt
source-wordcount: '725'
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
1. Välj **Prepare Form** i Verktygscentret.
1. Välj **Start**.
1. Välj **Redigera text och bilder** i verktygsfältet för att åtgärda stavfelet.
1. Välj **Välj** i verktygsfältet när du vill avsluta redigeringsläget.
1. Markera och ta bort det övre formulärfältet.
1. Välj **Förhandsgranska** för att visa formuläret.
1. Välj **Redigera** för att avsluta förhandsgranskningsläget.

Om du lägger till ett listfält minskar risken för misstag i formulärdata.

1. Markera och ta bort *HQ-plats* textfält.
1. Välj **Listruta** i verktygsfältet och placera ett nytt fält på platsen för det borttagna textfältet.
1. Typ *HQ-plats* i **Fält:**.
1. Välj **Alla egenskaper** och välja **Alternativ** -fliken.
1. Lägg till tre olika platser i **Objekt:** område.
1. Välj standardplatsen i **Objektlista:** område.
1. Välj **Stäng**.
1. Håll ned Skift-tangenten och välj fältet nedan.
1. Välj **Matcha bredd och höjd** och **Vänsterjustera** i det högra fönstret.

Datumväljarfält lägger till interaktivitet och eliminerar fel i ett formulär.

1. Markera och ta bort *Tidslinje för projekt* och *SLUTDATUM* fält.
1. Välj **Datumfält** i verktygsfältet och placera det nya fältet i det borttagna *Tidslinje för projekt* fältplats.
1. Typ *Projektstart* i **Fält:**.
1. Välj **Alla egenskaper** och välja **Format** -fliken.
1. Välj ett datumformatalternativ och välj **Stäng**.
1. Håll ned Ctrl + Skift (Cmd + Skift på Mac) för att duplicera fältet.
1. Dubbelklicka på det nya fältet och välj kommandot **Allmänt** och ändra namn på fältet *Projektslut*.
1. Välj **Stäng**.
1. Håll ned Skift-tangenten och markera alla tre fälten.
1. Välj **Matcha bredd och höjd** i det högra fönstret.
1. Använd piltangenterna för att justera varje fält om det behövs.

Kombinationsegenskaper används för att sprida text jämnt över ett textfälts bredd.

1. Dubbelklicka på *Hänvisningskod* och välja alternativet **Alternativ** -fliken.
1. Avmarkera alla rutor utom **Kam av**.
1. Typ *5* i rutan Tecken.
1. Välj **Utseende** och välja en färg på fliken **Kantfärg** -rutan.
1. Välj **Stäng**.
1. Välj **Förhandsgranska** och ange några siffror för att testa kombinationsfältet.
1. Välj **Mer** > **Rensa formulär** för att ta bort data i det högra delfönstret.

## Lär dig ställa in egenskaper för flera fält samtidigt, tabbordning och skydda ett formulär

<br> 

>[!VIDEO](https://video.tv.adobe.com/v/340096?hidetitle=true)

<br> 

## Vad du har lärt dig: ställa in egenskaper för flera fält samtidigt, tabbordning och skydda ett formulär

Ange egenskaper för flera fält samtidigt genom att tabbordna och säkra ett formulär. Genom att ställa in textfältegenskaper en gång sparar du tid och ger ett formulär visuell konsekvens.

1. Håll ner skifttangenten och markera alla text - och listfält i det högra delfönstret.
1. Högerklicka och välj **Egenskaper...**.
1. Välj *12* från **Teckenstorlek:** Listruta.
1. Välj **Stäng**.

Om du anger tabbordningen kan formulärifyllaren lätt flytta från fält till fält när du fyller i ett formulär.

1. Typ *Skift + N* för att visa tabbordningen.
1. Flytta *HQ-plats* området under *Antal anställda* i det högra delfönstret.
1. Flytta *Projektstart* och *Projektslut* områden under *E-POSTADRESS* i det högra delfönstret.

Genom att skydda ett formulär försäkrar du dig om att dokumentets fält eller innehåll inte kan ändras.

1. Typ *Ctrl + D (Cmd + D på Mac)* för att ta upp **Dokumentegenskaper** dialog.
1. Välj **Säkerhet** -fliken.
1. Välj **Lösenordssäkerhet** enligt **Säkerhetsmetod:** Listruta.
1. Kontroll **Begränsa redigering och utskrift av dokumentet. Ett lösenord krävs för att ändra behörighetsinställningarna.**
1. Välj **Hög upplösning** från **Utskrift tillåten:** Listruta.
1. Välj **Fylla i formulärfält och signera befintliga signaturfält** från **Tillåtna ändringar:** Listruta.
1. Ange ett starkt lösenord i rutan **Ändra lösenord för behörighet:** område.
1. Bekräfta lösenordet och välj **OK**.
1. Välj **OK** för att stänga dialogrutan.
