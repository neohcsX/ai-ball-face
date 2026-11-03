# KI-Kugel mit Gesicht — Firmware 9.0.0

XiaoZhi-Sprachassistent mit animiertem Gesicht statt Emoji-Anzeige.

**Nur für:** SpotPear ESP32-S3 AI-Kugel (ESP32-S3 **N16R8**, rundes 1,28"-Display 240×240,
Touch, Lautsprecher). Auf anderen Geräten läuft diese Datei nicht.

Datei: `ki-kugel-9.0.0-2026-11-02.bin` (eine Datei, wird ab Adresse 0x0 geschrieben)
SHA-256: `6fbff46442d3949026ddef17a368f4fe9fc2128d0465fa6b696abc185c3107c3`

Update-Datei: `ki-kugel-9.0.0-2026-11-02-update.bin` (behält die Einstellungen, wird ab Adresse **0xd000** geschrieben)
SHA-256: `b353be9df8a2cdd554c9907ca90b28a3e2b80ace8c23c3100ce9f6448d842651`

## Flashen

**Achtung:** Die volle Datei löscht dabei auch die gespeicherten Einstellungen (WLAN, Aktivierung,
gespeicherte Looks). Danach startet die Kugel wie neu. Ohne Datenverlust: siehe „Update ohne Datenverlust“.

### Variante A — im Browser (am einfachsten)
1. Chrome oder Edge öffnen: <https://espressif.github.io/esptool-js/>
2. Kugel per USB-C anstecken (Datenkabel, kein reines Ladekabel), **Connect**, Gerät
   „USB JTAG/serial debug unit“ wählen.
3. Flash Address `0x0`, Datei `ki-kugel-9.0.0-2026-11-02.bin` wählen, **Program**.
4. Nach „Done“ die Kugel kurz abstecken oder Reset drücken.

Klappt es nicht?
- Firefox und Safari können das nicht, nur Chrome oder Edge.
- Kein Gerät in der Liste: anderes Kabel oder anderen USB-Anschluss probieren. Unter Linux muss der
  Benutzer in der Gruppe `dialout` sein.
- „Failed to connect“: Ein anderes Programm (serieller Monitor, Arduino IDE) belegt den Anschluss — schließen.

### Update ohne Datenverlust
Läuft auf der Kugel schon eine frühere Version **dieser** Firmware, behält die Update-Datei WLAN,
Aktivierung und gespeicherte Looks. Gleich wie oben, aber Flash Address **`0xd000`** und Datei
`ki-kugel-9.0.0-2026-11-02-update.bin` — **nie an 0x0** schreiben, dann startet die Kugel nicht mehr
(dann einfach die volle Datei an 0x0 flashen). Kommandozeile:
`esptool --chip esp32s3 write-flash 0xd000 ki-kugel-9.0.0-2026-11-02-update.bin`
Bei Original-/Werks-Firmware oder Problemen immer die volle Datei nehmen.

### Variante B — Kommandozeile
```bash
pip install esptool
esptool --chip esp32s3 write-flash 0x0 ki-kugel-9.0.0-2026-11-02.bin
```
(Port wird meist selbst gefunden; sonst `-p /dev/ttyACM0` bzw. `-p COM5` ergänzen.)

## Erster Start
1. Die Kugel öffnet ein WLAN „Xiaozhi-…“. Mit dem Handy verbinden, im Browser das eigene
   WLAN eintragen. Sie merkt sich bis zu 10 WLANs; ein weiteres trägt man über das Menü ein
   (Extras → WLAN, zweimal tippen).
2. Danach zeigt sie einen **Aktivierungscode**. Auf <https://xiaozhi.me> ein Konto anlegen
   und das Gerät mit dem Code hinzufügen. Dort lassen sich Sprache, Stimme und Rolle einstellen.
   Die Kugel versteht die Wünsche auf Deutsch wie auf Englisch („Katze“ oder „cat“); ihre kurzen
   Bestätigungen („gern“ / „sure“) richten sich nach der Sprache, in der man mit ihr spricht.
3. Aufwecken mit **„Hi ESP“** (englisch: „Hai i-es-pi“, deutlich und nicht zu weit weg) oder kurz aufs Display tippen.

## Was sie kann (Auswahl, einfach sagen)
- **Farben:** 33 Farben (z. B. gold, türkis, navy, rose, olive) für Augen, Kugel, Hintergrund,
  Brille, Brauen, Mund und Pupille gleichermaßen
- **Aussehen:** „Mach die Augen blau“, „Cute-Look“, „Brille auf“, „Kugel rot“,
  „Schuhe aus“, „2D-Modus“, „halt still“ / „beweg dich wieder“ (Kopf, Blick und Heranzoomen stehen; im 2D füllt das Gesicht dann den ganzen Schirm), „würfel dein Aussehen“, „merk dir das“ / „speichere als Outfit …“, „zieh Outfit … an“
