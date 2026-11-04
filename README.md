# Ausblick – Turnos (Shift-Manager)

Einfacher Schichtplaner und **Basis für die Schichtplanung aller Ausblick-Kunden-Apps**. Aufgebaut wie `ausblick-clientes`: eine einzige `index.html` auf GitHub Pages, Daten in privaten Repos, Zugang per 12-stelligem Code.

## Funktionen (Planung)

- **Wochenleiste:** oben 7 Tageskacheln mit Ampel (grün ok · gelb unbesetzt · rot Konflikt oder Lücke). Bleibt beim Scrollen stehen. Antippen springt zum Tag. Am Handy wechselt Wischen die Woche (im Zeitstrahl: den Tag).
- **Drei Ansichten:**
  - **Días** – pro Tag, mit Avatar, Zeit und Rollen-Etikett. Vergangene Tage sind ausgegraut.
  - **Línea** – ein Tag als Zeitstrahl, eine Zeile pro Person, darunter Öffnungszeiten und Abdeckung (grün = Mindestbesetzung erfüllt, rot = fehlt, gold = jemand da). Er zeigt immer 0–24 Uhr; Öffnungs- und Betriebszeit sind darin farbig hinterlegt. In eine leere Zeile tippen legt dort eine Schicht an.
  - **Tabla** – Person × Tag mit Stundensumme. Am PC Schichten per **Drag & Drop** verschieben, mit Alt/Strg kopieren. Druckt im Querformat.
- **Schicht anlegen:** Datum, Von/Bis (Nachtschicht automatisch ☾), Rolle, Mitarbeiter, Notiz. „Turnos típicos“ füllen mit einem Tipp. „Repetir también en“ für weitere Tage. Bestehende Schicht: Löschen oder Duplizieren.
- **Personalgruppen** (z. B. Küche, Floor 1, Floor 2; Personal → Grupos oder Configuración):
  - Jede Person ist in höchstens einer Gruppe. Zeitstrahl und Personalliste zeigen die Namen eingerahmt pro Gruppe, die Tabelle mit einer Kopfzeile je Gruppe. Leere Gruppen bleiben als Ziel sichtbar.
  - **Drag & Drop:** Personen in eine andere Gruppe ziehen oder innerhalb der Gruppe umsortieren – im Zeitstrahl (am Namen), in der Tabelle (erste Spalte) und in der Personalliste. Maus: drücken und ziehen. Handy: kurz gedrückt halten, dann ziehen (normales Wischen scrollt weiter). Mit Rückgängig.
  - **Eigene Öffnungs- und Betriebszeiten pro Gruppe** (Personalgruppen → Button „Zeiten des Betriebs“ / „Eigene Zeiten“): z. B. Küche 10–22 mit 1 h Vor- und Nachbereitung, während der Betrieb 12–24 hat. Im Zeitstrahl bekommen die Zeilen der Gruppe ihre eigenen Zeiten hinterlegt, am PC steht die Zeit neben dem Gruppennamen. „Zeiten des Betriebs nehmen“ setzt eine Gruppe zurück.
  - **Gruppenname antippen** (im Zeitstrahl, in der Tabelle oder in der Personalliste) öffnet die Einstellungen der Gruppe: Name, Zeiten, wer drin ist, Löschen.
  - Gruppen umbenennen, sortieren (↑ ↓) und löschen; wird eine Gruppe gelöscht, sind ihre Leute „Ohne Gruppe“.
- **Öffnungs- und Betriebszeiten** (Configuración → Horario de apertura):
  - Pro Wochentag geöffnet von–bis oder geschlossen.
  - Dazu Vorbereitung vor Öffnung und Nachbereitung nach Schließung in Minuten; Betriebszeit = Öffnungszeit plus beides.
  - Gleiche Zeit für Öffnen und Schließen = 24 h. Schließt es früher als es öffnet (z. B. 18:00–02:00), endet der Tag nach Mitternacht.
  - Die Zeiten stehen in der Tagesansicht, in der Tabelle und in der Wochenleiste (geschlossene Tage gestrichelt).
  - Die Rubro-Modelle bringen typische Zeiten mit, wenn noch keine eingetragen sind (Cochera 24 h, Peluquería Di–Sa 9–20 …).
- **Warnungen:**
  - Doppelbelegung.
  - Zu wenig Ruhezeit (Standard 12 h, einstellbar, 0 = aus).
  - Abwesenheit.
  - Frei-Wunsch.
  - Fehlende Rolle.
  - **Mindestbesetzung** unterschritten, z. B. „Mo–Fr 06–22: mind. 1 Playero“. Unbesetzte Schichten zählen nicht als Abdeckung.
- Die Statistik-Chips oben lassen sich antippen: Unbesetzte filtern, nur Konflikte zeigen, zur ersten Lücke springen, Wünsche öffnen.
- **Personal:**
  - Rollen (keine = darf alles), Soll-Stunden, Notizen und Abwesenheiten.
  - **Stundenkonto** pro Monat: gearbeitet, Soll und Saldo. Soll = Wochenstunden ÷ 7 pro Tag; Urlaub und Krankheit zählen nicht.
  - Der Wochenplan geht per WhatsApp an die Person.
- **Woche:**
  - Vorwoche kopieren (Doppelte werden übersprungen).
  - **Plan als WhatsApp an alle**: ein Text pro Woche für die Team-Gruppe.
  - Drucken.
