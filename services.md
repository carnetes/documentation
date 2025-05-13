# Services in carnetes

## Datenbank Service

Der **Datenbank Dienst** stellt Funktionalitäten für die Interaktion mit einer **MsSql-Datenbank** bereit. Dieser Service ermöglicht eine effiziente und flexible Nutzung von Datenbanken innerhalb der IT-Infrastruktur von Carnetes.

---

### Instanzierung

- Es können **mehrere Instanzen** eines Datenbank Dienstes parallel laufen.
- Jede Instanz unterscheidet sich durch ihre spezifische **Verbindung zur Datenbank** (z. B. Nutzer sowie Schema).
- Diese Architektur bietet die Möglichkeit, unterschiedliche Datenbankkonfigurationen unabhängig voneinander zu betreiben.

---

### Gemeinsame Schnittstelle

Jeder Datenbank Dienst basiert auf einer gemeinsamen Schnittstelle, die eine konsistente und vereinheitlichte Nutzung gewährleistet. Es werden zwei Hauptfunktionen bereitgestellt:

#### Query

- Über die **Query-Funktion** können Abfragen definiert werden, deren Ergebnisse im **JSON-Format** zurückgeliefert werden.
- Syntax:
  - Die Querysyntax entspricht **Standard SQL**.
  - Datenbankspezifische Syntax oder spezielle Codes, die vom Datenbank-Managementsystem unterstützt werden, können ebenfalls verwendet werden.

#### Call

- Ein **Call** ermöglicht den direkten Aufruf einer **Stored Procedure**.
- Stored Procedures bieten die Möglichkeit, komplexe Datenbankoperationen zu kapseln und zur Wiederverwendung bereitzustellen.
- Diese Funktion ist ideal, um Datenbankaufrufe zu exportieren und in Anwendungen zu integrieren.

---

### Oracle
Der **Oracle-Service** ermöglicht die Verbindung zu einer Oracle-Datenbank. Die unterstützten Funktionen umfassen:
- **Abfragen:** Direkter Zugriff auf Datenbanken für SELECT-Anweisungen und Abfragen.
- **Datenmanipulation (DML):** Funktionen wie INSERT, UPDATE und DELETE zur Bearbeitung von Daten.
- **Stored Procedures:** Ausführung komplexer Datenbanklogik über gespeicherte Prozeduren. Der Service bietet eine zuverlässige Verbindung zu Oracle-Datenbanken, um große Datenmengen effizient zu verarbeiten.

---

### MsSql
Der **MsSql-Service** ist speziell für die Integration mit Microsoft SQL-Datenbanken konzipiert. Funktionen umfassen:
- **Abfragen:** Zugriff auf Daten über SQL SELECT-Anweisungen.
- **DML-Operationen:** Modifikation und Bearbeitung von Daten über Standard-DML-Anweisungen.
- **Stored Procedures:** Nutzung vordefinierter Logik innerhalb der Datenbank. Mit diesem Service wird eine nahtlose Integration und schnelle Verarbeitung von Daten in Microsoft SQL-Umgebungen gewährleistet.

---

## FileSystem
Der **FileSystem-Service** dient der Speicherung von Daten im Dateisystem. Er ermöglicht:
- **Datenablage:** Speichern von Dateien in definierten Verzeichnissen.
- **Strukturierte Speicherung:** Organisation von Daten für langfristige Nutzung und Backups. Dieser Service ist ideal für Anwendungen, die lokale Dateiverarbeitung benötigen.

---

## FTP
Mit dem **FTP-Service** können Daten sicher und effizient über das File Transfer Protocol übertragen werden. Die Funktionen umfassen:
- **Datentransfer:** Upload und Download von Dateien.
- **Verbindungssicherheit:** Unterstützung von FTP-Protokollen mit Verschlüsselung, z. B. FTPS. Der FTP-Service ermöglicht die Automatisierung von Datentransfers in verschiedene Umgebungen.

---

## Mail
Der **Mail-Service** verbindet sich mit einem Mail-Server und bietet Funktionen wie:
- **E-Mail-Versand:** Nachrichten mit Text und Anhängen senden.
- **SMTP-Unterstützung:** Konfiguration für gängige Mailserver-Standards. Dieser Service ist ideal für Anwendungen, die automatisierten Mailversand benötigen.

---

