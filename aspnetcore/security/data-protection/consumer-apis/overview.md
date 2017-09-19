---
title: "Übersicht über die Consumer-APIs"
author: rick-anderson
description: 
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: f69beb9d-a519-43a8-857c-f6b01886a903
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/overview
ms.openlocfilehash: d23a6ce50eef71f393124b9420f4ba473904d8b4
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/11/2017
---
# <a name="consumer-apis-overview"></a><span data-ttu-id="1aa74-103">Übersicht über die Consumer-APIs</span><span class="sxs-lookup"><span data-stu-id="1aa74-103">Consumer APIs overview</span></span>

<span data-ttu-id="1aa74-104">Die IDataProtectionProvider und IDataProtector sind die grundlegenden Schnittstellen, die über die Consumer der Datenschutzsystem verwenden.</span><span class="sxs-lookup"><span data-stu-id="1aa74-104">The IDataProtectionProvider and IDataProtector interfaces are the basic interfaces through which consumers use the data protection system.</span></span> <span data-ttu-id="1aa74-105">Sie befinden sich die Microsoft.AspNetCore.DataProtection.Abstractions-Paket.</span><span class="sxs-lookup"><span data-stu-id="1aa74-105">They are located in the Microsoft.AspNetCore.DataProtection.Abstractions package.</span></span>

## <a name="idataprotectionprovider"></a><span data-ttu-id="1aa74-106">IDataProtectionProvider</span><span class="sxs-lookup"><span data-stu-id="1aa74-106">IDataProtectionProvider</span></span>

<span data-ttu-id="1aa74-107">Die Provider-Schnittstelle stellt den Stamm der Datenschutzsystem dar.</span><span class="sxs-lookup"><span data-stu-id="1aa74-107">The provider interface represents the root of the data protection system.</span></span> <span data-ttu-id="1aa74-108">Er kann nicht direkt zu schützen oder Aufheben des Schutzes von Daten verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1aa74-108">It cannot directly be used to protect or unprotect data.</span></span> <span data-ttu-id="1aa74-109">Stattdessen muss der Consumer durch Aufrufen von IDataProtectionProvider.CreateProtector(purpose), wobei Zweck eine Zeichenfolge ist, die die beabsichtigte Consumer Anwendungsfall beschreibt einen Verweis auf einen IDataProtector erhalten.</span><span class="sxs-lookup"><span data-stu-id="1aa74-109">Instead, the consumer must get a reference to an IDataProtector by calling IDataProtectionProvider.CreateProtector(purpose), where purpose is a string that describes the intended consumer use case.</span></span> <span data-ttu-id="1aa74-110">Finden Sie unter [Zweck Zeichenfolgen](purpose-strings.md) viel mehr Informationen auf der Absicht dieses Parameters und wie Sie einen geeigneten Wert auswählen.</span><span class="sxs-lookup"><span data-stu-id="1aa74-110">See [Purpose Strings](purpose-strings.md) for much more information on the intent of this parameter and how to choose an appropriate value.</span></span>

## <a name="idataprotector"></a><span data-ttu-id="1aa74-111">IDataProtector</span><span class="sxs-lookup"><span data-stu-id="1aa74-111">IDataProtector</span></span>

<span data-ttu-id="1aa74-112">Die Schutzvorrichtung-Schnittstelle wird durch einen Aufruf von CreateProtector zurückgegeben und kann diese Schnittstelle, über die Consumer ausführen können, schützen und Aufheben des Schutzes von Operations.</span><span class="sxs-lookup"><span data-stu-id="1aa74-112">The protector interface is returned by a call to CreateProtector, and it is this interface which consumers can use to perform protect and unprotect operations.</span></span>

<span data-ttu-id="1aa74-113">Um Daten zu schützen, übergeben Sie die Daten an die Protect-Methode.</span><span class="sxs-lookup"><span data-stu-id="1aa74-113">To protect a piece of data, pass the data to the Protect method.</span></span> <span data-ttu-id="1aa74-114">Die grundlegende Schnittstelle definiert eine Methode an, welche konvertiert Byte [] -> Byte [], aber es gibt auch eine Überladung (angegeben als Erweiterungsmethode einer) der Zeichenfolge konvertiert -> Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="1aa74-114">The basic interface defines a method which converts byte[] -> byte[], but there is also an overload (provided as an extension method) which converts string -> string.</span></span> <span data-ttu-id="1aa74-115">Die Sicherheit durch die beiden Methoden ist identisch. Entwickler sollten auswählen, unabhängig davon, welche Überladung am einfachsten für ihre Verwendungsfall ist.</span><span class="sxs-lookup"><span data-stu-id="1aa74-115">The security offered by the two methods is identical; the developer should choose whichever overload is most convenient for their use case.</span></span> <span data-ttu-id="1aa74-116">Unabhängig von der Überladung gewählt, den Rückgabewert von schützen Methode jetzt geschützt ist (enciphered und manipulationssichere geprüft) und die Anwendung auf einem nicht vertrauenswürdigen Client senden.</span><span class="sxs-lookup"><span data-stu-id="1aa74-116">Irrespective of the overload chosen, the value returned by the Protect method is now protected (enciphered and tamper-proofed), and the application can send it to an untrusted client.</span></span>

