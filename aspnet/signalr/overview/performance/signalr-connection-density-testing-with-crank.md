---
uid: signalr/overview/performance/signalr-connection-density-testing-with-crank
title: "SignalR-Verbindung Dichte Testen mit tatsächlich | Microsoft Docs"
author: tfitzmac
description: "SignalR-Verbindung Dichte Testen mit tatsächlich"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/22/2015
ms.topic: article
ms.assetid: 148d9ca7-1af1-44b6-a9fb-91e261b9b463
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/signalr-connection-density-testing-with-crank
msc.type: authoredcontent
ms.openlocfilehash: a3e8fdb47bd80d819358f9c48cd82fd51d6c0400
ms.sourcegitcommit: fe880bf4ed1c8116071c0e47c0babf3623b7f44a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
<a name="signalr-connection-density-testing-with-crank"></a><span data-ttu-id="47d18-103">SignalR-Verbindung Dichte Testen mit tatsächlich</span><span class="sxs-lookup"><span data-stu-id="47d18-103">SignalR Connection Density Testing with Crank</span></span>
====================
<span data-ttu-id="47d18-104">durch [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="47d18-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="47d18-105">Dieser Artikel beschreibt, wie das kommt als Tool zum Testen einer Anwendung mit mehreren simulierten Clients.</span><span class="sxs-lookup"><span data-stu-id="47d18-105">This article describes how to use the Crank tool to test an application with multiple simulated clients.</span></span>


<span data-ttu-id="47d18-106">Sobald die Anwendung in seiner Hostingumgebung (entweder eine Azure Webrolle, IIS oder selbstgehosteten mit Owin) ausgeführt wird, können Sie die Anwendung als Antwort auf eine hohe Verbindung Dichte mit dem Tool tatsächlich testen.</span><span class="sxs-lookup"><span data-stu-id="47d18-106">Once your application is running in its hosting environment (either an Azure web role, IIS, or self-hosted using Owin), you can test application's response to a high level of connection density using the Crank tool.</span></span> <span data-ttu-id="47d18-107">Die Hostingumgebung kann ein Server Internet Information Services (IIS), eine Owin-Host oder ein Azure-Webrolle.</span><span class="sxs-lookup"><span data-stu-id="47d18-107">The hosting environment can be an Internet Information Services (IIS) server, an Owin host, or an Azure web role.</span></span> <span data-ttu-id="47d18-108">(Hinweis: Leistungsindikatoren sind nicht auf Azure App Service Web-Apps verfügbar, damit Sie keine Dichte Verbindungstest Leistungsdaten entnommen werden können.)</span><span class="sxs-lookup"><span data-stu-id="47d18-108">(Note: Performance counters are not available on Azure App Service Web Apps, so you will not be able to get performance data from a connection density test.)</span></span>

<span data-ttu-id="47d18-109">Verbindung Dichte bezieht sich auf die Anzahl gleichzeitiger TCP-Verbindungen, die auf einem Server hergestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="47d18-109">Connection Density refers to the number of simultaneous TCP connections that can be established on a server.</span></span> <span data-ttu-id="47d18-110">Jeder TCP-Verbindung eine eigene Rechenaufwand, und öffnen eine große Anzahl von Verbindungen im Leerlauf werden einen Speicherengpass schließlich zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="47d18-110">Each TCP connection incurs its own overhead, and opening a large number of idle connections will eventually create a memory bottleneck.</span></span>

<span data-ttu-id="47d18-111">[SignalR codebase](https://github.com/signalr/signalr) enthält ein Auslastungstests Tool namens **bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="47d18-111">[The SignalR codebase](https://github.com/signalr/signalr) includes a load-testing tool called **Crank**.</span></span> <span data-ttu-id="47d18-112">Die neueste Version der tatsächlich verwendbaren [der Verzweigung Dev](https://github.com/SignalR/signalr/tree/dev) auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="47d18-112">The latest version of Crank can be found in [the Dev branch](https://github.com/SignalR/signalr/tree/dev) on GitHub.</span></span> <span data-ttu-id="47d18-113">Sie können eine ZIP-Datei Archivieren von der Verzweigung Dev von SignalR codebase herunterladen [hier](https://github.com/SignalR/SignalR/archive/dev.zip).</span><span class="sxs-lookup"><span data-stu-id="47d18-113">You can download a Zip archive of the Dev branch of the SignalR codebase [here](https://github.com/SignalR/SignalR/archive/dev.zip).</span></span>

<span data-ttu-id="47d18-114">Tatsächlich kann zum vollständig der Arbeitsspeicher des Servers stark beanspruchen verwendet werden, um die Gesamtzahl von Verbindungen im Leerlauf auf die Serverhardware möglich zu berechnen.</span><span class="sxs-lookup"><span data-stu-id="47d18-114">Crank may be used to fully saturate the server's memory in order to calculate the total number of idle connections possible on the server hardware.</span></span> <span data-ttu-id="47d18-115">Alternativ können Sie auch tatsächlich für den Auslastungstest den Server unter eine bestimmte Menge an Speicher aufweist, durch verwenden Verbindungen Planungsansicht, bis eine bestimmte Anzahl oder einen bestimmten speicherschwellenwert erreicht ist.</span><span class="sxs-lookup"><span data-stu-id="47d18-115">Alternatively, you may also use Crank to load test the server under a certain amount of memory pressure, by ramping up connections until a specific count or a specific memory threshold is reached.</span></span>

<span data-ttu-id="47d18-116">Beim Testen, ist es wichtig, um remote-Clients zu verwenden, um alle Wettbewerb um Ressourcen (z. B. TCP-Verbindungen und Arbeitsspeicher) zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="47d18-116">When testing, it is important to use remote client(s) to avoid any competition for resources (i.e., TCP connections and memory).</span></span> <span data-ttu-id="47d18-117">Überwachen Sie die Clients, um sicherzustellen, dass sie Engpässe nicht aktiviert werden, die den Server erreichen der vollen Kapazität (Arbeitsspeicher oder CPU) verhindern.</span><span class="sxs-lookup"><span data-stu-id="47d18-117">Monitor the client(s) to ensure that they are not hitting any bottlenecks that may prevent the server from reaching its full capacity (memory or CPU).</span></span> <span data-ttu-id="47d18-118">Sie müssen möglicherweise die Anzahl der Clients zu erhöhen, um vollständig vom Server geladen werden.</span><span class="sxs-lookup"><span data-stu-id="47d18-118">You may need to increase the number of clients in order to fully load the server.</span></span>

### <a name="running-a-connection-density-test"></a><span data-ttu-id="47d18-119">Ausführen eines Tests der Verbindung Dichte</span><span class="sxs-lookup"><span data-stu-id="47d18-119">Running a Connection Density Test</span></span>

<span data-ttu-id="47d18-120">In diesem Abschnitt werden die Schritte zum Ausführen einer Verbindung Dichte-Tests auf einer SignalR-Anwendung beschrieben.</span><span class="sxs-lookup"><span data-stu-id="47d18-120">This section describes the steps needed to run a connection density test on a SignalR application.</span></span>

1. <span data-ttu-id="47d18-121">Herunterladen und erstellen Sie die [Verzweigung Dev von SignalR codebase](https://github.com/SignalR/SignalR/archive/dev.zip).</span><span class="sxs-lookup"><span data-stu-id="47d18-121">Download and build the [Dev branch of the SignalR codebase](https://github.com/SignalR/SignalR/archive/dev.zip).</span></span> <span data-ttu-id="47d18-122">Wechseln Sie in der Eingabeaufforderung zu &lt;Projektverzeichnis&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.</span><span class="sxs-lookup"><span data-stu-id="47d18-122">In a command prompt, navigate to &lt;project directory&gt;\src\Microsoft.AspNet.SignalR.Crank\bin\debug.</span></span>
2. <span data-ttu-id="47d18-123">Bereitstellen Sie Ihre Anwendung in der vorgesehenen Hostingumgebung.</span><span class="sxs-lookup"><span data-stu-id="47d18-123">Deploy your application to its intended hosting environment.</span></span> <span data-ttu-id="47d18-124">Notieren Sie den Endpunkt, den von der Anwendung verwendeten; Beispielsweise ist in der Anwendung in der [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), der Endpunkt ist `http://<yourhost>:8080/signalr`.</span><span class="sxs-lookup"><span data-stu-id="47d18-124">Make a note of the endpoint that your application uses; for example, in the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), the endpoint is `http://<yourhost>:8080/signalr`.</span></span>
3. <span data-ttu-id="47d18-125">Installieren Sie [SignalR-Leistungsindikatoren](signalr-performance.md#perfcounters) auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="47d18-125">Install [SignalR performance counters](signalr-performance.md#perfcounters) on the server.</span></span> <span data-ttu-id="47d18-126">Wenn Ihre Anwendung in Azure ausgeführt wird, finden Sie unter [SignalR-Leistungsindikatoren in einer Azure-Webrolle mithilfe von](using-signalr-performance-counters-in-an-azure-web-role.md).</span><span class="sxs-lookup"><span data-stu-id="47d18-126">If your application is running on Azure, see [Using SignalR Performance Counters in an Azure Web Role](using-signalr-performance-counters-in-an-azure-web-role.md).</span></span>

<span data-ttu-id="47d18-127">Sobald heruntergeladen und erstellt die Codebasis und Leistungsindikatoren auf dem Host installiert haben, kann das Befehlszeilentool "tatsächlich" gefunden werden, der `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` Ordner.</span><span class="sxs-lookup"><span data-stu-id="47d18-127">Once you've downloaded and built the codebase, and installed performance counters on your host, the Crank command-line tool can be found in the `src\Microsoft.AspNet.SignalR.Crank\bin\Debug` folder.</span></span>

<span data-ttu-id="47d18-128">Optionen für das Tool tatsächlich sind verfügbar:</span><span class="sxs-lookup"><span data-stu-id="47d18-128">Available options for the Crank tool include:</span></span>

- <span data-ttu-id="47d18-129">**/?** : Zeigt die Hilfe an.</span><span class="sxs-lookup"><span data-stu-id="47d18-129">**/?**: Shows the help screen.</span></span> <span data-ttu-id="47d18-130">Die verfügbaren Optionen werden auch angezeigt, wenn die **Url** Parameter ausgelassen wird.</span><span class="sxs-lookup"><span data-stu-id="47d18-130">The available options are also displayed if the **Url** parameter is omitted.</span></span>
- <span data-ttu-id="47d18-131">**/ Url**: die URL für SignalR-Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="47d18-131">**/Url**: The URL for SignalR connections.</span></span> <span data-ttu-id="47d18-132">Dieser Parameter ist erforderlich.</span><span class="sxs-lookup"><span data-stu-id="47d18-132">This parameter is required.</span></span> <span data-ttu-id="47d18-133">Der Pfad endet bei Verwendung der standardzuordnung SignalR-Anwendungen "/ Signalr".</span><span class="sxs-lookup"><span data-stu-id="47d18-133">For a SignalR application using the default mapping, the path will end in "/signalr".</span></span>
- <span data-ttu-id="47d18-134">**/ Transport**: der Name des Transports verwendet.</span><span class="sxs-lookup"><span data-stu-id="47d18-134">**/Transport**: The name of the transport used.</span></span> <span data-ttu-id="47d18-135">Die Standardeinstellung ist `auto`, werden die verfügbare Protokoll auswählen.</span><span class="sxs-lookup"><span data-stu-id="47d18-135">The default is `auto`, which will select the best available protocol.</span></span> <span data-ttu-id="47d18-136">Zu den Optionen gehören `WebSockets`, `ServerSentEvents`, und `LongPolling` (`ForeverFrame` ist keine Option für tatsächlich, seit der .NET Client statt Internet Explorer verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="47d18-136">Options include `WebSockets`, `ServerSentEvents`, and `LongPolling` (`ForeverFrame` is not an option for Crank, since the .NET client rather than Internet Explorer is used).</span></span> <span data-ttu-id="47d18-137">Weitere Informationen wie SignalR Transporte auswählt, finden Sie unter [Transporte und Zugriffe](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="47d18-137">For more information on how SignalR selects transports, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>
- <span data-ttu-id="47d18-138">**/ BatchSize**: die Anzahl der Clients, die in jedem Batch hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="47d18-138">**/BatchSize**: The number of clients added in each batch.</span></span> <span data-ttu-id="47d18-139">Der Standardwert ist 50.</span><span class="sxs-lookup"><span data-stu-id="47d18-139">The default is 50.</span></span>
- <span data-ttu-id="47d18-140">**/ ConnectInterval**: das Intervall in Millisekunden zwischen dem Hinzufügen von Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="47d18-140">**/ConnectInterval**: The interval in milliseconds between adding connections.</span></span> <span data-ttu-id="47d18-141">Der Standard ist 500.</span><span class="sxs-lookup"><span data-stu-id="47d18-141">The default is 500.</span></span>
- <span data-ttu-id="47d18-142">**/ Connections**: die Anzahl der Verbindungen verwendet, um die Anwendung Auslastungstest.</span><span class="sxs-lookup"><span data-stu-id="47d18-142">**/Connections**: The number of connections used to load-test the application.</span></span> <span data-ttu-id="47d18-143">Der Standardwert ist 100.000.</span><span class="sxs-lookup"><span data-stu-id="47d18-143">The default is 100,000.</span></span>
- <span data-ttu-id="47d18-144">**/ ConnectTimeout**: das Timeout in Sekunden, bevor der Test wird abgebrochen.</span><span class="sxs-lookup"><span data-stu-id="47d18-144">**/ConnectTimeout**: The timeout in seconds before aborting the test.</span></span> <span data-ttu-id="47d18-145">Der Standardwert ist 300.</span><span class="sxs-lookup"><span data-stu-id="47d18-145">The default is 300.</span></span>
- <span data-ttu-id="47d18-146">**MinServerMBytes**: das Minimum (MB) erreicht.</span><span class="sxs-lookup"><span data-stu-id="47d18-146">**MinServerMBytes**: The minimum server megabytes to reach.</span></span> <span data-ttu-id="47d18-147">Der Standard ist 500.</span><span class="sxs-lookup"><span data-stu-id="47d18-147">The default is 500.</span></span>
- <span data-ttu-id="47d18-148">**SendBytes**: die Größe der Nutzlast in Bytes an den Server gesendet.</span><span class="sxs-lookup"><span data-stu-id="47d18-148">**SendBytes**: The size of the payload sent to the server in bytes.</span></span> <span data-ttu-id="47d18-149">Der Standard ist 0.</span><span class="sxs-lookup"><span data-stu-id="47d18-149">The default is 0.</span></span>
- <span data-ttu-id="47d18-150">**SendInterval**: die Verzögerung in Millisekunden zwischen Nachrichten an den Server.</span><span class="sxs-lookup"><span data-stu-id="47d18-150">**SendInterval**: The delay in milliseconds between messages to the server.</span></span> <span data-ttu-id="47d18-151">Der Standard ist 500.</span><span class="sxs-lookup"><span data-stu-id="47d18-151">The default is 500.</span></span>
- <span data-ttu-id="47d18-152">**SendTimeout**: das Timeout in Millisekunden für Nachrichten an den Server.</span><span class="sxs-lookup"><span data-stu-id="47d18-152">**SendTimeout**: The timeout in milliseconds for messages to the server.</span></span> <span data-ttu-id="47d18-153">Der Standardwert ist 300.</span><span class="sxs-lookup"><span data-stu-id="47d18-153">The default is 300.</span></span>
- <span data-ttu-id="47d18-154">**ControllerUrl**: die Url, in denen ein Client einen Controller-Hub gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="47d18-154">**ControllerUrl**: The Url where one client will host a controller hub.</span></span> <span data-ttu-id="47d18-155">Der Standardwert ist null (kein Domänencontroller-Hub).</span><span class="sxs-lookup"><span data-stu-id="47d18-155">The default is null (no controller hub).</span></span> <span data-ttu-id="47d18-156">Die Controller-Hub wird gestartet, wenn die Sitzung tatsächlich gestartet wird; keine weiteren erfolgt Kontakt zwischen dem Controller Hub und tatsächlich.</span><span class="sxs-lookup"><span data-stu-id="47d18-156">The controller hub is started when the Crank session starts; no further contact between the controller hub and Crank is made.</span></span>
- <span data-ttu-id="47d18-157">**NumClients**: die Anzahl der simulierten Clients auf die Anwendung zugreifen.</span><span class="sxs-lookup"><span data-stu-id="47d18-157">**NumClients**: The number of simulated clients to connect to the application.</span></span> <span data-ttu-id="47d18-158">Der Standardwert ist 1.</span><span class="sxs-lookup"><span data-stu-id="47d18-158">The default is one.</span></span>
- <span data-ttu-id="47d18-159">**LogFile**: der Dateiname für die Protokolldatei für den Testlauf.</span><span class="sxs-lookup"><span data-stu-id="47d18-159">**Logfile**: The filename for the logfile for the test run.</span></span> <span data-ttu-id="47d18-160">Die Standardeinstellung ist `crank.csv`.</span><span class="sxs-lookup"><span data-stu-id="47d18-160">The default is `crank.csv`.</span></span>
- <span data-ttu-id="47d18-161">**SampleInterval**: die Zeit in Millisekunden zwischen Leistungsindikatorsamplings.</span><span class="sxs-lookup"><span data-stu-id="47d18-161">**SampleInterval**: The time in milliseconds between performance counter samples.</span></span> <span data-ttu-id="47d18-162">Der Standard ist 1000.</span><span class="sxs-lookup"><span data-stu-id="47d18-162">The default is 1000.</span></span>
- <span data-ttu-id="47d18-163">**SignalRInstance**: den Instanznamen für die Leistungsindikatoren auf dem Server.</span><span class="sxs-lookup"><span data-stu-id="47d18-163">**SignalRInstance**: The instance name for the performance counters on the server.</span></span> <span data-ttu-id="47d18-164">Die Standardeinstellung ist die Verwendung den Client-Verbindungsstatus.</span><span class="sxs-lookup"><span data-stu-id="47d18-164">The default is to use the client connection state.</span></span>

### <a name="example"></a><span data-ttu-id="47d18-165">Beispiel</span><span class="sxs-lookup"><span data-stu-id="47d18-165">Example</span></span>

<span data-ttu-id="47d18-166">Der folgende Befehl wird eine Site mit dem Testen `pfsignalr` in Azure, die eine Anwendung über Port 8080 mit einem Hub, mit dem Namen "ControllerHub" hostet, unter Verwendung von 100 Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="47d18-166">The following command will test a site called `pfsignalr` on Azure that hosts an application on port 8080 with a hub named "ControllerHub", using 100 connections.</span></span>

`crank /Connections:100 /Url:http://pfsignalr.cloudapp.net:8080/signalr`