## MQTT
Der **MQTT-Service** stellt einen MQTT-Broker sowie einen Client zur Verfügung, um Datenquellen zu koppeln. Funktionen:
- **Broker:** Zentraler Punkt für die Kommunikation zwischen MQTT-Publishern und -Subscriber.
- **Client:** Verbindung zu bestehenden MQTT-Datenquellen für Echtzeit-Updates. Der Service eignet sich für IoT-Anwendungen und ereignisbasierte Datenverarbeitung.

---

## ModBus
Der **ModBus-Service** stellt einen Client bereit, um Geräte zu koppeln, die über das ModBus-Protokoll kommunizieren. Funktionen umfassen:
- **Datenkommunikation:** Lesen und Schreiben von Daten auf ModBus-Geräten.
- **Kompatibilität:** Unterstützung für ModBus RTU und TCP. Der Service ist speziell für die Integration industrieller Hardware konzipiert.

---

## IBM MQ
Der **IBM MQ-Service** ermöglicht Messaging im Kontext des IBM Message Queuing-Systems. Funktionen:
- **Nachrichtentransport:** Asynchrone Datenkommunikation zwischen verschiedenen Anwendungen.
- **Zuverlässigkeit:** Sicherstellung der Nachrichtenzustellung durch Warteschlangenmechanismen. Ideal für Anwendungen mit hoher Kommunikationslast.

---

## SOAP
Der **SOAP-Service** bietet Funktionen für die Kommunikation über das SOAP-Protokoll. Er ermöglicht:
- **Webservice-Integration:** Kopplung an SOAP-basierte Dienste.
- **Datenkommunikation:** Austausch von strukturierten Daten mit XML. Der Service eignet sich für ältere Webservice-Standards.

---

## RTSP
Mit dem **RTSP-Service** können Funktionen des Real Time Streaming Protocols genutzt werden. Funktionen:
- **Streaming:** Verarbeitung von Echtzeit-Video- und Audio-Datenströmen.
- **Flexibilität:** Integration in streamingfähige Anwendungen. Der Service ist ideal für Echtzeit-Medienanwendungen.

---

## WaGo Enocean
Der **WaGo Enocean-Service** unterstützt die Nutzung von Geräten, die das WaGo Enocean-Protokoll verwenden. Funktionen:
- **Gerätesteuerung:** Interaktion mit WaGo Enocean-Geräten.
- **Integration:** Kopplung von Sensoren und Aktoren. Dieser Service eignet sich für smarte Gebäudetechnik.

---

## CloudAWS
Der **CloudAWS-Service** bietet Funktionen zur Nutzung von AWS-Diensten, insbesondere:
- **AWS Lambda:** Integration und Aufruf cloudbasierter Funktionen.
- **Skalierbarkeit:** Nutzung weiterer AWS-Dienste wie S3 oder EC2. Der Service optimiert Cloud-basierte Anwendungen.

---

## Cron
Der **Cron-Service** ermöglicht die Verwaltung und Nutzung zeitbasierter Events. Funktionen:
- **Eventplanung:** Definition von wiederholenden Ereignissen (z. B. stündlich, täglich).
- **Automatisierung:** Trigger für zeitgesteuerte Aktionen. Der Service ist ideal für geplante Aufgaben und Batch-Prozesse.

---

## RevPi I/O
Der **RevPi I/O-Service** bietet Funktionen zur Steuerung und Verwaltung von Revolution Pi (RevPi)-Pins. Funktionen:
- **GPIO-Steuerung:** Direkte Ansteuerung von Eingangs- und Ausgangspins.
- **Hardwareintegration:** Verbindung zu industriellen Geräten. Der Service ist speziell für Anwendungen in der Steuerungs- und Automatisierungstechnik konzipiert.

---

## Convert
Der **Convert-Service** ermöglicht die Konvertierung von Daten:
- **Quellenintegration:** Verarbeitung von Daten aus SocketService.
- **Ausgabe:** Export in Excel-Formate. Dieser Service ist ideal für Datenanalyse und Berichterstattung.

---

## AD
Der **AD-Service** unterstützt die Integration und Verwaltung von Active Directory:
- **Benutzerverwaltung:** Verwaltung von Benutzern und Gruppen.
- **Authentifizierung:** Sichere Anmeldung und Zugriffskontrolle. Der Service ist ideal für Unternehmensumgebungen.

---

## Carbone
Mit dem **Carbone-Service** können PDFs aus Carbone-Templates generiert werden. Funktionen:
- **Template-Verarbeitung:** Nutzung von Vorlagen für Dokumente.
- **Automatisierung:** Generierung von Berichten und Formularen. Ideal für Anwendungen, die strukturierte Dokumente erfordern.

