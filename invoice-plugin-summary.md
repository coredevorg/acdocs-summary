# Rechnungsworkflow summary

## Rechnungsworkflow

**Ab welcher Version verfügbar?**• *agorum core pro* 10.3.0

**Hinweis**: Diese Dokumentation bezieht sich auf die aktuellste Version des Plugins. [Aktualisieren](#) Sie ggf. das hier beschriebene Plugin, um die Dokumentation verwenden zu können.

Name: *agorum core invoice plugin*

Der Rechnungsworkflow unterstützt bei der Erfassung und Kontierung von Rechnungen.

Mithilfe des Rechnungsworkflows können Sie:

* Duplikate von Rechnungen prüfen
* Rechnungen erfassen und prüfen
* Freigaben für die Rechnungserfassung definieren
* Ausgabedateien für die Finanzbuchhaltung erzeugen

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/82432b20-f7a4-11ec-bc85-005056aa0ecc)

```auto
OCR: Abgeben, Speichern, Lieferantenname: Baumeister, Rechnungsnummer: 101/20, Weiterverrechnung, Referenznummer: Ist eine Gutschrift, Steuersatz, Summe Nettobetrag: 2612,5, Rabattierter Betrag, Lieferantennummer: 888795, Rechnungsdatum: 24.04.2021, Bezahlt, Eingangsdatum: 29.06.2022, Summe Steuerbetrag: 496,38, Summe Bruttobetrag: 3108,88, Zuschlag, Protokoll Log, Positionsliste 1-5 von Beschreibung, Nettobetrag, Bruttobetrag, MwSt, Konto, Gegenkonto, Kostenstelle, Arbeitszeit, 1650, 1963,5, 888795, Brandschott, 101,15, 888795, Fehlerstroms, 89,25, Sicherungsau, 130, 154,7, Verdrahtungs, 165, 196,35, 888795, 888795, 888795, Zahlungsbedingung Datum, Zahlungsbedingung Tage, Prozent, Zahlungsziel, Skontobetrag, Freigabeschritte, Freigabeschritte 0-0 von Rechnungsbetrag 1/1, Anzeigenname Beschreibung von Freigabetyp, Freigebender Eskalation Tage Eskalation Freigabe, Freigabe sachlich sachlich, Freigabe nur lesbar inhaltlich inhaltlich, Freigabe mit Kontier Benutzer roi roi, Benutzer roi roi Name, Freigabeschritte Lieferant speichern Beschreibung Betreff Zuletzt dui Letzte Inhalt von Kommentar 1-0 von Rechnung ablehnen docform Delegieren Direkt buchen Weiter zur
```

Übersicht: Rechnungsworkflow

### Voraussetzungen

* * *

Folgende Voraussetzungen müssen erfüllt sein, damit Sie den Rechnungsworkflow installieren und verwenden können:

* *agorum core docform* muss aktiviert sein.

[Aktivieren](#) Sie die notwendigen Module über das *agorum core support tool:*

* DocForm
* DocForm extended
* DocForm positions

#### Empfohlene Voraussetzungen: DATEV-Schnittstelle

Möchten Sie DATEV spezifische Ausgabedateien erzeugen, müssen Sie die DATEV-Schnittstelle ebenfalls über das *agorum core* *support tool* [aktivieren](#):

* DATEV CSV interface
* DATEV CSV interface (with positions)
* DATEV XML interface online
* DATEV XML interface online (with positions)

### Rechnungsworkflow konfigurieren

* * *

Sobald Sie die [Voraussetzungen](#voraussetzungen) erfüllt haben, konfigurieren Sie vor der ersten Benutzung den Rechnungsworkflow. Sie können die Konfigurationen zum Rechnungsworkflow jederzeit nachträglich ändern. Eine Änderung gilt jedoch nur für Rechnungsworkflows, die das System ab dem Zeitpunkt der Änderung erstellt.

So konfigurieren Sie den Rechnungsworkflow:

1. Klicken Sie oben rechts im Hauptmenü auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAA50lEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YBgIwMTExcHNzMwgJCTEwvn379v/nz58Hwh0YdvLy8jIwPnr06P9AhQy6i0AhxfjgwYP/gyJ4oI4YdRCh2MAaQrW7njG8+PybkF4UeQleVoZmNymS9GBTjNVBtjNuMTz++Iskw2X52RgOZ6iRpIdoB1FsKgUGDI1E7b/oLsPjDyRGmQAbw8Y4Zaxho6CggCEOLG6wqsUaQtR2EMhmZEfhcgxIHV2jDOQofI6hu4OISetDI9sPuoKRmKCllRq6JmpiPDH4HDToGmiDrgk72Br5ADojm9UgCytGAAAAAElFTkSuQmCC) und dann auf **agorum core invoice plugin > Rechnungsworkflow konfigurieren**.
2. Nehmen Sie die Konfigurationen zum Rechnungsworkflow vor.
3. Speichern Sie die Konfigurationen.

#### Maskeneinstellungen für die Rechnungserfassung

In der Registerkarte *Allgemein > Abschnitt „Maskeneinstellungen“* können Sie bei der Konfiguration des Rechnungsworkflows optional diverse Einstellungen vornehmen. Mit diesen Einstellungen steuern Sie das Aussehen und das Verhalten der Bedienoberfläche während der Rechnungserfassung.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/b2322ce0-f7a5-11ec-bc85-005056aa0ecc)

```auto
OCR: Maskeneinstellungen, Delegation, Direkte Freigabe, Kontierung, Dokumente
```

Maskeneinstellungen für die Rechnungserfassung

**Delegation**

Bei Aktivierung dieser Einstellung erscheint in der Bedienoberfläche unten die Schaltfläche *Delegieren an*. Mit dieser Schaltfläche können Sie die Rechnungserfassung an eine andere Kollegin oder anderen Kollegen abgeben. Diese Kollegin oder dieser Kollege erhält die gleiche Bedienoberfläche, Sie geben die Aufgabe also lediglich ab.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/c9a5a270-f7a6-11ec-bc85-005056aa0ecc)

```auto
OCR: Kommentar, Rechnung ablehnen, docform, Delegieren, Direkt buchen, Weiter zur
```

Schaltfläche *Delegieren an*

**Direkte Freigabe**

Bei Aktivierung dieser Einstellung erscheint in der Bedienoberfläche unten die Schaltfläche *Direkt buchen*. Mit dieser Schaltfläche beenden Sie den Workflow direkt und archivieren die Rechnung. Die archivierte Rechnung finden Sie im *agorum core smart assistant* in diesem Ordner:

```auto
Dateien/Akten/Lieferanten/<Buchstabe des Lieferanten>/<Name des Lieferanten>/Rechnungen/<Jahr>/<Monat>
```

Diese Schaltfläche steht nur zur Verfügung, wenn Sie die Einstellungen [Rechnungsdatenänderung](#Rechnungsdatenaenderung) und [Kontierung](#Kontierung) aktiviert haben.

**Rechnungsdatenänderung**

Bei Aktivierung dieser Einstellung können Sie die Rechnungsdaten bei der Rechnungserfassung eingeben oder ändern. Wenn Sie diese Einstellung nicht aktivieren, erscheinen die Daten einsehbar in der Bedienoberfläche, Sie können die Rechnungsdaten jedoch nicht mehr eingeben oder ändern.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/9b61b140-f7a8-11ec-bc85-005056aa0ecc)

```auto
OCR: Rechnungsnummer: 101/20, Weiterverrechnung:, Referenznummer:, Ist eine Gutschrift:, Steuersatz 1: 19, Summe Nettobetrag: 2612.5, Rabattierter Betrag:, Rechnungsdatum: 24.04.2021, Bezahlt:, Eingangsdatum*: 29.06.2022, Summe Steuerbetrag 1: 496.38, Summe Bruttobetrag: 3108.88, Zuschlag:
```

Rechnungsbezogene Daten sind änderbar

**Kontierung**

Bei Aktivierung dieser Einstellung können Sie die Kontierungsinformationen bei der Rechnungserfassung eingeben oder ändern. Wenn Sie diese Einstellung nicht aktivieren, erscheint der Abschnitt *Kontierungsinformationen* einsehbar in der Bedienoberfläche, Sie können jedoch keine Kontierungsinformationen eingeben oder ändern.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/7d440100-f7b6-11ec-bc85-005056aa0ecc)

```auto
OCR: -Kontierungsinformationen, Positionsliste, Beschreibung, Nettobetrag, Bruttobetrag, MwSt, Konto, Arbeitszeit, 1650, 1963.5, Brandschott, 101.15, Fehlerstroms, 89.25, Sicherungsau, 130, Verdrahtungs, 165, 154.7, 196.35, 888795, 888795, 888795, 888795, 888795, Gegenkonto, Kostenstelle, 1-5, von
```

Kontierungsinformationen sind änderbar

**Standard-Freigabeschritte**

Definieren Sie Standard-Freigabeschritte, um die Rechnung weiteren Benutzergruppen vorzulegen. Sie entscheiden dabei durch eine freie Textangabe, welche Schritte vorzunehmen sind und wer welchen Zugriff hat:

| Zugriff | Beschreibung |
| --- | --- |
| Nur lesend | Die zugewiesenen Rechnungsfreigebenden können die Rechnungsdaten nur sehen, nicht aber anpassen. |
| Rechnungsdatenänderung | Die zugewiesenen Rechnungsfreigebenden können die Rechnungsdaten bei Bedarf abändern. |
| Kontierung | Die zugewiesenen Rechnungsfreigebenden können die Rechnung kontieren. |

Ihre Angaben zeigt das System bei jeder Rechnungserfassung an. Ein Benutzer kann Sie jedoch überarbeiten und somit eine Anpassung pro Lieferant vornehmen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/8a86b410-fb72-11ec-bc85-005056aa0ecc)

```auto
OCR: Freigabeschritte, 1-3, Anzeigenname, Beschreibung, Freigabetyp, Freigebender, Eskalation, Eskalation, Freigabe, Freigabe, Tage, inhaltlicher Check, Kontrolle, Nur lesend, Benutzer, d4wdr, d4wdr_ma, Gruppe, GRP_agorum_invoice_Buchhaltung_Read, Kontrolle, Rechnu, Rechnungsdaten, Benutzer, d4wdr, d4wdr_gl, Gruppe, GRP_agorum_invoice_Buchhaltung_Read, Kontierung, Rechnung kontier, Kontierung, Gruppe, GRP_agorum_invoice_Buchhaltung_Read, Gruppe, GRP_agorum_invoice_Buchhaltung_Read, Freigabeschritte, Lieferant, speichern
```

