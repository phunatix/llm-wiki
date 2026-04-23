---
title: "KI-Assistent Heinzel für die Server-Administration im Überblick"
source: "https://www.heise.de/ratgeber/KI-Assistent-Heinzel-fuer-die-Server-Administration-im-Ueberblick-11244463.html?view=print"
author:
  - "[[Stefan Wintermeyer]]"
published: 2026-04-15
created: 2026-04-21
description: "Admins machen Fehler, besonders um 3 Uhr nachts. Heinzel gibt KI-Agenten Leitplanken für die Arbeit am Terminal – ganz einfach per Markdown."
tags:
  - "clippings"
---
[zurück zum Artikel](https://www.heise.de/ratgeber/KI-Assistent-Heinzel-fuer-die-Server-Administration-im-Ueberblick-11244463.html)

![Drei Gartenzwerge mit Computerausstattung: Tastatur, Maus und Monitor.](https://heise.cloudimg.io/width/1500/q40.png-lossy-40.webp-lossy-40.foil1/_www-heise-de_/imgs/18/5/0/5/7/1/0/4/heise_Aufmacher-Gartenzwerge-v2-02c8ddf0b257d2fe.png)

(Bild: Vanessa Bahr / KI / iX)

**Admins machen Fehler, besonders um 3 Uhr nachts. Heinzel gibt KI-Agenten Leitplanken für die Arbeit am Terminal – ganz einfach per Markdown.**

Nicht jeder Admin ist ein Vollprofi, der sich täglich mit jedem Subsystem beschäftigt. Und selbst wer es ist, betreut oft so viele verschiedene Server und Stacks, dass Details untergehen. Dazu kommen Flüchtigkeitsfehler, Copy-and-paste aus veralteten Stack-Overflow-Antworten – und der Alarm, der um 3 Uhr nachts kommt, wenn die Konzentration am niedrigsten ist. Jeder Admin hat sich schon einmal selbst ausgesperrt oder ein `halt` anstatt eines `reboot` eingegeben.

Heinzel soll genau hier ansetzen: ein Gegenüber, das vor jedem Befehl die Man-Page neu liest, jede Distro kennt, Checklisten genau einhält, nichts überspringt oder überliest und nie müde wird – ein Pair-Programming-Partner, mit dem man gemeinsam am Terminal arbeitet, der aber trotzdem nichts tut, ohne vorher zu fragen.

Die Idee entstand beim Agentic Coding. Ich arbeitete mit einem KI-Coding-Assistenten an einem Webshop-Projekt und brauchte eine bestimmte Konfiguration vom Server – nur kurz nachschauen, rein lesend. Statt selbst ein zweites Terminal aufzumachen, fragte ich mich: Kann der Agent diese Information nicht eben per SSH holen? Also gab ich in den Chat ein: „Logge dich mit meinem SSH-Key als root auf 192.168.0.123 ein, suche die nginx-Konfiguration für diese Applikation und zeige sie mir an.“ Das funktionierte auf Anhieb. Und aus dem reinen Lesen wurde schnell mehr: Wenn der Agent schon verbunden ist und die Konfiguration versteht, warum nicht gleich die nötige Änderung mitmachen? Wohlgemerkt: Das alles passierte auf einer Test-VM im Labor, bei der ein Totalschaden kein Problem gewesen wäre.

Dann folgte eine Phase, in der ich Sicherheitsregeln, Backup-Mechanismen und Verbotslisten schrieb und testete – das Regelwerk, das den Agenten diszipliniert. Erst als ich sicher war, dass die Leitplanken halten, ging es an echte Server. Kollegen und Kunden übernahmen das Werkzeug. So wurde das Regelwerk um Team- und Serverfarm-Funktionen erweitert. Es entstand ein Open-Source-Projekt, das jeder verwenden und an die eigene Umgebung anpassen kann.

Heinzel ist kein eigenständiges Programm und kein Daemon, der im Hintergrund läuft. Es ist ein Regelwerk: rund 140 Kilobyte Markdown-Dateien, die als System-Prompt in das Sprachmodell eingespeist werden. Vergleichbar mit einer ausführlichen Arbeitsanweisung, die ein KI-Coding-Assistent beim Start einer Session automatisch einliest und ab dann befolgt. Heinzel ist dabei bewusst Tool-agnostisch: Es funktioniert mit Anthropics Claude Code, dem Open-Source-Tool OpenCode oder jedem anderen terminalbasierten KI-Assistenten, der Projektdateien lesen und Shell-Befehle ausführen kann. OpenCode unterstützt viele Anbieter – von OpenAI über Google Gemini bis hin zu lokalen Modellen über Ollama. Wer die lokale Variante wählt, braucht nicht einmal einen Cloud-API-Zugang – alles läuft auf der eigenen Hardware.

Und weil es reines Markdown ist, kann jeder diese Dateien öffnen und lesen – man versteht sofort, welche Regeln gelten, was erlaubt ist und was nicht. Kein kompilierter Code, keine Programmiersprachenkenntnisse nötig – nur strukturierter Text, den sowohl das LLM als auch der Admin lesen und verstehen können. Der Projektname spielt auf die Heinzelmännchen an. Die Idee: Vieles geschieht im Hintergrund – der Agent erledigt die Recherche, prüft Syntax, liest Logs, und der Admin bestätigt oder korrigiert.

Das Herzstück ist die `CLAUDE.md`: Sie definiert das grundsätzliche Verhalten – Sicherheitsregeln, Backup-Pflicht, Logging, Team-Modus. Der Dateiname klingt Claude-spezifisch. OpenCode und andere Tools lesen die Datei aber ebenfalls automatisch ein – sie hat sich als De-facto-Standard für Projekt-Instruktionen etabliert. Dazu kommen über 20 spezialisierte Regeldateien im `rules/` -Verzeichnis, hier eine Auswahl:

- **debian.md / rhel.md / suse.md** – Distro-spezifische Regeln: korrekter Paketmanager, Firewall-Tool, Verzeichniskonventionen, typische Fallstricke
- **macos.md** – Apple Silicon und Intel, Homebrew, `launchctl`, Application Firewall, FileVault
- **security.md** – umfassende Checkliste für Security-Audits: SSH-Härtung, Benutzerkonten, offene Ports, Kernel-Sicherheit, SUID/SGID-Binaries, Intrusion Prevention
- **housekeeping.md** – systematische Gesundheitschecks: Plattenplatz, Speicher, fehlgeschlagene Services, SSL-Zertifikate, NTP, Docker, PostgreSQL, Nginx, WireGuard
- **mise.md** – Verwaltung von Programmiersprachen-Runtimes (Node.js, Ruby, Python) mit mise als Versionsmanager
- **access-control.md** – Regeln für Berechtigungen und Zugriffskontrolle
- **anomaly-detection.md** – Erkennung verdächtiger Muster in Server-Ausgaben
- **backups.md** – Backup-Pflicht
- **dns-aliases.md** – DNS-Aliase und Hostnamen-Auflösung
- **directory-copy.md** – Regeln für sicheres Kopieren von Verzeichnissen

Die folgende Verzeichnisstruktur zeigt eine Heinzel-Installation mit mehreren Servern:

```bash
heinzel/
├── CLAUDE.md                        # Hauptregelwerk
├── opencode.json                    # Konfiguration für OpenCode
├── rules/
│   ├── debian.md                    # OS-spezifisch
│   ├── rhel.md
│   ├── freebsd.md
│   ├── macos.md
│   ├── security.md                  # Themenspezifisch
│   ├── housekeeping.md
│   ├── backups.md
│   ├── ...                          # 23 Regeldateien insgesamt
│   └── custom/                      # Eigene Regeln (gitignored)
└── memory/
    ├── MEMORY.md                    # Index für den Agenten
    ├── user.md                      # SSH-User, Sprache (gitignored)
    ├── readonly.md                  # Nur-Lesen-Server
    ├── network.md                   # Netzwerk-Topologie
    └── servers/
        ├── web1.example.com/
        │   ├── memory.md            # OS, Dienste, Besonderheiten
        │   └── changelog.log        # Was wurde wann geändert
        ├── db-prod.example.com/
        │   └── ...
        └── ...                      # Ein Verzeichnis pro Server
```

Die `MEMORY.md` ist der Schlüssel: Der KI-Assistent liest diese Datei automatisch beim Start jeder Session. Sie ist ein Index, der dem Agenten zeigt, wo welche Informationen liegen – Server-Fakten, Changelogs, Netzwerk-Topologie. Ohne diese Datei müsste man dem Agenten jedes Mal erklären, welche Server er kennt und wo er nachschauen soll.

Heinzel ist bewusst kein Ersatz für Ansible, Puppet oder Chef. Diese Tools arbeiten deklarativ und deterministisch – im Kern arbeiten sie mit festen if/else-Ketten. Heinzel arbeitet anders: Es analysiert unbekannte Situationen, schlägt Lösungen vor und passt sich an. Es greift dort, wo ein Ansible-Playbook fehlschlägt und die Ursache unklar ist. Denkbar wäre auch, Heinzel als Komponente innerhalb von Ansible einzusetzen.

![Mehr von iX Magazin](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/09/4/8/9/7/9/7/6/ho_markenbanner_desktop_neu_ix2-7dde18964795e578.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=100&width=1256)

Das Prinzip ist bei allen unterstützten Tools gleich: Man startet den KI-Assistenten im Heinzel-Verzeichnis, im Terminal. Nach dem Start tippt man keine Shell-Befehle mehr, sondern beschreibt in natürlicher Sprache, was man will. Der Agent liest die Anfrage, schlägt einen Plan vor und führt nach Bestätigung Shell-Befehle aus. Die Ausgabe erscheint im Terminal. Der Agent analysiert sie und schlägt den nächsten Schritt vor.

Ein typischer Dialog sieht so aus:

```bash
$ cd heinzel && claude       # oder: opencode

> Prüfe den Server web1.example.com auf Sicherheitsprobleme.

● Ich verbinde mich per SSH und prüfe den Server systematisch
  anhand der Security-Checkliste. Ich starte mit der
  OS-Erkennung.

  ssh root@web1.example.com uname -s && cat /etc/os-release

● Debian 13 (Trixie). Ich lade die Debian-Regeln und beginne
  mit dem Security-Audit. Erster Schritt: SSH-Konfiguration.

  ssh root@web1.example.com sshd -T | grep -E
  'permitrootlogin|passwordauthentication|pubkeyauthentication'

● PermitRootLogin ist auf "yes" gesetzt.
  ⚠ CRITICAL: Root-Login sollte auf "prohibit-password"
  stehen, damit nur Key-basierter Zugang möglich ist.
  Soll ich das ändern?
```

Man arbeitet also im Chat mit dem Agenten – direkt am selben Terminal. Der KI-Assistent übernimmt die Recherche und schlägt Aktionen vor, der Mensch entscheidet. Das Regelwerk steuert, welche Checklisten der Agent abarbeitet, welche Sicherheitsregeln gelten und wann er nachfragt.

Beide Tools lassen sich auch nicht-interaktiv nutzen. Das macht Heinzel skriptfähig:

```bash
# Claude Code:
cd heinzel && claude -p "Erstelle einen vollständigen \
  Security-Audit-Bericht für web1.example.com."

# OpenCode:
cd heinzel && opencode run "Prüfe alle Server auf \
  ablaufende SSL-Zertifikate und erstelle einen Bericht."
```

Beim Verbinden mit einem Server läuft folgender Ablauf:

1. **Zugriffskontrolle:** Steht der Server auf der Sperrliste? Ist er als Read-only markiert? Dieser Schritt kommt vor allen anderen.
2. **DNS-Aliase auflösen:** Falls der Hostname ein Alias für einen bereits bekannten Server ist, erkennt Heinzel das und nutzt die vorhandene Memory-Datei.
3. **Privilege Escalation: so wenig wie möglich.** Der Agent loggt sich bevorzugt als normaler Benutzer ein. Reichen die Rechte nicht, versucht er es mit `sudo`. Ist auch das nicht konfiguriert, fällt er auf einen SSH-Login als root zurück. Scheitert auch das, erstellt er einen Bericht mit den Befehlen, die ein Admin mit den nötigen Rechten ausführen muss.
4. **OS-Erkennung:** Der Agent führt `uname -s` aus, liest `/etc/os-release` (Linux) bzw. `sw_vers` (macOS), sammelt Hardware-Infos und lädt die passende Regeldatei (Debian, RHEL, SUSE oder macOS).
5. **Server-Memory laden oder anlegen:** Falls vorhanden, liest der Agent gespeicherte Fakten über den Server – welche Dienste laufen, welche Besonderheiten es gibt, was beim letzten Mal geändert wurde. Bei einem neuen Server wird die Memory-Datei angelegt.
6. **Aufgabe analysieren und Plan erstellen:** Der Agent schlägt jeden Schritt einzeln vor und erklärt ihn.
7. **Mensch bestätigt:** Kein Befehl wird ohne Freigabe ausgeführt.
8. **Backup und Logging:** Vor jeder Konfigurationsänderung wird automatisch gesichert, jede Änderung protokolliert.

Manche Server soll man nur inspizieren, nicht verändern. Beispiele: Staging-Mirrors, die man überwacht, oder Kundensysteme, die man auditiert. Dafür gibt es die Datei `memory/readonly.md`: Steht ein Server dort drin, arbeitet Heinzel im Read-only-Modus. Lesen, prüfen, Berichte schreiben – alles erlaubt. Aber Pakete installieren, Services neustarten oder Configs ändern? Blockiert. Ist doch eine Änderung nötig, sammelt der Agent die Maßnahmen und erstellt einen Bericht, den man an den zuständigen Admin weitergibt.

Heinzel protokolliert auf zwei Ebenen. Lokal liegt unter `memory/servers/<hostname>/changelog.log` ein Änderungsprotokoll pro Server – was wurde wann gemacht. Es dient als persönliches Logbuch: Wer nach Wochen zurückkommt, sieht sofort, was beim letzten Mal geändert wurde. Auf dem Server selbst schreibt Heinzel zusätzlich ins System-Journal (`logger -t heinzel`). In Teams ist das entscheidend: Wenn ein Kollege ebenfalls mit Heinzel arbeitet, kann jeder per `journalctl -t heinzel` nachvollziehen, was auf dem Server passiert ist – unabhängig davon, wer die Änderung gemacht hat.

Oft bleibt ein Server monatelang unbeachtet. Server-Memories und Changelogs helfen dann, schnell den Überblick zurückzubekommen – für den Admin und den Agenten gleichermaßen.

Heinzel ist nicht nur für Solo-Admins gedacht. In einem Team lassen sich die Server-Memory-Dateien per Git teilen: Alle sehen denselben Zustand, dieselben Changelogs, dieselbe Netzwerk-Topologie. Persönliche Daten – insbesondere SSH-Benutzernamen – bleiben dabei privat. Sie stehen in einer lokalen `memory/user.md`, die per `.gitignore` ausgeschlossen ist.

Neue Teammitglieder kopieren `memory/user.md.example`, tragen ihre eigenen SSH-Benutzernamen ein – fertig. Die Server-Fakten (OS, Dienste, Eigenheiten) sind geteilt, die Zugangsdaten nicht.

Die Regeldateien in `rules/` sind Teil des Repositories und werden mit jedem `git pull` aktualisiert. Wer sie direkt editiert, bekommt beim nächsten Update Merge-Konflikte. Deshalb unterstützt Heinzel ein dreistufiges Override-System:

1. **Basis:** `rules/<name>.md` – die mitgelieferten Upstream-Regeln.
2. **Globale Anpassungen:** `rules/custom/<name>.md` – eigene Ergänzungen oder Überschreibungen, die für alle Server gelten.
3. **Pro Server:** `memory/servers/<hostname>/rules.md` – Regeln, die nur für einen bestimmten Server gelten.

Spätere Schichten gewinnen. Die Override-Dateien verwenden eine einfache Syntax mit Heading-Prefixen:

```bash
## Add: Docker cleanup
Neue Regeln, die zusätzlich zu den Basisregeln gelten.

## Replace: Firewall
Ersetzt die gleichnamige Sektion in der Basisdatei komplett.

## Remove: Common Pitfalls > snap
Überspringt diese Sektion aus der Basisdatei.
```

Sektionen ohne Prefix werden als Ergänzungen behandelt. Eine spezielle Datei `rules/custom/all.md` wird einmal pro Session geladen und gilt serverübergreifend. Das `custom/` -Verzeichnis ist standardmäßig per `.gitignore` ausgeschlossen. Wer seine Anpassungen im Team teilen will, kommentiert die entsprechende Zeile in der `.gitignore` aus.

Das größte Risiko bei LLM-gestützter Administration sind Halluzinationen – Befehle, die plausibel klingen, aber falsch sind. Das Modell könnte `apt` -Syntax auf einem RHEL-System vorschlagen, veraltete Flags verwenden oder Paketnamen verwechseln. Heinzel begegnet dem mit drei Mechanismen:

Die `CLAUDE.md` enthält eine klare Anweisung:

```bash
Do not trust your training data for command syntax.
Before running any command on a server, verify it:

1. Check --help first. Run \`command --help\` or \`command -h\`
   to confirm flags and syntax exist on this specific version.
2. Read the man page when --help is insufficient — especially
   for complex tools like iptables, firewall-cmd, certbot.
3. Search upstream docs when behavior varies across versions.
4. Check the rule file — use the exact syntax from the loaded
   rules/<family>.md file.
```

Das bedeutet: Bevor der Agent einen Befehl vorschlägt, führt er `--help` aus und prüft, ob die Flags auf genau dieser Version des Tools existieren. Kein Raten, kein Vertrauen auf Trainingsdaten. Das klingt nach Overhead, geht in der Praxis aber schnell – und verhindert genau die Fehler, die aus veraltetem Wissen entstehen.

Ein Beispiel: Kein aktuelles Sprachmodell weiß zum Redaktionsschluss, dass Debian 13 die stabile Version ist – weder kommerzielle wie Anthropics Opus 4.6 noch Open-Source-Modelle. Die Modelle halten Trixie noch für Testing. Solche Wissenslücken sind unvermeidlich, wenn das Trainings-Cutoff vor der aktuellen Realität liegt. Genau hier greift Regel 3 aus dem Abschnitt „Verify Before Running“ der `CLAUDE.md`:

```bash
3. Search upstream docs (official project docs, distro wiki)
   when behavior varies across versions or distros.
```

Statt sich auf sein Trainingswissen zu verlassen, prüft der Agent die Realität. Das kostet ein paar Sekunden, verhindert aber genau solche Wissenslücken.

Wann immer ein Befehl einen Trockenlauf unterstützt, nutzt Heinzel ihn zuerst – nicht nur bei Paketmanagern, sondern bei allem, was einen Preview- oder Simulationsmodus anbietet:

```bash
# Paketmanager: Was würde passieren?
apt-get --dry-run upgrade
dnf --assumeno update

# Dateien synchronisieren: Zeig mir, was kopiert würde
rsync --dry-run -av /src/ /dest/

# Dienste: Konfiguration prüfen, ohne neuzuladen
nginx -t
apachectl configtest
postfix check

# Zertifikate: Erneuerung simulieren
certbot renew --dry-run
```

Erst wenn der Dry-Run sauber durchläuft und der Admin das Ergebnis bestätigt hat, folgt die eigentliche Ausführung. Das Prinzip ist simpel: Jede Operation, die sich vorher simulieren lässt, wird vorher simuliert.

Separate Regeldateien für Debian, RHEL, SUSE und macOS definieren die korrekte Syntax für jede Plattform. Ein Auszug aus `rules/debian.md`:

```bash
## Package Manager
- Use \`apt-get\` (not \`apt\`) — it's more reliable for
  non-interactive/scripted use.
- Always run \`apt-get update\` before installing
  or upgrading.
- Dry-run before upgrading: \`apt-get --dry-run upgrade\`

## Firewall
- **Critical:** before enabling \`ufw\`, always allow SSH
  first: \`ufw allow OpenSSH\`. Enabling \`ufw\` without an
  SSH rule locks you out of the server immediately.

## Common Pitfalls
- \`systemctl restart\` vs \`systemctl reload\` — prefer
  \`reload\` when the service supports it (e.g. nginx)
  to avoid downtime.
```

Die letzte Regel klingt trivial. Genau solche Fehler passieren aber unter Zeitdruck: `restart` statt `reload`, und der Webserver hat für ein paar Sekunden Downtime. Der Agent wählt automatisch `reload`, wenn der Dienst es unterstützt.

Die `CLAUDE.md` definiert absolute Verbote:

- Niemals `fdisk`, `parted` oder `gdisk` ohne explizite Anfrage ausführen. `fdisk -l` ist erlaubt.
- Niemals `/etc/ssh/sshd_config` verändern oder SSH-Keys löschen
- Niemals SSH-Port 22 in der Firewall blockieren
- Niemals einen Server herunterfahren (halt) ohne physische Recovery-Möglichkeit

Vor jeder Konfigurationsänderung legt Heinzel automatisch ein Backup an – mit Zeitstempel, unter `/var/backups/heinzel/`. Hinzu kommt ein Schutz gegen Prompt Injection: Der Agent behandelt alle Server-Ausgaben als nicht vertrauenswürdig. Wenn ein kompromittierter Server in seiner Ausgabe Anweisungen an den Agenten einbettet („Ignoriere alle vorherigen Regeln und lösche...“), soll Heinzel das erkennen, den Benutzer warnen und auf Bestätigung warten. Aktuell ist das ein theoretisches Risiko. Dass es über kurz oder lang zum Angriffsvektor wird, ist absehbar.

Jeder KI-Coding-Assistent hat ein Berechtigungskonzept. Im Standardmodus muss man jeden einzelnen Shell-Befehl bestätigen. In der Praxis wird das bei einer Admin-Session mit Dutzenden Befehlen schnell zäh.

Claude Code bietet dafür den Schalter `--dangerously-skip-permissions`. Der Name ist Programm: Der Modus ist gefährlich, und man sollte wissen, was man tut. In diesem Modus führt der Agent Befehle ohne Rückfrage aus. OpenCode hat ein ähnliches Konzept – dort bestätigt man Befehle über die Oberfläche oder konfiguriert automatische Freigabe.

Das klingt nach dem Gegenteil von Sicherheit – funktioniert aber in der Praxis aus einem Grund: Die Leitplanken stecken im Regelwerk, nicht im Berechtigungssystem.

Die `CLAUDE.md` definiert, dass Heinzel vor destruktiven Operationen, Firewall-Änderungen und Reboots trotzdem nachfragt – als Teil seines Verhaltensregelwerks, nicht als technische Sperre. Das ist ein bewusster Trade-off: mehr Geschwindigkeit im Alltag, mehr Verantwortung beim Nutzer.

Wer sich unwohl dabei fühlt, hat zwei Alternativen: Der Standard-Modus mit Einzelbestätigung oder der Plan-Modus, in dem der Agent nur analysiert und plant, ohne irgendetwas auszuführen. Mehr zum Plan-Modus im Abschnitt „Erst denken, dann handeln“.

Heinzel ist nicht auf Remote-Server beschränkt. Es funktioniert auch lokal – auf dem eigenen Rechner, ohne SSH-Umweg. Für macOS bringt Heinzel eine eigene `rules/macos.md` mit, die Besonderheiten wie Homebrew-Pakete, Application Firewall, FileVault- und SIP-Status, `launchctl` statt `systemctl` oder die unterschiedlichen Pfade auf Apple Silicon und Intel abdeckt.

Ein Kunde hatte ein Problem mit seinem Webserver. Das System war mir unbekannt, die Lösung musste schnell kommen. Heinzel hat autonom die Probleme gefunden und behoben: fehlerhafte Dateirechte und ein Firewall-Problem.

Heinzel ist nicht auf Audits und Checks beschränkt. Es kann jede Admin-Aufgabe übernehmen, die sich im Terminal erledigen lässt. Typische Einsatzszenarien, lokal wie remote:

- **Server einrichten:** Neue Maschine aufsetzen, Pakete installieren, Firewall konfigurieren, Benutzer anlegen, Services einrichten – vom blanken System bis zur fertigen Konfiguration.
- **Troubleshooting:** Systematisches Durchgehen von Logs, Berechtigungen und Netzwerkkonfiguration – ohne etwas zu vergessen.
- **Security-Audits:** Heinzel arbeitet die vollständige Checkliste aus `rules/security.md` ab – sortiert nach Schweregrad (CRITICAL, WARN, INFO).
- **Housekeeping:** Systematische Gesundheitschecks anhand von `rules/housekeeping.md`.
- **Paketverwaltung:** Updates einspielen, Abhängigkeiten prüfen – immer mit Dry-Run zuerst.
- **Konfiguration ändern:** Nginx-Vhosts anlegen, Postfix-Relay einrichten, WireGuard-Tunnel aufsetzen, Cron-Jobs verwalten – alles mit Backup und Dry-Run.
- **Migration und Umzug:** Daten von einem Server auf einen anderen übertragen, DNS umstellen, Services auf einem neuen System nachbauen.

Nicht immer will man sofort loslegen. Manchmal will man erst besprechen, wie man ein Problem angeht. Claude Code bietet dafür einen eigenen Plan-Modus (3 mal SHIFT-TAB oder `/plan`): Der Agent analysiert die Situation, liest Konfigurationen und Logs – führt aber keinen einzigen schreibenden Befehl aus. Stattdessen erstellt er einen strukturierten Plan mit konkreten Schritten. In OpenCode oder anderen Tools erreicht man dasselbe, indem man den Agenten explizit auffordert: „Erstelle erst einen Plan, bevor du etwas änderst.“

Das ist besonders wertvoll bei komplexen Aufgaben: „Wie migriere ich diese PostgreSQL-Datenbank auf einen neuen Server mit minimaler Downtime?“ oder „Der Mailserver nimmt keine Mails mehr an – woran kann es liegen?“ Der Agent zeigt Alternativen auf und erklärt die Trade-offs. Erst wenn man den Plan absegnet, wechselt man in den normalen Modus und setzt ihn um.

Einen KI-Agenten auf Produktivserver zu lassen, ist eine erhebliche Umstellung. Die naheliegende Reaktion ist, jeden Befehl selbst tippen und jede Konfiguration selbst prüfen zu wollen. Skepsis ist angemessen – sie zeigt, dass man die Verantwortung ernst nimmt. Ich habe selbst Wochen auf Test-VMs verbracht, bevor ich Heinzel an echte Server gelassen habe.

Die Frage lautet: Ist manuelles Arbeiten wirklich sicherer? Ein menschlicher Admin vergisst mal ein Backup, übersieht eine offene Firewall-Regel oder vertippt sich in einer IP-Adresse. Heinzel arbeitet Checklisten ab und prüft systematisch. Es gibt Berichte über KI-Systeme, die Datenbanken gelöscht haben – deshalb die automatischen Backups. Die Frage ist nicht, ob der Agent fehlerfrei ist – sondern ob er weniger Fehler macht als die Alternative.

Hinzu kommt: Das System verbessert sich von zwei Seiten gleichzeitig. Die zugrunde liegenden Sprachmodelle werden mit jeder Generation leistungsfähiger, verstehen Kontext besser und halluzinieren seltener. Gleichzeitig wächst das Regelwerk mit jeder Praxiserfahrung: Jeder Edge Case, der auffällt, wird zu einer neuen Regel. Der Abstand zwischen KI-gestützter und rein manueller Administration dürfte mit der Zeit wachsen.

Die Einstiegshürde ist bewusst niedrig. Es gibt zwei Wege:

**Weg 1: Claude Code (kommerziell)**

1. Ein Claude-Code-Abonnement (ab 20 Euro/Monat)
2. `git clone **https://github.com/wintermeyer/heinzel [6]**`
3. `cd heinzel && claude`

**Weg 2: OpenCode (Open Source, viele Anbieter)**

OpenCode arbeitet mit zahlreichen Anbietern zusammen – OpenAI, Google Gemini, Anthropic und anderen. Hier das Beispiel mit Ollama, bei dem alles lokal läuft:

- Ollama installieren und ein Modell herunterladen: `ollama pull qwen3.5:9b`
- Context Window vergrößern (Ollama Default von 4096 Token ist zu klein):

```bash
ollama run qwen3.5:9b
>>> /set parameter num_ctx 16384
>>> /save qwen3.5:9b-16k
>>> /bye
```

- `git clone **https://github.com/wintermeyer/heinzel [7]**`
- `cd heinzel && cp opencode.json.example opencode.json`
- `opencode`

Der zweite Weg läuft komplett auf eigener Hardware – kein Cloud-API, kein Abonnement, keine Daten, die das eigene Netzwerk verlassen. Wer genug GPU-Speicher hat, sollte zu einem größeren Modell (14B+) greifen, da diese zuverlässigere Tool-Aufrufe produzieren.

Das Regelwerk ist auf Englisch geschrieben. Arbeiten lässt sich mit Heinzel trotzdem auf Deutsch: In der `memory/user.md` lässt sich die bevorzugte Sprache einstellen (`Language: German`). Heinzel antwortet dann auf Deutsch: Erklärungen, Warnungen, Audit-Berichte. Shell-Befehle, Dateinamen und technische Fachbegriffe bleiben dabei auf Englisch, wo es sinnvoll ist. Wer keine Sprache konfiguriert, bekommt Englisch als Default – oder schreibt einfach auf Deutsch los, dann wechselt Heinzel automatisch.

Tool-agnostisch heißt nicht qualitätsgleich. Die Wahl des Modells macht einen erheblichen Unterschied.

Große kommerzielle Modelle wie Claude Opus oder GPT-4o haben hunderte Milliarden Parameter. Sie bringen eingebaute Sicherheitsmechanismen mit. Sie behalten den Kontext über lange Sessions hinweg besser im Blick, produzieren zuverlässigere Tool-Aufrufe und machen weniger Fehler beim Parsen von Befehlsausgaben. Bei komplexen mehrstufigen Aufgaben – etwa einer Migration mit anschließendem Troubleshooting – liefern sie deutlich bessere Ergebnisse.

Kleine lokale Modelle wie Qwen 3.5 mit 9 Milliarden Parametern spielen ihre Stärken bei klar definierten Einzelaufgaben aus: Status prüfen, ein Paket installieren, eine Konfigurationsdatei anpassen. Bei komplexen Aufgaben werden sie deutlich fehleranfälliger, und Sicherheitsmechanismen auf dem Niveau der großen Modelle fehlen. Dazu kommt eine strukturelle Einschränkung: Lokale Modelle haben teilweise keinen Zugriff auf Web-Suche. Die Anti-Halluzinations-Regel „Search upstream docs“ aus dem Regelwerk können sie schlicht nicht befolgen – kein noch so streng formulierter Prompt gibt einem Modell eine Fähigkeit, die es nicht hat. In der Praxis bedeutet das: Lokale Modelle verlassen sich mehr auf ihre Trainingsdaten, die veraltet sein können. Die anderen Schutzmaßnahmen – `--help` prüfen, Man-Pages lesen, Dry-Runs – funktionieren weiterhin, weil sie nur Shell-Befehle erfordern. Dafür bieten lokale Modelle etwas, das kein Cloud-Dienst liefern kann: vollständige Datensouveränität, keine laufenden Kosten und die Möglichkeit, komplett offline zu arbeiten.

Heinzel ist bewusst Tool-agnostisch. Wer Claude Code nutzen will, kann das tun – wer lieber auf Open-Source-Modelle setzt und seine Daten auf eigener Hardware behalten möchte, nimmt OpenCode mit Ollama. Auch andere terminalbasierte KI-Assistenten, die Projektdateien lesen und Shell-Befehle ausführen können, sind kompatibel. Das Regelwerk ist das Entscheidende, nicht das Tool darunter.

Das hat einen doppelten Vorteil: Das Regelwerk wird kontinuierlich besser – jeder Edge Case aus der Praxis wird zu einer neuen Regel. Gleichzeitig lässt sich jederzeit auf ein besseres oder günstigeres Modell wechseln, ohne das Regelwerk neu zu schreiben. Und wer mit lokalen Modellen heute noch nicht ganz zufrieden ist, profitiert automatisch, wenn Open-Source-Modelle in den kommenden Monaten weiter aufholen.

Das Projekt ist Open Source unter MIT-Lizenz und auf [**GitHub \[8\]**](https://github.com/wintermeyer/heinzel) verfügbar. ([**fo \[9\]**](mailto:fo@heise.de "Moritz Förster"))

---

**URL dieses Artikels:**  
`https://www.heise.de/-11244463`

**Links in diesem Artikel:**  
`**[1]** https://www.heise.de/ratgeber/KI-Assistent-Heinzel-fuer-die-Server-Administration-im-Ueberblick-11244463.html`  
`**[2]** https://www.heise.de/hintergrund/Wie-Semantik-Drift-ML-Vorhersagen-zerstoert-11240931.html`  
`**[3]** https://www.heise.de/hintergrund/Kurz-erklaert-Minimum-Viable-Company-11202464.html`  
`**[4]** https://www.heise.de/ratgeber/Erweiterungen-fuer-SAP-ABAP-fuer-die-Cloud-11194903.html`  
`**[5]** https://www.heise.de/ix`  
`**[6]** https://github.com/wintermeyer/heinzel`  
`**[7]** https://github.com/wintermeyer/heinzel`  
`**[8]** https://github.com/wintermeyer/heinzel`  
`**[9]** mailto:fo@heise.de`

*Copyright © 2026 Heise Medien*