---
title: Integrationstests in ASP.NET Core
author: ardalis
description: "So verwenden Sie ASP.NET Core Integrationstests, um sicherzustellen, dass eine Komponenten einer Anwendung ordnungsgemäß funktionieren."
keywords: ASP.NET Core, Integrationstests zu legen, Razor
ms.author: riande
manager: wpickett
ms.date: 09/25/2017
ms.topic: article
ms.assetid: 40d534f2-89b3-4b09-9c2c-3494bf9991c9
ms.technology: aspnet
ms.prod: asp.net-core
uid: testing/integration-testing
ms.openlocfilehash: 155fd2f0663c6225531a4df6f323ebb30ab1ee73
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2017
---
# <a name="integration-testing-in-aspnet-core"></a>Integrationstests in ASP.NET Core

Von [Steve Smith](https://ardalis.com/)

Durch Integrationstests wird sichergestellt, dass die Komponenten einer Anwendung ordnungsgemäß funktionieren, wenn sie zusammengefügt werden. ASP.NET Core unterstützt Integrationstests mit Hilfe des Komponententest-Frameworks und einem integrierten Test Webhost, der verwendet werden kann, um dne Mehraufwand der Netzwerk-Anforderungen zu verarbeiten.

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/testing/integration-testing/sample) ([Vorgehensweise zum Herunterladen](xref:tutorials/index#how-to-download-a-sample))

## <a name="introduction-to-integration-testing"></a>Einführung in die Integrationstests

Mit Integrationstests stellen Sie sicher, dass unterschiedliche Teile einer Anwendung ordnungsgemäß zusammenarbeiten. Im Gegensatz zu [UnitTests](https://docs.microsoft.com/dotnet/articles/core/testing/unit-testing-with-dotnet-test), umfassen Integrationstests häufig Infrastruktur- und Anweungdsaspekte, z. B. eine Datenbank, das Dateisystem, Netzwerkressourcen, oder Webanforderungen und-Antworten . Komponententests benutzen Fake- oder Pseudoobjekte anstelle der echten Systeme, aber der Zweck der Integrationstests ist es, zu bestätigen, dass das System wie erwartet mit diesen Systemen arbeitet.

Integrationstests sind, tendenziell, weil sie größere Codesegmente ausführen und abhängig von Infrastrukturelemente sind, erheblich langsamer als Komponententests. Daher ist es eine gute Idee, die Anzahl der Integrationstests zu beschränken, die Sie schreiben, insbesondere dann, wenn Sie das gleiche Verhalten mit einem Komponententest testen können.

> [!NOTE]
> Wenn einige Verhaltensweisen sowohl mit einem Komponententest, als auch mit einem Integrationstest getestet werden kann, verwenden sie lieber den Komponententest, da er fast immer schneller wird. Sie werden wahrscheinlich Dutzende oder Hunderte von Komponententests mit vielen unterschiedlichen Eingaben haben, jedoch nur eine Handvoll Integrationstests, die die wichtigsten Szenarien abdecken.

Das Testen die Logik innerhalb der eigenen Methoden ist in der Regel der Bereich der Komponententests. Das Testen der Funktionsweise der Anwendung innerhalb seiner Frameworks, z. B. ASP.NET Core oder mit einer Datenbank, ist der Bereich in denen Integrationstests ins Spiel kommen. Es braucht nicht viele Integrationstests, um sicherzustellen, dass Sie eine Zeile in die Datenbank schreiben und wieder lesen können. Sie müssen nicht alle möglichen Permutation des Datenzugriffscodes testen – Sie müssen nur genug testen, um die Gewissheit zu erhalten, dass die Anwendung ordnungsgemäß funktioniert.

## <a name="integration-testing-aspnet-core"></a>Integrationstest mit ASP.NET Core

Um mit den Integrationstests zu beginnen, müssen Sie ein Testprojekt erstellen, Sie einen Verweis zum Projekt Web ASP.NET Core hinzufügen und einen Test Runner installieren. Dieser Prozess wird in der der [UnitTests](https://docs.microsoft.com/dotnet/articles/core/testing/unit-testing-with-dotnet-test) Dokumentation zusammen mit detaillierten Anweisungen zum Ausführen von Tests und Empfehlungen für die Benennung der Tests und Testklassen beschrieben.

> [!NOTE]
> Trennen Sie die Komponententests und Integrationstests, indem Sie unterschiedliche Projekte verwenden. Dadurch wird sichergestellt, dass Sie nicht versehentlich Infrastruktur-Aspekte in Komponententests einführen und dauruch können Sie problemlos auswählen, welchen Satz von Tests Sie ausführen.

### <a name="the-test-host"></a>Testhost

ASP.NET Core umfasst einen Testhost, der zu den Integrations-Testprojekten hinzugefügt werden kann und zum Hosten von verwendeten ASP.NET Core Anwendungen verwendeten werden kann, um Test.Anfragen ohne die Notwendigkeit einer echten Webhost zu beantworten. Das bereitgestellte Beispiel enthält ein Integrationstestprojekt das konfiguriert wurde,  [xUnit](https://xunit.github.io) und den Host zu vewenden. Er verwendet das `Microsoft.AspNetCore.TestHost` NuGet-Paket.

Sobald das `Microsoft.AspNetCore.TestHost` Paket im Projekt enthalten ist, können Sie einen TesServer in den Tests erstellen und konfigurieren. Der folgende Test zeigt, wie sicherzustellen ist, dass eine Anforderung auf das Stammverzeichnis einer Seite "Hello World!" zurückgibt und sollte erfolgreich gegen die standardmäßige ASP.NET Core leere Web-Vorlage, die von Visual Studio erstellt wurde, ausgeführt werden.

[!code-csharp[Main](../testing/integration-testing/sample/test/PrimeWeb.IntegrationTests/PrimeWebDefaultRequestShould.cs?name=snippet_WebDefault&highlight=7,16,22)]

Bei diesem Test wird das Arrange-Act-Assert-Muster verwendet. Der Arrange Schritt erfolgt im Konstruktor, der eine `TestServer` Instanz erstellt. Ein konfigurierter `WebHostBuilder` wird zum Erstellen eines `TestHost` verwendet; in diesem Beispiel die `Configure` Methode des zu testendes Systems (`system under test`, SUT), die `Startup` Klasse wird dem `WebHostBuilder` übergeben. Diese Methode wird zum Konfigurieren der Anforderungspipeline des `TestServer`, sodass es identisch mit der Konfiguration des Servers SUT sein würde.

In der Act-Teil des Tests wird eine Anforderung an die `TestServer` -Instanz für den Pfad "/" gestellt und die Antwort wird zurück in eine Zeichenfolge gelesen. Diese Zeichenfolge wird mit der erwarteten Zeichenfolge "Hello World!" verglichen. Wenn sie übereinstimmen, wird der Test erfolgreich; Andernfalls schlägt er fehl.

Jetzt können Sie einige zusätzliche Integrationstests hinzufügen, um sicherzustellen, dass die Primzahlen-Prüfen Funktionalität der Webanwendung funktioniert:

[!code-csharp[Main](../testing/integration-testing/sample/test/PrimeWeb.IntegrationTests/PrimeWebCheckPrimeShould.cs?name=snippet_CheckPrime)]

Beachten Sie, dass Sie mit diesen Tests nicht wirklich versuchen, die Richtigkeit von Primzahl Checker zu testen, vielmehr jedoch ob, die Webanwendung das tut, was Sie erwarten. Sie haben bereits Test-Coverage für Komponententests,  das Ihnen Vertrauen für `PrimeService` geben kann, wie Sie hier sehen können:

![Test-Explorer](integration-testing/_static/test-explorer.png)

Weitere Informationen finden Sie in den Informationen zu den Komponententests in dem [UnitTests](https://docs.microsoft.com/dotnet/articles/core/testing/unit-testing-with-dotnet-test) Artikel.


### <a name="integration-testing-mvcrazor"></a>Integrationstests für MVC/Razor

Testprojekte, die Razor-Ansichten enthalten, erfordern, dass `<PreserveCompilationContext>` auf true festgelegt wird, in der *csproj* Datei:


```xml
    <PreserveCompilationContext>true</PreserveCompilationContext>
```

Projekte, denen dieses Element fehlt, werden eine Fehlermeldung ähnlich der folgenden generieren:
```
Microsoft.AspNetCore.Mvc.Razor.Compilation.CompilationFailedException: 'One or more compilation failures occurred:
ooebhccx.1bd(4,62): error CS0012: The type 'Attribute' is defined in an assembly that is not referenced. You must add a reference to assembly 'netstandard, Version=2.0.0.0, Culture=neutral, PublicKeyToken=cc7b13ffcd2ddd51'.
```


## <a name="refactoring-to-use-middleware"></a>Refactoring, um Middleware zu verwenden

Unter Refactoring versteht man das Ändern des Codes einer Anwendung, um ihren Entwurf zu verbessern, ohne dessen Verhalten zu ändern. Es sollte idealerweise ausgeführt werden, wenn es eine Sammlung von erfolgreichen Tests gibt, da Sie mit dieser Hilfe sicherstellen können, dass das Verhalten des Systems vor und nach der Änderung unverändert ist. Beim Betrachten der Implementierung, die in dieser Webanwendung `Configure`-Methode zum Überprüfen von Primzahlen verwendet wird, sehen Sie:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }

    app.Run(async (context) =>
    {
        if (context.Request.Path.Value.Contains("checkprime"))
        {
            int numberToCheck;
            try
            {
                numberToCheck = int.Parse(context.Request.QueryString.Value.Replace("?", ""));
                var primeService = new PrimeService();
                if (primeService.IsPrime(numberToCheck))
                {
                    await context.Response.WriteAsync($"{numberToCheck} is prime!");
                }
                else
                {
                    await context.Response.WriteAsync($"{numberToCheck} is NOT prime!");
                }
            }
            catch
            {
                await context.Response.WriteAsync("Pass in a number to check in the form /checkprime?5");
            }
        }
        else
        {
            await context.Response.WriteAsync("Hello World!");
        }
    });
}
```

Dieser Code funktioniert, allerdings ist er weit davon entfernt, wie Sie diese Art von Funktionalität in einer ASP.NET Core umsetzen würden, sei sie noch so simpel. Stellen Sie sich vor, wie die `Configure` Methode aussehen würde, wenn jedes Mal so viel Code hinzugefügt werden müsste, wenn Sie einen anderen URL-Endpunkt hinzufügen.

Eine Option wäre das Hinzufügen von [MVC](xref:mvc/overview) zu Anwendung und Erstellen eines Controllers, um auf Primzahlen zu überprüfen. Allerdings wäre das, vorausgesetzt, dass Sie derzeit keine anderen MVC Funktionalität verwenden, ein wenig übertrieben.

Sie können jedoch von ASP.NET Core [Middleware](xref:fundamentals/middleware) profitieren, die uns hilft, die Primzahl-Überprüf-Logik in eine Klasse zu kapseln und so eine bessere [Trennung von Anliegen](http://deviq.com/separation-of-concerns/) in der `Configure` Methode zu erzielen.

Sie müssen es dazu ermöglichen, dass der Pfad, den die Middleware verwendet, als Parameter angegeben werden kann, d.h. die Middleware-Klasse erwartet eine `RequestDelegate` und eine `PrimeCheckerOptions` Instanz in seinem Konstruktor. Wenn der Pfad der Anforderung nicht mit dem übereinstimmt, mit dem diese Middleware konfiguriert ist, rufen Sie einfach die nächste Middleware in der Kette auf und unternehmen keine weiteren Aktionen. Der Rest der Code Implementierung, die vorher in `Configure` war, ist jetzt der `Invoke` Methode.

> [!NOTE]
> Da die Middleware vome `PrimeService` Service abhängt, fordern Sie auch eine Instanz dieses Diensts mit dem Konstruktor an. Das Framework bietet diesen Dienst über [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection) an, sofern es konfiguriert wurde, z. B. in `ConfigureServices`.

[!code-csharp[Main](../testing/integration-testing/sample/src/PrimeWeb/Middleware/PrimeCheckerMiddleware.cs?highlight=39-63)]

Da diese Middleware als Endpunkt in der Anforderungs-Delegierungskette fungiert, wenn ihr Pfad übereinstimmt, wird `_next.Invoke` nicht aufgerufen, wenn diese Middleware die Anforderung verarbeitet.

Mit dem Einsatz dieser Middleware und dem Erstellen einiger nützliche Erweiterungsmethoden, um die Konfiguration zu erleichtern, sieht die umgestaltete `Configure` -Methode folgendermaßen aus:

[!code-csharp[Main](../testing/integration-testing/sample/src/PrimeWeb/Startup.cs?highlight=9&range=19-33)]

Nach diesem Refactoring sind Sie sicher, dass die Webanwendung weiterhin wie zuvor funktioniert, da die Integrationstests weiterhin erfolgreich sind.

> [!NOTE]
> Es ist eine gute Idee, die Änderungen zur Quellcodeverwaltung zu übertragen, nachdem Sie eine Umgestaltung abschließen und die Tests bestanden werden. Wenn Sie testgesteuert entwickeln, erwägen Sie, den Commit dem [Red-Green-Refactor Zyklus](https://ardalis.com/rgrc-is-the-new-red-green-refactor-for-test-first-development) hinzuzufügen.

## <a name="resources"></a>Ressourcen

* [Komponententests](https://docs.microsoft.com/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [Middleware](xref:fundamentals/middleware)
* [Testen von Controllern](xref:mvc/controllers/testing)