Freigabeschritte einstellen

**Dokumente hinzufügen**

Bei Aktivierung dieser Einstellung können Sie bei der Rechnungserfassung im Abschnitt *Anhänge* einen beliebigen Anhang zur Rechnung hinzufügen, etwa Schriftverkehr wie E-Mails oder Bilddateien, die zur Rechnung gehören. Die Dateien müssen Sie zuvor in *agorum core* hochgeladen haben, oder Sie fügen diese hinzu, indem Sie die Dateien mit der Maus hineinziehen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/4b89a330-f7b7-11ec-bc85-005056aa0ecc)

```auto
OCR: Name, Beschreibung, Betreff, Zuletzt dui, Letzte Inhalt, Intern, akt ua von, 1-0, von
```

Dokumente bei der Rechnungserfassung hinzufügen

* Mit ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAWCAYAAADafVyIAAABKUlEQVRIS2P8//fn/3fvPzF8/fad4d+/fwzUAExMTAzcXJwMQoJ8DIxv37z+//nLV2qYi2EGLw83A+OjR4/+U8vl6DaAfML44MGD/zRxPtRQ+ltw9eUPhsDFdxl+/UX1GC87E8P+VDUGEW4WkjyM4YOWfS8Y5px+g9UQkCUWstxY5bw1+BkCtAUw5EiygJDTm1ylGOKMhFCUkWUBJysTAycLI8O7739RDEsxFWGocZKg3AKYQQqdV4aYBb3eMgzBOpgRaTvjFsPjj78YKA6iEKDhRtLcDDriHAx6kpwMyy68BwdRz6EX4Pig2AJYgNM8DiL0BRlyLMUYbGbcpE0k48oPRAURrqKCUCZjY2ZkWB+rzKANjB9kQP/CjpBLSZWnfYVD8yqT1pU+AL5y2r+2/MqhAAAAAElFTkSuQmCC) öffnen Sie die Ordnerauswahl und wählen eine Datei als Anhang aus.
* Mit ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAWCAYAAADafVyIAAAB90lEQVRIS2P8//fn/3fvPzF8/fad4d+/fwzUAExMTAzcXJwMQoJ8DIxv37z+//nLV2qYi2EGLw83A+OjR4/+U8vl6DaAfML44MGD/zRxPtRQvBZ8//2PoffwK4b99z4zgNgOSjwMGeaiDHICbES7CacFF59/Z4hZeZ/h889/DAKczAxMQCM/AdkgUOUowZBkIkyUJVgt+PjjL4PNjJtgA1ZHKzFoiHKA2SBfxK96wHDqyTeGZRGKDFby3AQtwWpB35FXDJOOvmLYGKfMoC/JiWLI77//GayBlisAg2kV0HJCAKsFIFfefvuT4VimOlb9jXufMyw+947hTqk2IfOxp6KwpfcYnn/+w3A4Qw2rAS37XjDMOf2G4UG5DnkWlG9/yrD2ygeGs7kaDPwczBiGuM29w8AMjPXtiSrkWXD15Q8G/0V3GYykOBmWAiOTlZkRbhDM9XXOkkSlJJzJdN6ZtwxNwLDmZGVicFfjYxDhYmHYc+czw4P3Pxm4gGJt7lIMAdoC5PkApuvG6x8MxVufMNx8/ZPhz7//DFJ8rAxZFqIML7/8Zph87DWDiwofw5xgObyWkF1UpKx9BPTRJ4KWkG0ByNnEWEKRBTBLTj7+wrA2RolBTQSS45EBxRaADHv++TeDJC8r1rigigX4Ypn2FQ7Nq0xaV/oAldQBzgDqjLIAAAAASUVORK5CYII=) öffnen Sie das *agorum core information center* und suchen nach einer Datei.
* Mit ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAWCAYAAADafVyIAAABbklEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YqAGYmJgYuLm5GYSEhBgY3759+//z58/UMBfDDF5eXgbGR48e/aeWy9FtAPmE8cGDB/9p4nyooURZcPH5d4bMDY8YfvyGxBEHKxPD9AA5Bn1JToJuw2nB1Zc/GLwX3CFoAEjB1gQVBm1xDqxqcVrw9NNvhobdz4iyoMFVikGaj5U0C0CqJx19xbDg7Fu8liQYCzPkWYvhVIM3Dlr2vWCYc/oNXgtSTEUYapwkKLeAhYmR4c8/SIJDZlPFAjMZLoaJfrIMgYvvgS1YH6vEkL7+EcMlYOqiigUSvKwMW+KVUYLBde4dhvff/1DHApDJoGQISo4gAEq+oGQMAlTxgSAnC8PuZIjhMEBVH+gBc+zMQDnaxQF6yqFaKuo8+JJh+onXePNBpoUoQ7m9OHn54Pff/wxJax4CI/Q7VgO0xTkZ5oXIM7AyM5JnAV6nEylJ+wqH5lUmrSt9ALI++NVritZNAAAAAElFTkSuQmCC) löschen Sie eine Datei aus dem Abschnitt *Anhänge*.
* Klicken Sie auf *Anhänge übernehmen*, um die gewählte Datei zur Rechnungserfassung hinzuzufügen. Die hinzugefügte Datei erscheint rechts im [Detailfenster](#) unterhalb der Rechnung.

#### Ausgabedatei Finanzbuchhaltung

Definieren Sie Ihre Ausgabedatei und nehmen Sie Einstellungen zur Kontierung und zu den Zahlungsbedingungen vor.

1. Klicken Sie oben rechts im Hauptmenü auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAA50lEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YBgIwMTExcHNzMwgJCTEwvn379v/nz58Hwh0YdvLy8jIwPnr06P9AhQy6i0AhxfjgwYP/gyJ4oI4YdRCh2MAaQrW7njG8+PybkF4UeQleVoZmNymS9GBTjNVBtjNuMTz++Iskw2X52RgOZ6iRpIdoB1FsKgUGDI1E7b/oLsPjDyRGmQAbw8Y4Zaxho6CggCEOLG6wqsUaQtR2EMhmZEfhcgxIHV2jDOQofI6hu4OISetDI9sPuoKRmKCllRq6JmpiPDH4HDToGmiDrgk72Br5ADojm9UgCytGAAAAAElFTkSuQmCC) und dann auf **agorum core invoice plugin > Rechnungsworkflow konfigurieren**.
2. Wechseln Sie in der sich öffnenden Oberfläche in die Registerkarte **Ausgabedatei Finanzbuchhaltung**.
3. Nehmen Sie die Konfigurationen zum Rechnungsworkflow vor.
4. Speichern Sie die Konfigurationen.
5. Erstellen Sie Ihre Ausgabedateien manuell: Klicken Sie oben rechts im Hauptmenü auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAA50lEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YBgIwMTExcHNzMwgJCTEwvn379v/nz58Hwh0YdvLy8jIwPnr06P9AhQy6i0AhxfjgwYP/gyJ4oI4YdRCh2MAaQrW7njG8+PybkF4UeQleVoZmNymS9GBTjNVBtjNuMTz++Iskw2X52RgOZ6iRpIdoB1FsKgUGDI1E7b/oLsPjDyRGmQAbw8Y4Zaxho6CggCEOLG6wqsUaQtR2EMhmZEfhcgxIHV2jDOQofI6hu4OISetDI9sPuoKRmKCllRq6JmpiPDH4HDToGmiDrgk72Br5ADojm9UgCytGAAAAAElFTkSuQmCC) und dann auf **agorum core invoice plugin > Ausgabedateien manuell erzeugen.**

**Tipps**:

* Zur Erstellung der Ausgabedatei benötigen Sie die DATEV-Module von *agorum core* (siehe [Voraussetzungen](#voraussetzungen)).
* Wählen Sie zur Fehlerbehandlung bei fehlgeschlagenen Ausgabedateien IT-affine Personen aus, da die Fehlermeldung oftmals auf einen regulären Ausdruck hinweist:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/810e2d70-fb9d-11ec-bc85-005056aa0ecc)

```auto
OCR: Ein- oder mehrere Dokumente konnten nicht korrekt exportiert werden. Sie hier die Rechnungen direkt den Rechnungsworkflow zur Fehlerkorrektur schicken. Fehlermeldungen der Dokumente, Dateiname der Rechnung RE50001 2018_11_25.txt, uuid 8d848460fb6a11ec9e58-02420a0a000f, Fehlermeldung UUID 8d848460fb6a11ec9e58-02420a0a000f, Hinweis REGEX Fail, Mapping key agorum_datev_entry_batch_account_number, Mapping value 9865A, Regex 1,9, Achtung bitte Kontonummer korrigieren, diese muss numerisch sein, Abbrechen von den Rechnungseingangsworkflow schicken.
```

Fehlermeldungen bei der Erstellung der Ausgabedateien

### E-Mail-Einstellungen vornehmen

* * *

Treffen Ihre Eingangsrechnungen per E-Mail in *agorum core* ein, stehen Ihnen diverse Einstellmöglichkeiten zur Verfügung:

1. Klicken Sie oben rechts im Hauptmenü auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAA50lEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YBgIwMTExcHNzMwgJCTEwvn379v/nz58Hwh0YdvLy8jIwPnr06P9AhQy6i0AhxfjgwYP/gyJ4oI4YdRCh2MAaQrW7njG8+PybkF4UeQleVoZmNymS9GBTjNVBtjNuMTz++Iskw2X52RgOZ6iRpIdoB1FsKgUGDI1E7b/oLsPjDyRGmQAbw8Y4Zaxho6CggCEOLG6wqsUaQtR2EMhmZEfhcgxIHV2jDOQofI6hu4OISetDI9sPuoKRmKCllRq6JmpiPDH4HDToGmiDrgk72Br5ADojm9UgCytGAAAAAElFTkSuQmCC) und dann auf **agorum core invoice plugin > E-Mail-Einstellungen konfigurieren**.
2. Nehmen Sie die [Konfigurationen](#Konfiguration-E-Mail-Einstellungen) vor.
3. Testen Sie Ihre regulären Ausdrücke mit einem Kontrollausdruck. Klicken Sie dazu auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABkAAAAUCAYAAAB4d5a9AAABjklEQVRIibXVvUrDUBTA8X9DcGhasA3dOlQHLY6Ci6hzOwkuvoCDg+Ai+ABOQhfBoUOfQenU7paMnURjB6W0i4SkgXKdJNehEZua0LSkZ8y9nF/OR0hKSikBHMdBCIHneSQRiqKgaRr5fJ6UlFI6jsN4PE4k+Wxks1kUACHESoDf3AqQWIvCwvO8CTIvLMOkdGvStJeDYiAC4+Ub+Kb1tlxb5yP2iJatclVWaT990l0F0u24tPUMpwcZKnxh9BJHLAwTKjs5CnqOqg61VythpDemhkp1WwM0jo/SYNoLL0BKSin7/X7IkaDZ+OAyJGHlcIP6vhYbia7EHtGKeOOoBeg2nyndvv87U6OMbselTZqH6012A/iQ84aL0YPdrSBwYkLlcA16wNRZRCWTgVPOBgGAkAX4Azao7xcDOETNxBZYukZhtoJHuDkrTp77dwYBIHxO4ZXMAvjts132GkMs/04cILqSqPDn0dbXuSu4XMYAFkemIeKv8uKID92/5biI+a2kpJRyMBis7J+iKAo/K1TQJeq+lbYAAAAASUVORK5CYII=).
4. Speichern Sie die Konfigurationen.

