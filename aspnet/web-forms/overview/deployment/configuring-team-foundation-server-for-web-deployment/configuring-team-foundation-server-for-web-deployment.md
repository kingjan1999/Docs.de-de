---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: "Konfigurieren von Team Foundation Server für Web Deploy | Microsoft Docs"
author: jrjlee
description: "In diesem Lernprogramm wird gezeigt, wie zum Konfigurieren von Team Foundation Server (TFS) 2010 zum Erstellen von Lösungen und Webinhalte auf verschiedenen zielumgebungen bereitstellen. Dies..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 72f60841a1381380c0ea6167077420f960180dc7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2017
---
<a name="configuring-team-foundation-server-for-web-deployment"></a><span data-ttu-id="0110f-104">Konfigurieren von Team Foundation Server für die Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="0110f-104">Configuring Team Foundation Server for Web Deployment</span></span>
====================
<span data-ttu-id="0110f-105">durch [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="0110f-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="0110f-106">PDF herunterladen</span><span class="sxs-lookup"><span data-stu-id="0110f-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="0110f-107">In diesem Lernprogramm wird gezeigt, wie zum Konfigurieren von Team Foundation Server (TFS) 2010 zum Erstellen von Lösungen und Webinhalte auf verschiedenen zielumgebungen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="0110f-107">This tutorial will show you how to configure Team Foundation Server (TFS) 2010 to build solutions and deploy web content to various target environments.</span></span> <span data-ttu-id="0110f-108">Dies schließt die fortlaufende Integration (CI)-Szenarien, in der Sie Inhalt automatisch bereitstellen jedes Mal, wenn ein Entwickler eine Änderung vornimmt.</span><span class="sxs-lookup"><span data-stu-id="0110f-108">This includes continuous integration (CI) scenarios, where you deploy content automatically every time a developer makes a change.</span></span> <span data-ttu-id="0110f-109">Er kann auch manuelle triggerszenarios enthalten, in denen Bereitstellung eines bestimmten Builds in einer Stagingumgebung auslösen, nachdem der Build wurde überprüft und validiert, in der testumgebung für ein Administrator möchte kann.</span><span class="sxs-lookup"><span data-stu-id="0110f-109">It can also include manual trigger scenarios, where an administrator may want to trigger deployment of a specific build to a staging environment once the build has been verified and validated in the test environment.</span></span> <span data-ttu-id="0110f-110">Die Themen in diesem Lernprogramm führt Sie durch den gesamten Konfigurationsprozess, einschließlich:</span><span class="sxs-lookup"><span data-stu-id="0110f-110">The topics in this tutorial will guide you through the entire configuration process, including:</span></span>
> 
> - <span data-ttu-id="0110f-111">Vorgehensweise: Erstellen Sie ein neues Teamprojekt in TFS.</span><span class="sxs-lookup"><span data-stu-id="0110f-111">How to create a new team project in TFS.</span></span>
> - <span data-ttu-id="0110f-112">Das Hinzufügen von Inhalt zur quellcodeverwaltung.</span><span class="sxs-lookup"><span data-stu-id="0110f-112">How to add content to source control.</span></span>
> - <span data-ttu-id="0110f-113">Wie Sie einen Build-Server zur Unterstützung von CI und Bereitstellung konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="0110f-113">How to configure a build server to support CI and deployment.</span></span>
> - <span data-ttu-id="0110f-114">Wie Sie eine Builddefinition erstellen, die Bereitstellung Logik enthält.</span><span class="sxs-lookup"><span data-stu-id="0110f-114">How to create a build definition that includes deployment logic.</span></span>
> - <span data-ttu-id="0110f-115">Gewusst wie: Konfigurieren von Berechtigungen für die automatisierte Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="0110f-115">How to configure permissions for automated deployment.</span></span>
> 
> <span data-ttu-id="0110f-116">Für einen italienischen Übersetzung mit diesen Lernprogrammen, besuchen Sie [http://www.lucamorelli.it](http://www.lucamorelli.it).</span><span class="sxs-lookup"><span data-stu-id="0110f-116">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="0110f-117">In diesem Lernprogramm wird davon ausgegangen, dass Sie TFS 2010 installiert und eine Teamprojektsammlung im Rahmen der Erstkonfiguration erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="0110f-117">This tutorial assumes that you have installed TFS 2010 and created a team project collection as part of the initial configuration process.</span></span> <span data-ttu-id="0110f-118">Die [Team Foundation-Installationshandbuch für Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) enthält umfassende Anleitungen zu diesen Aufgaben.</span><span class="sxs-lookup"><span data-stu-id="0110f-118">The [Team Foundation Installation Guide for Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) provides comprehensive guidance on these tasks.</span></span>

## <a name="context"></a><span data-ttu-id="0110f-119">Kontext</span><span class="sxs-lookup"><span data-stu-id="0110f-119">Context</span></span>

<span data-ttu-id="0110f-120">Dies ist Teil einer Reihe von Lernprogrammen, die basierend auf den Anforderungen des Enterprise-Bereitstellung eines fiktiven Unternehmens mit dem Namen Fabrikam, Inc. Diese Reihe von Lernprogrammen verwendet eine Beispielprojektmappe & #x 2014; die [Vorgesetzten Kontakts](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) Lösung & #x 2014; zum Darstellen einer Webanwendung mit einer realistischen Maß an Komplexität, einschließlich einer ASP.NET MVC 3-Anwendung, eine Windows Communication Foundation (WCF)-Dienst, und ein Datenbankprojekt.</span><span class="sxs-lookup"><span data-stu-id="0110f-120">This forms part of a series of tutorials based on the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="0110f-121">Die Bereitstellungsmethode das Herzstück mit diesen Lernprogrammen basiert auf der Teilung Datei Herangehensweise beschrieben [Verständnis des Build-Prozesses](../web-deployment-in-the-enterprise/understanding-the-build-process.md), in dem durch der Buildprozess gesteuert wird Projekt zwei Dateien & #x 2014; enthält Erstellen Sie für jede zielumgebung und enthält umgebungsspezifische Einstellungen für Build- und Bereitstellungsprozess geltenden Anweisungen, an.</span><span class="sxs-lookup"><span data-stu-id="0110f-121">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="0110f-122">Zur Buildzeit ist die Unabhängigkeit von der Umgebung-Projektdatei, einen vollständigen Satz von Buildanweisungen bilden die Projektdatei umgebungsspezifische zusammengeführt.</span><span class="sxs-lookup"><span data-stu-id="0110f-122">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="0110f-123">Übersicht über das Szenario</span><span class="sxs-lookup"><span data-stu-id="0110f-123">Scenario Overview</span></span>

<span data-ttu-id="0110f-124">Das allgemeine Szenario für diesen Lernprogrammen wird beschrieben, [Web Unternehmensbereitstellung: Szenarioübersicht](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-124">The high-level scenario for these tutorials is described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span></span> <span data-ttu-id="0110f-125">Es wird empfohlen, dass Sie in diesem Thema behandelt, bevor Sie auf diesem Lernprogramm beginnen.</span><span class="sxs-lookup"><span data-stu-id="0110f-125">We recommend that you review this topic before you get started on this tutorial.</span></span>

## <a name="how-to-use-this-tutorial"></a><span data-ttu-id="0110f-126">Verwendung dieses Tutorials</span><span class="sxs-lookup"><span data-stu-id="0110f-126">How to Use This Tutorial</span></span>

<span data-ttu-id="0110f-127">Wenn dies das erste Mal ist haben Sie die in diesem Lernprogramm beschriebenen Aufgaben ausgeführt, oder wenn Sie die Beispiele zur Verwendung der Beispielprojektmappe folgen soll, sollten Sie über die Lernprogrammthemen in Reihenfolge arbeiten.</span><span class="sxs-lookup"><span data-stu-id="0110f-127">If this is the first time you've performed the tasks described in this tutorial, or if you want to follow the examples using the sample solution, you should work through the tutorial topics in order.</span></span> <span data-ttu-id="0110f-128">Alternativ können Sie einzelne Themen als Leitfaden für bestimmte Aufgaben verwenden.</span><span class="sxs-lookup"><span data-stu-id="0110f-128">Alternatively, you can use individual topics as guidance for specific tasks.</span></span> <span data-ttu-id="0110f-129">Dieses Lernprogramm umfasst die folgenden Themen:</span><span class="sxs-lookup"><span data-stu-id="0110f-129">This tutorial includes these topics:</span></span>

- <span data-ttu-id="0110f-130">[Erstellen ein Teamprojekt in TFS](creating-a-team-project-in-tfs.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-130">[Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span> <span data-ttu-id="0110f-131">Ein Teamprojekt wird die grundlegende Einheit für die quellcodeverwaltung, Prozessmanagement und Builds in TFS.</span><span class="sxs-lookup"><span data-stu-id="0110f-131">A team project is the core unit for source control, process management, and build in TFS.</span></span> <span data-ttu-id="0110f-132">Sie müssen ein Teamprojekt erstellen, bevor Sie Inhalt an Datenquellen-Steuerelement, oder erstellen Sie Builddefinitionen hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="0110f-132">You need to create a team project before you can add content to source control or create build definitions.</span></span>
- <span data-ttu-id="0110f-133">[Hinzufügen von Inhalt zur Quellcodeverwaltung](adding-content-to-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-133">[Adding Content to Source Control](adding-content-to-source-control.md).</span></span> <span data-ttu-id="0110f-134">Wenn Sie ein Teamprojekt erstellt haben, können Sie beginnen, Hinzufügen von Inhalt zur quellcodeverwaltung.</span><span class="sxs-lookup"><span data-stu-id="0110f-134">Once you've created a team project, you can start adding content to source control.</span></span> <span data-ttu-id="0110f-135">Sie müssen die Projekte und Projektmappen, zusammen mit etwaigen externe Abhängigkeiten hinzufügen, bevor Sie Builds konfigurieren können.</span><span class="sxs-lookup"><span data-stu-id="0110f-135">You'll need to add your projects and solutions, together with any external dependencies, before you can start configuring builds.</span></span>
- <span data-ttu-id="0110f-136">[Konfigurieren eine TFS-Buildserver für Webbereitstellung](configuring-a-tfs-build-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-136">[Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span> <span data-ttu-id="0110f-137">Wenn Sie Ihrem Team projizieren von Inhalten erstellen möchten, müssen Sie einen Buildserver zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="0110f-137">If you want to build your team project content, you'll need to configure a build server.</span></span> <span data-ttu-id="0110f-138">In den meisten Fällen sollte dies auf einem separaten Computer aus der TFS-Installation.</span><span class="sxs-lookup"><span data-stu-id="0110f-138">In most cases, this should be on a separate machine from your TFS installation.</span></span> <span data-ttu-id="0110f-139">Um einem Build-Server zu konfigurieren, müssen Sie installieren und Konfigurieren des TFS-Build-Diensts, Visual Studio 2010, erstellen Buildcontroller und build-Agents, Produkte oder Komponenten, die Ihren Code benötigt, um erfolgreich erstellt und installiert die Internetinformationsdienste (IIS) Web Webbereitstellungstool (Web Deploy).</span><span class="sxs-lookup"><span data-stu-id="0110f-139">To configure a build server, you need to install and configure the TFS build service, install Visual Studio 2010, create build controllers and build agents, install any products or components that your code needs in order to build successfully, and install the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="0110f-140">[Erstellen einer Builddefinition, unterstützt die Bereitstellung von](creating-a-build-definition-that-supports-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-140">[Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="0110f-141">Bevor Sie beginnen können, queuing oder Builds in TFS auslösen, müssen Sie mindestens eine Builddefinition für das Teamprojekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0110f-141">Before you can start queuing or triggering builds in TFS, you need to create at least one build definition for your team project.</span></span> <span data-ttu-id="0110f-142">Die Builddefinition definiert jeden Aspekt des Builds, einschließlich, was in den Build enthalten sein soll, wodurch den Build ausgelöst werden soll und, in denen die Ausgaben des builddebugvorgangs Team Build senden soll.</span><span class="sxs-lookup"><span data-stu-id="0110f-142">The build definition defines every aspect of the build, including which things should be included in the build, what should trigger the build, and where Team Build should send the build outputs.</span></span> <span data-ttu-id="0110f-143">Sie können eine Builddefinition zum Ausführen von benutzerdefinierter Microsoft Build Engine (MSBuild)-Projektdateien, konfigurieren, die Bereitstellung Logik in automatisierten Builds enthalten können.</span><span class="sxs-lookup"><span data-stu-id="0110f-143">You can configure a build definition to run custom Microsoft Build Engine (MSBuild) project files, which lets you include deployment logic in your automated builds.</span></span>
- <span data-ttu-id="0110f-144">[Bereitstellen von einem bestimmten Build](deploying-a-specific-build.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-144">[Deploying a Specific Build](deploying-a-specific-build.md).</span></span> <span data-ttu-id="0110f-145">In einer Vielzahl von Szenarien sollten Sie den neuesten Build, statt einen bestimmten Build in einer zielumgebung bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="0110f-145">In a lot of scenarios, you'll want to deploy a specific build, rather than the latest build, to a target environment.</span></span> <span data-ttu-id="0110f-146">In diesem Fall können Sie eine Builddefinition konfigurieren, die Inhalte von einem bestimmten Ablageordner bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="0110f-146">In this case, you can configure a build definition that deploys content from a specific drop folder.</span></span>
- <span data-ttu-id="0110f-147">[Konfigurieren von Berechtigungen für Team Build-Bereitstellung](configuring-permissions-for-team-build-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-147">[Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span> <span data-ttu-id="0110f-148">Wenn der Builddienst zum Bereitstellen von Inhalt im Rahmen einer automatisierten Build ist, müssen Sie das Build-Dienstkonto auf einem beliebigen Ziel-Webserver und Datenbankserver verschiedene Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="0110f-148">If the build service is to deploy content as part of an automated build process, you need to grant various permissions to the build service account on any destination web servers and database servers.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="0110f-149">Schlüsseltechnologien</span><span class="sxs-lookup"><span data-stu-id="0110f-149">Key Technologies</span></span>

<span data-ttu-id="0110f-150">Dieses Lernprogramm konzentriert sich auf wie dieser Produkte und Technologien verwenden, um automatisierte Build- und Web Deploy zu unterstützen:</span><span class="sxs-lookup"><span data-stu-id="0110f-150">This tutorial focuses on how to use these products and technologies to support automated build and web deployment:</span></span>

- <span data-ttu-id="0110f-151">Visual Studio Team Foundation Server 2010</span><span class="sxs-lookup"><span data-stu-id="0110f-151">Visual Studio Team Foundation Server 2010</span></span>
- <span data-ttu-id="0110f-152">Teambuild und MSBuild</span><span class="sxs-lookup"><span data-stu-id="0110f-152">Team Build and MSBuild</span></span>
- <span data-ttu-id="0110f-153">Web Deploy</span><span class="sxs-lookup"><span data-stu-id="0110f-153">Web Deploy</span></span>

<span data-ttu-id="0110f-154">Das Lernprogramm erwähnt auch die Verwendung von Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0 und ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="0110f-154">The tutorial also touches on the use of Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="0110f-155">Weitere Lernprogramme in dieser Serie</span><span class="sxs-lookup"><span data-stu-id="0110f-155">Other Tutorials in This Series</span></span>

<span data-ttu-id="0110f-156">Dies bildet einen Teil einer Reihe von fünf Lernprogramme auf Unternehmensebene zur Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="0110f-156">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="0110f-157">Dies sind die anderen Lernprogramme in der Reihe:</span><span class="sxs-lookup"><span data-stu-id="0110f-157">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="0110f-158">[Bereitstellen von Webanwendungen in Enterprise-Szenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-158">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="0110f-159">Diese einführenden Inhalt enthält kontextbezogenen Hintergrund für die Reihe von Lernprogrammen.</span><span class="sxs-lookup"><span data-stu-id="0110f-159">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="0110f-160">Das Szenario des Lernprogramme beschrieben und veranschaulicht, wie die Aufgaben und exemplarische Vorgehensweisen beschrieben, die in der gesamten Reihe in einen größeren Application Lifecycle Management (ALM) Prozess passen.</span><span class="sxs-lookup"><span data-stu-id="0110f-160">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="0110f-161">[Die webbereitstellung im Unternehmen](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-161">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="0110f-162">Dieses Lernprogramm enthält eine grundlegende Einführung in MSBuild-Projektdateien, die Publishing Web Pipeline (WPP), Web Deploy und anderen verwandten Technologien.</span><span class="sxs-lookup"><span data-stu-id="0110f-162">This tutorial provides a conceptual introduction to MSBuild project files, the Web Publishing Pipeline (WPP), Web Deploy, and other related technologies.</span></span> <span data-ttu-id="0110f-163">Es wird erläutert, wie diese Tools gemeinsam verwendet werden können, um komplexe-bereitstellungstechnologien zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="0110f-163">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="0110f-164">[Konfigurieren von Serverumgebungen für die Bereitstellung](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-164">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="0110f-165">In diesem Lernprogramm beschreibt, wie Windows-Servern zum unterstützen verschiedene Bereitstellungsszenarien, einschließlich remote-Web-paketbereitstellung mithilfe der Webbereitstellungs-Agent-Dienst (der remote-Agent) oder Bereitstellen von Web-Handler und die Bereitstellung des Remotezugriffs zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="0110f-165">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the remote agent) or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="0110f-166">Sie erhalten Anweisungen zum Auswählen der geeigneten Bereitstellungsmethode für Ihre Umgebung, und es wird beschrieben, wie der Web Farm Framework (WFF) verwenden, um bereitgestellter Webanwendungen über alle Webserver in einer Serverfarm zu replizieren.</span><span class="sxs-lookup"><span data-stu-id="0110f-166">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the Web Farm Framework (WFF) to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="0110f-167">[Erweiterte Web Unternehmensbereitstellung](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0110f-167">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="0110f-168">In diesem Lernprogramm wird beschrieben, wie verschiedene erweiterte Bereitstellung, wie Datenbank-Bereitstellungen für mehrere Umgebungen anpassen, Ausschließen von Dateien und Ordner von der Bereitstellung und offline-Webanwendungen, die während des Bereitstellungsvorgangs Aufgaben .</span><span class="sxs-lookup"><span data-stu-id="0110f-168">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="0110f-169">Nächste</span><span class="sxs-lookup"><span data-stu-id="0110f-169">Next</span></span>](creating-a-team-project-in-tfs.md)