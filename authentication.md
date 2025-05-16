# Authentifikation

Die Authentifikation ist ein zentraler Bestandteil der Sicherheitsarchitektur von Carnetes und stellt sicher, dass nur autorisierte Benutzer und Systeme Zugriff auf geschützte Ressourcen erhalten. Dieses Kapitel bietet eine umfassende Übersicht über die verfügbaren Authentifikationsmethoden, mögliche Erweiterungen und spezifische Konfigurationen wie die Integration eines Active Directory Services.

---

## Anmeldemethoden

### Anmeldung über OAuth2
- **OAuth2** wird als Authentifikationsprotokoll verwendet und bietet eine flexible Lösung für die sichere Anmeldung.
- Mit der **OpenID-Erweiterung** wird eine präzise Identitätsverifizierung und der Zugriff auf erweiterte Nutzerinformationen ermöglicht.

### Rechteverwaltung für Clients
- Jeder Client besitzt **eigene Rechte (Scopes)**, die individuell definiert werden können, um den Zugriff auf Ressourcen zu steuern.

---

## Verfügbare Scopes
Die folgenden Scopes stehen zur Verfügung und definieren den Umfang der Rechte:
- **Admin**: Administrative Zugriffsrechte.
- **Profile**: Zugriff auf grundlegende Benutzerdaten wie Name und Avatar.
- **Email**: Zugriff auf die registrierte E-Mail-Adresse.
- **Groups**: Zugriff auf Gruppenmitgliedschaften und deren Daten.
- **Permissions**: Verwaltung und Prüfung von Berechtigungen.
- **SocketService**: Zugriff auf Aktionen und Events im SocketService.
- **ActiveDirectory**: Integration und Zugriff auf Active Directory.
- **Client Certificate**: Nutzung clientseitiger Zertifikate zur Authentifikation.
- **TOTP**: Unterstützung für Time-based One-Time Passwords (2-Faktor-Authentifizierung).

---

## Authentifizierungsmethoden
Carnetes unterstützt die folgenden Authentifizierungsmethoden:

- **Basic Authentication**:
  - Eigene Nutzerverwaltung mit Benutzername und Passwort.

- **SSPI**:
  - Für nahtlose Authentifizierung innerhalb von Windows-Umgebungen.

- **PKI**:
  - Zertifikatsbasierte Authentifizierung mit hohen Sicherheitsstandards.

- **Active Directory Service (ADS)**:
  - Erweiterte Integration von Active Directory zur zentralen Verwaltung von Benutzern und Zugriffsrechten.
  - ADS ermöglicht Single-Sign-On (SSO) und vereinfachte Synchronisation von Benutzerdaten direkt aus einer Active Directory-Instanz.
  - Die Integration erfolgt über **LDAP**-Protokoll, um Benutzerdaten sicher und effizient abzugleichen.

- **Erweiterungen**:
  - Zusätzliche Authentifizierungsmethoden können unter **carnetes/authentication** integriert werden. Dies bietet Flexibilität bei der Implementierung spezieller Anforderungen, wie z. B. CLM (Certificate Lifecycle Management).

---

## Automatische Anmeldung
- **Automatische Anmeldemethoden** können für jeden OAuth-Client konfiguriert werden, um die Benutzererfahrung zu verbessern und Anmeldevorgänge zu vereinfachen.

---

## Zwei-Faktor-Authentifizierung (2FA)
Zur Erhöhung der Sicherheit unterstützt Carnetes die **2-Faktor-Authentifizierung (2FA)**. Dies umfasst:

