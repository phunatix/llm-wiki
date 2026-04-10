---
title: "Talos: Ein Minimal-Linux für Kubernetes"
source: https://www.heise.de/ratgeber/Talos-Ein-Minimal-Linux-fuer-Kubernetes-aufgebaut-11094102.html?view=print
author:
  - "[[Niklas Dierking]]"
published: 2026-01-23
created: 2026-01-23
description: "Kahlschlag als Prinzip: Die Linux-Distribution Talos schmeißt alles raus, was man nicht für Kubernetes braucht. Sogar SSH."
tags:
  - clippings
  - heise
  - kubernetes
---
[zurück zum Artikel](https://www.heise.de/ratgeber/Talos-Ein-Minimal-Linux-fuer-Kubernetes-aufgebaut-11094102.html)

![Logo c't](https://www.heise.de/icons/svg/logos/svg/ct_claim.svg)

![](https://heise.cloudimg.io/bound/712x480/q60.png-lossy-60.webp-lossy-60.foil1/_www-heise-de_/imgs/18/4/9/8/5/6/3/3/https___xp-865cf899613994e5.jpeg)

**Kahlschlag als Prinzip: Die Linux-Distribution Talos schmeißt alles raus, was man nicht für Kubernetes braucht. Sogar SSH.**

Talos Linux ist eine Distribution, die für genau einen Anwendungsfall konzipiert wurde: Sie soll der ideale Untersatz für Kubernetes sein. Damit wollen die Entwickler einen tiefen Graben überbrücken: Zu den Stärken von Kubernetes, also der containerisierten Applikationsschicht, gehört die deklarative Konfiguration und die Fähigkeit zur Selbstheilung etwa durch Redundanz. Die darunterliegenden Betriebssysteme, etwa Linux-Distributionen wie Ubuntu oder Debian, orientieren sich jedoch oft noch an den Paradigmen des klassischen Serverbetriebs.

- Die Entwickler von Talos haben ihre Linux-Distribution als optimale Basis für Kubernetes entworfen.
- Talos verfügt über ein unveränderliches (immutable) Dateisystem und nimmt Befehle nur über ein gRPC-API an. Übliche Systemwerkzeuge wie systemd und SSH fehlen.
- Die minimale Basis soll die Angriffsfläche reduzieren. Die deklarative Natur des Systems soll Konfigurationsdrift verhindern.

Typische Server-Betriebssysteme sind langlebig, potenziell pflegeintensiv und wenn Admin A heute an der einen Schraube und Admin B morgen an der anderen Schraube dreht, stellt sich über die Zeit gern Konfigurationsdrift ein. Der gewünschte und der tatsächliche Zustand des Systems ist also nicht mehr deckungsgleich. Mit einem Automatisierungswerkzeug wie Ansible kann man den Konfigurationsdrift klassischer Linux-Distributionen im Zaum halten. Es knetet Linuxe zuverlässig nach den eigenen Vorstellungen zurecht, bedient sich dafür aber beim typischen Linux-Werkzeugkasten mit SSH, Paketmanager und Shell.

![](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/4/9/8/5/6/3/3/https___xp.heise.de_fileserver_images_2602_211334731319886_omni-2660a3f0cf4d12b2.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1600)

Sidero, das Unternehmen hinter Talos, bietet mit Omni ein ergänzendes SaaS-Produkt an, um Talos-Cluster einfach zu erstellen und zu verwalten. Wer Omni privat einsetzt, darf es kostenlos auf eigener Infrastruktur installieren.

Talos wirft all diese Werkzeuge über Bord, denn die sind nicht nur praktisch für Admins, sondern auch für Angreifer. Während sich klassische Linux-Distributionen möglichst breit aufstellen, kann man sich Talos eher wie eine Firmware für Kubernetes vorstellen. Statt SSH, APT und Bash gibt es talosctl, YAML und ein gRPC-API.

Talos ist eine von der Cloud Native Computing Foundation (CNCF) zertifizierte Kubernetes-Distribution. Sidero, das Unternehmen hinter Talos, ist selbst Mitglied der CNCF. Talos ist Open Source und unterliegt der Mozilla Public License Version 2.0. Geld verdient das Unternehmen mit Support-Verträgen für Talos und mit Omni, einer SaaS-Lösung (Software as a Service) zum Erstellen und Verwalten von Talos-Clustern. Omni ist unter der Business Source License 1.1 lizenziert. Die gewährt Zugriff auf den Quellcode, ist aber keine Open-Source-Lizenz nach Definition der OSI, denn sie erlaubt die Installation von Omni in Produktivumgebungen nur gegen Bezahlung.

In diesem Artikel bauen wir eine Talos-Testumgebung auf und zeigen, wo man beim Minimal-Linux umdenken muss. Als Beispielplattform nutzen wir die Virtualisierungsumgebung Proxmox Virtual Environment, Talos ist aber hardware- und cloudagnostisch. Der Aufbau eines Talos-Clusters bei einem Cloudanbieter oder bei der Installation auf echter Hardware, auch „bare metal“ genannt, läuft also ganz ähnlich ab. Sie benötigen dazu Linux- und Kubernetes-Vorwissen.

Installations-Images für die Kubernetes-Distribution stellt Sidero [**über die sogenannte Image Factory \[11\]**](https://factory.talos.dev/) bereit. Dort gibt es Images für alle möglichen Plattformen, vom Raspberry Pi 4 bis zu Amazon Web Services.

Auf der Startseite der Factory müssen Sie sich zunächst für einen Hardwaretyp entscheiden. Zur Auswahl stehen „Bare-metal Machine“, „Cloud Server“ und „Single Board Computer“. Proxmox fällt in den Bereich Cloud Server, weil Talos dort wie bei einem Cloudanbieter virtualisiert wird. Danach wählen Sie die Talos-Version, zum Redaktionsschluss war Version 1.21.1 aktuell. Bei der Wahl der Cloud klicken Sie „Nocloud“ an, das sind die Images für diverse Hypervisor. Danach wählen Sie amd64 als Architektur aus.

Im vorletzten Schritt werden Sie gefragt, ob Sie „System Extensions“ hinzufügen möchten. Das sind kleine Modifikationen, die das Image beispielsweise um zusätzliche Treiber oder Firmware erweitern. Wenn Pods im Talos-Cluster etwa Zugriff auf einen AMD-Grafikchip brauchen, wählt man die Erweiterung „siderolabs/amdgpu“ an. Für Proxmox empfiehlt sich die Erweiterung „siderolabs/qemu-guest-agent“. Der Qemu-Agent ist ein Daemon, der die Interaktion zwischen virtueller Maschine und Host erleichtert und unter anderem die IP-Adresse der Gastsysteme in der Proxmox-Weboberfläche anzeigt.

![](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/4/9/8/5/6/3/3/https___xp.heise.de_fileserver_images_2602_211334497179864_image_factory-71e2e81326b4a96c.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1600)

Talos à la carte: In der Image Factory gibt es Installationsmedien für diverse Plattformen und Anwendungszwecke.

Im letzten Schritt haben Sie die Gelegenheit, eigene Kernel-Parameter zu setzen und einen Bootloader zu wählen. Ersteres kann praktisch sein, um Talos eine Netzwerkkonfiguration einzuimpfen, falls es keinen DHCP-Server im Netzwerk gibt. Die Einstellung für den Bootloader können Sie auf „auto“ stehen lassen.

Die Image Factory spuckt jetzt eine ID und einen YAML-Schnipsel aus, mit denen Sie das Image später leicht reproduzieren können. Außerdem gibt es eine URL zum Download der ISO-Datei. Navigieren Sie in der Proxmox-Weboberfläche zum Menü für den lokalen Storage, meist „local (pve)“ genannt. Klicken Sie auf die Schaltfläche „Von URL herunterladen“, fügen Sie die Download-URL aus der Image Factory ein und laden Sie die ISO-Datei herunter.

![Mehr von c't Magazin](https://www.heise.de/ratgeber/www.w3.org/2000/svg'%20width='696px'%20height='391px'%20viewBox='0%200%20696%20391'%3E%3Crect%20x='0'%20y='0'%20width='696'%20height='391'%20fill='%23f2f2f2'%3E%3C/rect%3E%3C/svg%3E)

Klicken Sie in der Proxmox-Weboberfläche auf die Schaltfläche „Erstelle VM“ und legen Sie einen Namen und eine ID für die Talos-VM fest. Als Erstes erstellen Sie einen Talos-Knoten, der als Gehirn für Kubernetes dient (Control Plane). Unter „OS“ wählen Sie die zuvor heruntergeladene ISO-Datei als Installationsmedium. Setzen Sie im Menü „System“ den Haken bei „Qemu-Agent“.

Danach weisen Sie der VM Ressourcen zu. Die Talos-Entwickler geben für Worker-Knoten einen CPU-Kern und 2 GByte Arbeitsspeicher als Mininum an. Control-Plane-Knoten brauchen mindestens 2 Kerne und ebenfalls 2 GByte Arbeitsspeicher. Beide benötigen auch mindestens 10 GByte Speicherplatz. Talos setzt seit Version 1.0 einen Prozessor mit Mikroarchitektur-Level x86-64-v2 voraus. In unserem Testlauf hat Proxmox 9.1.4 bei der Zuweisung der Kerne automatisch den kompatiblen Typ x86-64-v2-AES ausgewählt.

Im Netzwerkmenü lassen Sie die Voreinstellungen (vmbro, VirtIO) unangetastet, Talos bezieht dann eine IP-Adresse via DHCP. Wiederholen Sie diese Schritte, um auch einen Worker-Knoten zu erstellen.

Jetzt ist es an der Zeit, den Control-Plane-Knoten zu starten. Über das Menü „Konsole“ können Sie der VM dabei über die Schulter schauen. Anders als bei anderen Server-Distributionen öffnet sich jetzt kein Installationsassistent, wo Sie Benutzerkonten erstellen und Passwörter vergeben, denn all das gibt es bei Talos nicht.

Stattdessen lädt es das initramfs in den Arbeitsspeicher, besorgt sich eine IP-Adresse per DHCP und startet dann den Dienst apid für die gRPC-Schnittstelle, die auf TCP-Port 50000 erreichbar ist. Der Dienst machined übernimmt anstelle von systemd die Rolle des Init-Systems. Der Talos-Knoten befindet sich jetzt im sogenannten Maintenance Modus und ist bereit, über das API eine Maschinenkonfiguration entgegenzunehmen. In der Web-Konsole von Proxmox sieht man außerdem das Dashboard. Hier werden diverse System- und Cluster-Informationen angezeigt. Talos gibt etwa Auskunft über die Version, in welchem Zustand es sich befindet, ob es bereit ist, eine Maschinenkonfiguration anzunehmen und ob der Knoten Teil eines Clusters ist.

![](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/4/9/8/5/6/3/3/https___xp.heise.de_fileserver_images_2602_211334967253210_talos_dashboard_maintenance-d85d985be87173b3.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1600)

Andere Linux-Distributionen für Server installiert man mit einem Installationsassistenten. Talos fährt hoch, schaltet in den Wartungsmodus und wartet dann darauf, eine Maschinenkonfiguration anzunehmen.

Um Talos jetzt zu installieren, brauchen Sie auf Ihrem lokalen Computer das Kommandozeilenwerkzeug talosctl. Sie interagieren über talosctl mit dem Talos-API analog zu kubectl, das das Kubernetes-API anzapft. Unter macOS installieren Sie das Tool am einfachsten mit dem Paketmanager Homebrew:

```
brew install siderolabs/tap/talosctl
```

Alternativ laden Sie die ausführbare Datei für Ihr Betriebssystem (macOS, Linux und Windows) aus dem Release-Bereich des GitHub-Repositorys von Talos herunter oder nutzen das Installationsskript. Sie müssen dann allerdings selbst dafür sorgen, talosctl aktuell zu halten.

Der folgende Befehl erstellt die Datei talosconfig sowie Maschinenkonfigurationen für Control-Plane- und Worker-Knoten:

```
talosctl gen config cttest-cluster  https://$CONTROL_PLANE_IP:6443  --output-dir talosconfigs
```

Statt `cttest-cluster` können Sie Ihrem Cluster einen eigenen Namen geben. Den Platzhalter `$CONTROL_PLANE_IP` müssen Sie hier und in allen folgenden Befehlen durch die IP-Adresse Ihres Control-Plane-Knotens ersetzen. Die Konfigurationsdateien werden in das Verzeichnis `talosconfigs` geschrieben, Sie können auch ein anderes Verzeichnis angeben. Nachdem Sie den Befehl ausgeführt haben, finden sich dort die Dateien controlplane.yaml, worker.yaml und talosconfig. Letztere ist später Ihr Schlüssel zum Cluster. Wenn Sie die Datei löschen oder verlieren, haben Sie keinen Zugriff mehr.

Öffnen Sie die Maschinenkonfiguration controlplane.yaml mit einem Texteditor. Prüfen Sie insbesondere, ob das Laufwerk im Abschnitt mit der Überschrift `install` zur Konfiguration Ihrer VM passt, standardmäßig ist das /dev/sda:

```
install:
        disk: /dev/sda
```

Wenn es Zweifel gibt, können Sie das aktuelle Layout der Laufwerke des Knotens mit folgendem Befehl auslesen:

```
talosctl get disks --insecure  --nodes $CONTROL_PLANE_IP
```

Um die Maschinenkonfiguration auf den Knoten anzuwenden, also Talos zu installieren, führen Sie den folgenden Befehl aus:

```
talosctl apply-config --insecure  --nodes $CONTROL_PLANE_IP --file  talosconfigs/controlplane.yaml
```

In der Web-Shell vom Proxmox können Sie jetzt zusehen, wie es rattert. Nach einem kurzen Neustart verlässt der Knoten den Maintenance-Modus. Verbindungen, die wie der obige Befehl mit `--insecure` versehen sind, nimmt er jetzt nicht mehr an, sondern akzeptiert nur noch authentifizierte Verbindungen und verschlüsselte Anfragen, die mit dem Zertifikat aus der Konfigurationsdatei `talosconfig` signiert wurden.

Das Talos-Dashboard sollte jetzt nach kurzer Zeit anzeigen, dass der Knoten Teil des Clusters cttest-cluster ist, dass der Knoten dem Typ controlplane angehört und das Kubernetes Kubelet healthy ist.

Prüfen Sie ebenfalls die Konfiguration für den Worker und wenden Sie ihn dann auf den Knoten an:

```
talosctl apply-config --insecure  --nodes $WORKER_IP  --file talosconfigs/worker.yaml
```

Ersetzen Sie den Platzhalter `$WORKER_IP` in diesem und allen folgenden Befehlen durch die IP-Adresse des Worker-Knotens. Die Dashboards der Talos-Knoten sollten nach kurzer Zeit melden, dass dem Cluster jetzt zwei Maschinen angehören.

Lassen Sie talosctl wissen, in welchem Verzeichnis die talosconfig zu finden ist, indem Sie eine die Umgebungsvariable `TALOSCONFIG ` setzen: `export TALOSCONFIG="talosconfigs/talosconfig"`. Dann legen Sie mit den Befehlen `talosctl config endpoint $CONTROL_PLANE_IP` und `talosctl config node $CONTROL_PLANE_IP` den Control-Plane-Knoten als API-Endpunkt fest.

Der Cluster ist fast bereit. Als letzten Schritt müssen Sie etcd starten, denn in einem neuen Cluster weiß der Control-Plane-Knoten nicht, ob er der Einzige bleibt oder noch auf weitere Mitglieder warten muss:

```
talosctl bootstrap
```

Dieser Befehl initialisiert auf dem Knoten einen neuen etcd-Cluster, in dem er das einzige Mitglied ist. Sie sind nicht mehr länger auf die Proxmox-Webshell als Informationsquelle angewiesen, sondern können das Talos-Dashboard jetzt auch mit dem Befehl `talos dashboard` aufrufen.

![](https://heise.cloudimg.io/v7/_www-heise-de_/imgs/18/4/9/8/5/6/3/3/https___xp.heise.de_fileserver_images_2602_211334275644790_kubectl-f57b049596abc089.png?force_format=avif%2Cwebp%2Cjpeg&org_if_sml=1&q=70&width=1600)

Kubernetes ist einsatzbereit. Damit hat Talos seinen einzigen Zweck erfüllt.

Kubernetes ist jetzt einsatzbereit. Navigieren Sie in das Verzeichnis talosconfigs und angeln Sie mit dem Befehl `talosctl kubeconfig .` die kubeconfig-Datei aus dem Cluster. So wie die talosconfig der Schlüssel zum Talos-API ist, berechtigt Sie die kubeconfig mit dem Kubernetes-API zu interagieren. Dafür nutzen Sie [**das Kommandozeilenwerkzeug kubectl \[13\]**](https://kubernetes.io/de/docs/tasks/tools/install-kubectl/).

Stoßen Sie kubectl mit dem Befehl `export KUBECONFIG=talosconfigs/kubeconfig` auf die kubeconfig-Datei. Jetzt können Sie via kubectl mit dem Kubernetes-API interagieren. Der Befehl `kubectl get nodes` sollte den Control-Plane- und den Worker-Knoten melden, so wie auf dem Screenshot. Der Cluster ist jetzt bereit, Workloads auszuführen.

Sie haben Talos, das Spezial-Linux für Kubernetes, sowie dessen Werkzeuge kennengelernt, können einen Cluster aufbauen und das Talos- und das Kubernetes-API bespielen. Talos nimmt viel Arbeit bei der Erstellung von Kubernetes-Clustern ab und minimiert durch seinen Read-only-Ansatz und den Verzicht auf die Linux-Serienausstattung gleichzeitig die Angriffsfläche enorm. Dafür muss man als Admin jedoch umdenken und sich möglicherweise von lieb gewonnenen Workflows und Werkzeugen verabschieden. In jedem Fall lohnt es sich, die [**Talos-Dokumentation \[14\]**](https://docs.siderolabs.com/talos) zu studieren, auch für Kubernetes-spezifische Themen. Beispielsweise muss man beim Anlegen eines Storage-Clusters mit Longhorn [**einige zusätzliche Schritte \[15\]**](https://docs.siderolabs.com/kubernetes-guides/csi/storage) erledigen.

Vollends entfaltet Talos seine Fähigkeiten im Zusammenspiel mit Omni und sogenannten Infratructure-Providern. Bindet man beispielsweise den Provider für Proxmox ein, klickt man sich seinen Cluster in der Weboberfläche von Omni zusammen, das die passenden VMs dann automatisch beim Hypervisor bestellt. Das ist aber Stoff für einen möglichen Folgeartikel.

([**ndi \[16\]**](https://www.heise.de/ratgeber/ "Niklas Dierking"))

---

**URL dieses Artikels:**  
`https://www.heise.de/-11094102`

**Links in diesem Artikel:**  
`**[1]** https://www.heise.de/ratgeber/Talos-Ein-Minimal-Linux-fuer-Kubernetes-aufgebaut-11094102.html`  
`**[2]** https://www.heise.de/ratgeber/Kubernetes-Cluster-von-Ingress-Nginx-zu-Traefik-migrieren-11094019.html`  
`**[3]** https://www.heise.de/tests/Containermanagement-Freier-Kubernetes-Orchestrierer-k0rdent-im-Test-10343842.html`  
`**[4]** https://www.heise.de/ratgeber/Crossplane-GitOps-fuer-die-Multi-Cloud-7456153.html`  
`**[5]** https://www.heise.de/ratgeber/Crossplane-Provisionierung-in-AWS-und-Azure-7494018.html`  
`**[6]** https://www.heise.de/ratgeber/Kubernetes-lernen-und-verstehen-Teil-1-Cluster-aus-drei-Linux-Servern-bauen-7308546.html`  
`**[7]** https://www.heise.de/ratgeber/Kubernetes-lernen-und-verstehen-Teil-2-Wie-Sie-Cluster-mit-Containern-fuellen-7325943.html`  
`**[8]** https://www.heise.de/ratgeber/Kubernetes-lernen-und-verstehen-Teil-3-Container-vernetzen-7351581.html`  
`**[9]** https://www.heise.de/hintergrund/Kubernetes-lernen-und-verstehen-Teil-4-Daten-speichern-7367376.html`  
`**[10]** https://www.heise.de/ratgeber/Kubernetes-lernen-und-verstehen-Teil-5-Sicherheitskonzepte-einsetzen-7445949.html`  
`**[11]** https://factory.talos.dev/`  
`**[12]** https://www.heise.de/ct`  
`**[13]** https://kubernetes.io/de/docs/tasks/tools/install-kubectl/`  
`**[14]** https://docs.siderolabs.com/talos`  
`**[15]** https://docs.siderolabs.com/kubernetes-guides/csi/storage`  
`**[16]** mailto:ndi@heise.de`  

*Copyright © 2026 Heise Medien*