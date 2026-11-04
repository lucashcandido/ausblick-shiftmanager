# Ausblick – Turnos (Shift-Manager)

Einfacher Schichtplaner und **Basis für die Schichtplanung aller Ausblick-Kunden-Apps**. Aufgebaut wie `ausblick-clientes`: eine einzige `index.html` auf GitHub Pages, Daten in einem privaten Repo, Zugang per 12-stelligem Code.

## Funktionen

- **Plan (Woche):** Ansicht „Días“ (pro Tag, fürs Handy) oder „Tabla“ (Person × Tag mit Stundensumme, für PC und Druck). Woche vor/zurück, „Hoy“, Filter nach Person oder „Sin asignar“.
- **Schicht anlegen:** Datum, Von/Bis (Nachtschicht über Mitternacht automatisch, ☾), Puesto, Mitarbeiter, Notiz. „Turnos típicos“ füllen Zeiten mit einem Tipp. Beim Anlegen „Repetir también en“ für weitere Tage derselben Woche. Bestehende Schicht: Löschen oder Duplizieren.
- **Konflikte** werden sofort angezeigt (im Formular, in der Liste und rot umrandet in der Tabelle): Doppelbelegung (auch über Mitternacht und Wochengrenze), Abwesenheit, Person ohne den Puesto. Soll-Stunden überschritten → Summe rot.
- **Mitarbeiterauswahl** im Formular: Wer den Puesto hat, steht oben; „ausente“ / „ocupado 06–14“ wird dabei angezeigt.
- **Personal:** Name, Telefon, Puestos (keiner = darf alles), Soll-Stunden pro Woche, Notizen, Abwesenheiten (Vacaciones / Enfermedad / Franco). Stunden der angezeigten Woche in der Liste. **„Enviar horario por WhatsApp“** schickt der Person ihre Schichten der Woche als Text.
- **Copiar semana anterior:** übernimmt alle Schichten der Vorwoche; doppelte werden übersprungen, mit Rückgängig.
- **Exportieren** (Configuración): Zeitraum wählen → „Turnos“ oder „Horas por persona“ als CSV für Excel. **Imprimir semana** druckt die Tabelle im Querformat.
- **Rubro-Modelle:** Cochera, Peluquería, Gastronomía, Comercio, General. Legt typische Puestos und Schichten an (nur was noch fehlt). Beim ersten Start angeboten, später unter Configuración → Puestos y turnos típicos.
- **Sprachen:** Español, English, Deutsch (nach Gerätesprache, umschaltbar). Woche beginnt Montag oder Sonntag.
- Offline-Änderungen werden später gespeichert; bei zwei Geräten gewinnt pro Eintrag die neuere Änderung. Alles mit „Deshacer“.

## Daten

Eine Datei `turnos.json` im privaten Repo, `{ v: 1, c: { id → Eintrag } }`. Jeder Eintrag hat eine Art `k`:

| k | Inhalt |
|---|---|
| `emp` | Mitarbeiter: `n`, `tel`, `pos` (IDs), `h` (Soll-Std./Woche), `notas` |
| `pos` | Puesto/Bereich: `n`, `col` |
| `tpl` | Turno típico: `n`, `a`, `b`, `pos` |
| `sh` | Schicht: `d` (YYYY-MM-DD), `a`/`b` (HH:MM; `b ≤ a` = endet am Folgetag), `pos`, `emp` (leer = sin asignar), `note`, `by` |
| `off` | Abwesenheit: `emp`, `from`, `to`, `kind` (`vac`/`sick`/`off`) |
| `set` | Einstellungen (id `set`): `biz` (Name), `ws` (1 = Mo, 0 = So) |

Alle Einträge haben `t` (letzte Änderung) und ggf. `del: true` (gelöscht, damit das Löschen auch auf andere Geräte kommt).

## Einrichtung (einmalig)

1. Privates, leeres Repo **`ausblick-shiftmanager-data`** anlegen.
2. In diesem Repo Settings → Pages → Branch `main` / root.
3. Fine-grained Token erstellen, der **nur** `ausblick-shiftmanager-data` erreicht (Repository permissions → Contents: Read and write).
4. App öffnen → „Primera vez (token)“ → `access.json` herunterladen und in dieses Repo hochladen. Alle anderen Geräte brauchen dann nur Name + Code.
5. Optional eigene Domain (z. B. `turnos.ausblicksistemas.com`) per `CNAME`.

Token erneuert: einmal „Primera vez“ mit dem neuen Token, neue `access.json` hochladen – die anderen Geräte holen ihn sich selbst (der Code bleibt gleich).

## Für einen Kunden übernehmen

Der Shift-Manager ist als Vorlage gedacht. Für einen Kunden (oder als Modul in einer Kunden-App):

1. `index.html` kopieren und **nur den Block `APP`** oben im Script ändern:
   ```js
   var APP = {
     repo: 'lucashcandido/<kunde>-turnos',        // öffentliches Repo mit index.html + access.json
     data: 'lucashcandido/<kunde>-turnos-data',   // privates Daten-Repo
     file: 'turnos.json',
     prefix: '<kurz>',                            // eigener Speicher-Präfix pro App, z. B. 'ap' für Angel Parking
     preset: 'parking'                            // Rubro, das zuerst angeboten wird
   };
   ```
2. Neue Branche? Einen Eintrag in `PRESETS` ergänzen (Puestos + typische Schichten in es/en/de).
3. Eigene Farbe: `--accent` in `:root` (hell und dunkel).
4. Einrichtung wie oben mit den Repos des Kunden.

Kundenspezifische Extras (z. B. Stempeluhr, Lohnabrechnung, Tausch-Anfragen) kommen in die Kopie; Verbesserungen am Kern zuerst hier, dann in die Kopien übernehmen.
