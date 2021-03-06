---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: "Testen die Stärke von Kennwörtern (c#) | Microsoft Docs"
author: wenz
description: "Kennwörter sind nahezu überall erforderlich, sodass lazy Benutzer einfache Kennwörter auswählen, über den leicht zu unterbrechen, sind tendenziell. In der ASP-Steuerelements \"PasswordStrength\"-Steuerelement. N..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: eda7baae1833b074ba34d8f10fa434df14cc592e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2017
---
<a name="testing-the-strength-of-a-password-c"></a>Testen die Stärke von Kennwörtern (c#)
====================
durch [Christian Wenz](https://github.com/wenz)

[Herunterladen von Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) oder [PDF herunterladen](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> Kennwörter sind nahezu überall erforderlich, sodass lazy Benutzer einfache Kennwörter auswählen, über den leicht zu unterbrechen, sind tendenziell. Das Steuerelement Steuerelements "PasswordStrength" in der ASP.NET AJAX-Steuerelement-Toolkit kann überprüfen, wie gut ein Kennwort ist.


## <a name="overview"></a>Übersicht

Kennwörter sind nahezu überall erforderlich, sodass lazy Benutzer einfache Kennwörter auswählen, über den leicht zu unterbrechen, sind tendenziell. Die `PasswordStrength` -Steuerelement in ASP.NET AJAX-Steuerelement-Toolkit kann überprüfen, wie gut ein Kennwort ist.

## <a name="steps"></a>Schritte

Die `PasswordStrength` Steuerelement ein Textfeld, das erweitert und überprüft, ob das Kennwort in es ausreichend ist. Es bietet eine Vielzahl von Optionen über Attribute. Hier sind nur einige von ihnen:

- `MinimumNumericCharacters`minimale Anzahl von Zeichen im Kennwort erforderlich
- `MinimumSymbolCharacters`minimale Anzahl von Symbolzeichen (nicht Buchstaben und Ziffern), die im Kennwort erforderlich
- `PreferredPasswordLength`die Mindestlänge des Kennworts
- `RequiresUpperAndLowerCaseCharacters`Gibt an, ob das Kennwort muss Großbuchstaben und Kleinbuchstaben verwenden.

Die `StrengthIndicatorType` enthält die Informationen wie die Stärke der das Kennwort als Text vorhanden (Wert `"Text"`) oder als eine Art von Statusanzeige (Wert `"BarIndicator"`). In der `DisplayPosition` -Attribut, die Sie konfigurieren, in dem die Informationen angezeigt. Hier ist ein vollständiges Beispiel, einschließlich ASP.NET AJAX `ScriptManager` -Steuerelement, das `PasswordStrength` -Steuerelement und natürlich ein Textfeld, in dem der Benutzer ein Kennwort eingeben kann. Aus Gründen der Demo ist letztere Formularfelds ein normales Textfeld und nicht um ein Kennwortfeld, sodass Sie während der Entwicklung sehen können, was Sie eingeben.

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

Führen Sie die Seite, und geben Sie sofort: nur nachdem Kleinbuchstaben, Großbuchstaben, Ziffern und Symbole eingegeben haben, das Kennwort als untrennbares wiederhergestellt werden kann.


[![Jetzt ist das Kennwort (relativ) gut](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

Jetzt das Kennwort (relativ) gut ist ([klicken Sie hier, um das Bild in voller Größe angezeigt](testing-the-strength-of-a-password-cs/_static/image3.png))

>[!div class="step-by-step"]
[Nächste](testing-the-strength-of-a-password-vb.md)
