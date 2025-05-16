# Konfiguration

Die Konfiguration eines Dienstes in Carnetes ist sowohl über die Benutzeroberfläche als auch direkt über das Dateisystem möglich. Dieses Kapitel beschreibt die allgemeinen Konfigurationsmöglichkeiten, Anforderungen an die Sicherheit und Zertifikate sowie spezifische Anpassungen zur Authentifikation und Autorisation.

---

## Allgemeine Konfiguration eines Dienstes

### Installation und Konfiguration

- **Über die Benutzeroberfläche**:
  - Ein Dienst kann einfach über Dialoge in der Weboberfläche installiert und konfiguriert werden. Die Benutzerführung begleitet dabei die Einrichtung der Konfiguration.

- **Über das Dateisystem**:
  - Dienste befinden sich unter dem Pfad:
    ```
    carnetes\package\@socketservice
    ```
  - Die Konfigurationen der jeweiligen Dienste werden unter:
    ```
    {service}\.instance\{instancename}\carnetes.json
    ```
    gespeichert.
  - In dieser Datei können je nach Art des Dienstes spezifische Einstellungen wie **Zertifikate**, **Brokereinstellungen** oder **Verbindungen** festgelegt werden.

---

## Sicherheit und Zertifikate

### Nutzung von Zertifikaten

- Für eine gesicherte Kommunikation zwischen den Diensten sowie zum Broker werden **Zertifikate im PEM-Format** benötigt.
- Der Speicherort der Zertifikate ist flexibel wählbar. Wichtig ist jedoch, dass die Dienste entsprechend konfiguriert werden.
- **Zertifikate erneuern**:
  - Im Falle eines abgelaufenen Zertifikats reicht es aus, die Datei im entsprechenden konfigurierten Verzeichnis zu ersetzen.
  - Bei Umbenennungen der Zertifikate müssen alle zugehörigen Konfigurationen angepasst werden.

### Zugriff mittels JWT

- Die Dienste nutzen **Json Web Token (JWT)** für die Zugriffskontrolle.
- JWT wird durch einen Dienst ausgestellt, der nach der **OAuth2-Spezifikation** integriert ist.
- Für die Authentifikation über **Active Directory (AD)** ist ein spezieller Dienst erforderlich, der die Verbindung zum Authorization Server (AS) bereitstellt.

---

## Anpassung von Authentifikation und Autorisation

### Authentifikation

- Die Authentifikation kann flexibel angepasst werden:
  - Unter **Broker > Security / Authentication** kann die jeweilige Instanz direkt bearbeitet werden.
  - Die Loginseite liegt als Referenz im 'www' Ordner der jeweiligen Methode und kann individuell gestaltet werden.
  - Beispiel für ein Input-Element:
    ```html
    <input id="pin" name="pin" type="password" placeholder="Pin" inputmode="none" >
    ```
  - Die Eingaben können in der 'route'-Methode verarbeitet werden, z. B.:
    ```typescript
    const pin = request.body.pin;
    ```

- Alternativ kann die Authentifikation direkt über das Dateisystem bearbeitet werden:
	```
	\carnetes\authentication\{methode}\authentication.ts
	```

Nach einer Anpassung ist ein Neustart des Dienstes erforderlich.

- Bearbeitung über die Webansicht:
- In der Weboberfläche können Änderungen online vorgenommen werden. Über die Aktionen **Deploy** und **Undeploy** kann die Funktion online oder offline gesetzt werden.

### Autorisation

- Die Autorisation kann ebenso individuell gestaltet werden:
- Unter **Broker > Security / Authorization** können Regeln definiert werden, welche Aktionen ein Nutzer zu welchem Zeitpunkt ausführen darf.

---
