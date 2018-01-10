---
title: Ansichten im Kern der ASP.NET MVC
author: ardalis
description: Erfahren Sie, wie Ansichten der app-datendarstellung und die Benutzerinteraktion in ASP.NET Core MVC behandeln.
keywords: ASP.NET Core, MVC, Razor, Viewmodel, Viewdata, Viewbag anzeigen
ms.author: riande
manager: wpickett
ms.date: 12/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/overview
ms.openlocfilehash: 2562d4e5fb85159e6ccb47990f54448ddc188077
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="24f87-104">Ansichten im Kern der ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="24f87-104">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="24f87-105">Durch [Steve Smith](https://ardalis.com/) und [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="24f87-105">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="24f87-106">Dieses Dokument erläutert, Ansichten, die in ASP.NET Core MVC-Anwendungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="24f87-106">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="24f87-107">Informationen für Razor-Seiten finden Sie unter [Einführung in Razor-Seiten](xref:mvc/razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="24f87-107">For information on Razor Pages, see [Introduction to Razor Pages](xref:mvc/razor-pages/index).</span></span>

<span data-ttu-id="24f87-108">In der **M**Odel -**V**vorhandenes -**C**Ontroller (MVC)-Muster, die *Ansicht* verarbeitet die app Daten Präsentation und Benutzerinteraktion.</span><span class="sxs-lookup"><span data-stu-id="24f87-108">In the **M**odel-**V**iew-**C**ontroller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="24f87-109">Eine Sicht ist eine HTML-Vorlage mit eingebetteten [Razor Markup](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="24f87-109">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="24f87-110">Razor-Markup ist Code, der Interaktion mit HTML-Markup, um eine Webseite zu erzeugen, die an den Client gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="24f87-110">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="24f87-111">In ASP.NET-MVC Core Ansichten sind *cshtml* Dateien, die [C#-Programmiersprache](/dotnet/csharp/) in Razor-Markup.</span><span class="sxs-lookup"><span data-stu-id="24f87-111">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="24f87-112">In der Regel anzeigen von Dateien in Ordnern für jede von der app gruppiert [Controller](xref:mvc/controllers/actions).</span><span class="sxs-lookup"><span data-stu-id="24f87-112">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="24f87-113">Die Ordner befinden sich einem *Ansichten* Ordner im Stammverzeichnis der app:</span><span class="sxs-lookup"><span data-stu-id="24f87-113">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Ordner Views in Projektmappen-Explorer von Visual Studio ist mit dem Basisordner anzuzeigende About.cshtml Contact.cshtml und Index.cshtml Dateien öffnen öffnen](overview/_static/views_solution_explorer.png)

<span data-ttu-id="24f87-115">Die *Home* Controller wird dargestellt, indem Sie eine *Home* Ordner innerhalb der *Ansichten* Ordner.</span><span class="sxs-lookup"><span data-stu-id="24f87-115">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="24f87-116">Die *Home* Ordner enthält Ansichten für die *zu*, *Kontakt*, und *Index* (Startseite) Webseiten.</span><span class="sxs-lookup"><span data-stu-id="24f87-116">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="24f87-117">Wenn ein Benutzer fordert eine der drei Webseiten, Controlleraktionen in der *Home* Controller zu ermitteln, welche der drei Ansichten zum Erstellen und Zurückgeben einer Webseite für den Benutzer verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="24f87-117">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="24f87-118">Verwendung [Layouts](xref:mvc/views/layout) konsistent Webseite Abschnitte und codewiederholungen reduzieren.</span><span class="sxs-lookup"><span data-stu-id="24f87-118">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="24f87-119">Layouts enthalten oft den Header, Navigation und im Menü-Elemente und die Fußzeile.</span><span class="sxs-lookup"><span data-stu-id="24f87-119">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="24f87-120">Kopf- und Fußzeilen enthalten normalerweise Textbaustein Markup für viele Metadatenelementen sowie Links zu Skripts und des Stils Bestand.</span><span class="sxs-lookup"><span data-stu-id="24f87-120">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="24f87-121">Layouts können Sie die diesem Textbaustein Markup in Ihren Ansichten zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="24f87-121">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="24f87-122">[Teilansichten](xref:mvc/views/partial) Codeduplikaten durch die Verwaltung von wieder verwendbare Teile der Ansichten reduzieren.</span><span class="sxs-lookup"><span data-stu-id="24f87-122">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="24f87-123">Eine Teilansicht eignet sich z. B. für ein Autor Profildaten für eine Blogwebsite, die in mehreren Ansichten angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="24f87-123">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="24f87-124">Ein Autor Profildaten ist Normalansicht Inhalt und erfordert Code zum Ausführen, um den Inhalt für die Webseite zu erzeugen.</span><span class="sxs-lookup"><span data-stu-id="24f87-124">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="24f87-125">Autor Profildaten Inhalt ist an die Ansicht von allein, wurden die modellbindung verfügbar, deshalb ideal eine Teilansicht für diesen Typ von Inhalt zu verwenden ist.</span><span class="sxs-lookup"><span data-stu-id="24f87-125">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="24f87-126">[Anzeigen von Komponenten](xref:mvc/views/view-components) sind partielle ähnlich wie Ansichten, sie codewiederholungen reduzieren können, aber das erscheint für Inhalt anzeigen, die auf dem Server ausgeführt wird, um die Webseite rendern Code erfordert geeignet.</span><span class="sxs-lookup"><span data-stu-id="24f87-126">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="24f87-127">Anzeigen von Komponenten sind nützlich, wenn es sich bei der gerenderte Inhalt Datenbankinteraktion haben, z. B. für eine Website mit dem Einkaufswagen ist erforderlich.</span><span class="sxs-lookup"><span data-stu-id="24f87-127">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="24f87-128">Ansichtskomponenten sind nicht begrenzt auf die um Bindung zu modellieren, um die Ausgabe der Webseite.</span><span class="sxs-lookup"><span data-stu-id="24f87-128">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="24f87-129">Vorteile der Verwendung von Sichten</span><span class="sxs-lookup"><span data-stu-id="24f87-129">Benefits of using views</span></span>

<span data-ttu-id="24f87-130">Ansichten zur Verfügung, zum Herstellen einer [ **S**Eparation **o**f **C**Oncerns (SoC) Entwurf](http://deviq.com/separation-of-concerns/) innerhalb einer MVC-app durch die Trennung von Benutzer-Schnittstelle Markup aus andere Teile der app.</span><span class="sxs-lookup"><span data-stu-id="24f87-130">Views help to establish a [**S**eparation **o**f **C**oncerns (SoC) design](http://deviq.com/separation-of-concerns/) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="24f87-131">SoC Entwurf nach macht Ihre app modular aufgebaut, die bietet mehrere Vorteile:</span><span class="sxs-lookup"><span data-stu-id="24f87-131">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="24f87-132">Die app ist einfacher zu verwalten, da es besser organisiert ist.</span><span class="sxs-lookup"><span data-stu-id="24f87-132">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="24f87-133">Ansichten werden im Allgemeinen von app-Funktion gruppiert.</span><span class="sxs-lookup"><span data-stu-id="24f87-133">Views are generally grouped by app feature.</span></span> <span data-ttu-id="24f87-134">Dies erleichtert die zugehörige Sichten zu suchen, bei der Arbeit auf eine Funktion.</span><span class="sxs-lookup"><span data-stu-id="24f87-134">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="24f87-135">Die Teile der app sind lose verbunden.</span><span class="sxs-lookup"><span data-stu-id="24f87-135">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="24f87-136">Erstellen und aktualisieren die app-Ansichten getrennt von der Logik und die Daten Zugriff Geschäftskomponenten.</span><span class="sxs-lookup"><span data-stu-id="24f87-136">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="24f87-137">Sie können die Ansichten der app ändern, ohne unbedingt andere Teile der app zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="24f87-137">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="24f87-138">Es ist einfacher, das Benutzeroberflächenkomponenten der app zu testen, da die Ansichten separaten Einheiten sind.</span><span class="sxs-lookup"><span data-stu-id="24f87-138">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="24f87-139">Aufgrund der besseren Organisation ist es weniger wahrscheinlich, dass Sie versehentlich wiederholen Abschnitte der Benutzeroberfläche werden.</span><span class="sxs-lookup"><span data-stu-id="24f87-139">Due to better organization, it's less likely that you'll accidently repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="24f87-140">Erstellen einer Ansicht</span><span class="sxs-lookup"><span data-stu-id="24f87-140">Creating a view</span></span>

<span data-ttu-id="24f87-141">Sichten, die für einen Controller spezifisch sind werden erstellt, der *Ansichten / [ControllerName]* Ordner.</span><span class="sxs-lookup"><span data-stu-id="24f87-141">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="24f87-142">Sichten, die für Domänencontroller, freigegeben werden befinden sich der *Ansichten/freigegeben* Ordner.</span><span class="sxs-lookup"><span data-stu-id="24f87-142">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="24f87-143">Um eine Ansicht zu erstellen, fügen Sie eine neue Datei hinzu, und geben Sie ihm den gleichen Namen wie der Aktion zugeordneten Controller mit dem *cshtml* Dateierweiterung.</span><span class="sxs-lookup"><span data-stu-id="24f87-143">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="24f87-144">Eine Sicht erstellt, der mit übereinstimmt der *zu* Aktion in der *Home* Controller, erstellen eine *About.cshtml* in der Datei die *Ansichten/Start*Ordner:</span><span class="sxs-lookup"><span data-stu-id="24f87-144">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[Main](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="24f87-145">*Razor* Markup beginnt mit der `@` Symbol.</span><span class="sxs-lookup"><span data-stu-id="24f87-145">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="24f87-146">Zur C#-Anweisungen durch Platzieren von C#-code in [Razor Codeblöcke](xref:mvc/views/razor#razor-code-blocks) abgegrenzt von geschweiften Klammern (`{ ... }`).</span><span class="sxs-lookup"><span data-stu-id="24f87-146">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="24f87-147">Finden Sie beispielsweise die Zuweisung von "About" um `ViewData["Title"]` oben.</span><span class="sxs-lookup"><span data-stu-id="24f87-147">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="24f87-148">Sie können Werte in HTML anzeigen, indem Sie einfach verweisen auf den Wert mit dem `@` Symbol.</span><span class="sxs-lookup"><span data-stu-id="24f87-148">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="24f87-149">Den Inhalt der `<h2>` und `<h3>` oben aufgeführten Elemente.</span><span class="sxs-lookup"><span data-stu-id="24f87-149">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="24f87-150">Den Inhalt der oben gezeigten ist nur ein Teil der gesamten Webseite, die für dem Benutzer gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="24f87-150">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="24f87-151">Der Rest der Seite Layout und andere allgemeine Aspekte der Sicht werden angegeben, in anderen Dateien anzeigen.</span><span class="sxs-lookup"><span data-stu-id="24f87-151">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="24f87-152">Weitere Informationen finden Sie unter der [Layout Thema](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="24f87-152">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="24f87-153">Wie Controller Ansichten angeben</span><span class="sxs-lookup"><span data-stu-id="24f87-153">How controllers specify views</span></span>

<span data-ttu-id="24f87-154">Ansichten werden in der Regel zurückgegeben, von Aktionen als ein [ViewResult](/aspnet/core/api/microsoft.aspnetcore.mvc.viewresult), d. h. einen Typ von [ActionResult](/aspnet/core/api/microsoft.aspnetcore.mvc.actionresult).</span><span class="sxs-lookup"><span data-stu-id="24f87-154">Views are typically returned from actions as a [ViewResult](/aspnet/core/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/aspnet/core/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="24f87-155">Die Aktionsmethode erstellen und zurückgeben kann eine `ViewResult` direkt, jedoch, ist nicht im Allgemeinen vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="24f87-155">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="24f87-156">Da die meisten Domänencontroller erben [Controller](/aspnet/core/api/microsoft.aspnetcore.mvc.controller), verwenden Sie einfach die `View` Hilfsmethode zurückzugebenden der `ViewResult`:</span><span class="sxs-lookup"><span data-stu-id="24f87-156">Since most controllers inherit from [Controller](/aspnet/core/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="24f87-157">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="24f87-157">*HomeController.cs*</span></span>

[!code-csharp[Main](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="24f87-158">Wenn diese Aktion zurückgegeben wird, die *About.cshtml* anzeigen, die im vorherigen Abschnitt gezeigt als der folgenden Webseite gerendert wird:</span><span class="sxs-lookup"><span data-stu-id="24f87-158">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![Zu den Seiten im Edge-Browser gerendert](overview/_static/about-page.png)

<span data-ttu-id="24f87-160">Die `View` -Hilfsmethode verfügt über mehrere Überladungen.</span><span class="sxs-lookup"><span data-stu-id="24f87-160">The `View` helper method has several overloads.</span></span> <span data-ttu-id="24f87-161">Optional können Sie Folgendes angeben:</span><span class="sxs-lookup"><span data-stu-id="24f87-161">You can optionally specify:</span></span>

* <span data-ttu-id="24f87-162">Eine explizite Ansicht zurückgeben:</span><span class="sxs-lookup"><span data-stu-id="24f87-162">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="24f87-163">Ein [Modell](xref:mvc/models/model-binding) Übergabe an die die Sicht:</span><span class="sxs-lookup"><span data-stu-id="24f87-163">A [model](xref:mvc/models/model-binding) to pass to the the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="24f87-164">Eine Sicht und ein Modell:</span><span class="sxs-lookup"><span data-stu-id="24f87-164">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="24f87-165">View-Ermittlung</span><span class="sxs-lookup"><span data-stu-id="24f87-165">View discovery</span></span>

<span data-ttu-id="24f87-166">Ein Prozess wird aufgerufen, wenn eine Aktion eine Sicht zurückgegeben wird, *Ansicht Ermittlung* erfolgt.</span><span class="sxs-lookup"><span data-stu-id="24f87-166">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="24f87-167">Dieser Prozess wird bestimmt, welche Datei verwendet wird anhand des Ansichtsnamens.</span><span class="sxs-lookup"><span data-stu-id="24f87-167">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="24f87-168">Das Standardverhalten der `View` Methode (`return View();`) ist eine Sicht mit dem gleichen Namen wie die Aktionsmethode zurückgeben, von dem sie aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="24f87-168">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="24f87-169">Z. B. die *zu* `ActionResult` Methodennamen des Controllers wird zur Suche nach einer Datei anzeigen, die mit dem Namen *About.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="24f87-169">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="24f87-170">Die Common Language Runtime sucht zuerst die *Ansichten / [ControllerName]* Ordner für die Ansicht.</span><span class="sxs-lookup"><span data-stu-id="24f87-170">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="24f87-171">Wenn es keine entsprechende Ansicht gefunden werden, sucht der *Shared* Ordner für die Ansicht.</span><span class="sxs-lookup"><span data-stu-id="24f87-171">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="24f87-172">Es spielt keine Rolle, wenn Sie, implizit zurückkehren die `ViewResult` mit `return View();` oder übergeben Sie den Namen der Ansicht, um explizit die `View` Methode mit `return View("<ViewName>");`.</span><span class="sxs-lookup"><span data-stu-id="24f87-172">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="24f87-173">Zeigen Sie in beiden Fällen Ermittlung sucht nach einer übereinstimmenden Ansichtsdatei, in der angegebenen Reihenfolge aus:</span><span class="sxs-lookup"><span data-stu-id="24f87-173">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="24f87-174">*Ansichten /\[ControllerName]\[ViewName] cshtml*</span><span class="sxs-lookup"><span data-stu-id="24f87-174">*Views/\[ControllerName]\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="24f87-175">*Ansichten/freigegeben/\[ViewName] cshtml*</span><span class="sxs-lookup"><span data-stu-id="24f87-175">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="24f87-176">Anstatt ein Ansichtsname kann ein Dateipfad für die Sicht angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="24f87-176">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="24f87-177">Wenn einen absoluten Pfad, angefangen beim Stamm app verwenden (optional beginnend mit "/" oder "~ /"), wird die *cshtml* Erweiterung muss angegeben werden:</span><span class="sxs-lookup"><span data-stu-id="24f87-177">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="24f87-178">Sie können auch einen relativen Pfad zum Angeben von Ansichten in verschiedenen Verzeichnissen ohne die *cshtml* Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="24f87-178">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="24f87-179">Innerhalb der `HomeController`, können Sie zurückkehren, die *Index* -Ansicht Ihrer *verwalten* Ansichten mit einem relativen Pfad:</span><span class="sxs-lookup"><span data-stu-id="24f87-179">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="24f87-180">Auf ähnliche Weise können Sie angeben, das aktuelle Controller-spezifische Verzeichnis mit dem ". /" Präfix:</span><span class="sxs-lookup"><span data-stu-id="24f87-180">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="24f87-181">[Teilansichten](xref:mvc/views/partial) und [anzeigen Komponenten](xref:mvc/views/view-components) ähnliche (aber nicht identisch) Ermittlungsmechanismus verwenden.</span><span class="sxs-lookup"><span data-stu-id="24f87-181">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="24f87-182">Sie können anpassen, dass die Standardkonvention dafür, wie Ansichten innerhalb der app gespeichert werden, mithilfe ein benutzerdefinierten [IViewLocationExpander](/aspnet/core/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span><span class="sxs-lookup"><span data-stu-id="24f87-182">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/aspnet/core/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="24f87-183">Ermittlung der Ansicht basiert auf Dateinamen Suchen von Dateien anzeigen.</span><span class="sxs-lookup"><span data-stu-id="24f87-183">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="24f87-184">Wenn das zugrunde liegende Dateisystem Groß-/Kleinschreibung beachtet wird, werden Sichtnamen wahrscheinlich Groß-/Kleinschreibung beachtet.</span><span class="sxs-lookup"><span data-stu-id="24f87-184">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="24f87-185">Aus Kompatibilitätsgründen betriebssystemübergreifende übereinstimmen Sie Schreibweise und die zwischen Controller und Aktion und zugeordnete Ansicht-Ordner und Dateinamen.</span><span class="sxs-lookup"><span data-stu-id="24f87-185">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="24f87-186">Wenn ein Fehler aufgetreten ist, den eine Datei nicht gefunden werden kann, bei der Arbeit mit einem Dateisystem Groß-/Kleinschreibung beachtet wird, vergewissern Sie sich, dass die Groß-/Kleinschreibung zwischen die angeforderte Ansicht-Datei und den Dateinamen der tatsächlichen Ansicht übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="24f87-186">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="24f87-187">Führen Sie die bewährte Methode zum Organisieren von der Dateistruktur für Ihre Ansichten, um die Beziehungen zwischen Domänencontrollern, Aktionen und Ansichten für die Verwaltbarkeit und Klarheit widerzuspiegeln.</span><span class="sxs-lookup"><span data-stu-id="24f87-187">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="24f87-188">Übergeben von Daten mit Ansichten</span><span class="sxs-lookup"><span data-stu-id="24f87-188">Passing data to views</span></span>

<span data-ttu-id="24f87-189">Sie können Daten mit Ansichten mithilfe von mehreren Ansätzen übergeben.</span><span class="sxs-lookup"><span data-stu-id="24f87-189">You can pass data to views using several approaches.</span></span> <span data-ttu-id="24f87-190">Die zuverlässigste Methode ist die Angabe einer [Modell](xref:mvc/models/model-binding) Typ in der Ansicht.</span><span class="sxs-lookup"><span data-stu-id="24f87-190">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="24f87-191">Dieses Modell wird häufig als bezeichnet eine *Viewmodel*.</span><span class="sxs-lookup"><span data-stu-id="24f87-191">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="24f87-192">Sie können eine Instanz des Typs Viewmodel zur Ansicht übergeben, von der Aktion.</span><span class="sxs-lookup"><span data-stu-id="24f87-192">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="24f87-193">Ein Viewmodel Daten an eine Ansicht zu übergeben, können die Ansicht zu nutzen *starken* Überprüfung des Typs.</span><span class="sxs-lookup"><span data-stu-id="24f87-193">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="24f87-194">*Starke Typisierung* (oder *stark typisierte*) bedeutet, dass jede Variable und jede Konstante einen explizit definierten Typ aufweist (z. B. `string`, `int`, oder `DateTime`).</span><span class="sxs-lookup"><span data-stu-id="24f87-194">*Strong typing* (or *strongly-typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="24f87-195">Die Gültigkeit der Typen, die in einer Ansicht verwendet, die zum Zeitpunkt der Kompilierung aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="24f87-195">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="24f87-196">[Visual Studio](https://www.visualstudio.com/vs/) und [Visual Studio Code](https://code.visualstudio.com/) Liste stark typisierte Klasse, Elemente mit einem Feature [IntelliSense](/visualstudio/ide/using-intellisense).</span><span class="sxs-lookup"><span data-stu-id="24f87-196">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly-typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="24f87-197">Wenn Sie die Eigenschaften von einem Viewmodel anzeigen möchten, geben Sie den Variablennamen ein für das Viewmodel, gefolgt von einem Punkt (`.`).</span><span class="sxs-lookup"><span data-stu-id="24f87-197">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="24f87-198">Dadurch können Sie Code schneller mit weniger Fehlern zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="24f87-198">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="24f87-199">Geben Sie ein Modell mithilfe der `@model` Richtlinie.</span><span class="sxs-lookup"><span data-stu-id="24f87-199">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="24f87-200">Verwenden Sie das Modell mit `@Model`:</span><span class="sxs-lookup"><span data-stu-id="24f87-200">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="24f87-201">Um das Modell zur Ansicht bereitzustellen, übergibt er der Controller als Parameter:</span><span class="sxs-lookup"><span data-stu-id="24f87-201">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="24f87-202">Es gelten keine Einschränkungen für die Typen, die Sie eine Ansicht bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="24f87-202">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="24f87-203">Es wird empfohlen, **P**unformatierten **O**%ld **C**LR **O**Viewmodels-Objekt (POCO), mit wenigen oder gar keinen Verhalten (Methoden) definiert.</span><span class="sxs-lookup"><span data-stu-id="24f87-203">We recommend using **P**lain **O**ld **C**LR **O**bject (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="24f87-204">Viewmodel-Klassen werden in der Regel entweder gespeichert, der *Modelle* Ordner oder ein separates *ViewModels* Ordner im Stammverzeichnis der app.</span><span class="sxs-lookup"><span data-stu-id="24f87-204">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="24f87-205">Die *Adresse* Viewmodel verwendet, die im obigen Beispiel ist eine POCO-Viewmodel gespeichert in einer Datei namens *Address.cs*:</span><span class="sxs-lookup"><span data-stu-id="24f87-205">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

> [!NOTE]
> <span data-ttu-id="24f87-206">Nichts daran hindert Sie die gleichen Klassen für die Viewmodel-Typen und Ihre Business-Modelltypen verwenden.</span><span class="sxs-lookup"><span data-stu-id="24f87-206">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="24f87-207">Verwenden von separaten Modellen kann jedoch Ihre Ansichten unabhängig von der Geschäftslogik und die Daten Zugriff Teile Ihrer app variieren.</span><span class="sxs-lookup"><span data-stu-id="24f87-207">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="24f87-208">Trennung von Modellen und Viewmodels bietet zudem Sicherheitsvorteile, wenn Modelle verwenden [modellbindung](xref:mvc/models/model-binding) und [Überprüfung](xref:mvc/models/validation) für Daten, die an die app vom Benutzer gesendet.</span><span class="sxs-lookup"><span data-stu-id="24f87-208">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>


<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-and-viewbag"></a><span data-ttu-id="24f87-209">Schwach typisierte Daten (ViewData und ViewBag)</span><span class="sxs-lookup"><span data-stu-id="24f87-209">Weakly-typed data (ViewData and ViewBag)</span></span>

<span data-ttu-id="24f87-210">Hinweis: `ViewBag` ist in der Razor-Seiten nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="24f87-210">Note: `ViewBag` is not available in the Razor Pages.</span></span>

<span data-ttu-id="24f87-211">Zusätzlich zu den stark typisierten Ansichten Ansichten haben Zugriff auf eine *schwach typisierte* (so genannte *lose typisierten*) Sammeln von Daten.</span><span class="sxs-lookup"><span data-stu-id="24f87-211">In addition to strongly-typed views, views have access to a *weakly-typed* (also called *loosely-typed*) collection of data.</span></span> <span data-ttu-id="24f87-212">Im Gegensatz zu starke Typen *unsichere Typen* (oder *lose Typen*) bedeutet, dass Sie explizit den Typ der Daten deklarieren nicht, Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="24f87-212">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="24f87-213">Die Auflistung der schwach typisierten Daten können für kleine Mengen von Daten aus dem Controller und Ansichten übergeben.</span><span class="sxs-lookup"><span data-stu-id="24f87-213">You can use the collection of weakly-typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="24f87-214">Übergeben von Daten zwischen einem...</span><span class="sxs-lookup"><span data-stu-id="24f87-214">Passing data between a ...</span></span>                        | <span data-ttu-id="24f87-215">Beispiel</span><span class="sxs-lookup"><span data-stu-id="24f87-215">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="24f87-216">Controller und einer Ansicht</span><span class="sxs-lookup"><span data-stu-id="24f87-216">Controller and a view</span></span>                             | <span data-ttu-id="24f87-217">Auffüllen einer Dropdownliste mit Daten.</span><span class="sxs-lookup"><span data-stu-id="24f87-217">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="24f87-218">Anzeigen und eine [Layoutansicht](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="24f87-218">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="24f87-219">Festlegen der  **\<Title >** Elementinhalt in der Layoutansicht aus einer Datei anzeigen.</span><span class="sxs-lookup"><span data-stu-id="24f87-219">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="24f87-220">[Teilansicht](xref:mvc/views/partial) und einer Ansicht</span><span class="sxs-lookup"><span data-stu-id="24f87-220">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="24f87-221">Ein Widget, das Daten basierend auf der Webseite, die vom Benutzer angeforderte anzeigt.</span><span class="sxs-lookup"><span data-stu-id="24f87-221">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="24f87-222">Diese Auflistung kann verwiesen werden, entweder über die `ViewData` oder `ViewBag` Eigenschaften für Controller und Ansichten.</span><span class="sxs-lookup"><span data-stu-id="24f87-222">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="24f87-223">Die `ViewData` Eigenschaft ist ein Wörterbuch von schwach typisierte Objekte.</span><span class="sxs-lookup"><span data-stu-id="24f87-223">The `ViewData` property is a dictionary of weakly-typed objects.</span></span> <span data-ttu-id="24f87-224">Die `ViewBag` Eigenschaft ist ein Wrapper um `ViewData` , dynamische Eigenschaften bereitstellt, für das zugrunde liegende `ViewData` Auflistung.</span><span class="sxs-lookup"><span data-stu-id="24f87-224">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="24f87-225">`ViewData`und `ViewBag` dynamisch zur Laufzeit aufgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="24f87-225">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="24f87-226">Seit der Kompilierung typüberprüfung bieten nicht, sind beide im Allgemeinen mehr als fehleranfällig als die Verwendung einer Viewmodel.</span><span class="sxs-lookup"><span data-stu-id="24f87-226">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="24f87-227">Aus diesem Grund einige Entwickler bevorzugen Minimal oder nie `ViewData` und `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="24f87-227">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>


<a name="VD"></a>

<span data-ttu-id="24f87-228">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="24f87-228">**ViewData**</span></span>

<span data-ttu-id="24f87-229">`ViewData`ist eine [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) Objekt erfolgt über `string` Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="24f87-229">`ViewData` is a [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="24f87-230">Zeichenfolgendaten können gespeichert und ohne die Notwendigkeit einer Typumwandlung direkt verwendet werden, jedoch müssen Sie eine Umwandlung andere `ViewData` Objektwerten auf bestimmte Typen, wenn Sie zu extrahieren.</span><span class="sxs-lookup"><span data-stu-id="24f87-230">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="24f87-231">Sie können `ViewData` übergeben von Daten von Controller mit Ansichten und in Ansichten, einschließlich [Teilansichten](xref:mvc/views/partial) und [Layouts](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="24f87-231">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="24f87-232">Im folgenden ist ein Beispiel, das Werte für einen Gruß und eine Adresse mit `ViewData` in einer Aktion:</span><span class="sxs-lookup"><span data-stu-id="24f87-232">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="24f87-233">Arbeiten Sie mit den Daten in einer Ansicht:</span><span class="sxs-lookup"><span data-stu-id="24f87-233">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

<span data-ttu-id="24f87-234">**ViewBag**</span><span class="sxs-lookup"><span data-stu-id="24f87-234">**ViewBag**</span></span>

<span data-ttu-id="24f87-235">Hinweis: `ViewBag` ist in der Razor-Seiten nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="24f87-235">Note: `ViewBag` is not available in the Razor Pages.</span></span>

<span data-ttu-id="24f87-236">`ViewBag`ist eine [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) -Objekt, das dynamischen Zugriff auf die Objekte, die in gespeicherten `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="24f87-236">`ViewBag` is a [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="24f87-237">`ViewBag`ist besonders angenehm beim besser zu handhaben, da es keine Typumwandlung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="24f87-237">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="24f87-238">Das folgende Beispiel zeigt, wie Sie `ViewBag` dasselbe Ergebnis erzielt als mit `ViewData` oben:</span><span class="sxs-lookup"><span data-stu-id="24f87-238">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="24f87-239">**ViewData und ViewBag gleichzeitig zu verwenden**</span><span class="sxs-lookup"><span data-stu-id="24f87-239">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="24f87-240">Hinweis: `ViewBag` ist in der Razor-Seiten nicht verfügbar.</span><span class="sxs-lookup"><span data-stu-id="24f87-240">Note: `ViewBag` is not available in the Razor Pages.</span></span>

<span data-ttu-id="24f87-241">Da `ViewData` und `ViewBag` finden Sie in den gleichen zugrunde liegende `ViewData` -Auflistung, können Sie beide `ViewData` und `ViewBag` mischen und zwischen ihnen beim Lesen und Schreiben von Werten entsprechen.</span><span class="sxs-lookup"><span data-stu-id="24f87-241">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="24f87-242">Legen Sie den Titel mit `ViewBag` und die Beschreibung mit `ViewData` am oberen Rand einer *About.cshtml* anzeigen:</span><span class="sxs-lookup"><span data-stu-id="24f87-242">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="24f87-243">Lesen der Eigenschaften jedoch die Verwendung von reverse `ViewData` und `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="24f87-243">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="24f87-244">In der *_Layout.cshtml* Datei, rufen Sie den Titel mit `ViewData` und rufen Sie die Beschreibung mit `ViewBag`:</span><span class="sxs-lookup"><span data-stu-id="24f87-244">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="24f87-245">Beachten Sie, dass Zeichenfolgen eine Umwandlung für erfordern `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="24f87-245">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="24f87-246">Sie können `@ViewData["Title"]` ohne Umwandlung.</span><span class="sxs-lookup"><span data-stu-id="24f87-246">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="24f87-247">Mit beiden `ViewData` und `ViewBag` auf die gleiche Uhrzeit funktioniert wie mischen und anpassen, lesen und schreiben die Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="24f87-247">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="24f87-248">Das folgende Markup gerendert wird:</span><span class="sxs-lookup"><span data-stu-id="24f87-248">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="24f87-249">**Zusammenfassung der Unterschiede zwischen ViewData und ViewBag**</span><span class="sxs-lookup"><span data-stu-id="24f87-249">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="24f87-250">`ViewBag`ist nicht verfügbar in der Razor-Seiten.</span><span class="sxs-lookup"><span data-stu-id="24f87-250">`ViewBag` is not available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="24f87-251">Leitet sich von [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), sodass er Wörterbucheigenschaften verfügt, die hilfreich sein, z. B. `ContainsKey`, `Add`, `Remove`, und `Clear`.</span><span class="sxs-lookup"><span data-stu-id="24f87-251">Derives from [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="24f87-252">Schlüssel im Wörterbuch sind Zeichenfolgen, daher Leerzeichen zulässig ist.</span><span class="sxs-lookup"><span data-stu-id="24f87-252">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="24f87-253">Ein Beispiel: `ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="24f87-253">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="24f87-254">Beliebiger Typ außer einem `string` umgewandelt werden muss, in der Ansicht mit `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="24f87-254">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="24f87-255">Leitet sich von [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), daher lässt die Erstellung von dynamischen Eigenschaften, die Verwendung der Punktnotation (`@ViewBag.SomeKey = <value or object>`), und es ist keine Typumwandlung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="24f87-255">Derives from [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="24f87-256">Die Syntax des `ViewBag` ist es schneller, Controller und Ansichten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="24f87-256">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="24f87-257">Einfacher, die null-Werte zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="24f87-257">Simpler to check for null values.</span></span> <span data-ttu-id="24f87-258">Ein Beispiel: `@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="24f87-258">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="24f87-259">**Wann ViewData oder ViewBag verwenden**</span><span class="sxs-lookup"><span data-stu-id="24f87-259">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="24f87-260">Beide `ViewData` und `ViewBag` sind gleichermaßen gültig Ansätze für kleine Mengen von Daten zwischen Controllern und Ansichten übergeben.</span><span class="sxs-lookup"><span data-stu-id="24f87-260">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="24f87-261">Die Wahl des welcher Typ verwendet basiert auf bevorzugt.</span><span class="sxs-lookup"><span data-stu-id="24f87-261">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="24f87-262">Mischen und zuordnen `ViewData` und `ViewBag` Objekte, die Code ist jedoch einfacher zu lesen und zu verwalten, mit der ein Ansatz besteht darin, die konsistent verwendet.</span><span class="sxs-lookup"><span data-stu-id="24f87-262">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="24f87-263">Beide Vorgehensweisen sind dynamisch zur Laufzeit aufgelöst und anfällig für Laufzeitfehler verursachen.</span><span class="sxs-lookup"><span data-stu-id="24f87-263">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="24f87-264">Einige Entwicklungsteams vermeiden.</span><span class="sxs-lookup"><span data-stu-id="24f87-264">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="24f87-265">Dynamische Ansichten</span><span class="sxs-lookup"><span data-stu-id="24f87-265">Dynamic views</span></span>

<span data-ttu-id="24f87-266">Geben Sie Sichten, die ein Modell zu deklarieren, nicht mit `@model` jedoch eine Modellinstanz übergebenen aufweisen (z. B. `return View(Address);`) können die Eigenschaften der Instanz dynamisch verweisen:</span><span class="sxs-lookup"><span data-stu-id="24f87-266">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="24f87-267">Diese Funktion bietet Flexibilität, aber es bietet keine Kompilierung Schutz noch IntelliSense zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="24f87-267">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="24f87-268">Wenn die Eigenschaft nicht vorhanden ist, schlägt die Webseite Generation zur Laufzeit fehl.</span><span class="sxs-lookup"><span data-stu-id="24f87-268">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="24f87-269">Weitere Funktionen</span><span class="sxs-lookup"><span data-stu-id="24f87-269">More view features</span></span>

<span data-ttu-id="24f87-270">[Kennzeichnen von Hilfsprogrammen](xref:mvc/views/tag-helpers/intro) erleichtern das serverseitige Verhalten vorhandenen HTML-Tags hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="24f87-270">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="24f87-271">Verwenden von Tag-Hilfsprogrammen vermeidet die Notwendigkeit zum Schreiben von benutzerdefiniertem Code oder Hilfsprogramme in Ihren Ansichten.</span><span class="sxs-lookup"><span data-stu-id="24f87-271">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="24f87-272">Tag-Hilfsprogrammen, die als Attribute auf HTML-Elemente angewendet werden und von Editoren, die sie nicht verarbeiten können ignoriert werden.</span><span class="sxs-lookup"><span data-stu-id="24f87-272">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="24f87-273">Dadurch können Sie zum Bearbeiten und Rendern von Markup der Sicht in einer Vielzahl von Tools.</span><span class="sxs-lookup"><span data-stu-id="24f87-273">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="24f87-274">Generieren von benutzerdefinierten HTML-Markup kann mit vielen integrierten HTML-Hilfsmethoden erreicht werden.</span><span class="sxs-lookup"><span data-stu-id="24f87-274">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="24f87-275">Komplexere Benutzeroberflächenlogik kann behandelt werden, indem [Ansichtskomponenten](xref:mvc/views/view-components).</span><span class="sxs-lookup"><span data-stu-id="24f87-275">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="24f87-276">Ansichtskomponenten finden Sie die gleichen SoC, Controller und Ansichten bieten.</span><span class="sxs-lookup"><span data-stu-id="24f87-276">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="24f87-277">Sie können angeben, entfällt der Bedarf für Aktionen und Ansichten, die mit Daten, die durch allgemeine Elemente der Benutzeroberfläche verwendet.</span><span class="sxs-lookup"><span data-stu-id="24f87-277">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="24f87-278">Wie viele andere Aspekte von ASP.NET Core Ansichten unterstützen [Abhängigkeitsinjektion](xref:fundamentals/dependency-injection), sodass Dienste sind [in Sichten eingefügt](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="24f87-278">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>