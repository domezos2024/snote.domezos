# snote.domezos
Teile vertrauliche Nachrichten mit automatischer Selbstzerstörung. Vollständig lokal verschlüsselt. Keine Speicherung. 100 % Datenschutz. DSGVO Kommunikation, AES-AES-GCM-256, sichere Dateiübertragung, snote.domezos
# 🛡️ snote.domezos – Privacy-first Messaging Platform

**snote.domezos** ist eine modulare Web-App zum Teilen von selbstzerstörenden, lokal verschlüsselten Nachrichten. Sie kombiniert moderne Kryptografie mit minimaler Serverexposition und maximaler Nutzerkontrolle.

## 🔐 Features

- **AES-GCM-256 Verschlüsselung**  
  Nachrichten werden clientseitig mit AES-GCM (256 Bit) verschlüsselt – inklusive Authenticated Encryption für Integrität und Vertraulichkeit.

- **Random Key Generation**  
  Jeder Text wird mit einem zufällig generierten Schlüssel verschlüsselt. Der Schlüssel wird niemals gespeichert oder übertragen – nur lokal verwendet.

- **Lokale Ver- und Entschlüsselung**  
  Die gesamte Kryptografie erfolgt im Browser. Der Server sieht niemals Klartext oder Schlüsselmaterial.

- **Selbstzerstörende Nachrichten**  
  Einmal geöffnet, wird die Nachricht gelöscht. Optional: Zeitbasierte Selbstzerstörung (z. B. nach 10 Minuten).

- **Teilen per Link**  
  Der verschlüsselte Text wird als Payload gespeichert. Der Schlüssel wird als Fragment (`#key`) im Link übergeben – außerhalb des HTTP-Requests.

  Beispiel: https://domezos-ware.org/test.php?file.txt&pass=xxxxx

  
## 🧩 Architektur

| Komponente        | Beschreibung |
|------------------|--------------|
| **Frontend**      | HTML/JS mit WebCrypto API, keine externen Libraries |
| **Backend (PHP)** | Speichert nur verschlüsselte Payloads, keine Logs, keine IPs |
| **Storage**       | Temporäre Dateiablage mit automatischer Löschung |
| **Link-Handling** | Schlüssel im Fragment, nicht übertragbar an Server |

## 🚀 Ablauf

1. Nutzer schreibt Nachricht → `msg`  
2. Browser generiert `key` (256 Bit)  
3. `msg` wird mit `key` via AES-GCM verschlüsselt → `ciphertext`  
4. `ciphertext` wird an Server gesendet, `key` bleibt lokal  
5. Link wird generiert: `https://snote.domezos/?id=XYZ#key`  
6. Empfänger öffnet Link → Browser extrahiert `key` aus Fragment  
7. `ciphertext` wird geladen, lokal entschlüsselt  
8. Nachricht wird angezeigt und sofort gelöscht  

## 🧪 Sicherheitshinweise

- **Zero Knowledge**: Server kennt keine Schlüssel, keine Klartexte  
- **Kein Tracking**: Keine Cookies, keine IP-Logs, keine Analytics  
- **Replay-Schutz**: Einmal geöffnet = gelöscht  
- **XSS/CSRF geschützt**: Keine evals, keine dynamischen Injections  

## 📦 Deployment

- PHP ≥ 7.4  
- Schreibrechte für temporäre Dateiablage  
- HTTPS zwingend erforderlich (WebCrypto)  

## 🧠 Erweiterungsideen

- QR-Code-Generierung für Links  
- Ablaufzeit im Link kodieren  
- Datei-Upload mit clientseitiger Verschlüsselung  
- Admin-Panel zur Speicherüberwachung

- 
  