#### Konfigurationen

Die Konfigurationen befinden sich unten in den E-Mail-Einstellungen in Form von Spalten:

| Spalte | Beschreibung |
| --- | --- |
| E-Mail-Adresse/Domäne | Angabe der E-Mail-Adresse oder E-Mail-Domäne, auf die sich die anderen beiden Spalten beziehen. |
| Übergabe bestimmter E-Mail-Anhänge an docform | Sollte die E-Mail des Lieferanten mehrere Anhänge besitzen, tragen Sie einen regulären Ausdruck ein, der die entsprechende Rechnung und keinen der andere Anhänge an agorum core docform weiterleitet. Tragen Sie keinen regulären Ausdruck ein, startet jeder einzelne E-Mail-Anhang einen Rechnungsworkflow. Besitzt die E-Mail keinen Anhang, reicht das System die E-Mail an den Workflow. Soll eine Regel für die Übergabe generell für alle E-Mail-Adressen gelten, setzen Sie in der Spalte E-Mail-Adresse/Domäne den Wert .\* Möchten Sie weitere Anhänge zulassen, setzen Sie in dieser Spalte pro E-Mail-Adresse einen weiteren Anhangstyp: \\.(pdf|docx|doc|txt). In diesem Fall extrahiert das System auch Anhänge vom Typ txt. |
| Übergabe an OCR | Mit dieser Einstellung übergeben Sie Ihre Rechnung trotz vorhandener Textinformationen an die OCR. Das ist etwa der Fall, wenn Sie während des docform-Trainings feststellen, dass die Identifikationspunkte für ein docform-Training als Bild und nicht als Textinformationen vorliegen. Durch diesen OCR-Zwang stellen Sie sicher, dass bei neu eingehenden Dokumenten der Bildbereich als Textinformation im Training vorliegt und ein Benutzer ihn markieren kann. Diese Einstellung wird in der Regel nicht sofort eingestellt, sondern ergibt sich mit der Zeit und aus dem Feedback der docfom-Verantwortlichen. Für diesen Anwendungsfall ist keine Angabe bei Übergabe bestimmter E-Mail-Anhänge an docform notwendig. |

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/703a6610-fb9f-11ec-bc85-005056aa0ecc)

```auto
OCR: Mail Einstellungen konfigurieren, diesen Mail Einstellungen definieren Sie unter anderem das System von bestimmten Mail Adressen nur einen bestimmten Anhang den Rechnungsworkflow reicht und diesen die OCR Engine schickt Hinweise Definieren Sie Ihren Ausdruck genau wie Das System unterscheidet bei nicht zwischen Groß- und Kleinschreibung Falls Sie negieren wollen setzen Sie Beginn ein zip Das System bearbeitet die Einstellung jede Mail von oben nach unten und der erste passende Eintrag greift Sie daher die Reihenfolge Ihrer Angaben Kontrollausdruck, Angabe eines Beispieltextes zum Testen Ihres Ausdrucks Zur klicken Sie unten der jeweiligen Zeile neben dem testenden Ausdruck auf den Ausdruck der Mail Adresse gegen Kontrollausdruck testen Text RE12345678.pdf, Mail Adresse buchhaltung@lieferantenbeispiel.com, info@musterfirma.*, rechnungen@agorum.com, Abbrechen 1-4 von bestimmter Mail docform OCR pdf docx doc pdf 0-9 .pdf pdf doc doc txt Speichern
```

E-Mail-Einstellungen konfigurieren

### CSV-Dateien pflegen

* * *