- **TOTP (Time-based One-Time Password)**:
  - Unterstützung für gängige Authenticator-Apps wie:
    - **Google Authenticator**: Kostenfrei im [Google Play Store](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=de) erhältlich.
    - **Microsoft Authenticator**: Kostenfrei im [Google Play Store](https://play.google.com/store/apps/details?id=com.azure.authenticator&hl=en-us) verfügbar.
  - Beide Apps generieren Einmal-Codes für die Authentifikation und funktionieren auch offline.

- **Unterstützte Anbieter**:
  - Neben Google und Microsoft Authenticator werden auch Apps wie **Duo Security** oder **Authy** unterstützt.

---

## Sicherheit durch Verschlüsselung
- Alle Kommunikation zwischen Services erfolgt verschlüsselt, um die Integrität und Vertraulichkeit der Daten zu gewährleisten.

---

## Authentifikationskonzept

Die folgende Abbildung veranschaulicht das Authentifikationskonzept von Carnetes:

![Authentifikationskonzept](docs/pics/auth.png)

Die Grafik zeigt die verschiedenen Komponenten und Prozesse innerhalb des Authentifikationsframeworks, einschließlich der sicheren Kommunikation zwischen den Diensten, der Integration von Active Directory und der Rollenverteilung durch die Scopes.

---

## Codebeispiel: PIN-Authentifizierung

Das folgende Beispiel zeigt eine Implementierung einer Authentifikationsroute mit PIN. Dieses Verfahren wird **aus Sicherheitsgründen nicht empfohlen**, da es potenzielle Risiken birgt. Es dient jedoch zur Demonstration, wie eigene Erweiterungen unter **carnetes/authentication** integriert werden können.

```typescript
@Route({
    path: "/start"
})
public route(request: HttpRequest, response: HttpResponse): Promise<void | OpenIDUserInfo> {
    Logger.log(Authentication, 'route ...');
    const promise = new Promise<void | OpenIDUserInfo>((resolve, reject) => {
        try {
            const pin = request.body.pin;
            if (Util.isDefined(pin)) {
                Logger.log(Authentication, 'pin', pin);
                this.execute<any[]>("@socketservice/mssql/**/query/GetLoginByPIN", pin).then(response => {
                    const user = response.data.shift();
                    if (Util.isDefined(user)) {
                        Logger.log(Authentication, 'user', user);
                        resolve({
                            sub: user.RowGuid,
                            name: user.Name,
                            pin: pin,
                            initials: user.Initials
                        });
                    } else {
                        reject(new Error('wrong Pin'));
                    }
                }).catch(error => {
                    Logger.error(Authentication, error);
                    reject(error);
                });
            } else {
                reject(new Error('Nicht korrekt'));
            }
        } catch (exception) {
            Logger.error(Authentication, exception);
            reject(exception);
        }
    });
    return promise;
}
```

### Sicherheitshinweis zur PIN-basierten Authentifizierung

Die PIN-basierte Authentifizierung birgt potenzielle Sicherheitsrisiken, da sie leicht kompromittiert werden kann. Es wird dringend empfohlen, sicherere Authentifizierungsmethoden wie **OAuth2** in Kombination mit **TOTP (Time-based One-Time Password)** oder **PKI (Public Key Infrastructure)** zu verwenden.

Dieses Beispiel dient ausschließlich der Demonstration einer möglichen Erweiterung und sollte nicht in produktiven Umgebungen eingesetzt werden, wo höhere Sicherheitsanforderungen bestehen.

---

# Authorization

Die Authorization spielt eine entscheidende Rolle in der Sicherheitsarchitektur von Carnetes, um sicherzustellen, dass der Zugriff auf geschützte Ressourcen streng kontrolliert und verwaltet wird. Dieses Kapitel bietet eine Übersicht über die Mechanismen zur Zugriffskontrolle, die Flexibilität von Autorisierungs-Händlern und die Möglichkeiten zur Erweiterung.

---

## Blocken von Zugriffen

- Mit dem Authorization-Framework von Carnetes können **Zugriffe gezielt blockiert** werden, basierend auf spezifischen Bedingungen oder definierten Regeln.
- Durch die Implementierung granularer Kontrollmechanismen wird sichergestellt, dass nur berechtigte Benutzer und Systeme Zugriff auf bestimmte Ressourcen erhalten.
- Beispiele für blockierte Zugriffe:
  - Ungültige oder abgelaufene Token.
  - Fehlende Berechtigungen innerhalb eines definierten Scopes.
  - Verstöße gegen Zugriffsbeschränkungen, die auf Benutzerrollen oder anderen Richtlinien basieren.

---

## Autorisierungs-Händler

- **Autorisierungs-Händler** sind zentrale Bausteine im Authorization-Framework und übernehmen die Prüfung, ob eine Anfrage den geltenden Zugriffsvorgaben entspricht.
- Sie ermöglichen die Auswertung von Berechtigungen auf Basis von:
  - Benutzerrollen.
  - Token-Scopes.
  - Regeln für spezifische Ressourcen oder Endpunkte.

### Flexibilität durch Erweiterbarkeit

- Autorisierungs-Händler sind vollständig modular aufgebaut und können **beliebig erweitert** werden.
- Diese Erweiterbarkeit ermöglicht die Integration unternehmensspezifischer Anforderungen oder zusätzlicher Logik für Zugriffskontrollen.
- Neue Händler können unter Berücksichtigung der bestehenden Architektur einfach hinzugefügt werden, um spezifische Geschäftsanforderungen abzudecken.

Das Authorization-Framework von Carnetes ermöglicht die einfache Erweiterung der Zugriffskontrollen durch die Erstellung und Integration eigener Autorisierungs-Händler. Diese Erweiterungen können direkt im Pfad **carnetes/authorization/** abgelegt oder über die Weboberfläche bearbeitet werden.

---

## Unterstützung mehrerer Autorisierungs-Händler

- Jeder **OAuth-Client** kann mehrere Autorisierungs-Händler haben, um komplexe Zugriffskontrollen zu realisieren.
- Diese Konfiguration ermöglicht es, die Anforderungen verschiedener Ressourcen oder Dienste innerhalb eines Clients individuell zu adressieren.
- Die parallele Nutzung mehrerer Händler verbessert die Granularität und Effizienz der Zugriffskontrolle.

---

## Beispiel: Erweiterung der Authorization

Der folgende Code zeigt, wie die Authorization erweitert werden kann. Diese Erweiterung kann unter dem Pfad **carnetes/authorization/** abgelegt werden oder über die Weboberfläche von Carnetes einfach bearbeitet werden:

```typescript
import { Injectable } from '@carnetes/core';
import { Authorizator, OAuth2Client, Logger, OpenIDUserInfo } from '@carnetes/authorization';

@Injectable()
export class Authorization extends Authorizator {

    public authorize(user: OpenIDUserInfo, client: OAuth2Client): Promise<boolean> {
        const promise = new Promise<boolean>((resolve, reject) => {
            try {
                // YOUR CODE STARTS HERE
                resolve(true);
            } catch (exception) {
                Logger.error(Authorization, exception);
                reject(exception);
            }
        });
        return promise;
    }

}
```

---
