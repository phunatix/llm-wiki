---
title: "Security Operations mit n8n automatisieren"
source: "https://www.heise.de/ratgeber/Security-Operations-mit-n8n-automatisieren-11167335.html?seite=all"
author:
  - "[[Frank Neugebauer]]"
published: 2026-02-24
created: 2026-03-10
description: "Die Workflows und Integrationen sind sehr gut für Security-Routinearbeiten geeignet, aber auch auf andere Themenfelder jenseits der IT-Sicherheit übertragbar."
tags:
  - "clippings"
---
Die Menge an Sicherheitsereignissen, Protokolldaten und Alarmen übersteigt in modernen IT-Infrastrukturen häufig die Kapazitäten für eine manuelle Bearbeitung. Analysten im Security Operations Center (SOC) sehen sich vielen False Positives und repetitiven Aufgaben gegenüber.

Automatisierung schafft Abhilfe: Durch definierte Arbeitsabläufe (Workflows) übernimmt das System Standardaufgaben wie die Anreicherung von Alarmen mit Threat-Intelligence-Daten an das System. Das senkt die Reaktionszeit (Mean Time to Respond) und schafft Freiräume für die Analyse komplexerer Sicherheitsvorfälle.

- n8n automatisiert Security Operations und Incident Response, indem es Standardaufgaben wie Alarmanreicherung delegiert.
- Das Tutorial stellt zwei Workflows vor: Der erste prüft verdächtige IP-Adressen on demand über Shodan, AbuseIPDB, VirusTotal und AlienVault über parallele API-Abfragen und erzeugt einen HTML-Report.
- Der zweite Workflow verarbeitet Alarme eines SIEM (Wazuh) ereignisgesteuert, lässt sie von einem Sprachmodell analysieren und versendet Empfehlungen per E-Mail.
- Die Workflows zeigen, wie man n8n-Nodes nutzt, Credentials verwaltet, Sprachmodelle einbindet und n8n mit Wazuh integriert.