Nachdem Sie den [Rechnungsworkflow konfiguriert](#RechnungsworkflowKonfigurieren) haben, pflegen Sie Ihre CSV-Dateien für die Finanzbuchhaltung. In diesen CSV-Dateien befinden sich etwa Konten, Gegenkonten oder Kostenstellen. Die Pflege ist notwendig, damit Sie diese Daten später bei den Kontierungsinformationen in der Rechnungserfassung auswählen können.

Die nachfolgend aufgeführten CSV-Dateien enthalten bereits Daten, die bei DATEV standardmäßig vorkommen. Ersetzen Sie diese mit Ihren eigenen Angaben.

| Was wollen Sie pflegen? | Pfad zur CSV-Datei |
| --- | --- |
| Konten | Eigene Dateien‎/Administration‎/workspace‎/agorum.invoice‎/csv‎/accounts.csv |
| Gegenkonten | Eigene Dateien‎/Administration‎/workspace‎/agorum.invoice‎/csv‎/contra-accounts.csv |
| Kostenstellen | Eigene Dateien‎/Administration‎/workspace‎/agorum.invoice‎/csv‎/cost\_center.csv |
| MwSt.-Sätze | Eigene Dateien‎/Administration‎/workspace‎/agorum.invoice‎/csv‎/tax\_rates.csv |
| Zahlungsfälligkeiten | Eigene Dateien‎/Administration‎/workspace‎/agorum.invoice‎/csv‎/payment\_conditions.csv |
| Datum für Zahlungsfälligkeiten | Eigene Dateien‎/Administration‎/workspace‎/agorum.invoice‎/csv‎/payment\_conditions\_date.csv Weitere Informationen zum Aufbau dieser CSV-Datei finden Sie unter Aufbau der CSV-Datei „payment\_conditions\_date.csv“. |

**Hinweis:** Der Workflow bearbeitet nur die Spalten *value* und *text*:**value**Das System setzt diesen Wert als Metadatum auf das Dokument. Das Metadatum ist anschließend in den Exportdateien enthalten.**text**Das System zeigt diesen Wert den Benutzern in den Oberflächen an.

#### Aufbau der CSV-Datei "payment\_conditions\_date.csv"

```auto
receiptDate;discount1;dueDate1;month1;discount2;dueDate2;month2;discount3;dueDate3;month3
10;3;20;0;0;31;0;;;
20;2;31;0;0;10;1;;;
31;3;10;1;0;20;1;;;
```

| Spalte | Beschreibung |
| --- | --- |
| receiptDate | Rechnungsdatum |
| discount1 | Skonto in Prozent für das erste Fälligkeitsdatum |
| dueDate1 | 1\. Fälligkeitstag, etwa bis zum 10. dieses Monats |
| month1 | Definiert, ob sich der 1. Fälligkeitstag auf den jetzigen Monat (0) oder auf den nächsten Monat (1) bezieht. |
| discount2 | Skonto in Prozent für das zweite Fälligkeitsdatum |
| dueDate2 | 2\. Fälligkeitstag, etwa bis zum 20. dieses Monats |
| month2 | Definiert, ob sich der 2. Fälligkeitstag auf den jetzigen Monat (0) oder auf den nächsten Monat (1) bezieht. |
| discount3 | Skonto in Prozent für das dritte Fälligkeitsdatum |
| dueDate3 | 3\. Fälligkeitstag, etwa bis zum 31. dieses Monats |
| month3 | Definiert, ob sich der 3. Fälligkeitstag auf den jetzigen Monat (0) oder auf den nächsten Monat (1) bezieht. |

### Rechnungsworkflow starten

* * *

Nachdem Sie den [Rechnungsworkflow konfiguriert](#RechnungsworkflowKonfigurieren) und Ihre [CSV-Dateien gepflegt](#csv-dateien) haben, starten Sie den Rechnungsworkflow auf zwei Arten:

* [automatisch](#RechnungsworkflowAutomatischStarten)
* [manuell](#RechnungsworkflowManuellStarten)

#### Rechnungsworkflow automatisch starten

Das System startet den Rechnungsworkflow automatisch, wenn es:

* Dokumente in den Verarbeiten-Ordner unter */agorum/roi/Files/Eingänge/Eingangsrechnung/Dokumente/Verarbeiten* geschoben und verarbeitet hat
* Dokumente in den Trennen-Ordner unter */agorum/roi/Files/Eingänge/Eingangsrechnung/Dokumente/Trennen* geschoben, getrennt und anschließend zur weiteren Verarbeitung unter */agorum/roi/Files/Eingänge/Eingangsrechnung/Dokumente/Verarbeiten* geschoben hat
* E-Mails mit Anhängen vom Ordner */agorum/roi/Files/Eingänge/Eingangsrechnung/Mails* abgeholt und die Anhänge extrahiert hat (nur Anhänge vom Typ *pdf*, *docx* oder *doc*).

**Tipp**: Ihr Administrator kann auch [eigene Regeln für das Extrahieren von Anhängen anlegen](#Eigene Regeln für das Extrahieren von Anhängen anlegen), um etwa weitere Anhangstypen zuzulassen.

* Doppelte Dokumente mit gleichem Dateinamen ignoriert das System. Diese Dokumente gelangen nicht erneut in den Rechnungsworkflow.
* Wenn eine E-Mail keinen Anhang hat, betrachtet das System die E-Mail als Rechnung und schickt sie an *docform*. Anschließend verarbeitet *docform* die Rechnung.

#### Rechnungsworkflow manuell starten

Sie können den Rechnungsworkflow manuell über das Kontextmenü starten, um ein beliebiges Dokument an den Rechnungsworkflow zu senden.

So starten Sie den Rechnungsworkflow manuell:

1. Öffnen Sie auf der Startseite von *agorum core* den **Smart assistant**.
2. Markieren Sie ein Dokument mit der rechten Maustaste.
3. Wählen Sie im Kontextmenü **An Rechnungsworkflow senden**.**Ergebnis**: Das System sendet das gewählte Dokument an den Rechnungsworkfow. Es prüft nicht, ob das Dokument bereits einen Rechnungsworkflow durchlaufen hat.

### Fehlende Lieferantenakte

* * *

Rechnungen archiviert das System automatisch in den entsprechenden Lieferantenakten:

```auto
Dateien/Akten/Lieferanten/<Lieferantenname> - <Lieferantennummer>/Rechnungen/<Rechnungsjahr>/<Rechnungsmonat>
```

Sollte die in *docform* angegebene Lieferantennummer sowie der Lieferantenname mit keiner Akte übereinstimmen, erscheint dieser Workflowschritt:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/85589da0-fb77-11ec-bc85-005056aa0ecc)

```auto
OCR: Hinweis, Der angegebene Lieferant 9865A existiert nicht, Stimmen alle Angaben wie Lieferantenname und -nummer legen Sie diesem Schritt die Lieferantenakte neu an, Sind die Angaben jedoch falsch schicken Sie die Rechnung mit einem Hinweis docform damit der Ausleseprozess des Dokumentes korrigiert wird, Lieferantenname Lang und Kurz GmbH, Lieferantennummer 9865A, Kommentar die Anzeige innerhalb von docform Audit, Bitte tragen Sie hier einen Kommentar das Audit docform ein Beispielsweise "Bitte Training anpassen die Lieferantennummer ist nicht korrekt", docform Lieferantenakte erstellen
```

Fehlende Lieferantenakte

Sie entscheiden an dieser Stelle, ob die *docform-*Verantwortlichen einen Fehler gemacht haben und das Dokument korrigiert gehört (Schaltfläche *Zurück an docform*), oder ob alle Angaben korrekt sind und die fehlende Lieferantenakte angelegt wird (Schaltfläche *Lieferantenakte erstellen*).

**Tipp**: Tragen Sie als Lieferantennummer die in DATEV genutzte Kontonummer ein. Dieser Wert trägt das System als Standard-Wert bei der Kontierung in die Konto-Spalte ein. Dadurch sparen Sie sich einige Klicks und müssen lediglich Gegenkonto und Kostenstelle ausfüllen.

### Duplikatsprüfung

* * *

Bevor die Rechnungserfassung startet, überprüft der Rechnungsworkflow, ob die eingegangene Rechnung ein Duplikat ist. Hierzu prüft das System die Belegnummer, das Belegdatum sowie die Lieferantennummer. Liegt ein Duplikat vor, erscheint folgender Workflowschritt:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/25419450-fb6b-11ec-bc85-005056aa0ecc)

```auto
OCR: wurde ein Duplikat gefunden, Bitte Sie die Rechnung verworfen oder die Rechnung dennoch weiterverarbeitet werden soll, Kommentar die Anzeige innerhalb von docform Audit, Bitte tragen Sie hier einen Kommentar das Audit docform ein Beispielsweise Bitte Training anpassen die Lieferantennummer ist nicht korrekt, Rechnung verwerfen, docform, Dennoch verarbeiten
```

Duplikatsprüfung

In der Duplikatsprüfung stehen Ihnen drei Optionen in Form von Schaltflächen zur Verfügung:

| Schaltfläche | Beschreibung |
| --- | --- |
| Rechnung verwerfen | Das System löscht die eingegangene Rechnung. Ein Administrator kann die Rechnung bei Bedarf über den Serverpapierkorb wiederherstellen. |
| Zurück an docform | Das System reicht die Rechnung mit dem eingetragenen Kommentar zurück an docform. |
| Dennoch verarbeiten | Das System leitet die Rechnung an die Rechnungserfassung weiter. Zudem markiert das System die Rechnung als Duplikat. Ein Benutzer kann die Rechnung über den Filter Eingangsrechnungen in der Suche erneut suchen und finden. |

### Rechnungserfassung

* * *

Die Rechnungserfassung enthält je nach Konfiguration folgende Informationen:

| Abschnitte | Beschreibung |
| --- | --- |
| Lieferantenbezogene Daten | Lieferantenname und Lieferantennummer Diese Werte können Sie nur korrigieren, wenn Sie oder ein Benutzer das Dokument zurück an docform gesendet haben. |
| Rechnungsbezogene Daten | Die rechnungsbezogenen Daten stammen aus docform und enthalten die Kopf- sowie Positionsmetadaten der Rechnung. Diese Werte können Sie manuell anpassen oder die Rechnung zurück nach docform senden. Je nach Konfiguration können Sie diese Werte nur lesen und nicht bearbeiten. |
| Kontierungsinformationen | Kontieren Sie die Rechnung. Dieser Abschnitt ist optional. Ihr Administrator kann ihn aktivieren. Konto, Gegenkonto und Kostenstelle pflegen Sie in CSV-Dateien. |
| Zahlungsbedingungen | Wählen Sie die passenden Zahlungsbedingungen aus. Dieser Abschnitt ist optional. Ihr Administrator kann ihn aktivieren. Zahlungsbedingungen pflegen Sie in CSV-Dateien. |
| Freigabeschritte | Zeigt Ihnen die Standard-Freigabeschritte an. Bei Bedarf können Sie diese pro Lieferant überarbeiten. Klicken Sie dazu nach Ihren Änderungen auf die Schaltfläche Freigabeschritte für Lieferanten speichern. Ihre Freigabeschritte werden nacheinander (von oben nach unten) von Ihren Arbeitskollegen bearbeitet. Ihr Administrator konfiguriert die Standard-Freigabeschritte. Wenn Ihr Administrator keine Standard-Freigabeschritte konfiguriert hat, stellt das System die Liste leer dar. |
| Anhänge | Fügen Sie dem Workflow weitere Dokumente wie Bestellungen oder Lieferscheine hinzu. Sie dienen zur weiteren Informationsbeschaffung für die Freigabeschritte oder der Buchungskontrolle und Kontierung. Klicken Sie auf die Schaltfläche Anhänge übernehmen, übernimmt das System Ihre Dateien in die rechte Ansicht der Dokumente. Dieser Abschnitt ist optional. Ihr Administrator kann ihn aktivieren. Sie können Dokumente auch hinzufügen, indem Sie sie mit der Maus hineinziehen. Das System fügt diese nur dem Workflow hinzu und archiviert sie in keinen anderen Ordner. |
| Kommentar | Geben Sie einen Kommentar an, um die Rechnung abzulehnen oder zurück an docform zu senden. |

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/82432b20-f7a4-11ec-bc85-005056aa0ecc)

```auto
OCR: Abgeben, Speichern, Lieferantenname: Baumeister, Rechnungsnummer: 101/20, Weiterverrechnung, Referenznummer: Ist eine Gutschrift, Steuersatz, Summe Nettobetrag: 2612,5, Rabattierter Betrag, Lieferantennummer: 888795, Rechnungsdatum: 24.04.2021, Bezahlt, Eingangsdatum: 29.06.2022, Summe Steuerbetrag: 496,38, Summe Bruttobetrag: 3108,88, Zuschlag, Protokoll Log, Positionsliste 1-5 von Beschreibung, Nettobetrag, Bruttobetrag, MwSt, Konto, Gegenkonto, Kostenstelle, Arbeitszeit, 1650, 1963,5, 888795, Brandschott, 101,15, 888795, Fehlerstroms, 89,25, Sicherungsau, 130, 154,7, Verdrahtungs, 165, 196,35, 888795, 888795, 888795, Zahlungsbedingung Datum, Zahlungsbedingung Tage, Prozent, Zahlungsziel, Skontobetrag, Freigabeschritte, Freigabeschritte 0-0 von Rechnungsbetrag 1/1, Anzeigenname Beschreibung von Freigabetyp, Freigebender Eskalation Tage Eskalation Freigabe, Freigabe sachlich sachlich, Freigabe nur lesbar inhaltlich inhaltlich, Freigabe mit Kontier Benutzer roi roi, Benutzer roi roi Name, Freigabeschritte Lieferant speichern Beschreibung Betreff Zuletzt dui Letzte Inhalt von Kommentar 1-0 von Rechnung ablehnen docform Delegieren Direkt buchen Weiter zur
```

Rechnungserfassung

Die Rechnungserfassung bietet Ihnen zudem je nach Einstellung des Rechnungsworkflows folgende Schaltflächen zur Verarbeitung der Rechnung an:

| Schaltfläche | Beschreibung |
| --- | --- |
| Rechnung ablehnen | Lehnen Sie die Rechnung ab, beendet das System den Workflow. Sie finden die abgelehnten Rechnungen in agorum core information center im Filter Eingangsrechnungen unter Freigaben > abgelehnt. Abgelehnte Rechnungen schützt das System vor Benutzeränderungen, setzt diese Rechnungen aber nie revisionssicher. Ihr Administrator kann diese Rechnungen daher manuell löschen. |
| Zurück an docform | Die rechnungsbezogenen Daten stammen aus docform und enthalten die Kopf- sowie Positionsmetadaten der Rechnung. Diese Werte können Sie manuell anpassen oder die Rechnung zurück nach docform senden. Je nach Konfiguration können Sie diese Werte nur lesen und nicht bearbeiten. |
| Delegieren an | Übergeben Sie die Rechnungserfassung an einen anderen Kollegen. Die Auswahl eines Benutzers oder einer Benutzergruppe zeigt Ihnen das System nach Klick auf diese Schaltfläche an. Diese Schaltfläche ist optional. Ihr Administrator kann sie aktivieren. |
| Direkt buchen | Überspringen Sie die Freigabeschritte und beenden Sie den Workflow. Diese Schaltfläche ist optional. Ihr Administrator kann sie aktivieren. |
| Weiter zur Prüfung | Starten Sie die anschließenden Freigabeschritte und abschließende Buchungskontrolle. |

### Freigabeschritte

* * *

Die in der Rechnungserfassung definierten Freigabeschritte arbeiten die Bearbeiter von oben nach unten nacheinander ab. Dabei haben die Freigeber Zugriff auf eine ähnliche Bedienoberfläche zur Rechnungserfassung, nur mit unterschiedlichen Rechten aufgrund des gewählten Freigabetyps:

| Freigabetyp | Beschreibung |
| --- | --- |
| Nur lesend | Der Freigebende kann nur lesend auf die Daten der Rechnungserfassung zugreifen. |
| Rechnungsdatenänderung | Der Freigebende kann die Rechnungsdaten abändern, hat aber auf alle anderen Werte nur lesenden Zugriff. |
| Kontierung | Der Freigebende kann wie auch in der Rechnungserfassung die Rechnungsdaten, Zahlungsbedingungen sowie Kontierung bearbeiten. |

Ein Freigebender kann nie:

* dem Workflow Dokumente hinzufügen
* Freigabeschritte definieren

Ob ein Freigebender eine Rechnung freigegeben oder abgelehnt hat, sehen Sie in einer Freigabehistorie, die am Anfang der Bedienoberfläche des Workflows erscheint:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/6a3824d0-fba6-11ec-bc85-005056aa0ecc)

```auto
OCR: Freigabehistorie,Von,Datum,Kommentar,roi,roi,04.07.2022,16:32,Rechnung ist mich i.O.,roi,roi,04.07.2022,16:32,Rechnung ist mich i.O.,roi,GRP_agorum,invoic,04.07.2022,16:33,Achtung Fehler Betrag Position stimmt nicht ausgemacht waren 100 und keine 120,e_invoice_mails_Rea,Aktion,Rechnungserfassung,Freigegeben,Abgelehnt,Lieferantenbezogene Daten,Lieferantenname,Schill GmbH,Lieferantennummer,72000
```

Freigabehistorie

#### Freigebender lehnt eine Rechnung ab

Wenn ein Freigebender eine Rechnung ablehnt, kann der Workflow zwei Wege einschlagen, die in Abhängigkeit zur [abschließenden Buchungskontrolle](#Buchungskontrolle) stehen:

**Es findet keine abschließende Buchungskontrolle statt**Falls Ihr Administrator den optionalen Schritt der Buchungskontrolle nicht aktiviert hat, ist die Entscheidung der Freigebenden maßgebend. Lehnt etwa der erste Freigebende die Rechnung ab, schickt das System die Rechnung nicht mehr an die anderen Freigebenden. Stattdessen lehnt das System diese Rechnung direkt ab und beendet den Workflow. Die abgelehnten Rechnungen finden Sie im *agorum core information center* im [Filter](#Filter) *Eingangsrechnungen* unter *Freigaben > abgelehnt*.

**Es findet eine abschließende Buchungskontrolle statt**Falls Ihr Administrator den optionalen Schritt der Buchungskontrolle nicht aktiviert hat, ist die Entscheidung der Freigebenden lediglich eine Information. Lehnt etwa der erste Freigebende die Rechnung ab, schickt das System die Rechnung dennoch an die weiteren Freigebenden. Erst nachdem alle Freigebenden ihre Entscheidung getroffen haben, startet das System die abschließende Buchungskontrolle, und die Rückmeldung zu den Freigabeschritten liegt vor. In der abschließenden Buchungskontrolle können die Verantwortlichen die nächsten Schritte einplanen und bei Bedarf die Rechnung dennoch abrechnen.

### Abschließende Buchungskontrolle

* * *

Die optionale abschließende Buchungskontrolle dient als abschließende Kontrolle, in der die Verantwortlichen nicht nur alle Rechnungsinformationen editieren können, sondern auch die Freigabehistorie einsehen können.

In der abschließenden Buchungskontrolle stehen Ihnen drei Optionen in Form von Schaltflächen zur Verfügung:

| Schaltfläche | Beschreibung |
| --- | --- |
| Rechnung ablehnen | Lehnen Sie die Rechnung ab, beenden Sie den Workflow. Sie finden die abgelehnten Rechnungen im agorum core information center im Filter Eingangsrechnungen unter Freigaben > abgelehnt. Abgelehnte Rechnungen schützt das System vor Benutzeränderungen, setzt diese Rechnungen aber nie revisionssicher. Ihr Administrator kann diese Rechnungen daher manuell löschen. |
| Dennoch verarbeiten | Das System leitet die Rechnung an die Rechnungserfassung weiter. Zudem markiert das System die Rechnung als Duplikat. Ein Benutzer kann die Rechnung über den Filter Eingangsrechnungen in der Suche erneut suchen und finden. |
| Buchen | Beenden Sie den Workflow. Das System erstellt eine Ausgabedatei erstellen, um die Rechnung zu bezahlen. |

### Fehlerhafter Export

* * *

Sollte ein Export einer Rechnung fehlgeschlagen sein, gibt das System eine Fehlermeldung aus. Dazu erzeugt das System einen Workflowschritt für die entsprechende Benutzergruppe:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/810e2d70-fb9d-11ec-bc85-005056aa0ecc)

```auto
OCR: Ein- oder mehrere Dokumente konnten nicht korrekt exportiert werden. Sie hier die Rechnungen direkt den Rechnungsworkflow zur Fehlerkorrektur schicken. Fehlermeldungen der Dokumente, Dateiname der Rechnung RE50001 2018_11_25.txt, uuid 8d848460fb6a11ec9e58-02420a0a000f, Fehlermeldung UUID 8d848460fb6a11ec9e58-02420a0a000f, Hinweis REGEX Fail, Mapping key agorum_datev_entry_batch_account_number, Mapping value 9865A, Regex 1,9, Achtung bitte Kontonummer korrigieren, diese muss numerisch sein, Abbrechen von den Rechnungseingangsworkflow schicken.
```

Fehlgeschlagener Export

Ziehen Sie Kollegen aus Ihrer IT hinzu, um schnell die Ursache aufgrund der angegebenen Fehlermeldung identifizieren zu können. Dieses Team kann mit einem entsprechenden Kommentar die Rechnung an den Rechnungseingangsworkflow zurückschicken.

Wenn Sie die Schaltfläche *Abbrechen* wählen, brechen Sie den Vorgang ab, und das System erstellt keine Exportdatei, da der Fehler nie korrigiert wurde.

### Ausgabedateien erzeugen

* * *

Ausgabedateien für die Finanzbuchhaltung können Sie auf zwei Arten erzeugen:

* manuell
* automatisch

#### Ausgabedateien manuell erzeugen

1. Klicken Sie oben rechts im Hauptmenü auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAA50lEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YBgIwMTExcHNzMwgJCTEwvn379v/nz58Hwh0YdvLy8jIwPnr06P9AhQy6i0AhxfjgwYP/gyJ4oI4YdRCh2MAaQrW7njG8+PybkF4UeQleVoZmNymS9GBTjNVBtjNuMTz++Iskw2X52RgOZ6iRpIdoB1FsKgUGDI1E7b/oLsPjDyRGmQAbw8Y4Zaxho6CggCEOLG6wqsUaQtR2EMhmZEfhcgxIHV2jDOQofI6hu4OISetDI9sPuoKRmKCllRq6JmpiPDH4HDToGmiDrgk72Br5ADojm9UgCytGAAAAAElFTkSuQmCC) und dann auf **agorum core invoice plugin > Ausgabedateien manuell erzeugen**.**Ergebnis:** Das System verarbeitet alle im *agorum core information center*\-Filter *Zum Sammeln markierte Dokumente* vorliegende Rechnungen und erstellt das gewünschte Ausgabeformat.Sie finden die erzeugten Dateien in diesem Ordner:

    ```auto
    Bereiche/Buchhaltung/Archiv Ausgabedatei | Ausgabedateien
    ```

#### Ausgabedateien automatisch erzeugen

1. Klicken Sie oben rechts im Hauptmenü auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAA50lEQVRIS2P8DwTv3r1j+Pr1K8O/f/8YBgIwMTExcHNzMwgJCTEwvn379v/nz58Hwh0YdvLy8jIwPnr06P9AhQy6i0AhxfjgwYP/gyJ4oI4YdRCh2MAaQrW7njG8+PybkF4UeQleVoZmNymS9GBTjNVBtjNuMTz++Iskw2X52RgOZ6iRpIdoB1FsKgUGDI1E7b/oLsPjDyRGmQAbw8Y4Zaxho6CggCEOLG6wqsUaQtR2EMhmZEfhcgxIHV2jDOQofI6hu4OISetDI9sPuoKRmKCllRq6JmpiPDH4HDToGmiDrgk72Br5ADojm9UgCytGAAAAAElFTkSuQmCC) und dann auf **agorum core invoice plugin > Rechnungsworkflow konfigurieren**.
2. Wechseln Sie in der sich öffnenden Oberfläche in die Registerkarte **Ausgabedatei Finanzbuchhaltung**.
3. Unter **Format der Ausgabedatei für die Finanzbuchhaltung** definieren Sie die Uhrzeit des täglichen Exports (Stunde sowie Minute).