- **Export:** Schichten und Stunden pro Person (inkl. Soll/Saldo) als CSV für Excel.
- **Rubro-Modelle:** Cochera, Peluquería, Gastronomía, Comercio, General. Sie legen Rollen und typische Schichten an; die Vorlagen bekommen dabei die erste Rolle des Modells.
- ES / EN / DE, Woche ab Montag oder Sonntag, offline-fähig, „Deshacer“ überall.

## „Mis turnos“ für Mitarbeitende

Mitarbeitende öffnen dieselbe App mit einem **eigenen Code**. Sie sehen nur ihre eigenen Schichten (mit „Con: …“, wer gleichzeitig arbeitet) und können **Frei-Wünsche** abgeben. Der Chef sieht die Wünsche im Plan (lila) und bei der Planung („pidió franco“). Er kann sie genehmigen (das legt automatisch eine Abwesenheit an) oder ablehnen; den Status sieht die Person in ihrer App.

Sicherheit:
- Der Mitarbeiter-Token erreicht **nur** das Team-Repo und kann den echten Plan weder lesen noch ändern.
- Die App des Chefs veröffentlicht dort bei jedem Speichern eine abgespeckte Kopie (`plan.json`): Namen, Rollen und Schichten von einer Woche zurück bis drei Monate voraus. Telefonnummern, Personalnotizen und Abwesenheitsgründe sind nicht enthalten.
- Beim Erstellen des Mitarbeiter-Codes prüft die App, dass der Token **nicht** an das Daten-Repo kommt.

## Repos und Dateien

| Repo | Sichtbarkeit | Inhalt |
|---|---|---|
| `ausblick-shiftmanager` | öffentlich (Pages) | `index.html`, `access.json`, `access-staff.json` |
| `ausblick-shiftmanager-data` | privat | `turnos.json` – der Plan |
| `ausblick-shiftmanager-team` | privat | `plan.json` (Kopie für Personal), `wishes.json` (Frei-Wünsche) |

`turnos.json` = `{ v: 1, c: { id → Eintrag } }`, jeder Eintrag mit Art `k`:

| k | Inhalt |
|---|---|
| `emp` | Mitarbeiter: `n`, `tel`, `pos` (IDs), `h` (Soll-Std./Woche), `notas` |
| `pos` | Rolle: `n`, `col`, `o` |
| `grp` | Personalgruppe: `n`, `o` (Reihenfolge), optional eigene `hours`/`pre`/`post` (wie bei `set`); beim Mitarbeiter `g` (Gruppe) und `o` (Platz in der Gruppe) |
| `tpl` | Typische Schicht: `n`, `a`, `b`, `pos` |
| `need` | Mindestbesetzung: `pos` (leer = egal), `days` (0 = So … 6 = Sa), `a`, `b`, `n` |
| `sh` | Schicht: `d`, `a`/`b` (`b ≤ a` = endet am Folgetag), `pos`, `emp` (leer = unbesetzt), `note`, `by` |
| `off` | Abwesenheit: `emp`, `from`, `to`, `kind` (`vac`/`sick`/`off`), `note` |
| `set` | Einstellungen (id `set`): `biz`, `ws` (1 = Mo, 0 = So), `rest` (Std.), `hours` (`{0–6: {o, c}}`, fehlender Tag = geschlossen, `null` = keine Zeiten), `pre`/`post` (Min.) |

`wishes.json` hat dasselbe Format: `emp`, `from`, `to`, `note`, `st` (`''`/`ok`/`no`), `by`. Alle Einträge haben `t` (letzte Änderung, neuere gewinnt) und ggf. `del: true`.

## Einrichtung (einmalig)

1. Private, leere Repos **`ausblick-shiftmanager-data`** und **`ausblick-shiftmanager-team`** anlegen.
2. In diesem Repo Settings → Pages → Branch `main` / root.
3. **Chef-Token:** Fine-grained Token mit Zugriff auf **beide** privaten Repos, Contents: Read and write.
4. App öffnen → „Primera vez (token)“, Daten- und Team-Repo eintragen → `access.json` herunterladen und hier hochladen. Weitere Chef-Geräte brauchen dann nur Name + Code.
5. **Mitarbeiter-Token:** zweiter Fine-grained Token **nur** für `ausblick-shiftmanager-team`, Contents: Read and write.
6. In der App Configuración → „Acceso para el personal“ → Token einfügen → `access-staff.json` herunterladen und hier hochladen. Den Mitarbeiter-Code an das Personal geben.

Ohne Team-Repo funktioniert alles außer „Mis turnos“. Token erneuert: einmal „Primera vez“ mit dem neuen Token und neue `access.json` hochladen; die anderen Geräte holen ihn sich selbst.

## Für einen Kunden übernehmen

1. `index.html` kopieren und **nur den Block `APP`** oben im Script ändern:
   ```js
   var APP = {
     repo: 'lucashcandido/<kunde>-turnos',
     data: 'lucashcandido/<kunde>-turnos-data',
     team: 'lucashcandido/<kunde>-turnos-team',
     file: 'turnos.json',
     prefix: '<kurz>',          // eigener Speicher-Präfix pro App
     preset: 'parking'          // Rubro, das zuerst angeboten wird
   };
   ```
2. Neue Branche? Einen Eintrag in `PRESETS` ergänzen (Rollen + typische Schichten in es/en/de).
3. Eigene Farbe: `--accent` in `:root` (hell und dunkel).
4. Einrichtung wie oben mit den Repos des Kunden.

Verbesserungen am Kern zuerst hier, dann in die Kopien übernehmen.