[Nachdem der erste Teil des n8n-Tutorials die Installation und die grundlegende Einrichtung der Plattform gezeigt hat](https://www.heise.de/ratgeber/Prozessautomatisierung-mit-n8n-am-Beispiel-erklaert-11134008.html), widmet sich dieser zweite Teil der praktischen Anwendung im Bereich der IT-Sicherheit. Er stellt zwei konkrete Workflows vor, die typische Szenarien in der Incident Response abbilden und gleichzeitig die Möglichkeiten komplexer Workflows und Integrationen in n8n demonstrieren, die nicht nur für Securityverantwortliche relevant sind.

Ziel im ersten Workflow ist, eine verdächtige IP-Adresse über einen einfachen Webaufruf an mehrere Reputationsdienste zu senden und das Ergebnis in Form einer übersichtlichen HTML-Tabelle im Browser darzustellen. Für eine fundierte Einschätzung der Bedrohungslage werden in diesem Arbeitsablauf vier spezialisierte, einander ergänzende Dienste abgefragt. Jeder dieser Dienste liefert einen spezifischen Blickwinkel auf die potenzielle Bedrohung.

[Shodan](https://shodan.io/) ist eine Suchmaschine für mit dem Internet verbundene Geräte. In der Incident Response dient sie dazu, offene Ports, Bannerinformationen und bekannte Schwachstellen der untersuchten IP-Adresse zu identifizieren. Die [Datenbank AbuseIPDB](https://abuseipdb.com/) sammelt Missbrauchsmeldungen zu IP-Adressen. Ein hoher „Abuse Confidence Score“ deutet darauf hin, dass die IP aktiv für Angriffe, Spam oder Brute-Force-Attacken genutzt wurde. Der Dienst [VirusTotal](https://virustotal.com/) prüft Dateien und URLs durch Dutzende von Antiviren-Engines. Bei IP-Adressen liefert er historische Daten darüber, ob die Adresse mit der Verbreitung von Malware oder schädlichen URLs in Verbindung steht. Schließlich kommt mit [AlienVault](https://otx.alienvault.com/) noch eine Community-basierte Plattform für Threat Intelligence zum Einsatz, um zu prüfen, ob die IP-Adresse in bekannten „Pulses“ (Sammlungen von Indikatoren für Kompromittierungen/IoCs) auftaucht.

Bei der Konzeption des Workflows stand ein didaktischer Ansatz im Vordergrund: Anstatt den minimalistischsten Lösungsweg zu wählen, ist die Struktur bewusst so gestaltet, dass eine möglichst breite Vielfalt an n8n-Komponenten zum Einsatz kommt. Die Kombination von Webhooks, Codeausführung, parallelen API-Abfragen, Datenzusammenführungen (Merge) und HTML-Aufbereitung demonstriert praxisnah das Zusammenspiel der unterschiedlichen Knotentypen. Der so entstandene Workflow prüft somit nicht nur effizient IP-Adressen gegen diverse Threat-Intelligence-Quellen, sondern fungiert gleichzeitig als umfassendes Beispiel für die modulare Logik der n8n-Plattform.

![Der Workflow für den Reputation-Check einer URL demonstriert die Verwendung verschiedener Knotentypen (Abb. 1)., ](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/5/0/2/3/0/9/5/abbildungen_abbildung_1-8996132c59ed6c21.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1220)

Der Workflow für den Reputation-Check einer URL demonstriert die Verwendung verschiedener Knotentypen (Abb. 1).

![Mehr von iX Magazin](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/09/4/8/9/7/9/7/6/ho_markenbanner_desktop_neu_ix2-7dde18964795e578.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=100&width=1256)

Mehr von iX Magazin

Der Workflow verarbeitet die Daten linear von der Eingabe über die Abfrage bis zur Ausgabe über eine Folge von Nodes. Der Startpunkt des Workflows ist ein Webhook-Node, der so konfiguriert ist, dass er HTTP-GET-Anfragen entgegennimmt. Die zu untersuchende IP-Adresse wird als Parameter in der URL übergeben. Der Workflow lässt sich später direkt im Browser aufrufen. Hierbei unterscheidet n8n zwischen zwei Arten von URLs: Eine Test-URL enthält den Pfadbestandteil /test/ und funktioniert nur bei einem im n8n-Editor manuell über „Execute Workflow“ gestarteten Workflow. Sie dient ausschließlich der Entwicklung und Fehlersuche. Nach dem Aktivieren des Workflows über den Schalter Publish ist er über die Production-URL permanent erreichbar. Diese URL ist im operativen Einsatz für Ad-hoc-Abfragen gedacht.

![Webhooks arbeiten immer mit zwei URLs, einer für Tests und einer für den Produktivbetrieb. Letztere wird in der n8n-Oberfläche über den Schalter Publish aktiviert (Abb. 2). , ](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/5/0/2/3/0/9/5/abbildungen_abbildung_2-ef61f8e329b56f95.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1220)

Webhooks arbeiten immer mit zwei URLs, einer für Tests und einer für den Produktivbetrieb. Letztere wird in der n8n-Oberfläche über den Schalter Publish aktiviert (Abb. 2).

Um die Stabilität des Workflows zu gewährleisten, wird die eingehende Anfrage validiert. Ein Code-Node, in Abbildung 1 mit „Valid IP“ bezeichnet, extrahiert die IP-Adresse und bereinigt das Format, um Fehler in den nachfolgenden API-Aufrufen zu vermeiden. Am besten verarbeitet n8n Python- und JavaScript-Code.

![Ein Code-Node extrahiert die IP-Adressen, hier mit regulären Ausdrücken in JavaScript (Abb. 3)., ](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/5/0/2/3/0/9/5/abbildungen_abbildung_3-5c2bc32e47fbcc1e.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1220)

Ein Code-Node extrahiert die IP-Adressen, hier mit regulären Ausdrücken in JavaScript (Abb. 3).

Unmittelbar nach der Validierung der IP-Adresse übernimmt der If-Node die Steuerung des weiteren Ablaufs. An dieser Stelle wertet n8n das Ergebnis der vorherigen Prüfung aus. Die Bedingung ist so konfiguriert, dass der Prozess nur dann im True-Pfad fortgesetzt wird, wenn es sich um eine gültige öffentliche IP-Adresse handelt. Dazu wertet sie den Wert von `valid` im Rückgabewert aus der Abbildung oben aus. Es genügt hier, als Bedingung `{{ $json.valid }}` als True festzulegen. Wird dagegen der False-Pfad beschritten, gibt n8n eine Fehlermeldung aus, die als Webhook-Node angelegt ist.

![Um eine Fehlermeldung auszugeben, ist ein eigener Webhook-Node nötig (Abb. 4)., ](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/5/0/2/3/0/9/5/abbildungen_abbildung_5-e57045155c2c6cba.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1220)

Um eine Fehlermeldung auszugeben, ist ein eigener Webhook-Node nötig (Abb. 4).

Beim Datenabruf per HTTP-Request-Nodes verzweigt sich der Workflow. Für jeden der vier Dienste Shodan, AbuseIPDB, VirusTotal und AlienVault ist ein eigener HTTP-Request-Node nötig. Diese Nodes senden die Anfragen an die jeweiligen REST-APIs. Nahezu alle kommerziellen und Community-basierten Threat-Intelligence-Dienste erfordern einen gültigen API-Schlüssel, um Anfragen zu autorisieren und Limits (Rate Limits) zu verwalten. In n8n stehen zwei Methoden zur Verfügung, um diese sensitiven Zugangsdaten zu verwalten.

Die empfohlene Vorgehensweise ist, die Schlüssel zentral zu verwalten und im n8n-Hauptmenü unter dem Punkt Credentials zu hinterlegen. Hier erhält jeder Dienst einen neuen Eintrag, in dem der API-Key sicher gespeichert wird. Im HTTP-Request-Node muss man anschließend nur noch die entsprechende Credential-Referenz auswählen. Das erhöht nicht nur die Sicherheit, da die Schlüssel nicht im Klartext im Workflow sichtbar sind, sondern erleichtert auch die Wartung: Ändert sich ein Schlüssel, muss man ihn nur an einer zentralen Stelle aktualisieren, damit alle verknüpften Arbeitsabläufe die Änderung automatisch übernehmen. Die Zugangsdaten für den HTTP-Request von AlienVault sind zum Beispiel in der zentralen Verwaltung hinterlegt.

API-Schlüssel sollte man vorzugsweise zentral hinterlegen (Abb. 5).

Alternativ lässt sich die Authentifizierung direkt innerhalb des HTTP-Request-Nodes konfigurieren. Hierbei muss man die erforderlichen Parameter – je nach API-Spezifikation oft als Header-Eintrag, etwa über x-apikey, oder als URL-Parameter – manuell in den Einstellungen des Nodes eintragen. Diese Methode eignet sich vorwiegend für schnelle Tests oder für Dienste, für die n8n noch keinen vordefinierten Credential-Typ anbietet. In diesem Beispiel sind die Zugangsdaten für den HTTP-Request der Shodan-Anfrage direkt in der URL hinterlegt.

Alternativ können Secrets auch als Bestandteil der URL übergeben werden (Abb. 6).

Nachdem die externen Dienste ihre Antworten geliefert haben, liegen die Daten meist als komplexe, tief verschachtelte JSON-Strukturen vor. Diese Rohdaten enthalten oft Metadaten oder technische Details, die für den Endanwender irrelevant sind. Der Edit-Fields-Node übernimmt an dieser Stelle die Aufgabe der Datenbereinigung und -selektion. Am Beispiel des AbuseIPDB-Checks lässt sich dieser Vorgang verdeutlichen.

In Nodes vom Typ Edit Fields lassen sich per Drag and Drop Felder auswählen und zuordnen (Abb. 7).

In der Konfiguration des Nodes definiert man zunächst die gewünschten Zielvariablen. Die Zuordnung der Werte erfolgt in n8n intuitiv über die grafische Oberfläche: Die linke Seite des Editorfensters zeigt die Eingangsdatenstruktur (Input-Schema) des vorangegangenen HTTP-Requests an. Die benötigten Felder – im Falle von AbuseIPDB etwa der Vertrauenswert oder die Anzahl der Reports – wählt man nun individuell aus und zieht sie per Drag-and-drop direkt in das entsprechende Wertefeld auf der rechten Seite. Dieses visuelle Mapping stellt eine feste Verbindung her, sodass der Workflow bei jedem Durchlauf dynamisch den korrekten Wert aus der JSON-Antwort extrahiert und der neu definierten Variablen zuweist. Das Ergebnis ist ein bereinigter Datensatz, der ausschließlich die für die Weiterverarbeitung notwendigen Informationen enthält.

Nachdem die externen Dienste geantwortet haben und die benötigten Felder selektiert wurden, müssen die vier separaten Datenstränge wieder vereint werden. Der Merge-Node wartet auf den Abschluss aller HTTP-Requests und bündelt die JSON-Antworten zu einem einzigen Datensatz. Er benötigt einen Modus, hier Append, und die Anzahl der Inputs, also 4.

Nach dem Merge-Vorgang liegen die Ergebnisse der vier Dienste in n8n standardmäßig als vier separate Items (Datenobjekte) vor. Die n8n-Logik sieht vor, dass nachfolgende Nodes für jedes Item einmal ausgeführt werden. Das würde bedeuten, dass n8n den HTML-Report viermal generiert – jeweils nur mit den Daten eines einzigen Dienstes. Der Aggregate-Node verhindert das. Er fasst die vier einzelnen Datenobjekte zu einer einzigen Liste (Array) innerhalb eines einzigen Items zusammen. Dadurch stehen dem nachfolgenden Node zur HTML-Erstellung alle Informationen (Abuse-Score, Shodan-Ports, VirusTotal-Ergebnis et cetera) gleichzeitig in einem Datensatz zur Verfügung und können in eine gemeinsame Tabelle geschrieben werden. Damit das funktioniert, belegt man in diesem Node das Auswahlfeld Aggregate mit „All Item Data (Into a Single List)“, wählt das Ausgabefeld data und erfasst mit „All Fields“ im Auswahlfeld Include alle Felder.

Der nachfolgende Schritt, die Reportgenerierung, definiert ein HTML-Grundgerüst, das man auch per CSS optisch aufbereiten kann. Die zuvor gesammelten Werte – wie der Abuse Confidence Score, offene Ports oder gefundene Malware-Indikatoren – bettet n8n als dynamische Variablen in dieses statische Gerüst ein. Konkret werden die JSON-Werte in die Zellen einer HTML-Tabelle injiziert.

Dynamische Variablen werden als JSON in ein HTML-Gerüst injiziert, um den Report zu erzeugen (Abb. 8).

Das Ergebnis dieser Operation ist ein einzelner Textstring, der den vollständigen Quellcode der Ergebnisseite enthält. Dieser String wird anschließend an den finalen Node, den Respond-to-Webhook-Node, übergeben, der ihn als HTTP-Antwort an den Browser des Anfragenden ausliefert. Damit entsteht aus den abstrakten API-Daten ein schnell erfassbarer Statusbericht.

Der Respond-to-Webhook-Node wertet $json.html aus, das den HTML-Code der Ergebnisseite enthält (Abb. 9).

Sobald der Workflow vollständig konfiguriert und getestet ist, erfolgt der Wechsel in den operativen Produktivbetrieb. Hierfür aktiviert man den Prozess zunächst über den Schalter Publish in der oberen rechten Ecke der Benutzeroberfläche. Durch diese Umstellung gelangt der Workflow permanent in den Hintergrundprozess des n8n-Servers, sodass er dauerhaft auf Ereignisse lauscht, auch wenn der Editor geschlossen ist. Mit dieser Aktivierung geht zwingend die Verwendung der Production-URL einher, die im Webhook-Node abzurufen ist.

```
https://n8n.fnme.de/webhook/ca7446ce-5cbb-4d5b-a961-60ad66958626/ip-check/195.178.xxx.xx
```

Die beispielhafte URL verdeutlicht den Aufbau eines Webhook-Aufrufs. Nach der Adresse des Servers weist webhook auf einen aktiven Produktionsaufruf hin. Im Gegensatz dazu stünde webhook-test für die Entwicklungsumgebung. Darauf folgt eine eindeutige Identifikationsnummer. Diese automatisch generierte UUID ordnet die Anfrage dem korrekten Workflow zu. ip-check ist ein benutzerdefinierter Pfad zur besseren Lesbarkeit. Abschließend übergibt der Teil 195.178.xxx.xx die zu prüfende IP-Adresse als Parameter an den Workflow. Das Ergebnis der Abfrage stellt der Browser als HTML-Ausgabe dar.

Ein Ausschnitt aus dem formatierten Statusreport in der Browserdarstellung (Abb. 10).

Während Administratoren den ersten Workflow manuell anstoßen müssen, zeigt das zweite Szenario eine ereignisgesteuerte Automatisierung. Hierbei fungiert n8n als Middleware für ein SIEM-System (Security Information and Event Management), in diesem Fall Wazuh. Durch diese Integration gelangen sicherheitskritische Vorfälle ab einem Schweregrad von 10, die das SIEM detektiert, ohne Verzögerung an n8n. Dort kann eine KI anschließend die Alarmdaten analysieren und Vorschläge zur Behandlung des Incidents machen. Das Ergebnis der Analyse schickt das System per E-Mail zur weiteren Bearbeitung an einen Mitarbeiter des SOC.

Eine ereignisgesteuerte Automatisierung integriert das SIEM-System Wazuh (Abb. 11).

Damit Wazuh Alarme an n8n senden kann, muss man die Konfigurationsdatei des Wazuh-Managers anpassen. Zusätzlich sind sogenannte „Custom Integrations“ erforderlich, die die Zusammenarbeit von Wazuh und n8n gewährleisten.

Die Kommunikation mit Wazuh erfolgt über einen Webhook, der JSON-formatierte Daten an die Production-URL des n8n-Workflows übermittelt. Die Einrichtung erfolgt über einen zusätzlichen Integrationsblock in der zentralen Konfigurationsdatei des Wazuh-Managers (typischerweise /var/ossec/etc/ossec.conf). Der XML-Ausschnitt im Listing zeigt die notwendige Konfiguration.

**Listing:** Wazuh-Integration

```
<integration>
  <name>custom-n8n</name>
  <hook_url>https://n8n.fnme.de/webhook/d9f7d5e6-640e-4743-bf36-d4170ebe7d46</hook_url>
  <level>10</level>
  <alert_format>json</alert_format>
</integration>
```

In `<name>custom-n8n\</name>` wird ein eindeutiger Name für die Integration definiert – da n8n nicht standardmäßig in Wazuh mit dem Präfix `custom-` vordefiniert ist. Der wichtigste Parameter ist die von `<hook_url>...\</hook_url>` umschlossene URL. Hier tragen Administratoren die vollständige Production-URL des n8n-Webhooks ein (siehe Erläuterung im vorherigen Abschnitt). Es darf nicht die Test-URL sein, da die Alarme sonst im regulären Betrieb nicht verarbeitet werden.

Der Filter `<level>10\</level>` bestimmt, ab welchem Schweregrad (Severity Level) ein Alarm weitergeleitet wird. Im Beispiel ist der Wert 10 gesetzt. Das bedeutet, dass das System Alarme mit einer niedrigeren Priorität (beispielsweise einfache Login-Informationen) ignoriert, während kritische Ereignisse (ab Level 10) den Workflow auslösen. Das dient der Rauschunterdrückung und verhindert eine Überlastung des Automatisierungssystems. Schließlich legt `<alert_format>json\</alert_format>` fest, dass die Daten als strukturiertes JSON-Objekt übertragen werden, was die Weiterverarbeitung in n8n (Parsing) erleichtert.

Da Wazuh standardmäßig keine native Schnittstelle für n8n bereitstellt, ist dort eine Custom Integration nötig. Sie besteht technisch aus zwei Komponenten, die im Verzeichnis /var/ossec/integrations/ auf dem Wazuh-Server liegen müssen.

Die Datei custom-n8n ist ein Shellskript, das als Einstiegspunkt für den Wazuh-Integrator-Daemon dient. Primär stellt es die korrekte Laufzeitumgebung bereit. Da Wazuh eine eigene, gekapselte Python-Version mitbringt, sorgt dieses Skript dafür, dass für die Ausführung der Logik nicht der Python-Interpreter des Betriebssystems, sondern die interne Wazuh-Umgebung verantwortlich ist. Das verhindert Kompatibilitätsprobleme und stellt sicher, dass alle benötigten Bibliotheken verfügbar sind. Es ermittelt dynamisch die Pfade und übergibt die Ausführung an das eigentliche Python-Skript.

Das Python-Skript custom-n8n.py übernimmt die eigentliche Datenverarbeitung und Kommunikation. Es liest die vom Wazuh-Daemon übergebene Alarmdatei ein und analysiert das JSON-Objekt. Um die Weiterverarbeitung in n8n zu erleichtern, extrahiert das Skript gezielt relevante Felder wie IP-Adressen, Agentennamen oder MITRE-ATT&CK-Informationen und wandelt diese in eine flache Struktur um. Abschließend generiert es die HTTP-POST-Anfrage und sendet die aufbereitete Payload an den konfigurierten n8n-Webhook. Die für die Integration notwendigen Dateien stehen nicht standardmäßig in Wazuh oder n8n zur Verfügung, man muss sie manuell anlegen. [Der Quellcode für das Shellskript sowie das Python-Skript finden sich auf GitHub](https://github.com/eaglefn/wazuh-n8n-workflow.git).

Beide Dateien müssen ausführbar sein und dem Benutzer root sowie der Gruppe wazuh gehören. Nach der Platzierung im Integrationsverzeichnis ist ein Neustart des Wazuh-Managers erforderlich, damit das System die neuen Skripte registriert.

```
chmod 750 /var/ossec/integrations/custom-n8n\*
chown root:wazuh /var/ossec/integrations/custom-n8n\*
systemctl restart wazuh-manager
```

Der Arbeitsablauf folgt einer ereignisgesteuerten Logik. Im Gegensatz zum manuellen Abruf im ersten Beispiel reagiert dieser Workflow automatisch auf eingehende Signale des SIEM-Systems. Der Einstiegspunkt ist erneut ein Webhook-Node, diesmal konfiguriert für die HTTP-Methode POST. Er fungiert als Empfänger für die Datenpakete, die der Wazuh-Manager via Python-Skript schickt.

Die eingehende JSON-Payload enthält den vollständigen Datensatz des Sicherheitsalarms. Der Node „Edit Fields“ ist dafür verantwortlich, die operativ relevanten Schlüsselinformationen zu extrahieren. Er löst Felder wie den Agentennamen, die Regel-ID, die Beschreibung des Vorfalls und den Zeitstempel aus der hierarchischen Struktur und überführt sie in flache Variablen für die Weiterverarbeitung.

Der Edit-Field-Node ist dafür verantwortlich, relevante Schlüsselinformationen zu extrahieren und in eine flache Datenstruktur umzuwandeln (Abb. 12).

Der KI-Agent fungiert als virtueller Analyst. Anstatt die technischen Rohdaten des Wazuh-Alarms (JSON) lediglich weiterzuleiten, analysiert ein Sprachmodell – etwa OpenAI GPT-4o, Google Gemini oder ein lokales Modell via Ollama – den Kontext des Vorfalls. Um das Sprachmodell anzubinden, wählt man im Node „Google Gemini Chat Model“ zunächst das entsprechende API-Credential für die Authentifizierung gegenüber dem Google-Dienst.

Bei der anschließenden Auswahl des Sprachmodells hat sich für zeitkritische Incident-Response-Szenarien die Variante `models/gemini-2.5-flash` bewährt. Sie kombiniert geringe Latenz mit ausreichender Analysefähigkeit. Im Feld Prompt erhält der Agent eine umfangreiche, strukturierte Anweisung, den Sicherheitsvorfall zu bewerten, mögliche Ursachen zu identifizieren und konkrete Handlungsempfehlungen für den Administrator zu formulieren (siehe Prompt). Um zu verhindern, dass der KI-Agent bei gleichen Alarmen mehrfach startet, muss im Reiter Settings die Option „Execute Once“ aktiviert sein.

**Prompt:** Anweisungen zur Bewertung des Vorfalls im HTML-Format (gekürzt)

```
Du bist ein erfahrener SOC-Analyst. Analysiere den folgenden Wazuh-Alarm und ERZEUGE als Ausgabe ausschließlich eine versandfertige HTML-E-Mail (vollständiges <html>-Dokument). Wenn Felder fehlen, setze sie auf "UNKNOWN". Werte dürfen NICHT erfunden werden. Alle dynamischen Inhalte HTML-escapen.

[EXTRACTED_FIELDS]  (liefert echte Werte für die HTML-Ausgabe)
agent_name: {{ $json.body.fields.agent_name }}
...
mitre_id: {{ $json.body.fields.rule_mitre_id }}
mitre_technique: {{ $json.body.fields.rule_mitre_technique }}
mitre_tactic: {{ $json.body.fields.rule_mitre_tactic }}
timestamp_raw: {{ $json.body.alert.predecoder.timestamp }}
raw_log: {{ $json.body.alert.full_log }}

AUFGABE
1) Zeitstempel bestimmen:
   - Primär \`timestamp_raw\` verwenden.
   - Falls leer, Zeitstempel aus \`raw_log\` extrahieren.
   - Zusätzlich ISO-8601 angeben (wenn ableitbar).
2) MITRE ATT&CK (ID, Technik, Taktik) zuordnen.
3) Einschätzen, ob wahrscheinlich ein Angriff vorliegt; kurze Begründung.
4) Schweregrad (low|medium|high) festlegen; kurze Begründung.
5) Konkrete Empfehlungen liefern:
   - Quick Actions (2–5 Sofortmaßnahmen)
   - Investigation (3–7 Prüf-/Jagdschritte)
   - Containment (2–5 Eindämmungsmaßnahmen)
   - Hardening (2–5 nachhaltige Maßnahmen)
6) IOCs sammeln (IPs, User, Hosts), falls vorhanden.

AUSGABEFORMAT (AUSCHLIESSLICH HTML; KEIN zusätzlicher Text, KEINE Code-Fences):
- Vollständiges HTML-Dokument mit <!doctype html>, <html lang="de">, <head><meta charset="utf-8">.
- Ein einspaltiges zentriertes Container-Table (max-Breite ≈ 600px) für breiten Support.
- **Nur inline CSS** in style-Attributen verwenden; keine externen Styles, keine Skripte, keine externen Bilder.
- Struktur:
  * Kopfzeile mit Titel "Wazuh-Alarmanalyse" und Datum/Zeit.
  * Zusammenfassung (Kurzbewertung und Schweregrad).
  * Details (Agent, Source IP, Regel und Beschreibung, MITRE).
  * Handlungsempfehlungen: 4 Listen (Quick Actions, Investigation, Containment, Hardening).
  * IOCs (Liste).
  * Rohlog im <pre> Block (escaped).
- Farbliche Kennzeichnung des Schweregrads über simple inline-Styles (z. B. green/orange/red), ohne komplexe CSS-Features.

BEISPIEL-SKELETT (fülle mit den oben gelieferten Werten):
<!doctype html>
...

<tr><td style="padding:4px 0;color:#6b7280;">Quell-IP</td><td style="padding:4px 0;"><!-- source_ip --></td></tr>
            <tr><td style="padding:4px 0;color:#6b7280;">Regel</td><td style="padding:4px 0;">ID <!-- rule_id -->  <!-- rule_description --></td></tr>
            <tr><td style="padding:4px 0;color:#6b7280;">MITRE</td><td style="padding:4px 0;"><!-- mitre_id --> | <!-- mitre_technique --> | <!-- mitre_tactic --></td></tr>
          </table>

...

<h3 style="margin:20px 0 8px;font:600 14px/1.3 system-ui;">Empfehlungen</h3>
          <p style="margin:0 0 6px;font-weight:600;">Quick Actions</p>
          <ul style="margin:0 0 12px 18px;padding:0;"><!-- LI --></ul>
          <p style="margin:0 0 6px;font-weight:600;">Investigation</p>
          <ul style="margin:0 0 12px 18px;padding:0;"><!-- LI --></ul>
          <p style="margin:0 0 6px;font-weight:600;">Containment</p>
          <ul style="margin:0 0 12px 18px;padding:0;"><!-- LI --></ul>
          <p style="margin:0 0 6px;font-weight:600;">Hardening</p>
          <ul style="margin:0 0 12px 18px;padding:0;"><!-- LI --></ul>
...

</html>
```

Den Abschluss des Workflows bildet die aktive Übermittlung der Analyseergebnisse an das Sicherheitsteam. In diesem Schritt wird der Google-Mail-Node (Gmail) mit den zentral hinterlegten Credentials verwendet, um die vom KI-Agenten generierte Bewertung sowie die technischen Metadaten des Alarms als E-Mail im HTML-Format zu versenden. Im Feld Resource wählt man Message aus, die Message selbst ist der Inhalt von `{{ $json.output }}`.

Um die Funktionsfähigkeit der gesamten Alarmierungskette – vom SIEM-Agenten über den Wazuh-Manager bis hin zur weiteren Verarbeitung in n8n – zu validieren, ist die Durchführung eines kontrollierten Angriffsszenarios erforderlich. Hierfür eignet sich die Distribution Kali Linux, die standardmäßig über eine Reihe von Werkzeugen für Penetrationstests verfügt.

Für die Simulation einer Brute-Force-Attacke auf den SSH-Dienst des überwachten Linux-Servers kommt das Tool Hydra zum Einsatz. Ziel ist es, innerhalb kurzer Zeit eine hohe Anzahl fehlgeschlagener Anmeldeversuche zu generieren, um die entsprechenden Schwellenwerte im Wazuh-Regelwerk zu überschreiten. Der Angriff wird über die Kommandozeile von Kali Linux gestartet, typischerweise wie folgt:

```
cd /usr/share/metasploit-framework/data/wordlists
sudo hydra -I -V -L namelist.txt -P password.lst 192.168.171.125 ssh
```

Den Angriff leitet man ein, indem man Hydra im Verzeichnis mit Wortlisten mit administrativen Rechten startet. Der Aufruf initiiert eine Brute-Force-Attacke gegen den SSH-Dienst der Zieladresse 192.168.171.125. Dabei holt sich Hydra die Benutzernamen aus der Datei namelist.txt für die Passwörter aus password.lst.

Das Resultat der automatisierten Analyse schickt n8n per E-Mail an den zuständigen Administrator oder Operator. Inhaltlich umfasst die Nachricht die vom KI-Agenten generierte Bewertung des Sicherheitsvorfalls mit einer Zusammenfassung, Details zum Angriffsweg sowie konkrete Handlungsempfehlungen für die Absicherung.

Auszug aus der Wazuh-Alarmanalyse mit Handlungsempfehlungen (Abb. 13).

Automatisierungslösungen wie n8n entlasten Security Operations Center signifikant, indem sie repetitive Aufgaben und die initiale Datenanreicherung an das System delegieren. Dennoch stellt die Technik keinen Ersatz für menschliche Expertise dar. Automatisierte Prozesse und KI-gestützte Analysen fungieren als effiziente Assistenzsysteme, jedoch nicht als autonome Entscheidungsträger. Die finale Bewertung komplexer Bedrohungslagen und die kritische Kontrolle der automatisierten Ergebnisse bleiben unverzichtbare Kompetenzen des erfahrenen Sicherheitsanalysten.

([ulw](https://www.heise.de/ratgeber/ "Ulrich Wolf"))

![Frank Neugebauer](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/71/3/6/6/2/6/4/5/0x0_n-abfbe2c3686bbc06.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=672)

Frank Neugebauer

Frank Neugebauer hat als Offizier der Bundeswehr über 25 Jahre auf dem Gebiet der IT-Sicherheit gearbeitet. Seit 2017 ist er im Ruhestand und noch immer als Berater und externer Mitarbeiter tätig.

Push-Nachrichten von heise online abonnieren