<span data-ttu-id="1aa74-117">Übergeben Sie zum Aufheben des Schutzes von einer zuvor geschützten Datenmenge, die geschützten Daten an die Unprotect-Methode.</span><span class="sxs-lookup"><span data-stu-id="1aa74-117">To unprotect a previously-protected piece of data, pass the protected data to the Unprotect method.</span></span> <span data-ttu-id="1aa74-118">(Es gibt Byte []-basiert und zeichenfolgenbasierte Überladungen der Einfachheit halber Developer.) Geschützte Nutzlast durch einen früheren Aufruf von Protect für diese gleichen IDataProtector generiert wurde, gibt die Unprotect-Methode die ursprünglichen ungeschützte Nutzlast zurück.</span><span class="sxs-lookup"><span data-stu-id="1aa74-118">(There are byte[]-based and string-based overloads for developer convenience.) If the protected payload was generated by an earlier call to Protect on this same IDataProtector, the Unprotect method will return the original unprotected payload.</span></span> <span data-ttu-id="1aa74-119">Wenn die geschützte Nutzlast manipuliert wurde oder von einem anderen IDataProtector erzeugt wurde, löst die Unprotect-Methode CryptographicException.</span><span class="sxs-lookup"><span data-stu-id="1aa74-119">If the protected payload has been tampered with or was produced by a different IDataProtector, the Unprotect method will throw CryptographicException.</span></span>

<span data-ttu-id="1aa74-120">Das Konzept der gleiche im Vergleich zu anderen IDataProtector bindet wieder auf das Konzept der Zweck.</span><span class="sxs-lookup"><span data-stu-id="1aa74-120">The concept of same vs. different IDataProtector ties back to the concept of purpose.</span></span> <span data-ttu-id="1aa74-121">Wenn zwei Instanzen von IDataProtector aus demselben Stamm IDataProtectionProvider jedoch über die unterschiedlichen Zweck Zeichenfolgen im Aufruf der IDataProtectionProvider.CreateProtector generiert wurden, werden Sie als [unterschiedliche Schutzvorrichtungen](purpose-strings.md), und eine ist nicht in der Lage sind, Aufheben des Schutzes von Nutzlasten, die von der anderen generiert.</span><span class="sxs-lookup"><span data-stu-id="1aa74-121">If two IDataProtector instances were generated from the same root IDataProtectionProvider but via different purpose strings in the call to IDataProtectionProvider.CreateProtector, then they are considered [different protectors](purpose-strings.md), and one will not be able to unprotect payloads generated by the other.</span></span>

## <a name="consuming-these-interfaces"></a><span data-ttu-id="1aa74-122">Nutzen diese Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="1aa74-122">Consuming these interfaces</span></span>

<span data-ttu-id="1aa74-123">Für eine Komponente DI-fähig ist die beabsichtigte Verwendung an, dass die Komponente einen IDataProtectionProvider-Parameter in seinem Konstruktor annehmen und das System DI automatisch diesen Dienst bereitstellt, wenn die Komponente instanziiert wird.</span><span class="sxs-lookup"><span data-stu-id="1aa74-123">For a DI-aware component, the intended usage is that the component take an IDataProtectionProvider parameter in its constructor and that the DI system automatically provides this service when the component is instantiated.</span></span>

> [!NOTE]
> <span data-ttu-id="1aa74-124">Einige Anwendungen (z. B. konsolenanwendungen oder 4.x ASP.NET-Anwendungen) möglicherweise nicht DI-fähigen daher den Mechanismus beschrieben kann hier verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1aa74-124">Some applications (such as console applications or ASP.NET 4.x applications) might not be DI-aware so cannot use the mechanism described here.</span></span> <span data-ttu-id="1aa74-125">Für diese Szenarien finden Sie in der [nicht bewusst DI-Szenarien](../configuration/non-di-scenarios.md) Dokument für Weitere Informationen zum Abrufen einer Instanz von IDataProtection-Anbieter ohne DI durchlaufen.</span><span class="sxs-lookup"><span data-stu-id="1aa74-125">For these scenarios consult the [Non DI Aware Scenarios](../configuration/non-di-scenarios.md) document for more information on getting an instance of an IDataProtection provider without going through DI.</span></span>