#### Fehlerhafte Ausgabedateien

Konnte der Prozess für ein oder mehrere Rechnungen keine Ausgabedatei erzeugen, erstellt das System einen neuen Workflowschritt:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/810e2d70-fb9d-11ec-bc85-005056aa0ecc)

```auto
OCR: Ein- oder mehrere Dokumente konnten nicht korrekt exportiert werden. Sie hier die Rechnungen direkt den Rechnungsworkflow zur Fehlerkorrektur schicken. Fehlermeldungen der Dokumente, Dateiname der Rechnung RE50001 2018_11_25.txt, uuid 8d848460fb6a11ec9e58-02420a0a000f, Fehlermeldung UUID 8d848460fb6a11ec9e58-02420a0a000f, Hinweis REGEX Fail, Mapping key agorum_datev_entry_batch_account_number, Mapping value 9865A, Regex 1,9, Achtung bitte Kontonummer korrigieren, diese muss numerisch sein, Abbrechen von den Rechnungseingangsworkflow schicken.
```

Fehlerhafter Export

In diesem Beispiel konnte das System keine Ausgabedatei erstellen, da dem DATEV-Parameter *agorum\_datev\_entry\_batch\_account\_number* ein fehlerhafter Eintrag übergeben wurde. Statt einer Zahlenfolge enthält die Lieferantennummer einen Buchstaben: 9865A**.**

Entweder Sie ignorieren diese Fehlermeldung über die Schaltfläche *Abbrechen*, oder Sie schicken die Rechnung zurück an den Rechnungseingangsworkflow, mit der Bitte, die Lieferantennummer in *docform* anzupassen.

#### Ausgabedateien an Buchhaltungssoftware übergeben

Das folgende Vorgehen stellt eine Momentaufnahme dar, insbesondere das Vorgehen in DATEV. Wenden Sie sich bei Fragen zum Vorgehen in DATEV an Ihren DATEV-Experten.