---

## Lambda
Der **Lambda-Service** ermöglicht die Bereitstellung von Functions-as-a-Service (FaaS). Funktionen:
- **Flexibilität:** Schnelle Entwicklung und Bereitstellung kleiner Funktionen.
- **Skalierbarkeit:** Ressourcennutzung auf Abruf. Dieser Service ist optimiert für ereignisbasierte Anwendungen und Anpassungen.

### Lambda Service

Der **Lambda Dienst** stellt **Function as a Service (FaaS)** bereit. Dies ermöglicht es, beliebige serverseitige Funktionalitäten zur Laufzeit zu definieren und auszuführen. Derzeit wird **TypeScript** als einzige Sprache unterstützt. 

Die Instanzen eines Lambda-Dienstes stellen eine Art Gruppierung von Funktionen dar, wodurch diese theoretisch auch als eigenständiger Dienst abgebildet werden können. Jede Instanz wird unabhängig von den anderen ausgeführt.

---

#### Aufbau einer Lambda

Eine Lambda-Funktion folgt immer dem gleichen Aufbau, wie im folgenden Beispiel dargestellt:

```typescript
import { Injectable, Action, Init, Destroy } from '@carnetes/core';
import { HttpRequest, HttpResponse } from '@carnetes/runtime';
import { ActionHandler, Logger } from '@carnetes/lambda';

@Injectable()
export class Lambda extends ActionHandler {

    constructor() {
        super();
    }

    @Init()
    public init(): Promise<void> {
        Logger.log(Lambda, 'init ...');
        const promise = new Promise<void>((resolve, reject) => {
            try {
                /**
                 * YOUR CODE
                 */
                Logger.log(Lambda, 'init complete');
                resolve();
            } catch (exception) {
                reject(exception);
            }
        });
        return promise;
    }

    @Destroy()
    public destroy(): Promise<void> {
        Logger.log(Lambda, 'destroy ...');
        const promise = new Promise<void>((resolve, reject) => {
            try {
                /**
                 * YOUR CODE
                 */
                Logger.log(Lambda, 'destroy complete');
                resolve();
            } catch (exception) {
                reject(exception);
            }
        });
        return promise;
    }

    @Action({
        arguments: [
            { name: 'value', type: String, array: false }
        ],
        return: { type: String, array: false }
    })
    public handleAction(value: string, request: HttpRequest, response: HttpResponse): Promise<string> {
        Logger.log(Lambda, 'handleAction ...');
        const promise = new Promise<string>((resolve, reject) => {
            try {
                /**
                 * YOUR CODE
                 */
                Logger.log(Lambda, 'handleAction complete');
                resolve(value);
            } catch (exception) {
                Logger.error(Lambda, exception);
                reject(exception);
            }
        });
        return promise;
    }

}
```

#### Einsprungpunkte

Es gibt drei Einsprungpunkte, die je nach Zustand der Lambda-Funktion aufgerufen werden:

1. **Init**:
   - Wird einmalig beim Start einer Funktionalität ausgeführt.
   - Beispiel: Ressourcen initialisieren, Verbindungen herstellen.

2. **Destroy**:
   - Wird ausgeführt, wenn die Funktion beendet wird.
   - Beispiel: Ressourcen freigeben, Verbindungen schließen.

3. **handleAction**:
   - Enthält die Hauptlogik der Funktion.
   - Wird bei jedem Aufruf der Lambda-Funktion ausgeführt.
   - Die Parameter werden in der **Annotation** definiert und müssen in der Handlerfunktion entsprechend verarbeitet werden.

---

#### Aktualisierung einer Lambda

##### Online über die Weboberfläche
- Änderungen können direkt in der **Weboberfläche** durchgeführt werden.
- Nach einer Änderung kann die Funktion über die Aktionen **Deploy** und **Undeploy** online oder offline gesetzt werden.

##### Dateibasierte Bearbeitung
- Der Funktionscode befindet sich unter dem Verzeichnis:
```
carnetes/package/@carnetes/lambda/.instance/{instance_name}/actions/{func_name}
```

- Die Funktionalität wird in der Datei 'lambda.ts' bearbeitet.
- Alternativ kann der gesamte Actions-Ordner ausgetauscht werden, um ein Update durchzuführen.
- **Neustart des Brokerdienstes**:
- Nach Änderungen sollte der Brokerdienst neugestartet werden, um die Aktualisierungen zu übernehmen.

---