<span data-ttu-id="1aa74-126">Das folgende Beispiel zeigt drei einzelkonzepten:</span><span class="sxs-lookup"><span data-stu-id="1aa74-126">The following sample demonstrates three concepts:</span></span>

1. <span data-ttu-id="1aa74-127">[Hinzufügen der Datenschutzsystem](../configuration/overview.md) dem Dienstcontainer</span><span class="sxs-lookup"><span data-stu-id="1aa74-127">[Adding the data protection system](../configuration/overview.md) to the service container,</span></span>

2. <span data-ttu-id="1aa74-128">Mithilfe der Abhängigkeitsinjektion zum Empfangen von einer Instanz von einem IDataProtectionProvider und</span><span class="sxs-lookup"><span data-stu-id="1aa74-128">Using DI to receive an instance of an IDataProtectionProvider, and</span></span>

3. <span data-ttu-id="1aa74-129">Erstellen einen IDataProtector aus einem IDataProtectionProvider und dazu verwenden, schützen und Aufheben des Schutzes von Daten.</span><span class="sxs-lookup"><span data-stu-id="1aa74-129">Creating an IDataProtector from an IDataProtectionProvider and using it to protect and unprotect data.</span></span>

<span data-ttu-id="1aa74-130">[!code-csharp[Main](../using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]</span><span class="sxs-lookup"><span data-stu-id="1aa74-130">[!code-csharp[Main](../using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]</span></span>

<span data-ttu-id="1aa74-131">Das Paket Microsoft.AspNetCore.DataProtection.Abstractions enthält eine Erweiterungsmethode IServiceProvider.GetDataProtector als Annehmlichkeit Developer.</span><span class="sxs-lookup"><span data-stu-id="1aa74-131">The package Microsoft.AspNetCore.DataProtection.Abstractions contains an extension method IServiceProvider.GetDataProtector as a developer convenience.</span></span> <span data-ttu-id="1aa74-132">Sie kapselt als einzelner Vorgang sowohl eine IDataProtectionProvider vom Dienstanbieter abrufen und IDataProtectionProvider.CreateProtector aufrufen.</span><span class="sxs-lookup"><span data-stu-id="1aa74-132">It encapsulates as a single operation both retrieving an IDataProtectionProvider from the service provider and calling IDataProtectionProvider.CreateProtector.</span></span> <span data-ttu-id="1aa74-133">Das folgende Beispiel veranschaulicht die Verwendung.</span><span class="sxs-lookup"><span data-stu-id="1aa74-133">The following sample demonstrates its usage.</span></span>

<span data-ttu-id="1aa74-134">[!code-csharp[Main](./overview/samples/getdataprotector.cs?highlight=15)]</span><span class="sxs-lookup"><span data-stu-id="1aa74-134">[!code-csharp[Main](./overview/samples/getdataprotector.cs?highlight=15)]</span></span>

>[!TIP]
> <span data-ttu-id="1aa74-135">Instanzen von IDataProtectionProvider und IDataProtector sind threadsicher für mehrere Aufrufer.</span><span class="sxs-lookup"><span data-stu-id="1aa74-135">Instances of IDataProtectionProvider and IDataProtector are thread-safe for multiple callers.</span></span> <span data-ttu-id="1aa74-136">Es richtet sich an, dass nach eine Komponente einen Verweis auf einen IDataProtector über einen Aufruf an CreateProtector abruft, dieser Verweis für mehrere Aufrufe von Protect verwendet wird und Unprotect.A Aufruf Unprotect löst CryptographicException aus, wenn die geschützte Nutzlast nicht möglich nicht überprüft oder entschlüsselt.</span><span class="sxs-lookup"><span data-stu-id="1aa74-136">It is intended that once a component gets a reference to an IDataProtector via a call to CreateProtector, it will use that reference for multiple calls to Protect and Unprotect.A call to Unprotect will throw CryptographicException if the protected payload cannot be verified or deciphered.</span></span> <span data-ttu-id="1aa74-137">Einige Komponenten Fehler ignorieren möchten Aufheben des Schutzes von während der Vorgänge eine Komponente, die Authentifizierungscookies liest möglicherweise diesen Fehler zu behandeln und die Anforderung zu behandeln, als ob es überhaupt kein Cookie hatte anstelle der sofortiges Anforderung schlägt fehl.</span><span class="sxs-lookup"><span data-stu-id="1aa74-137">Some components may wish to ignore errors during unprotect operations; a component which reads authentication cookies might handle this error and treat the request as if it had no cookie at all rather than fail the request outright.</span></span> <span data-ttu-id="1aa74-138">Komponenten, die über dieses Verhalten soll sollten CryptographicException speziell statt Angriffspunkt alle Ausnahmen abfangen.</span><span class="sxs-lookup"><span data-stu-id="1aa74-138">Components which want this behavior should specifically catch CryptographicException instead of swallowing all exceptions.</span></span>