- **Looks (eingebaut):** Roboter, Visier, Cute, Box, **Katze**, Pille, Pixel, Ei, Hex, **Otto**, **Kapsel** — „Kapsel-Look“ bringt hohe,
  leuchtend cremeweiße Augen (fröhlich als Bogen, mit Bäckchen). „mach den Otto-Look“ bringt
  hellblaue Kastenaugen mit Bildschirmzeilen und einen kleinen gefüllten Mund (Strich, Lächeln, Hügel oder
  kleines „o“ je nach Stimmung, öffnet sich beim Sprechen). „sei eine Katze“ bringt
  Mandelaugen mit Schlitzpupille, Katzenohren auf der Kugel (im 2D-Modus als zwei Striche über den Augen), Schnauze mit Schnurrhaaren und Pfoten; ab und zu miaut sie, und statt des Fußballs spielt sie mit einem Wollknäuel
  (als Schuhe und statt der Hände)
- **Einzeln:** „Katzenohren / runde Ohren / Ohren weg“, „orange Ohren“, „Ohren hinter den Kopf“,
  „Katzenschnauze“, „Schnurrhaare an/aus“, „Schnurrhaare pink“, „Linien-Augen“ / „Linien-Augen mit Umrandung“ („3D“ zurück), „Pfoten statt Hände“, „Stiefel an“, „Augenform Sechseck“,
  „Schlitzpupille“, „mach die Pupillen glatter“, „glatte Augenränder“
- **Mund/Brauen:** „Mund an“, „gefüllter Mund“, „Mund höher/breiter“, „runde Augenbrauen“, „Brauen braun“
- **Timer / Wecker:** „Timer 5 Minuten“, „erinnere mich in 20 Minuten an den Tee“ (zeigt „tea“), „weck mich um 7 Uhr“, „ist ein Wecker gestellt?“ — ein
  laufender Timer zeigt einen Ring, ein gestellter Wecker einen schwachen hellblauen Ring wie ein
  12-Stunden-Zifferblatt (Punkt = Weckzeit)
- **Gesten & Spaß:** „tanz mal“, „kick den Ball“, „spiel mit dem Ball“, „jonglier mal“, „winke mal“,
  „schlaf jetzt ein“ (schnarcht dann; im Schlaf weckt Antippen zuverlässiger als „Hi ESP“), „Seifenblasen“, „lass eine Fliege / einen Schmetterling fliegen“,
  „zeichne ein Herz / einen Stern“, „hüpf mit den Augen“, „mach Froschaugen“, „gähn mal“, „streck dich“
- **Für ihn malen:** „Ich möchte dir was malen“ — mit dem Finger auf dem Display malen, danach
  „Was habe ich gemalt?“ fragen; er schaut sich das Bild an und rät
- **Er malt für dich:** „Mal mir eine Katze / ein Auto / Pac-Man“ — die KI denkt sich eine Strichzeichnung
  aus, die Kugel malt sie mit Leuchtstift. „Mal mir eine Überraschung“ = Ratespiel („guess what it is!“).
  „Schau dir dein Bild nochmal an“ = er lässt sein eigenes Bild prüfen und bessert nach
  (die Bilder sind kindlich-einfach und gelingen nicht immer — das gehört zum Spiel)
- **Er komponiert:** „Spiel mir ein Lied“, „mach eine Melodie mit Glockenspiel“ — die KI erfindet
  Noten, die Kugel spielt sie (8–30 s, Chiptune oder Glockenspiel); manchmal summt er sie später nach
  — zu einem gemalten Bild spielt er oft eine passende Melodie
- **Galerie:** „Zeig mir deine Bilder“ — er malt seine letzten Bilder (bis zum Neustart) noch einmal,
  jedes mit seiner Melodie