1. Starten Sie **DATEV**.
2. Öffnen Sie das **Rechnungswesen**.
3. Klicken Sie **Stapelverarbeitung** an.
4. Klicken Sie in dem sich neu geöffneten Fenster auf die Schaltfläche **Importieren**.
5. Wählen Sie dieses Quellverzeichnis aus:

    ```auto
    Bereiche/Buchhaltung/Ausgabedateien
    ```

    **Tipp**: Sie können per [smb](#) oder [WebDav](#) auf das Quellverzeichnis in *agorum core* zugreifen.

6. Importieren Sie die Ausgabedateien und wählen Sie**,** falls gewünscht, **Daten nach Importieren löschen**.

    **Hinweis**: Die Ausgabedateien finden Sie ebenfalls hier:

    ```auto
    Bereiche/Buchhaltung/Archiv Ausgabedatei | Ausgabedateien
    ```

7. Beginnen Sie mit der Stapelverarbeitung.

### Ablage (Ordnerstruktur)

* * *

Sobald Ihr Administrator oder Sie das Plugin installiert haben, erweitert sich die Ordnerstruktur im *agorum core smart assistant* unter *Dateien* wie folgt:

* Akten
    *   Lieferanten
        *   <Lieferant> - <Lieferantennummer>
            *   Mails
            *   Rechnungen
* Bereiche
    *   Buchhaltung
        *   Archiv Ausgabedatei
        *   Ausgabedateien
        *   Eingangsrechnungen
        *   Mails
* Eingänge
    *   Eingangsrechnungen
        *   Dokumente
            *   Trennen
            *   Verarbeiten
        *   Mails

#### Ordner „Akten“

In den Akten befinden sich die Lieferantenakten. In diesen legt das System die eingegangenen Rechnungen und E-Mails ab.

* Akten
    *   Lieferanten
        *   <Lieferant> - <Lieferantennummer>
            *   Mails
                *   <Jahr des Maileingangs>
                    *   <Monat des Maileingangs>
            *   Rechnungen
                *   <Jahr des Rechnungsdatums>
                    *   <Monat des Rechnungsdatums>

#### Ordner „Bereiche“

Der Bereichsordner enthält einen Ordner zur Buchhaltung, in den das System Rechnungen sowie Ausgabedateien und E-Mails archiviert:

* Bereiche
    *   Buchhaltung
        *   Archiv Ausgabedatei: In diesem Ordner archiviert das System alle erstellten Ausgabedateien.
        *   Ausgabedateien: Dieser Ordner dient zur Abholung durch DATEV. Da durch die Übergabe die Ausgabedateien eventuell gelöscht werden könnten, stellt der Ordner *Archiv Ausgabedatei* sicher, dass die Ausgabedateien Ihnen immer vorliegen.
        *   Eingangsrechnungen: Ablage aller eingegangenen Rechnungen.
        *   Mails: Ablage aller E-Mails, die das System in den Eingangsordner *Mails* abgelegt hat. Die Ablage erfolgt nach dem Importdatum des Dokumentes nach *agorum core.*

**Hinweis:** Das System verlinkt die Eingangsrechnungen sowie E-Mails in die entsprechenden Lieferantenakten.

#### Ordner „Eingänge“

Über die Eingangsordner startet das System den Rechnungsworkflow automatisiert.

* Eingänge
    *   Eingangsrechnungen
        *   Dokumente
            *   Trennen**:** Fügen Sie in diesen Ordner PDFs ein, damit *docform* Rechnungen ausliest.
            *   Verarbeiten**:** Fügen Sie in diesen Ordner Stapelscans (PDFs) ein, um aus einem PDF, das etwa 5 Rechnungen enthält, 5 einzelne PDFs zu erzeugen. Das System übergibt die Rechnungen anschließend automatisch dem Trennen-Ordner und startet den Ausleseprozess.
        *   Mails: Legen Sie diesem Ordner E-Mails ab, die entweder selbst eine zu verarbeitende Rechnung im E-Mail-Text enthalten, oder die im Anhang Eingangsrechnungen aufweisen.

### Aktionen im Kontextmenü

* * *

Ihnen stehen diverse Kontextmenü-Aktionen zur Verfügung:

| Aktionen | Beschreibung | Wo erscheint die Aktion? |
| --- | --- | --- |
| Als bezahlt markieren | Markieren Sie diese Rechnung als bezahlt. Diese Einstellung hat keinen Einfluss auf den Verlauf des Workflows. Stattdessen können Sie diese Rechnungen über das agorum core information center wiederfinden: Filter: Eingangsrechnungen Gesetzte Einstellungen: Eingangsrechnungen > Bezahlt | Klicken Sie eine nicht als bezahlt markierte Rechnung mit der rechten Maustaste an. |
| Bezahlte Markierung zurücksetzen | Entfernen Sie die Markierung, die die Rechnung als bezahlt kennzeichnet. | Klicken Sie eine als bezahlt markierte Rechnung mit der rechten Maustaste an. |
| Als weiterzuverrechnen markieren | Markieren Sie eine Rechnung als weiterzuverrechnen. Diese Einstellung hat keinen Einfluss auf den Verlauf des Workflows. Stattdessen können Sie diese Rechnungen über das agorum core information center wiederfinden: Filter: Eingangsrechnungen Gesetzte Einstellungen: Eingangsrechnungen > Weiterverrechnung > weiterverrechnen | Klicken Sie eine als nicht weiterzuverrechnende Rechnung mit der rechten Maustaste an. |
| Markierung zum Weiterverrechnen zurücksetzen | Entfernen Sie die Markierung, die die Rechnung als weiterzuverrechnen kennzeichnet. | Klicken Sie eine als weiterzuverrechnen markierte Rechnung mit der rechten Maustaste an. |
| Als weiterverrechnet markieren | Haben Sie eine Rechnung weiterverrechnet, können Sie diese über diese Aktion kennzeichnen. Diese Einstellung hat keinen Einfluss auf den Verlauf des Workflows. Stattdessen können Sie diese Rechnungen über das agorum core information center wiederfinden: Filter: Eingangsrechnungen Gesetzte Einstellungen: Eingangsrechnungen > Weiterverrechnung > bereits weiterverrechnet | Die Aktion erscheint, sobald Sie eine Rechnung mit der rechten Maustaste anklicken. |
| Rechnungsworkflow starten | Übergeben Sie diese Rechnung erneut dem Rechnungsworkflow. | Die Aktion erscheint, sobald Sie eine Rechnung mit der rechten Maustaste anklicken. |
| Lieferantenakte ändern | Ändern Sie nachträglich den Namen oder Nummer des entsprechenden Lieferanten. | Die Aktion erscheint, sobald Sie eine Lieferantenakte mit der rechten Maustaste anklicken. Akten Lieferanten <Lieferant> - <Lieferantennummer> |

### Rechnungen in docform trainieren

* * *

Der Rechnungseingang basiert darauf, dass die für die Buchhaltung wichtigen Werte in *docform* ausgelesen werden:

* Eingänge
    *   Eingangsrechnungen
        *   Dokumente
            *   Trennen**:** Fügen Sie in diesen Ordner PDFs ein, damit *docform* Rechnungen ausliest.
            *   Verarbeiten**:** Fügen Sie in diesen Ordner Stapelscans (PDFs) ein, um aus einem PDF, die etwa 5 Rechnungen enthält, 5 einzelne PDFs zu erzeugen. Das System übergibt die Rechnungen anschließend automatisch dem Trennen-Ordner und startet den Ausleseprozess.
        *   Mails: Legen Sie diesem Ordner E-Mails ab, die entweder selbst eine zu verarbeitende Rechnung im E-Mail-Text enthalten, oder die im Anhang Eingangsrechnungen aufweisen

Lesen Sie folgende Dokumentationen, um den *docform-*Prozess einsetzen zu können:

* docform Trennen:
    *   [Dokumente trennen](#)
* docform Verarbeiten:
    *   [Dokumente trainieren für Anfänger](#)
    *   [Dokumente trainieren für Fortgeschrittene](#)
    *   [Dokumente trainieren für Profis](#)

#### Besonderheiten bei Metadaten

| Metadatum | Besonderheit |
| --- | --- |
| Währung | Übergeben Sie in docform keine Währung, sind es standardgemäß EUR, falls Sie DATEV ASCII als Ausgabedatei konfiguriert haben. |
| Lieferantennummer | Tragen Sie als Lieferantennummer die in DATEV genutzte Kontonummer ein. Diesen Wert trägt das System als Standard bei der Kontierung in der Konto-Spalte ein, dadurch sparen Sie sich einige Klicks und müssen lediglich Gegenkonto und eventuell Kostenstelle ausfüllen. |

### Filter im agorum core information center

* * *

Sie können im *agorum core information center* nach Rechnungen, Lieferanten, Zahlungsfälligkeiten oder fehlgeschlagenen Ausgabedateien suchen. Verwenden Sie dazu diese Filter:

| Filter | Beschreibung |
| --- | --- |
| Eingangsrechnungen | Finden Sie Ihre Eingangsrechnungen anhand von diversen Suchoptionen, wie Rechnungsnummer, Rechnungsdatum, Lieferantenname, Nettobetrag, Steuersatz und so weiter wieder. |
| Fehlgeschlagene Exportdateien | Fehlgeschlagene Rechnungen inklusive Fehlerlog (pro Rechnung) |
| Lieferanten | Lieferanten |
| Zahlungsfälligkeiten | Zahlungsfälligkeiten |
| Zum Sammeln markierte Dokumente | Rechnungen, die bereit sind, an DATEV exportiert zu werden Fehlgeschlagene Rechnungen inklusive Fehlerlog (pro Rechnung) Bereits exportierte Rechnungen |

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/29a5cd90-f7a1-11ec-bc85-005056aa0ecc)

```auto
OCR: agorum core information center, Filter Suchergebnis 19190, Alles Objektarten Dokumente Mails 2929, Dokumente 2925, Notizen Ordner 2574, Suchbegriff eingeben, Administration Administration von son 27.06.2022 12:11:15, Adressen Aktive Ordner Alles Demo Eingangsrechnung 29.06.2022 12:00:06, Mails Name freie Eingabe 19190, Volltext freie Eingabe 19190, Dokumentinhalt freie Eingabe, Erstelldatum Heute 178, Gestern Woche 15691, aktueller Monat 15691, letzter Monat freie Eingabe 19190, Eingang aktuell Eingang alles Eingangsrechnungen, Fehlgeschlagene Exportdateien, Lieferanten Serverpapierkorb Workflow Aufgaben Workflow Prozesse, Zum Sammeln markierte Dokumente, Weitere ..., Heute 243, /workspace/agorum.temporary/temp mporary temp ration workspace agorum.temporary temp /workspace/agorum.temporary/temp/2022 mporary temp 2022 ration workspace agorum.temporary temp 2022 agorum.temporary temp 2022 nome cigene Dateien Administration workspace agorum.temporary temp 2022 /Root/agorum/roi/workspace/agorum.temporary/temp/2022/06 Root Home roi Eigene Dateien Administration workspace agorum.temporary temp 2022 Eigene Dateien Administration workspace agorum.temporary temp 2022 29.06.2022 12:00:06, 29.06.2022 12:00:05
```

Filter zum Rechnungsworkflow im *agorum core information center*

#### Hervorzuhebende Suchoptionen

| Suchwunsch | Sucheinstellungen |
| --- | --- |
| Anzeige aller erfolgreich exportierten Rechnungen | Filter: Zum Sammeln markierte Dokumente Gesetzte Einstellung: Gesammelte Dokumente > Gesammelt |
| Anzeige aller nicht exportierten Rechnungen aufgrund eines Fehlers | Filter: Zum Sammeln markierte Dokumente Gesetzte Einstellung: Fehlgeschlagene Exportdokumente > Fehlgeschlagen Filter: Fehlgeschlagene Exportdateien Gesetzte Einstellung: - |
| Anzeige aller noch zu exportierten Rechnungen | Filter: Zum Sammeln markierte Dokumente:  Gesetzte Einstellung: Sammelkennung > Sammelkennung |
| Anzeige aller Rechnungen, die abgelehnt oder freigegebenen wurden | Filter: Eingangsrechnungen Gesetzte Einstellung: Eingangsrechnungen > Freigabestatus > Abgelehnt / Freigegeben |
| Anzeige aller Duplikatsrechnungen | Filter: Eingangsrechnungen Gesetzte Einstellung: Eingangsrechnungen > Freigabestatus > Duplikat |

### Berechtigungen vergeben (für Administratoren)

* * *

Der Rechnungsworkflow ist im Standard nur für den Super-Administrator *roi* sichtbar. Über folgende ACLs und Benutzergruppen können Sie als Administrator auch anderen Benutzern Zugriff auf den Rechnungsworkflow geben.

| ACL | Benutzergruppen | Beschreibung |
| --- | --- | --- |
| ACL\_agorum.invoice | – | ohne Funktion |
| ACL\_agorum.invoice.wizard | – | Steuert den Zugriff auf die Schaltfläche agorum core invoice plugin > Rechnungsworkflow konfigurieren im Hauptmenü. |
| ACL\_agorum\_invoice\_invoice\_mails | GRP\_agorum\_invoice\_invoice\_mails\_All GRP\_agorum\_invoice\_invoice\_mails\_Read GRP\_agorum\_invoice\_invoice\_mails\_Write | Steuert den Zugriff auf den Ordner Dateien > Eingänge > Eingangsrechnungen > Mails. |
| ACL\_agorum\_invoice\_invoice\_documents | GRP\_agorum\_invoice\_invoice\_documents\_Read | Steuert den Zugriff auf die Ordner Dateien > Eingänge > Dokumente > Trennen bzw. Verarbeiten. |
| ACL\_agorum\_invoice\_Eingänge | GRP\_agorum\_invoice\_Eingänge\_Read | Steuert den Zugriff auf die Ordner unterhalb von Dateien > Eingänge. |
| ACL\_agorum\_invoice\_Bereiche | GRP\_agorum\_invoice\_Bereiche\_Read | Steuert den Zugriff auf die Ordner unterhalb von Dateien > Bereiche. |
| ACL\_agorum\_invoice\_Buchhaltung | GRP\_agorum\_invoice\_Buchhaltung\_Read | Steuert den Zugriff auf die Ordner unterhalb von Dateien > Bereiche > Buchhaltung. |
| ACL\_agorum\_invoice\_Archiv Ausgabedatei | GRP\_agorum\_invoice\_Archiv Ausgabedatei\_All GRP\_agorum\_invoice\_Archiv Ausgabedatei\_Read GRP\_agorum\_invoice\_Archiv Ausgabedatei\_Write | Steuert den Zugriff auf den Ordner Dateien > Bereiche > Buchhaltung > Archiv Ausgabedatei. |
| ACL\_agorum\_invoice\_Ausgabedateien | GRP\_agorum\_invoice\_Ausgabedateien\_All GRP\_agorum\_invoice\_Ausgabedateien\_Read GRP\_agorum\_invoice\_Ausgabedateien\_Write | Steuert den Zugriff auf den Ordner Dateien > Bereiche > Buchhaltung > Ausgabedateien. Steuert den Zugriff auf die Schaltfläche agorum core invoice plugin > Ausgabedatei manuell erzeugen im Hauptmenü. |
| ACL\_agorum\_invoice\_Eingangsrechnungen | GRP\_agorum\_invoice\_Eingangsrechnungen\_All GRP\_agorum\_invoice\_Eingangsrechnungen\_Read GRP\_agorum\_invoice\_Eingangsrechnungen\_Write | Steuert den Zugriff auf den Ordner Dateien > Bereiche > Buchhaltung > Eingangsrechnungen. Steuert die Aktionen: Rechnungsworkflow starten als bezahlt markieren/zurücksetzen als weiterverrechnen markieren/zurücksetzen |
| ACL\_agorum\_invoice\_Mails | GRP\_agorum\_invoice\_Mails\_All GRP\_agorum\_invoice\_Mails\_Read GRP\_agorum\_invoice\_Mails\_Write | Steuert den Zugriff auf den Ordner Dateien > Bereiche > Buchhaltung > Mails. |
| ACL\_agorum\_invoice\_Akten | GRP\_agorum\_invoice\_Akten\_Read | Steuert den Zugriff auf die Ordner unterhalb von Dateien > Akte. |
| ACL\_agorum\_invoice\_Lieferanten | GRP\_agorum\_invoice\_Lieferanten\_All GRP\_agorum\_invoice\_Lieferanten\_Read GRP\_agorum\_invoice\_Lieferanten\_Write | Steuert den Zugriff auf den Ordner Dateien > Akte > Lieferanten. Steuert, ob Benutzer neue Lieferanten im Workflowschritt anlegen können und ob im agorum core smart assistant die Schaltfläche zum Anlegen einer Lieferantenakte erscheint. Wenn Sie einen Benutzer in diese ACL eintragen, fügt das System ihn automatisch zur Benutzergruppe GRP\_agorum\_invoice\_Lieferanten\_All hinzu. Soll der Benutzer keinen Zugriff mehr auf die Ordner und die Schaltfläche Lieferantenakte anlegen haben, entfernen Sie ihn manuell aus dieser Benutzergruppe. Steuert, ob Benutzer im agorum core smart assistant die Lieferantenakte über die Kontextmenü-Aktion Lieferantenakte ändern ändern können. |
| ACL\_agorum\_invoice\_docform\_process | GRP\_agorum\_invoice\_docform\_process\_All GRP\_agorum\_invoice\_docform\_process\_Read GRP\_agorum\_invoice\_docform\_process\_Write | Steuert den Zugriff auf den Ordner Eingänge > Eingangsrechnung > Dokumente > Verarbeiten. Fügen Sie Benutzer zur Benutzergruppe GRP\_agorum\_invoice\_docform\_process\_All hinzu, damit Benutzer Dokumente über docform und docform Trennen an den Rechnungsworkflow senden können. |
| ACL\_agorum\_invoice\_docform\_split | GRP\_agorum\_invoice\_docform\_split\_All GRP\_agorum\_invoice\_docform\_split\_Read GRP\_agorum\_invoice\_docform\_split\_Write | Steuert den Zugriff auf den Ordner Eingänge > Eingangsrechnung > Dokumente > Trennen. |

Sie finden diese ACLs folgendermaßen:

1. Öffnen Sie auf der Startseite von *agorum core* die **Administration**.
2. Wählen Sie links im Menü **Rechte (ACLs)**.
3. Öffnen Sie diesen Pfad:

    ```auto
    ACLs/Rechte/<Name des Workflows>
    ```

Für das Berechtigen von Benutzern mit ALCs und Einfügen in Benutzergruppen siehe [Berechtigungen in der Administration verwalten](#).

## Detailfenster kennenlernen

Das Detailfenster ist ein multifunktionales Fenster, mit dem Sie Details und Informationen übersichtlich einsehen und bearbeiten können.

Einen detaillierten Einblick liefert der dazugehörige [Screencast](https://www.youtube.com/watch?v=B1CR7RnvS94).

**Hinweis**: Die Konfiguration dieses Detailfensters geschieht unter [agorum.composite.details](#).

### Registerkarte „Ansicht“

* * *

**Hinweis**: Nur unterstützte Dokumentenformate werden konvertiert und in Ansicht und Vorschau dargestellt.

In der Ansicht haben Sie je nach Selektion zwei Möglichkeiten:

**Schnellvorschau einer Datei in einer optimal definierten Ansicht**Die Ansicht wird bei nicht aktiven [Dokumententypen](#) in Form eines scrollbaren PDFs angezeigt, bei aktiven Dokumententypen können Sie direkt in der Bedienoberfläche arbeiten und etwa auf eine E-Mail antworten.

**Inhaltsübersicht eines Ordners mit filterbarer Suchfunktion**Die Ansicht ist vollständig individuell konfigurierbar. Sie können etwa die Bilder eines Ordners darstellen. OpenOffice dient dabei als Basis der Erzeugung von PDFs.

Mit Angabe einer ACL steuern Sie, wer Zugriff auf diese Registerkarte hat:

```auto
Administration/ACLs/Rechte‎/agorum.composite‎/agorum.composite.details‎/ACL_agorum.composite_agorum.composite.details_view
```

### Registerkarte „Übersicht“

* * *

In dieser Registerkarte können Sie:

*  alle Workflows einsehen, in denen das Objekt bisher verwendet wurde
* die Metadata-Kollektion, d. h. diverse Metadaten eines Objekts, einsehen oder eine Metadata-Kollektion und die Metadaten über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAAiElEQVQ4EZ3Syw2AIAwA0K7LFh3DoyuYMAAJNxyAqydX4FhTQOUTSfHQcOFBfxBCIFE4S4A7Hfk+iJHSBBwZi6BxlvCGfC6expDTU5rQcTn+wbidA5hRTK/AJj4SPmCDapya2acqQNzQGgpRDSfQCydRgj9QhCvmjSgGnOY2XkVooQR1P0oRwws90I203Q2j0wAAAABJRU5ErkJggg==) bearbeiten.

Für Details zur Oberfläche von Workflows siehe [Mit Workflows arbeiten](#).

**Hinweis**: Voraussetzung zur Auswahl einer Kollektion im Feld *Typ* ist, dass Ihr Administrator diese Kollektion zur Bearbeitung [freigeschaltet](#) hat.

Mit Angabe einer ACL steuern Sie, wer Zugriff auf diese Registerkarte hat:

```auto
Administration/ACLs/Rechte‎/agorum.composite‎/agorum.composite.details‎/ACL_agorum.composite_agorum.composite.details_overview
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/5cdf80f0-cddd-11eb-b06b-005056aa0ecc)

```auto
OCR: Metadaten,Kollektion,Ansicht,Vorschau,Vorschau,Objekt,Info,Notizen,Rechte,Audit,Typ,Beispiel,Daten,Daten,Typ,werwer,Daten,Beschreibung,test,Daten,Eingabe,15.06.2021,Datenpositionen,Position,Workflow,Prozesse,Prozess,rl.test.unwrap,rl.test.unwrap,rl.test.unwrap,rl.test.unwrap,rl.test.unwrap,rl.test.unwrap,von,Bezeichnung,Positionsmenge,Prozessbeschreibung,Status,Erstelldatum,Been,Beendet,05.02.2021,14:31:45,05.02,Beendet,05.02.2021,14:13:52,05.02,Beendet,Beendet,Beendet,05.02.2021,12:35:05,05.02,05.02.2021,12:33:04,05.02,05.02.2021,12:31:36,05.02,Beendet,05.02.2021,12:26:47,05.02,1-6,von
```

Registerkarte *Übersicht* mit Anzeige der Metadata-Kollektion und den Workflow-Prozessen

### Registerkarte „Vorschau“

* * *

**Hinweis**: [Ansicht und Vorschau](#) ähneln sich, unterscheiden sich aber stark in Hinblick auf Speicherverbrauch. Bei der Erzeugung der Vorschau verbraucht das System pro Seite ca. 1 MB Speicher.

Die Vorschau zeigt Ihnen das Objekt im JPG-Format an. Der Inhalt wird übersichtlich in Einzelseiten mit einer Auflösung von 300 dpi präsentiert.

Wird ein Dokument länger als 3 Monate nicht in der Vorschau aufgerufen, wird diese gespeicherte Vorschau gelöscht.

Mit Angabe einer ACL steuern Sie, wer Zugriff auf diese Registerkarte hat:

```auto
Administration/ACLs/Rechte‎/agorum.composite‎/agorum.composite.details‎/ACL_agorum.composite_agorum.composite.details_preview
```

### Registerkarte „Objektinfo“

* * *

Diese Registerkarte enthält folgende Informationen:

* Allgemein
* Metadaten
* Zugehörigkeit
* Ablageorte
* Tags
* Workflows
* Historie

Mit Angabe einer ACL steuern Sie, wer Zugriff auf diese Registerkarte hat:

```auto
Administration/ACLs/Rechte‎/agorum.composite‎/agorum.composite.details‎/ACL_agorum.composite_agorum.composite.details_objectInfo
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/9adb14a0-b6ef-11eb-b06b-005056aa0ecc)

```auto
OCR: Objekt,Info,Ansicht,Vorschau,Objekt,Info,Notizen,Allgemein,Name,Beschreibung,Ordner,Thorsten,Breuer,Ersteller,Erstelldatum,Mittwoch,12. Mai 2021,14:49:21,Besitzer,Thorsten,Breuer,Zuletzt durch,Thorsten,Breuer,Zuletzt,Mittwoch,12. Mai 2021,14:49:21,Inhalt,Intern,aktualisiert,Mittwoch,12. Mai 2021,14:49:21,Ablaufdatum,Gesperrt durch,809512190,Objekt,Objekt,UUID,790ea3a0b320-11ebb06b005056aa0ecc,ACL,Private,Scope,ACLs,Ablageorte,Eigene Dateien,Beispiele,Ordnersymbole,Ordner
```

Registerkarte *Objektinfo* im Detailfenster

#### Allgemein

**Hinweis**: Bei Erreichen des Ablaufdatums wird das Objekt automatisch gelöscht.

#### Metadaten

Metadaten werden bei Eingang in das System indiziert. Neben den konfigurierbaren Metadaten werden die Area-Metadaten aufgeführt, die Auskunft über die lokale Position des Objekts geben.

#### Ablageort

Per Klick auf den Dateipfad gelangen Sie direkt zum Ablageorte des Objekts. Ein Objekt kann mehrere Ablageorte haben, etwa bei Verlinkungen, wird aber nur ein einziges Mal in der Datenbank gespeichert.

Diese Verlinkungen werden auch im Suchergebnis angezeigt.

#### Zugehörigkeit, Abhängigkeit, Anhänge, Verwandt

Diese Informationen betreffen primär Projekte, Vorgänge und Aufgaben. Objekte können durch Verknüpfungen aneinander angehängt, Zugehörigkeiten definiert und Abhängigkeiten festgelegt werden.

#### Tags

Zeigt Benutzer- und Globale Tags. Jeder Benutzer sieht nur seine eigenen Tags.

#### Workflows

Bietet eine Übersicht der entsprechenden Workflows.

#### Historie

Zeigt Versionierungen des Objekts.

### Registerkarte „Notizen“

* * *

Über diese Registerkarte können Sie eine Notiz an das selektierte Objekt hängen, um einfach und gezielt mit Ihrem Team zu kommunizieren.

Mit Angabe einer ACL steuern Sie, wer Zugriff auf diese Registerkarte hat:

```auto
Administration/ACLs/Rechte‎/agorum.composite‎/agorum.composite.details‎/ACL_agorum.composite_agorum.composite.details_notes
```

### Registerkarte „Rechte“

* * *

Diese Registerkarte hat einen rein informativen Zweck und dient dazu, gewählte Benutzer über gesetzte ACLs auf dem gewählten Objekt zu informieren. Dadurch können Sie als Administrator schneller überprüfen, welche ACLs und SCOPE-ACLs mit den jeweiligen Benutzergruppen / Benutzern und den dazugehörigen Rechten auf dem Objekt sitzen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/0b54b280-5ef5-11ea-b692-005056aa0ecc)

```auto
OCR: Ansicht, Vorschau, Objekt, Info, Notizen, Rechte, Audit, Smart Assistant, Alles, Suchbegriff eingeben, Schulungseinheiten, Ordner, Name, acds, acdsacademy, Administration von agorum core, 010 Systemadministration Technische Voraussetzung.html, 020 Systemadministration Installation.html, 030 Systemadministration Datenblatt.html, 040 Systemadministration agorum core starten und beenden.html, 050 Systemadministration agorum core Browser, 060 Systemadministration Schulungsunterlagen importieren.html, 070 Systemadministration roihost einstellen.html, Rechte, ACL, ACL_acds1153064_acdsacademy, ACL_acds1153064_acdsacademy, ACL_acds1153064_acdsacademy, ACL_acds_creator, Mitglied, GRP_acds1153064_acdsacademy_Read, GRP_acds1153064_acdsacademy_Write, GRP_acds1153064_acdsacademy_All, GRP_acds_creator, Suche, Berechtigung, READ, WRITE, ALL, ALL
```

Registerkarte *Rechte*

Wer Zugriff auf diese Registerkarte hat, bestimmen Sie, indem Sie Mitglieder in das vorhandene PAI eintragen oder entfernen:

```auto
ACL: <PAI|ParameterAccessIdentifierAcls>/ACL_PAI_PERMISSIONS_
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/3e1148a0-5ef5-11ea-b692-005056aa0ecc)

```auto
OCR: ACLs, Rechte, ParameterAccessIdentifierAcls, ACLs, Rechte, Name, ACL_PAI_ExpirationDate_, ACL_PAI_ExtendedSearch_, Beschreibung, ACL, Gesperrt, Published, Published, ACL_PAI_MetaDbProperty_Administration_, ACL_PAI_MetaDbProperty_Editing_, Published, Published, ACL_PAI_MyFilesArea_, ACL_PAI_MyFilesList_, Published, Published, ACL_PAI_NewFolder_, ACL_PAI_NewIcon_, ACL_PAI_NewMail_, ACL_PAI_NgOsAdminSync_, ACL_PAI_NoteObjectCreate_, Published, Published, Published, Published, Published, ACL_PAI_ObjectEdit_, Published, ACL_PAI_ObjectInfo_, Published, ACL_PAI_ParameterAccessIdentifierList_, Published, ACL_PAI_PDFView_, Published, ACL_PAI_PERMISSIONS_, Published, ACL_PAI_PortalMenuAdministration_, Published, ACL_PAI_PortalMenuControlPanel_, Published, ACL_PAI_PortalMenuPrivate_, Published, ACL_PAI_PortalMenuPrivateBookmark_, ACL_PAI_PortalMenuPublic_, ACL_PAI_ProjectTimeExport_, Published, Published, Published, von, 100, von, 134
```

ACL *ACL\_PAI\_PERMISSIONS\_* in der Administration finden

### Registerkarte „Audit“

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/bf8b3ac0-5ef6-11ea-b692-005056aa0ecc)

```auto
OCR: Audit, audit, Ansicht, Vorschau, Vorschau, Objekt, Info, Notizen, Rechte, Audit, 1-3, von, Name, Aktion, Ordner, Benutzer, Datum, Willkommen.png, roi, roi, 02.08.2021, 13:57:20, Files, roi, roi, 30.11.2020, 09:16:07, Willkommen.pdf, erstellt, roi, roi, 30.11.2020, 09:16:07
```

Registerkarte *Audit* im Detailfenster

In dieser Registerkarte werden Änderungen angezeigt, die an dem gewählten Dokument umgesetzt wurden. Dies schließt folgende Änderungsmöglichkeiten ein:

* Namensänderung
* Inhaltsänderung
* Ordner einhängen, verlinken, abhängen

Metadatenänderungen werden nicht angezeigt.

*acaudit* ist rein informell. Die dargestellten Informationen sind aus der Audit-Tabelle entnommen und geben dem freigegebenen Benutzer einen Überblick über die Änderungen an dem gewählten Objekt.

Mit Angabe einer ACL steuern Sie, wer Zugriff auf diese Registerkarte hat:

```auto
Administration/ACLs/Rechte‎/acaudit/ACL_agorum core audit
```

Mehr Möglichkeiten, um nachzuvollziehen, was mit Objekten passiert ist, erhalten Sie mithilfe des [agorum core audit tools](#).

