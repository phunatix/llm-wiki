---
title: "Linux Foundation, Google, Anthropic: Wer den Standard für KI-Agenten setzt"
source: https://www.golem.de/news/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt-2603-206812.html
author:
  - "[[Nils Matthiesen]]"
published: 2026-03-24
created: 2026-03-31
description: "MCP, A2A, UCP: Rund um KI-Agenten entsteht eine neue Protokollschicht. Wer sie kontrolliert, bestimmt, wie autonome Systeme mit der Welt interagieren."
tags:
  - clippings
  - golem
  - agentic-ai
---
![Ohne gemeinsame Standards entstehen schnell Insellösungen. (Bild: Bru-nO/Pixabay)](https://www.golem.de/2603/206812-568351-568348.jpg)

Ohne gemeinsame Standards entstehen schnell Insellösungen. Bild: Bru-nO/Pixabay

Inhalt
1. [Linux Foundation, Google, Anthropic: Wer den Standard für KI-Agenten setzt](https://www.golem.de/news/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt-2603-206812.html)
2. [[#Risiko durch versteckte Prompt Injections]]
3. [Wie die Schnittstelle zum Teil der Governance wird](https://www.golem.de/news/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt-2603-206812-3.html)
4. [Die wahre Bewährungsprobe liegt im Betrieb](https://www.golem.de/news/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt-2603-206812-4.html)

*Dieser Golem-Plus-Text ist 24 Stunden frei verfügbar.*

In der klassischen Software-Entwicklung war die Rollenverteilung lange klar. Anwendungen riefen definierte Schnittstellen auf, erhielten strukturierte Antworten und verarbeiteten diese nach festem Schema. Das Modell funktioniert gut, solange die beteiligten Systeme und deren Aufgaben im Voraus bekannt sind.

Doch mit dem Aufstieg agentischer Systeme verändert sich diese Logik. Moderne KI-Agenten beschränken sich nicht mehr auf das Erzeugen von Text, sie greifen auf Werkzeuge zu, behalten interne Zustände im Blick und können Aufgaben an andere Agenten weiterreichen. In einigen Fällen übernehmen sie sogar vorbereitende Schritte für Oberflächen oder Transaktionen.

## Insellösungen vermeiden

An dieser Stelle entsteht eine neue Protokollschicht. Diese legt fest, wie Agenten mit externen Systemen sprechen, welche Fähigkeiten sie ankündigen, wie sie Ergebnisse austauschen und wo Sicherheitsgrenzen verlaufen. Für Unternehmen ist das keine akademische Frage. Fehlen gemeinsame Standards, entstehen schnell Insellösungen mit unklaren Berechtigungen und schwierig nachzuvollziehenden Abhängigkeiten.

Gemeinsame Protokolle erleichtern dagegen die Integration: Agenten lassen sich eher in vorhandene Systeme einfügen, ohne dass für jede Schnittstelle neu gebastelt werden muss.

## Warum MCP derzeit die wichtigste Referenz ist

Am weitesten fortgeschritten ist die Entwicklung aktuell bei der Anbindung externer Werkzeuge und Datenquellen. Das Model Context Protocol – kurz MCP – (modelcontextprotocol.io) beschreibt einen offenen Standard, über den KI-Anwendungen mit externen Systemen verbunden werden können.

In der Praxis bedeutet das: Ein Agent muss nicht mehr für jede Datenbank, jedes Ticketsystem oder jedes Dateiverzeichnis eine eigene proprietäre Integration erhalten. Stattdessen [spricht er mit einem MCP-Server(öffnet im neuen Fenster)](https://github.com/modelcontextprotocol/servers), der Fähigkeiten standardisiert bereitstellt.

MCP ist nicht nur deshalb interessant, weil es den Zugriff auf Werkzeuge vereinheitlicht. Spannend wird es vor allem dort, wo ein Server offenlegt, welche Funktionen überhaupt verfügbar sind. Das macht den Umgang mit einem Agenten deutlich flexibler. Ein Server kann offenlegen, welche Werkzeuge, Ressourcen oder Aktionen verfügbar sind. Ein Agent kann dadurch dynamischer arbeiten, statt nur fest verdrahtete Aufrufe abzufeuern. Diese Abstraktion macht MCP für agentische Systeme attraktiv.

# Risiko durch versteckte Prompt Injections

Führende Anbieter wie Microsoft, AWS und Google haben damit begonnen, MCP-Unterstützung in Teilen ihrer Entwickler-Toolchains zu integrieren. Damit erreicht der Standard die notwendige kritische Masse, um als herstellerübergreifende Schnittstelle ernst genommen zu werden. Dass Anthropic MCP Ende 2025 in die [Agentic AI Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) eingebracht hat, spricht ebenfalls für eine breitere institutionelle Verankerung. Es beendet die technische Debatte aber nicht.

Ein mögliches Angriffsszenario zeigt das Problem: Ein Angreifer platziert eine versteckte Prompt Injection in einer E-Mail. Ein lokaler Agent verarbeitet die Nachricht und ruft daraufhin über einen MCP-Server ein vermeintlich harmloses Diagnosewerkzeug auf.

Wenn dieses Werkzeug unzureichend isoliert ist, kann Schadcode mit den Rechten des Nutzers ausgeführt werden. Da der Datenverkehr lokal bleibt, greifen klassische Netzwerkschutzmechanismen unter Umständen nicht.

## Implementierung mit zu großen Freiheiten

MCP ist allerdings nicht unsicher, weil das Protokoll an sich problematisch wäre. [Risiken entstehen](https://owasp.org/www-project-top-10-for-large-language-model-applications/) vor allem dann, wenn eine Implementierung zu große Freiheiten bekommt, Werkzeuge nicht sauber voneinander getrennt sind oder ein Agent durch manipulierte Eingaben zu ungewollten Aktionen verleitet wird.

[Prompt Injection](https://www.anthropic.com/engineering/code-execution-with-mcp), zu weitreichende Tool-Berechtigungen und unzureichend abgeschottete Laufzeitumgebungen sind auch deshalb nicht bloß Detailfragen, sondern entscheiden maßgeblich über die Sicherheit jeder MCP-Integration.

## Warum minimalistische Ansätze relevant bleiben

Parallel zu MCP gibt es Gegenentwürfe, die bewusst weniger Abstraktion vorsehen. Dazu zählt das [Universal Tool Calling Protocol (UTCP)](https://github.com/universal-tool-calling-protocol), das auf möglichst direkte und einfache Tool-Aufrufe setzt.

Das Argument dahinter ist nachvollziehbar: Je weniger Vermittlungsschichten ein System besitzt, desto einfacher lässt sich dessen Verhalten analysieren und desto geringer fällt unter Umständen die operative Komplexität aus. Ganz so eindeutig ist die Sachlage jedoch nicht. Denn weniger Abstraktion reduziert nicht automatisch die Angriffsfläche. Auch direkte Tool-Protokolle müssen Authentifizierung, Rechtebegrenzung, Eingabevalidierung und Fehlerbehandlung sauber lösen.

Der eigentliche Unterschied liegt daher weniger in sicher gegen unsicher als in der Architekturfrage: Soll ein Agent mit einem reichhaltigen, entdeckbaren Werkzeugraum arbeiten oder mit bewusst schmalen, klar begrenzten Aufrufen?

## Multi-Agenten-Systeme: Wenn ein Agent nicht reicht

Sobald Aufgaben komplexer werden, stößt das Modell des einzelnen Allzweckagenten schnell an Grenzen. Recherche, Planung, Ausführung, Kontrolle und Dokumentation lassen sich oft besser auf mehrere spezialisierte Einheiten verteilen. Dafür entstehen Protokolle zur Agent-zu-Agent-Kommunikation.

A2A – Agent2Agent – ist in dem Zusammenhang ein wichtiger Referenzpunkt. Das Protokoll soll es Agenten ermöglichen, Fähigkeiten zu beschreiben, Aufgaben zu übergeben und Zustände standardisiert zurückzumelden.

In Unternehmensumgebungen ist das relevant, weil sich so verteilte Agentenketten über Systemgrenzen hinweg koordinieren lassen, ohne dass jede Plattform eine eigene Integrationslogik mitbringt.

## Identität, Vertrauen, Beobachtbarkeit

Google hatte A2A im Jahr 2025 vorgestellt, später wurde das Projekt in die Linux-Foundation-Struktur eingebettet. Dort lief auch eine [Konsolidierung mit ACP](https://www.ibm.com/think/topics/agent2agent-protocol), das offiziell in A2A aufgegangen ist.

Damit aus der A2A-Spezifikation tragfähige Infrastruktur entsteht, braucht es mehr als reine Nachrichtenformate. Zentral sind Regeln für Identität, Vertrauen und Beobachtbarkeit.

Wer darf wen aufrufen? Welche Nachweise liefert ein Agent für seine Fähigkeiten? Wie kann nachvollzogen werden, warum eine Aufgabe scheitert oder an welchem Zwischenstand sie hängen bleibt? An den Punkten zeigt sich, ob eine Spezifikation praxistauglich ist.

## Wenn Agenten nicht nur antworten

Ein zweiter Bereich mit viel Bewegung betrifft dynamische Benutzeroberflächen. Klassische Chatfenster reichen für viele Aufgaben nicht mehr aus. Bei der Reiseplanung, dem Produktvergleich oder der Einholung von Freigaben sind strukturierte Eingaben, Zustandswechsel und interaktive Elemente vorteilhaft.

[A2UI](https://github.com/google/A2UI) verfolgt diesen Ansatz. Das Projekt von Google soll Agenten befähigen, strukturierte, aktualisierbare Oberflächen zu beschreiben, die Clients anschließend rendern können.

[AG-UI](https://docs.ag-ui.com/introduction) setzt einen anderen Schwerpunkt. Dort steht eine ereignisbasierte Verbindung zwischen Frontend und agentischem Backend im Mittelpunkt. Beide Ansätze adressieren ähnliche Probleme, aber aus unterschiedlicher Perspektive.

# Wie die Schnittstelle zum Teil der Governance wird

A2UI beschreibt stärker die UI-Repräsentation, AG-UI stärker das bidirektionale Laufzeitverhalten zwischen Anwendung und Agent. Beide Projekte sind zwar relevant, haben aber noch nicht den Entwicklungsstand von MCP erreicht.

Für Unternehmen ist das trotzdem schon heute wichtig. Die Frage lautet nicht länger, welches Modell antwortet. Es geht ebenfalls darum, wie eine Anwendung Nutzer sicher durch einen agentischen Ablauf führt. Sobald ein Agent Eingaben strukturiert abfragt, Ergebnisse schrittweise aktualisiert oder Freigaben anfordert, wird die Schnittstelle zum Teil der Governance.

## Warum Commerce und Payments eine eigene Schicht brauchen

Sobald Agenten nicht nur recherchieren, sondern im Auftrag von Nutzern oder Unternehmen handeln sollen, reicht klassische Tool-Interoperabilität nicht aus. Dann geht es um Verfügbarkeiten, Warenkörbe, Bezahlvorgänge, Limits und Haftungsfragen.

Anders ausgedrückt: Die größte Hürde für den produktiven Einsatz im E-Commerce ist Vertrauen. Ein Agent, der autonom einkauft, benötigt Zugangsdaten und ein hartes Regelwerk.

Frühe Experimente zeigten die Gefahr: Ohne Kontrolle akzeptierten Agenten aufgrund von Halluzinationen [absurde Preise oder verschenken sogar Geld](https://www.golem.de/news/claude-agent-ki-automat-verschenkt-waren-fuer-hunderte-dollar-2512-203439.html). In dem Bereich entstehen derzeit mit UCP und AP2 die wohl spannendsten und gleichsam unreifsten Bausteine der Protokollschicht.

## Agentische Systeme werden zu handelnden Akteuren

UCP, das [Universal Commerce Protocol](https://developers.google.com/merchant/ucp), soll eine gemeinsame Sprache für agentische Handelsabläufe liefern. Shopify und Google positionieren es als offenen Standard, mit dem Produktsuche, Angebotsdarstellung, Checkout-Prozesse und die Anbindung bestehender Handelsinfrastruktur standardisiert werden können.

[AP2, das Agent Payments Protocol](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol), ergänzt diese Ebene um Regeln für sichere und nachvollziehbare Zahlungen. Ziel ist eine gemeinsame Sprache für autorisierte, auditierbare und kompatible Transaktionen zwischen Agenten, Händlern und Zahlungsanbietern.

Beide Protokolle sind strategisch relevant, weil sie ein zentrales Problem adressieren: Ein Agent darf nicht einfach nur technisch zahlen können. Er muss Zahlungen innerhalb klarer Grenzen ausführen, Verantwortlichkeiten dokumentieren und Freigaben in kontrollierbare Abläufe einbetten.

Noch ist offen, wie breit sich solche Standards jenseits erster Partnerökosysteme durchsetzen. Deren Erscheinen zeigt aber, wohin sich agentische Systeme entwickeln: weg vom reinen Assistenten, hin zu handelnden Softwareakteuren.

So wichtig offene Standards sind, so rasch verleiten sie zu einem Missverständnis. Ein standardisiertes Protokoll allein macht ein System noch nicht kontrollierbar. Im Gegenteil: Je einfacher es für Agenten wird, externe Werkzeuge, Oberflächen oder Zahlungen einzubinden, desto mehr gewinnen Punkte wie Isolation, Rechtekonzepte und menschliche Freigaben an Bedeutung.

Für den produktiven Einsatz bedeutet das: Werkzeuge brauchen klar definierte Berechtigungen, Laufzeitumgebungen müssen isoliert werden, kritische Aktionen gehören hinter explizite Freigaben, und jede relevante Interaktion muss beobachtbar bleiben.

Unternehmen, die agentische Systeme einführen, sollten deshalb nicht mit der Modellwahl beginnen, sondern mit einer Inventur ihrer Systeme und Rechte. Erst wenn klar ist, welche Datenquellen, Werkzeuge und Prozesse überhaupt geöffnet werden dürfen, lässt sich sinnvoll entscheiden, welche Protokolle im jeweiligen Umfeld tragfähig sind.

## Frameworks sind nicht dasselbe wie Protokolle

In der Diskussion geht häufig unter, dass Frameworks und Protokolle unterschiedliche Aufgaben erfüllen. Frameworks wie [Langchain](https://docs.langchain.com/oss/python/integrations/tools/mcp_toolbox), Autogen oder Crew AI helfen bei der Entwicklung und Orchestrierung agentischer Anwendungen. Protokolle wie MCP oder A2A definieren dagegen, wie diese Anwendungen mit der Außenwelt interoperabel kommunizieren.

Für Unternehmen ist diese Trennung strategisch wichtig. Wer sich intern an ein bestimmtes Framework bindet, geht zunächst eine Entwicklungsentscheidung ein. Wer sich extern an ein Protokoll bindet, legt fest, wie offen oder anschlussfähig das eigene System nach außen bleibt. Beides sollte nicht vermischt werden.

## Fazit

Rund um KI-Agenten bildet sich gerade eine neue Infrastruktur-Schicht. Deren Zweck ist nicht, Modelle zu ersetzen, sondern deren Handlungsfähigkeit kontrollierbar zu machen.

MCP hat sich beim Werkzeugzugriff als wichtigster Bezugspunkt etabliert. A2A adressiert die Zusammenarbeit mehrerer Agenten. A2UI und AG-UI zeigen, wie sich dynamische Oberflächen standardisieren lassen. Und UCP und AP2 markieren den Versuch, auch Commerce und Payments in eine interoperable Form zu bringen.

Ob daraus ein stabiler Stack entsteht, ist offen. Deutlich wird vor allem eines: Der Wettbewerb dreht sich längst nicht mehr allein um die Modelle. Entscheidend sind zunehmend die Protokolle, Berechtigungen und Sicherheitsgrenzen, über die sich diese Modelle mit der realen Welt verbinden.

_Nils Matthiesen schreibt als freier Mitarbeiter über Technik, KI-Werkzeuge und digitale Alltagshelfer. Ein Schwerpunkt seiner Arbeit liegt auf Smartwatches, Drohnen, Actioncams und anderen vernetzten Geräten. Seit mehr als 25 Jahren arbeitet er als Technikjournalist und legt Wert auf verständliche Einordnung, kritische Tests und klaren Praxisbezug._

_**Dieser Artikel erscheint bei Golem Plus, weil ...**_  
... er nicht nur neue Protokolle aufzählt, sondern einordnet, welche technischen und strategischen Folgen diese Standards für Unternehmen haben. Er zeigt, warum sich der Wettbewerb bei KI-Agenten längst nicht mehr nur auf Modelle konzentriert, sondern auf die Schnittstellen, Regeln und Machtstrukturen dahinter.