- **Spiele zum Antippen:**
  - „Lass uns Simon spielen“ — vier farbige Tasten am Rand, er spielt eine Tonfolge vor, du tippst sie
    nach (das Viertel des Displays zählt); jede Runde ein Ton mehr
  - „Hütchenspiel“ — er zeigt den Ball unter einem von drei Bechern und mischt; tipp auf den richtigen
    (links/Mitte/rechts). Jede Runde schneller
  - „Tic Tac Toe“ — du bist das rote X, er das gelbe O; danach gleich die nächste Partie (Stand oben)
  - „Maulwurf hauen“ — 30 Sekunden lang Maulwürfe antippen, immer schneller
  - „Reaktionstest“ — tippen, sobald der Rand grün wird; 5 Versuche, dann der Schnitt in Millisekunden
  - „Memory“ — 8 verdeckte Kärtchen im Kreis um ihn, Paare finden mit möglichst wenig Versuchen
  - „Ballon“ — ins Mikrofon pusten bläst den Ballon auf; rechtzeitig aufhören, bevor er platzt
  - „Schere, Stein, Papier“ — gegen ihn, wer zuerst 3 Runden gewinnt
  - „Zahlenraten“ — du denkst dir eine Zahl, er rät und du sagst höher/tiefer
  - „Snake“ — die Schlange läuft auf einem runden Feld; wischen (oder in die Richtung tippen) lenkt,
    Futter macht sie länger und schneller, Rand oder sich selbst beißen = Ende
  - „Lass uns Ping Pong spielen“ (oder Menü → Spiele → gegen ihn → „round“ / „square“) — seine Augen
    werden zu Schlägern, die Pupillen fliegen zusammen zum Ball. Rund im Gesichtsfeld: dein
    Schläger ist der rechte Bogen, mit dem Finger am Rand führen; „eckig“ gibt das klassische Feld im
    Gesichtsbereich (rechter Schläger, Finger hoch/runter). Wer zuerst 5 Punkte hat;
    danach wird er wieder zum Gesicht. Ohne Finger spielt er beide Seiten; bei Langeweile spielt er
    auch von selbst allein — ein Finger im Feld steigt ein, Ansprechen beendet es. Klassische Pong-Pieptöne
  - **Abbrechen:** 1 Sekunde aufs Display drücken
  - Er legt danach selbst auf; Ansprechen („Hi ESP“) beendet das Spiel, bei Tic Tac Toe auch 20 s ohne
    Zug
  - **Rekorde** bleiben gespeichert (neuer Rekord: „NEW RECORD!“ + Applaus); „Was sind meine Rekorde?“,
    „Lösch den Maulwurf-Rekord“ / „Lösch alle Rekorde“
- **Menü (ohne Sprache / ohne Internet):** lang aufs Display drücken. Drei Felder:
  **Spiele** (allein | gegen ihn), **Extras** (Uhr, WLAN einrichten, Bewegung an/aus, 2D-Ohren an den Augen / am Kopf, Glow schwach/mittel/stark), **Einstellungen**
  (Lautstärke, Effekte, Helligkeit). Die Mitte geht zurück bzw. schließt. Die Spiele laufen ganz auf der Kugel
- **Lautstärke:** „Effekte leiser / aus“ (Ball, Brabbeln, Spielgeräusche … getrennt von Sprache und
  Wecker), „zeig die Lautstärke dauerhaft an“, „zeig den Akkustand an“
- **Von selbst:** brabbelt ab und zu, beschäftigt sich bei Langeweile (Ball, Blasen, Fliege,
  Schmetterling, Zeichnen, Musik mit Summen, Spielen mit Konsolen-Tönen, Tic Tac Toe gegen sich selbst,
  Maulwurf hauen allein — Antippen weckt ihn trotzdem wie immer), gähnt beim Einschlafen und streckt
  sich beim Aufwachen, **tanzt mit**, wenn im Raum Musik mit deutlichem Takt läuft (Kopf und Füße im Takt)
- **Uhr:** senkrecht übers Display wischen (Klappuhr → Analog → Gesicht);
  waagerecht wischen = streicheln (mehrmals schnell hintereinander = kitzeln), lang drücken = Menü

## Hinweise
- Die Firmware meldet sich als Version 9.0.0, damit XiaoZhi sie **nicht** automatisch durch
  die Original-Firmware ersetzt. Wer zur Original-Firmware zurück will, flasht diese neu.
- Gespräche laufen über die Server von xiaozhi.me (Cloud). Gesicht, Töne und Animationen
  laufen komplett auf der Kugel. Ein gemaltes Bild geht nur dann an den Server (Bilderkennung),
  wenn man fertig gemalt hat bzw. danach fragt — gespeichert wird es auf der Kugel nicht.
  Seine eigenen Bilder schickt er nur, wenn man ihn bittet, sie nachzusehen.
- Die Kugel meldet sich alle 2 Sekunden im eigenen WLAN (UDP-Port 4210, nur lokales Netz, nicht ins
  Internet) mit Name, Look und Stimmung — für das Zusammenspiel mit weiteren Gesichtern. Von anderen
  Geräten nimmt sie nur Look-Befehle an (Look, Farbe, Pupille, Brauen, Mund).
- Lizenzhinweise der enthaltenen Software (XiaoZhi, ESP-IDF, LovyanGFX u. a.): `LIZENZEN.txt` —
  bei einer Weitergabe bitte immer mitgeben.
