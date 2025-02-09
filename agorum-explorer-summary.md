# Konfigurationen zum agorum core explorer summary

## Konfigurationen zum agorum core explorer

Den *agorum core explorer* können Sie individuell konfigurieren, um ihn an Ihre eigenen Bedürfnisse anzupassen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/7b3b74c0-1c20-11ef-b611-005056aa0ecc)

```auto
OCR: Suchen, Eingang, aktuell, demo, demo, Explorer, Dateien, Demo, Navigationsleiste, Weitere Apps, Dateien, acds, Suche, agorum, core, basic, archive, agorum, core, basic, archive, docform, Akten, Bereiche, d4wdemo, d4wdr, Demo, DemoWorkflows, kutestordner, Eigene Dateien, Mail, Eingang, Workflow, Aufgaben, Benutzerdokumentation, agorum, core, Dokumentation, Verschlagwortung und Ablage, Administration, Serverpapierkorb, Sitzungsinfo, Dokumentation, intern, Dokumentation, Dokumentation, Partner, Navigationsbaum, Name, Entwicklung, Informationen, Projekte, Vertrieb, Verwaltung, Einstieg, agorum, cor, Willkommen.pdf, Toolbar, Betreff, Ordnerinhalt, Seitennavigation, von HOO, Willkommen.pdf, Ausschneiden, Kopieren, hier, Workflow, Rechte vergeben, Benutzerberechtigung anzeigen, Administration mit Chat, agorum, core, Basic, Archive, agorum, core, basic, archive, docform, Senden, Development, Eingang, agorum, core, template manager, agorum, core, template manager, Edit Detaila, Neu, Details, Herunterladen, Hochladen, Ablageort, Explorer anzeigen, Umbenennen, Vorlagentyp setzen, Bearbeiten mit Konvertieren, new menu entry ersicht, Vorschau, Objektinfo, Notizen, Rechte Wiederhe von Detailfenster, core, Open Source Dokumentenmanagement rise Content Management, Ihre digitale bei agorum core, Ihrem zentralen System, Rund Blick auf Ihr ganzes Unternehmen, anpassbare Open Source basierte ECM verbindet Dokumentenmanagement systems DMS mit stomer Relationship Management CRM, Projekt- management sowie Features effizi- Arbeiten auch Homeoffice italisierungstrategie auf einem zentralen und ament auf digitale Spitzenreiter werden und bleiben, ein paar Links auf unsere Website was agorum core leistet, Unsere Online Demo zum Einstieg, Terminvereinbarung Kundenberater kontaktieren sich genauer agorum core informieren, Registrieren Sie sich unseren Newsletter Sachen ECM Digitalisierung Co. auf dem Lau- fenden bleiben, Noch ein Hinweis Sie jederzeit von agorum core
```

Aufbau der Explorer-Oberfläche

| Thema | Beschreibung | Link |
| --- | --- | --- |
| Navigationsbaum und Ordnerinhalt | In dieser Dokumentation erfahren Sie, wie Sie die Explorer-Anzeige anpassen können. | Explorer-Darstellung anpassen (agorum.explorer) |
| Detailfenster | Diese Dokumentation zeigt, wie Sie die Standard-Reihenfolge von Reitern im Detailfenster ändern. | Reihenfolge der Reiter im Detailfenster ändern oder Reiter ausblenden |
| URL | Diese Dokumentation zeigt, wie Sie eine URL aus dem agorum core explorer aufrufen. | URL aus dem agorum core explorer aufrufen |
| Ordnerinhalt Toolbar | Diese Dokumentation zeigt, wie Sie oberhalb der Ordnerdarstellung im agorum core explorer Schaltflächen einfügen, um den agorum core explorer zu individualisieren. | Eigene Schaltflächen in den agorum core explorer einfügen |
| Hauptmenü, Toolbar, Kontextmenü und Open-Aktion | In diesem Dokument erfahren Sie, wie Sie Overrides verwenden, um Standardfunktionen zu überschreiben. | Standardfunktionen im Explorer überschreiben |

## Explorer-Darstellung anpassen (agorum.explorer)

Das Widget `agorum.explorer` steuert, wie Ordner und Dateien angezeigt werden, wenn Sie im Navigationsbaum im Explorer einen Ordner auswählen. Mithilfe des Widgets können Sie etwa steuern,

* welche Ordner im Navigationsbaum als Wurzelordner angezeigt werden
* welcher Ordner im Ordnerinhalt angezeigt wird
* welcher Ordnerinhalt angezeigt wird (Sucheinschränkung etwa auf Ordner oder Dateien)
* ob das Detailfenster angezeigt wird

### Verwendung

* * *

Wenn Sie den Explorer ohne weitere Einstellungen aufrufen, werden alle vorhandenen Wurzelordner angezeigt.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/1fcc2ba0-2717-11ef-8dc6-005056aa0ecc)

```auto
OCR: Root, Root, Root, MetaDB, Benutzer, Gruppen, ACLs, Rechte, Home, Dateien, Eigene Dateien, Mail, Name, Administration, agorum, Home von, Beschreibung, Admin, Folder, Root, Folder from, ...Home, Folder, Betreff, Zuletzt dui, Letzte Inhalt, roi, roi, 01.01.1970, 01:00:02, 29.12.2004, 08:41:02, roi, 01.01.1970, 01:00:02, 1-3, von
```

Explorer-Anzeige ohne Einschränkungen

Sie verwenden das Widget `agorum.explorer` wie folgt, um zu steuern, welche Ordner angezeigt werden:

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.explorer',
  // --- Properties
  // UUID des geöffneten Ordners (wird konvertiert, wenn nötig)
  id: '/agorum/roi/Files/Demo/Projekte',
  roots: ['/agorum/roi/Files/Demo'],
});
widget;
```

Die Property `roots` dient dazu, einen oder mehrere Ordner anzugeben, die in der Navigation als Wurzelordner angezeigt werden. Die `id` steuert, welcher Ordnerinhalt angezeigt wird. In diesem Beispiel ist der Wurzelordner für die Navigation der Ordner *Demo*, im Detailfenster werden die Inhalte aus dem Unterordner *Projekte* angezeigt. Alternativ können Sie auch mit `config` einen *smart assistant konfigurator*\-Einsprungspunkt als Wurzelordner festlegen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/9e9c4990-270f-11ef-8dc6-005056aa0ecc)

```auto
OCR: Projekte, Demo, Demo, Projekte, Name, Akten, Normen, Vorlagen, Beschreibung, Betreff, Zuletzt, dui, Letzte, Inhalt, roi, 28.04.2011, 17:49:47, roi, 28.04.2011, 17:49:48, roi, 28.04.2011, 17:49:48, von, 1-3, von
```

Beispiel für die Verwendung von *agorum.explorer*

### Properties und Parameter

* * *

Sie können den Explorer-Aufruf durch folgende Eigenschaften anpassen. Diese Eigenschaften können nachträglich durch den Benutzer geändert werden.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| id | Gibt den Ordner an, dessen Inhalt angezeigt wird. Die Angabe ist optional. | Pfad oder ID des Ordners |
| roots | Gibt einen oder mehrere Ordner an, die als Wurzelordner im Navigationsbaum angezeigt werden. Die Angabe ist optional. | Array von Ordnerangaben (Pfade oder IDs der Ordner) roots: \['/agorum/roi/Files/Demo', '/agorum/roi/Files/DemoWorkflows'\], |
| sort | Initiale Sortierung der Objekte in der Anzeigeliste. Der Benutzer kann die Sortierung verändern. Sie können mehrere Sortierkriterien angeben, die in absteigender Reihenfolge angewendet werden. Die Angabe ist optional. | Array von Sortierangaben bestehend aus dem Sortierkriterium und der Sortierreihenfolge sort: \[ { property: 'name', descending: true, }, \], |
| view | Definiert optional Kriterien für die Anzeige der Ordnerdetails über Suchkritieren. | Die Suchkritieren werden für baseQuery angegeben view: { type: 'search', // zusätzlich immer eingeschränkt über inpath\_uuid:<id> baseQuery: 'isfolder:false', }, |
| displayName | Anzeigename des Ordners | \- (nur lesbar) |
| selection | Informationen zu den Selektionskriterien. | \- (nur lesbar) |

Zusätzlich können Sie folgende Parameter angeben, die nachträglich nicht geändert werden können.

| Parameter | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| config | Verweist auf einen smart assistant konfigurator-Einsprungspunkt. | Name des Einsprungspunkts wie in smart assistant konfigurator definiert |
| initiallyVisibleDepth | Definiert die Anzahl der Ordnerebenen, die im Navigationsbaum angezeigt werden. Hinweis: Die Einstellung sollte nur nach sorgfältiger Prüfung auf 1 oder höher gesetzt werden. Abhängig von der Zahl der enthaltenen Objekte kann es zu Performance-Einbußen kommen. | Ganzzahl, Standardwert: 0 |
| noHistory | Gibt an, dass die Benutzerhistorie nicht beim Öffnen der Ansicht berücksichtigt werden soll. | Boolescher Wert, Standardwert: false |
| showDetails | Legt fest, dass das Detailfenster zusätzlich zum Ordnerinhalt angezeigt wird. | Boolescher Wert, Standardwert: false |

### Beispiele

* * *

#### Beispiel: Anzeige des Detailfensters

Sie können durch Angabe von `showDetails` steuern, dass das Detailfenster angezeigt wird.

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.explorer',
  // --- Properties
  // UUID des geöffneten Ordners (wird konvertiert, wenn nötig)
  id: '/agorum/roi/Files/Demo',
  roots: ['/agorum/roi/Files'],
  // --- Parameter
  showDetails: true,
});
widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/993888e0-272f-11ef-8dc6-005056aa0ecc)

```auto
OCR: Demo, Dateien, Demo, Dateien, Name, Entwicklung, Informationen, Projekte, Vertrieb, Verwaltung, Einstieg, agorum, core.docx, Willkommen.pdf, Ansicht, Vorschau, Objektinfo, Notizen, Rechte, Bescl, Allgemein, Name, Demo, Beschreibung, Ersteller, roi, Erstelldatum, Dienstag 04. 2008 14:54:55, Besitzer, roi, Zuletzt durch, roi, Zuletzt, Dienstag 04. 2008 14:55:40, Inhalt, Intern, aktualisiert, Mittwoch 24. August 2011 17:05:03, Ablaufdatum, Gesperrt durch, Objekt, 1026136, Objekt UUID, 71aaf127 ce62-11e0 b47a 0800276e2399, ACL, ACLDemo, Scope, ACLs von 1-9 von Ablageorte
```

Explorer-Anzeige mit Detailfenster

#### Beispiel: Einschränkung der Anzeige in den Ordnerdetails

Sie können die Anzeige der Ordnerdetails anpassen, indem Sie die Suche anpassen. In diesem Beispiel werden Ordner nicht in den Ordnerdetails angezeigt, sondern nur die beiden vorhandenen Dateien:

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.explorer',
  // --- Properties
  // UUID des geöffneten Ordners (wird konvertiert, wenn nötig)
  id: '/agorum/roi/Files/Demo',
  roots: ['/agorum/roi/Files'],
  view: {
    type: 'search',
    // zusätzlich immer eingeschränkt über inpath_uuid:<id>
    baseQuery: 'isfolder:false',
  }
});
widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/e90d2140-2730-11ef-8dc6-005056aa0ecc)

```auto
OCR: Demo Dateien, Demo Dateien, Administration PDF, Ergebnis Willkommen.pdf, 113,9, Dateien Demo DOCX, Einstieg agorum core.docx, 139,5, Dateien Demo, 24.05, 09:52, 24.05, 09:52
```

Explorer mit Ordnerinhalt-Anzeige ohne Unterordner

#### Beispiel: Verwendung von agorum.explorer in einer Form

Das Widget `agorum.explorer` kann in einer Form verwendet werden, etwa wie folgt:

```auto
let aguila = require('common/aguila');
let form = aguila.create({
  type: 'agorum.border',
  width: 600,
  height: 400,
  docked: {
    top: {
      type: 'agorum.toolBar',
      items: [
        {
          type: 'agorum.button',
          text: '',
        },
      ],
    },
    bottom: {
      type: 'agorum.toolBar',
      items: [
        {
          type: 'agorum.button',
          text: '',
        },
      ],
    },
    left: {
      type: 'agorum.toolBar',
      items: [
        {
          type: 'agorum.button',
          text: '',
        },
      ],
    },
    right: {
      type: 'agorum.toolBar',
      items: [
        {
          type: 'agorum.button',
          text: '',
        },
      ],
    },
    center: {
      type: 'agorum.explorer',
      name: 'explorer',
      showDetails: true,
    },
  },
});

form.down('explorer').roots = ['/agorum/roi/Files/Demo'];

form;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/ec40e2c0-2735-11ef-8dc6-005056aa0ecc)

```auto
OCR: Demo, Demo, Vorschau, Objektinfo, Name, Allgemein, Entwicklung, Name, Informationen, Beschreibung, Projekte, Vertrieb, Verwaltung, Einstieg, agorum, core.docx, Willkommen.pdf, Ersteller, Erstelldatum, Besitzer, Zuletzt durch, Zuletzt aktualisiert, Inhalt von, Intern
```

Verwendung von agorum.explorer in einer Form

## Reihenfolge der Registerkarten im Detailfenster ändern oder Registerkarten ausblenden

### Reihenfolge der Registerkarten im Detailfenster ändern

* * *

Die Registerkarten im Detailfenster werden standardmäßig in folgender Reihenfolge angezeigt:

* Ansicht
* Vorschau
* Objekt-Info
* Notizen

So ändern Sie die Standard-Reihenfolge:

1. Öffnen Sie auf der Startseite von *agorum core* **Administration**.
2. Wählen Sie links im Menü **MetaDb**.
3. Öffnen Sie den Pfad:

    ```auto
    MAIN_MODULE_MANAGEMENT/home/control/Details/Views
    ```

4. Doppelklicken Sie auf einen der Einträge, um ihn zu bearbeiten.
5. Ändern Sie die Ziffern eines Eintrags, etwa der **NotesList**, um die Reihenfolge zu ändern.
6. Speichern Sie die Änderungen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/7ab12cd0-688a-11ec-b51c-005056aa0ecc)

```auto
OCR: MetaDb, Administration, Benutzer, Gruppen, Rechte, ACLS, MetaDb, Root, Ordner, Serverpapierkorb, Mail, Filter, Suche, QSuche, von, Audit, Tool, home, control, Details, Views, MetaDB, MAIN_ACL_MANAGEMENT, MAIN_COMMON, MANAGEMENT, MAIN_GROUP_MANAGEMENT, MAIN_MACHINE_MANAGEMENT, MAIN_MODULE_MANAGEMENT, accompdoc, activefolder, agceptitclient, agorumboost, agorumcoreoutlook, agorumcoresync, agorumcoresync2, aguila, api, backend, home, control, Apps, Browser, Categories, Details, Views, ExternalLink, Libraries, Modules, Scripts, Styles, metadata, Name, acaudit, Beschreibung, ACL, Published, agorum.searchView.t, 500, Main, Published, 525, Overview, Published, 550, Preview, Published, 600, Info, Published, 700, NotesList, Published, 800, Rechte, Published, von
```

Reihenfolge der Registerkarten durch MetaDb-Einträge ändern

### Eine Registerkarte ausblenden

* * *

Durch Auskommentieren des entsprechenden Eintrags können Sie die Registerkarten *Ansicht*, *Vorschau*, *Objekt-Info* oder *Notizen* im *agorum core smart assistant* ausblenden.

1. Öffnen Sie auf der Startseite von *agorum core* **Administration**.
2. Wählen Sie links im Menü **MetaDb**.
3. Öffnen Sie den Pfad:

    ```auto
    MAIN_MODULE_MANAGEMENT/home/control/Details/Views
    ```

4. Doppelklicken Sie auf einen der Einträge, um ihn zu bearbeiten.
5. Setzen Sie ein **#** vor die Ziffern, um die entsprechende Registerkarte auszublenden.
6. Speichern Sie die Änderungen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/58d241c0-688b-11ec-b51c-005056aa0ecc)

```auto
OCR: von, von, agorumcoresync, agorumcoresync2, aguila, api, backend, home, control, Apps, Browser, Categories, Details, Views, ExternalLink, Libraries, Modules, Scripts, Styles, metadata, MAIN_ACL_MANAGEMENT, MAIN_COMMON, MANAGEMENT, MAIN_GROUP_MANAGEMENT, MAIN_MACHINE_MANAGEMENT, Name, acaudit, Beschreibung, ACL, Published, agorum.searchView.t, ...Published, 550, Preview, Published, MAIN_MODULE_MANAGEMENT, accompdoc, activefolder, agceptitclient, 500, Main, Published, 525, Overview, Published, 600, Info, Published, agorumboost, agorumcoreoutlook, 700, NotesList, Published, 800, Rechte, Published, home, control, Details, Views, MetaDB, MetaDb, Administration, Benutzer, Gruppen, Rechte, ACLS, MetaDb, Root, Ordner, Serverpapierkorb, Mail, Filter, Suche, QSuche, von, Audit, Tool
```

Registerkarte durch Auskommentieren der MetaDb-Einträge ausblenden

### Eine Registerkarte als aguila-Widget einfügen

* * *

Wenn Sie eine neue Registerkarte als *aguila*\-Widget einfügen, kommt es darauf an, ob diese Ansicht die „Bricke“-Welt auch enthält. Wenn diese nicht implementiert ist, muss ein Mapping stattfinden von *Bricke* nach *aguila*.

**Beispiel**

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.composite.details.view.searchView'
});

setImmediate(() => widget.form.on('show', ([ id ]) => widget.id = id));

widget;
```

Dieses Widget nimmt das *show*\-Event, der von der *Bricke* kommt, und mappt diesen in die *id*, das in *aguila* als *properties: \[ 'id' \]* definiert ist.

Um das Beispiel zu vervollständigen, folgen nachfolgend alle MetaDB-Einträge als Beispiel, wie Sie etwa *search-view* als eigene Registerkarte einbinden:

1. Öffnen Sie auf der Startseite von *agorum core* **Administration**.
2. Wählen Sie links im Menü **MetaDb**.
3. Öffnen Sie den Pfad:

    ```auto
    MAIN_MODULE_MANAGEMENT/home/control/Details/Views/570 Preview (SV)
    ```

4. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAAXklEQVQokWN8sHHXf4UdvxjwAX8PI4YVboIY4kx4dREAjN+/f/9PrmaWl7sOMxDn7I8MnUV3Gc4jeYEiZ7OIu9kyfHcjRulHDBHKAgxXVCH7swGXZuJD+wF1A4wizQD1ISunKVViAQAAAABJRU5ErkJggg==) die folgenden zwei **Property-Entrys** an:***Property-Entry 1*****Name**Name**Datentyp**Zeichenkette (String)**Wert (String)**570 Vorschau SV***Property-Entry 2*****Name**Title**Datentyp**Zeichenkette (String)**Wert (String)**570 Vorschau SV
5. Öffnen Sie **Views****.**
6. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAAAiklEQVQokWP8/uD0/4jOlwwbGdABP8OBPhMGcwxxBGB8sHHXf4Udv/AowQYgBjORqAsKPjI4FO0lVzMEEKXZ38OI4XufMkMDOZpxAbwB1pDozFCuiy76nmFl5zmGhJe0tBkG/D2MGFa4fWToLLqL4m+KbGYhRtHGHecYOHdgijOJ6wsy+JNlLxsDADrnLNVFUgDCAAAAAElFTkSuQmCC) folgendes **Property-Bundle** an:**Name**100 agorum.composite.details.view.searchView
7. Öffnen Sie das angelegte Property-Bundle und legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAAXklEQVQokWN8sHHXf4UdvxjwAX8PI4YVboIY4kx4dREAjN+/f/9PrmaWl7sOMxDn7I8MnUV3Gc4jeYEiZ7OIu9kyfHcjRulHDBHKAgxXVCH7swGXZuJD+wF1A4wizQD1ISunKVViAQAAAABJRU5ErkJggg==) folgende **Property-Entrys** an:***Property-Entry 1*****Name**Brick**Datentyp**Zeichenkette (String)**Wert (String)**Aguila.Frame***Property-Entry 2*****Name**Description**Datentyp**Zeichenkette (String)**Wert (String)**search-view***Property-Entry 3*****Name**Name**Datentyp**Zeichenkette (String)**Wert (String)**search.view.details.widgetdefinition.brickSearchView***Property-Entry 4*****Name**Selector**Datentyp**Zeichenkette (String)**Wert (String)**Leer lassen
8. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAAAiklEQVQokWP8/uD0/4jOlwwbGdABP8OBPhMGcwxxBGB8sHHXf4Udv/AowQYgBjORqAsKPjI4FO0lVzMEEKXZ38OI4XufMkMDOZpxAbwB1pDozFCuiy76nmFl5zmGhJe0tBkG/D2MGFa4fWToLLqL4m+KbGYhRtHGHecYOHdgijOJ6wsy+JNlLxsDADrnLNVFUgDCAAAAAElFTkSuQmCC) folgendes **Property-Bundle** an:**Name**Config
9. Öffnen Sie das angelegte Property-Bundle und legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAAXklEQVQokWN8sHHXf4UdvxjwAX8PI4YVboIY4kx4dREAjN+/f/9PrmaWl7sOMxDn7I8MnUV3Gc4jeYEiZ7OIu9kyfHcjRulHDBHKAgxXVCH7swGXZuJD+wF1A4wizQD1ISunKVViAQAAAABJRU5ErkJggg==) folgendes **Property-Entry** an:**Name**type**Datentyp**Zeichenkette (String)**Wert (String)**search.view.details.widgetdefinition.brickSearchView

blockquote { font-style: italic; padding: 2px 0; border-style: solid; border-color: #ccc; border-width: 0; padding-left: 20px; padding-right: 8px; border-left-width: 5px; } hr { border: 0px; border-top: 1px solid #ccc; }

## URL aus dem agorum core smart assistant aufrufen

Um eine URL aus dem *agorum core smart assistant* aufzurufen, existieren mehrere Möglichkeiten.

* über den *agorum core client*, der die URL im Standard-Browser öffnet
* als Client-Aktion im *agorum core smart assistant*, dann wird die URL im aktuell benutzten Browser aufgerufen.

### URL über den agorum core client aufrufen

* * *

Nachfolgend finden Sie ein Beispiel einer Aktion, die eine URL über den *agorum core client* im Standard-Browser öffnet. Bei diesem Beispiel wird davon ausgegangen, dass im Beschreibungsfeld eines Objekts (description) eine URL steht.

In der *agorum core smart assistant*\-Konfiguration als Server-Aktion, Registerkarte *JavaScript*:

```auto
/* global sessionController, sessionControllerAdmin, folder, objects, data */

let ret = '';
let description = objects[0].description;

if (description && (description.startsWith('http://') || description.startsWith('https://'))) {
  ret = 'url:agorum:open:' + encodeURIComponent(description);
} else {
  throw 'Keine URL enthalten';
}

ret;
```

### URL im Browser aufrufen

* * *

Nachfolgend finden Sie ein Beispiel einer Aktion, die eine URL direkt im aktuell benutzten Browser öffnet. Bei diesem Beispiel wird davon ausgegangen, dass im Beschreibungsfeld eines Objekts (description) eine URL steht. Diese Konfiguration benötigt eine Server-Aktion und eine Client-Aktion.

In der *agorum core smart assistant*\-Konfiguration als Server-Aktion, Registerkarte *JavaScript*:

```auto
/* global sessionController, sessionControllerAdmin, folder, objects, data */

let ret = '';
let description = objects[0].description;

if (description && (description.startsWith('http://') || description.startsWith('https://'))) {
ret = 'action:_ImBrowseröffnen:' + description;
} else {
  throw 'Keine URL enthalten';
}

ret;
```

Die zugehörige Client-Aktion lautet *\_ImBrowseröffnen* (Feld *Name intern*).

In der *agorum core smart assistant*\-Konfiguration als Client-Aktion, Registerkarte *JavaScript*:

```auto
/* global window, folderId, ids */

window.open(ids.join(':'));
```

### Beispiel einer agorum core smart assistant-Konfiguration

* * *

Für ein Beispiel einer *agorum core smart assistant*\-Konfiguration als Add-on siehe [URL im Browser öffnen - Beispiele.zip](#).

## Eigene Schaltflächen in den agorum core explorer einfügen

Sie können oberhalb der Ordnerdarstellung im *agorum core explorer* Schaltflächen einfügen, um den *agorum core explorer* zu individualisieren.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/547cfed0-3e5a-11ed-9c7e-005056aa0ecc)

```auto
OCR: Dateien,Eigene Dateien,Mail,Name,agorum,core,basic,archive,agorum,core,mail,archive,d4wdemo,d4wdr,Demo,DemoWorkflows,Objekt herunterladen,11.0.png,Beschreibung,Betreff,d4wdemo,d4wdr,Zuletzt durch roi,roi,roi,roi,roi,roi
```

Toolbar mit Schaltflächen im *agorum core explorer*

Eine Schaltfläche benötigt eine Toolbar, damit das System diese Schaltfläche darstellen kann.

### Eine Toolbar erstellen

* * *

1. Öffnen Sie links in der Seitenleiste **Administration** und dann **MetaDB**.
2. Öffnen Sie den Pfad:

    ```auto
    MAIN_MODULE_MANAGEMENT/customers/agorum.explorer/toolbars
    ```

3. Klicken Sie auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAQCAYAAADJViUEAAABBklEQVQoU2P8/v37fwY4+MNw9dJThlOfESI4Wbz8DIzImj8cOs0gs+ETw18i9DIwMKJqvrThKIP5oR+oWllYGETZGRi+fv/D8O0fqhTjrcNn/pdeZGfIT1Zh4MamWV2N4Xs6D0N1yzmGvndomk8u3/Pf/BAnw7w+IwZtqmhmYmYQ5GRiYAFZpKbM8CiWh6Gr/yLDFLDN/+FeYMRqs5AUw8kaTQY9rAH3Hu4F7JopshnZRvoGGLLN+OIZOcA8SU1hyJojGUBp+z7D7NNfGF7gTaKsDPqmMgwooR1JVJpGKGJ8vvPQf+IzAwODop0Rw7UAQbAJwFz1+T/R2RCoQUBWkiFQjg2sGQD/0MtlI4lWAAAAAABJRU5ErkJggg==), um eine MetaDb-Gruppe anzulegen.**Beispiel**

    ```auto
    [ example.package ]
    ```

4. Klicken Sie auf ![Hinweis: Beachten Sie die Reihenfolge und Nummerierung von Toolbars.](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAAAxUlEQVQoU2P8fvvif5NJjxmu/mFABZyCDPMqjBgiedHEkbiMJ5fv+W9+6Ad2FZxcDK5KHAxcGLKsDPr6Egz4NeO2FCjDSJxmZjYWBiFWBoaPX/8w/CLa2VCFinZGDNcCvjAEFd1i2E4XzZ7hzgzrzNE9/p6huuUcQ987oK/xhbaOiQpDljwDg4CsJEOg3E+G/UffMTxg+Mmwfsdjht1fCWiG2UmRn+XMtBl2u35lSG99wHCA1ADDFd2MOJMn3gQClGThYgAAsw9tO9Do/XwAAAAASUVORK5CYII=), um ein MetaDb-Bundle anzulegen.

    **Hinweis**: Beachten Sie die [Reihenfolge und Nummerierung von Toolbars](#ReihenfolgeUndNummerierung).

    **Beispiel**

    ```auto
    0300 example.package.toolbar
    ```

5. Klicken Sie auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAAlklEQVQoU2O8dfjM/9KLvxjwAWl9NYZeE24MJYwnl+/5b37oB17NinZGDNcCBDE1f//+/T9enXgkGYl39jeGvrlPGJ4ieYEEZ39hCCq6xXADyQuMxDv7Mabm5zdv/1//+C+GzwRkJRkC5X4y7D/6juEBWPYjw7S1rxleqMoyNOmxg0VwOhsSwhCnbscRaJQ5myI/U6IZAD2yZ1V1Qb7vAAAAAElFTkSuQmCC), um [Property-Entrys einer Toolbar](#PropertyEntryToolbar) anzulegen.

#### Reihenfolge und Nummerierung von Toolbars

Das System zeigt Toolbars in aufsteigender Reihenfolge von links nach rechts oberhalb der Ordnerdarstellung an.

Die Reihenfolge und Nummerierung von Toolbars gelten auch für Schaltflächen.

Folgende Konvention für die Nummerierung gilt.

| Nummerierung | Beschreibung |
| --- | --- |
| 0000 - 0099 | Definiert Toolbars, die das System vor den Standard-Toolbars anzeigt. |
| 0100 - 0199 | Definiert Standard-Toolbars, die das System ganz vorn am Anfang anzeigt. Die mitgelieferten Schaltflächen Suchen in diesem Ordner und Neuer Ordner im agorum core explorer gehören zu dieser Kategorie. |
| 0200 - 0299 | Definiert Standard-Toolbars, die nicht am Anfang stehen müssen. Die mitgelieferten Admin-Toolbars für Benutzer, Benutzergruppen und ACLs in der MetaDB gehören zu dieser Kategorie. |
| 0300 - 9999 | Nicht reserviert, steht zur freien Verfügung. |

#### Property-Entrys einer Toolbar

| Property-Entry | Beschreibung | Beispiel |
| --- | --- | --- |
| visible | Definiert optional anhand eines Selektors oder eines Arrays von Selektoren, in welchen Ordnern (oder ordnerähnlichen Objekten wie Benutzergruppen) das System diese Toolbar anzeigen soll. Wenn Sie dieses Property-Entry nicht anlegen, ist die Toolbar überall sichtbar. | \[isFolder\]\[~~area=Kundenakte\] Zeigt die Toolbar im agorum core explorer an, wenn das Objekt: ein Ordner ist das Metadatum area den Wert Kundenakte besitzt (eine Kundenakte ist) |

### Eine Schaltfläche erstellen

* * *

1. Öffnen Sie Ihre erstellte [Toolbar](#EineToolbarErstellen) unter:

    ```auto
    [ exmaple.package]
    ```

2. Klicken Sie auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAAAxUlEQVQoU2P8fvvif5NJjxmu/mFABZyCDPMqjBgiedHEkbiMJ5fv+W9+6Ad2FZxcDK5KHAxcGLKsDPr6Egz4NeO2FCjDSJxmZjYWBiFWBoaPX/8w/CLa2VCFinZGDNcCvjAEFd1i2E4XzZ7hzgzrzNE9/p6huuUcQ987oK/xhbaOiQpDljwDg4CsJEOg3E+G/UffMTxg+Mmwfsdjht1fCWiG2UmRn+XMtBl2u35lSG99wHCA1ADDFd2MOJMn3gQClGThYgAAsw9tO9Do/XwAAAAASUVORK5CYII=), um das MetaDB-Bundle **buttons** anzulegen.
3. Klicken Sie auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAAAxUlEQVQoU2P8fvvif5NJjxmu/mFABZyCDPMqjBgiedHEkbiMJ5fv+W9+6Ad2FZxcDK5KHAxcGLKsDPr6Egz4NeO2FCjDSJxmZjYWBiFWBoaPX/8w/CLa2VCFinZGDNcCvjAEFd1i2E4XzZ7hzgzrzNE9/p6huuUcQ987oK/xhbaOiQpDljwDg4CsJEOg3E+G/UffMTxg+Mmwfsdjht1fCWiG2UmRn+XMtBl2u35lSG99wHCA1ADDFd2MOJMn3gQClGThYgAAsw9tO9Do/XwAAAAASUVORK5CYII=), um ein MetaDB-Bundle anzulegen.

    **Hinweis**: Die [Reihenfolge und Nummerierung von Toolbars](#ReihenfolgeUndNummerierung) gelten auch für Schaltflächen.

    **Beispiel**

    ```auto
    0100 exmaple.button
    ```

4. Klicken Sie auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAAlklEQVQoU2O8dfjM/9KLvxjwAWl9NYZeE24MJYwnl+/5b37oB17NinZGDNcCBDE1f//+/T9enXgkGYl39jeGvrlPGJ4ieYEEZ39hCCq6xXADyQuMxDv7Mabm5zdv/1//+C+GzwRkJRkC5X4y7D/6juEBWPYjw7S1rxleqMoyNOmxg0VwOhsSwhCnbscRaJQ5myI/U6IZAD2yZ1V1Qb7vAAAAAElFTkSuQmCC), um [Property-Entrys einer Schaltfläche](#PropertyEntrysSchaltflaeche) anzulegen.

#### Property-Entrys einer Schaltfläche

| Property-Entry | Beschreibung | Beispiel |
| --- | --- | --- |
| action | Definiert die Aktion aus dem agorum core smart assistant konfigurator, die das System ausführt, wenn ein Benutzer die Schaltfläche anklickt. Das System blendet diese Schaltfläche aus, wenn diese Aktion für die aktuell gewählten Objekte nicht verfügbar ist. Sie können dieses Property-Entry nicht zusammen mit dem Property-Entry structure verwenden. | agorum\_admin\_tools\_create\_folder |
| enabled | Definiert optional einen Selektor oder ein Array von Selektoren, die definieren, für welche Objekte diese Schaltfläche aktiv ist. Wenn Sie dieses Property-Entry nicht anlegen, ist die Schaltfläche immer sichtbar. | \[isFolder\] |
| icon | Definiert das agorum-Icon als Zeichenkette (String), das das System für diese Schaltfläche anzeigt. Sie können dieses Property-Entry nicht zusammen mit dem Property-Entry iconCls verwenden. | mdi:person;color=#0069b5 |
| iconCls | Definiert das Icon (gegeben als CSS-Klasse), das das System für diese Schaltfläche anzeigt. Sie können dieses Property-Entry nicht zusammen mit dem Property-Entry icon verwenden. | aguila-icon person |
| structure | Definiert die Anlage-Konfiguration aus dem agorum core smart assistant konfigurator, die das System ausführt, wenn ein Benutzer die Schaltfläche anklickt. Sie können dieses Property-Entry nicht zusammen mit dem Property-Entry action verwenden. | agorum\_admin\_tools\_search\_folder |
| target | Definiert optional mit dem Wert parent, dass sich eine Schaltfläche auf den aktuell sichtbaren Ordner bezieht (etwa Neuer Ordner). Im Standard bezieht sich eine Schaltfläche auf die aktuell gewählten Elemente. | parent |
| text | Definiert optional den Text, den das System für diese Schaltfläche als Tooltip anzeigt. | Neuer Ordner |
| visible | Definiert optional anhand eines Selektors oder eines Arrays von Selektoren, für welche Objekte das System diese Schaltfläche anzeigen soll. Wenn Sie dieses Property-Entry nicht anlegen, ist die Schaltfläche immer sichtbar. | \[isFolder\] |

## Standardfunktionen im Explorer überschreiben

Sie können Standardfunktionen im Explorer durch ein Skript überschreiben. Sie können Folgendes anpassen:

* das Hauptmenü,
* das Kontextmenü,
* die Toolbar im Explorer,
* die Aktion beim Öffnen.

Die Konfiguration erfolgt über Property-Bundles und eine Property-Group in der MetaDB sowie über ein JavaScript.

### Einbinden eines override-Skripts

* * *

Gehen Sie wie folgt vor, um die Standardeinstellung für Hauptmenü, Kontextmenü, Toolbar oder die Aktion beim Öffnen zu überschreiben.

1. Öffnen Sie links in der Seitenleiste **Administration** und erstellen Sie das neue Skript, etwa unter folgendem Pfad im Administrationsbereich:

    ```auto
    Root/agorum/roi/customers/agorum.doc.test/js/override/explorer.js
    ```

2. Legen Sie ein neues Modul in der MetaDB an. Öffnen Sie dazu links in der Seitenleiste **Administration** und dann **MetaDB**.
3. Rufen Sie folgenden Pfad auf:

    ```auto
    MAIN_MODULE_MANAGEMENT/customers/agorum.explorer
    ```

4. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAMCAYAAABSgIzaAAAAYElEQVQoFWPwz9zynwEDH/5/4Pv3/9/xYAZMTdgMQhaDGEqGRqghpNtIpEb/jc/+f/9+/X8DejgQspFkjQ2nsIXqs/8LGgg4lWyNMC+Q7FSKNcIMwKCxJznklIKNves/AEgdk/R3SHLmAAAAAElFTkSuQmCC) folgendes Property-Bundle an und rufen Sie es danach auf:**Name**: settings
5. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAOCAYAAADwikbvAAAAeElEQVQ4EWP4/v37fzg+dfg/Q+YW4jFc4/fv/x9s3EW8RpAlEA2H/x/ApXnG9f/fvz/7v6ABi4sGmeaG0/8fIAckChvJC4PM2chxTVFoIxuEzkb283dSUxiKZnCoXv/fgG4DBh+SqFBSGHJSJYbNQKpT/Tc+g2ckAPtHMHI4ZOg6AAAAAElFTkSuQmCC)  eine Property-Group an und rufen Sie sie danach auf. Idealerweise verwenden Sie einen Projektnamen:**Name**: name-des-projekts

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/97c46d80-1c0d-11ef-b611-005056aa0ecc)

    ```auto
    OCR: Neue MetaDb Property-Group anlegen, Ablageort: /MAIN_MODULE_MANAGEMENT/customers/agorum.explorer/settings, Name: [agorum.doc.test], Beschreibung: , Abbrechen, Speichern, Neue MetaDb Property Group anlegen, Ablageort: /MAIN_MODULE_MANAGEMENT/customers/agorum.explorer/settings, Name: agorum.doc.test, Beschreibung: , Abbrechen, Speichern
    ```

    Beispiel für eine Property-Group mit Projektnamen

6. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAMCAYAAABSgIzaAAAAYElEQVQoFWPwz9zynwEDH/5/4Pv3/9/xYAZMTdgMQhaDGEqGRqghpNtIpEb/jc/+f/9+/X8DejgQspFkjQ2nsIXqs/8LGgg4lWyNMC+Q7FSKNcIMwKCxJznklIKNves/AEgdk/R3SHLmAAAAAElFTkSuQmCC) ein Property-Bundle an und rufen Sie es danach auf. Idealerweise verwenden Sie einen Namen, der die Verwendung genauer spezifiziert:**Name**: name-des-bundles

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/619f1470-1c0e-11ef-b611-005056aa0ecc)

    ```auto
    OCR: Neues MetaDb Property-Bundle anlegen, Ablageort: /MAIN_MODULE_MANAGEMENT/customers/agorum.explorer/settings/[ agorum.doc.test], Name: agorum.doc.test.override, Beschreibung: , Abbrechen, Speichern
    ```

    Beispiel für ein Property-Bundle mit Namen

7. Legen Sie im zuletzt angelegten Property-Bundle über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAASklEQVQoFWN4sHHXf4bMLXix/8Zn/79//46BGSjSjM1EYsVIsPn6/4bMLf+RvUCZZmKd+P07Fpsp0owrtCF+g9iGMyopsnnANAMAdi8bRRmARxAAAAAASUVORK5CYII=) das folgende Property-Entry an:**Name**: js**Datentyp**: Zeichenkette (String)**Wert (String)**: <Pfad zur erstellten JavaScript-Datei und Name der Datei ohne Dateiendung>

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/840c6000-1c11-11ef-b611-005056aa0ecc)

    ```auto
    OCR: Neuen MetaDb Property Entry anlegen, Ablageort: /MAIN_MODULE_MANAGEMENT/customers/agorum.explorer/settings/, agorum.doc.test, /agorum.doc.test.override, Name: Zeichenkette (String), Wert: String (/agorum/roi/customers/agorum.doc.test/js/override/explorer), Beschreibung, Abbrechen, Speichern
    ```

    Beispiel für ein JavaScript Property-Entry mit Pfadangabe

8. Optional können Sie ein weiteres Property-Entry mit dem Schlüssel (Namen) **acl** anlegen, um einzuschränken, für wen das Skript geladen werden soll. Die ACL-Gruppe geben Sie als Wert an.

### override-Skript schreiben

* * *

Sie können mit einem override-Skript Einträge im Hauptmenü, im Kontextmenü oder in der Toolbar ergänzen oder ändern. Außerdem können Sie die Aktion ändern, die beim Öffnen eines Objekts ausgeführt wird. Dazu verwenden Sie verschiedene Overrides:

* mainMenuOverride: Ändert das Hauptmenü
* menuOverride: Ändert das Kontextmenü
* toolbarOverride: Ändert die Toolbar in den Ordnerdetails
* openOverride: Ändert die Aktion, die beim Öffnen eines Objekts ausgeführt wird, etwa durch einen Doppelklick

Das folgende Beispiel zeigt, wie Sie eine Gruppe von Einträgen zum Kontextmenü und eine Schaltfläche zur Toolbar in den Ordnerdetails hinzufügen können.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/e2b6c6b0-1c2d-11ef-b611-005056aa0ecc)

```auto
OCR: Name, Entwicklung, Informationen, Projekte, Vertrieb, Verwaltung, Einstieg, agorum, cor, Willkommen.pdf, Beschreibung, Betreff, Willkommen.pdf, Testgruppe, Ausschneiden, Kopieren, hier, Test, als, Aktion, Test, mit, Handler, 49:47, 49:47, Workflow, 49:47, 49:48, Rechte, vergeben, 49:47, Benutzerberechtigung, anzeigen, 49:48, Administration, 06:07, 08.02.2024, mit, Chat, 06:08, 08.02.2024, agorum, core, Basic, Archive, agorum, core, basic, archive, docform, Senden, Development, Eingang, agorum, core, template, manager, agorum, core, template, manager, Detailansicht, Seitenleiste, anheften
```

Hinzugefügte Gruppe im Kontextmenü und Schaltfläche in der Toolbar

```auto
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

exports.settings = user => [
  {
    name: 'agorum.doc.test.override',

    // Fügt eine Gruppe neuer Einträge zum Kontextmenü hinzu
    menuOverride: (items, objs, parent) => {
      console.log('menu override called', items, objs, parent);
      items = [
        {
          name: 'testGroup',
          icon: 'aguila-icon settings_ethernet',
          text: 'Testgruppe',
          type: 'group',
          items: [
            {
              name: 'testAction', // Name der Aktion
              text: 'Test als Aktion',
              type: 'action',
              icon: icons.cls('agorum:agorum-logo;color=#0069b5'),
            },
            {
              name: 'testHandler',
              text: 'Test mit Handler',
              handler: () => console.log('Test-Handler'),
            },
          ],
        },
        '-',
      ].concat(items);
      return items;
    },
    // Fügt eine Schaltfläche zur Toolbar in den Ordnerdetails hinzu
    toolbarOverride: (items, objs, parent) => {
      console.log('toolbar override called', items, objs, parent);
      items.push({
        type: 'agorum.button',
        meta: {
          parent: parent,
          objects: objs,
          //action: 'testActionTB',
          //structure: 'testStructureTB',
        },
        tooltip: 'Test-Aktion auf Toolbar',
        icon: icons.cls('mdi:person;color=#0069b5'),
        disabled: !objs[0],
      });
      //return [];
      return items;
    },
  },
];
```

#### Eintrag im Kontextmenü ergänzen

Sie können mit einem Skript nach folgendem Muster einen einzelnen neuen Eintrag im Kontextmenü ergänzen, etwa den Eintrag:

![embedded image](data:image/png;base64,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)

```auto
exports.settings = user => [
  {
    // eindeutiger Name
    name: 'my-context-menu',

    /**
     * menuOverride: Wird aufgerufen, nachdem das Menü durch den Explorer erstellt wurde
     * Parameters:
     *   items: Die Menü-Items (Array der erstellten Menü-Items)
     *   objects: Das Array der agorum core-Objekte, die durch den Explorer selektiert wurden
     *   parent: Das zugehörige parent folder object, von dem das Kontextmenü geöffnet wurde (optional)
     */
    menuOverride: (items, objects, parent) => {
      // Fügt einen neuen Eintrag zum Kontextmenü hinzu
      items.push({
        // Zeigt das Menü-Item als inaktiv an (true/false)
        disabled: false,

        // Der Handler, der aufgerufen wird, wenn das Menü-Item angeklickt wird
        handler: () => {
          let names = '';
          let parentName = '';

          if (objects) names = objects.map(item => item.name).join(', ');
          if (parent) parentName = parent.name;

          console.log('Das folgende Menü-Item wurde angeklickt: Objects: ' + names + ', Parent: ' + parentName);
        },

        // Icon für den Menü-Eintrag
        icon: 'aguila-icon sentiment_satisfied',

        // Eindeutiger Name für den Menü-Eintrag
        name: 'my-menu-entry-1',

        // Der Text des Menü-Eintrags
        text: 'My new menu entry',
      });

      return items;
    },
  },
];
```

#### Einträge aus dem Kontextmenü entfernen

Sie können Einträge entfernen und nur noch bestimmte Einträge zulassen, auch abhängig von der Benutzergruppe, indem Sie

1. eine Liste von zulässigen Einträgen definieren und
2. alle anderen Einträge für bestimmte Benutzergruppen unter bestimmten Bedingungen aus dem Kontextmenü entfernen

Sie könnten etwa das Kontextmenü für das Starten von Workflows auf folgende Einträge reduzieren

![embedded image](data:image/png;base64,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)

Das können Sie mit einem Skript nach folgendem Muster erreichen:

```auto
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');
let objects = require('common/objects');
let beans = require('common/beans');

let tokenAllowed = {
  startWorkflow: true,
  Detailsanzeigen: true,
};

let removeItem = (items, objects, allowed, selectors) => {
  if (objects.some(obj => beans.selected(obj, selectors))) {
    items = items.filter(item => allowed[item.name]);
  }

  return items;
};

exports.settings = user => [
  {
    // eindeutiger Name
    name: 'my-context-menu',

    menuOverride: (items, objects, parent) => {
      console.log('context menu override called', items, objects);
      if (!sc.adminEnabled) {
         items = removeItem(items, objects, tokenAllowed, '<REPLACESELECTOR>');

      }
      return items;
    },
  },
];
```

#### Toolbar-Schaltfläche ergänzen

Sie können mit einem Skript nach folgendem Muster ein Toolbar-Icon ergänzen, etwas das Icon:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/877fa4d0-1cc1-11ef-b611-005056aa0ecc)

```auto
OCR: Bitte gib mir den OCR-Text, den ich zusammenfassen soll. Ich werde dann:
```

```auto
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

exports.settings = user => [
  {
    name: 'agorum.doc.test.override',

    toolbarOverride: (items, objs, parent) => {
      console.log('toolbar override called', items, objs, parent);
      items.push({
        type: 'agorum.button',
        meta: {
          parent: parent,
          objects: objs,
          //action: 'testActionTB',
          //structure: 'testStructureTB',
        },
        tooltip: 'Test-Aktion auf Toolbar',
        icon: icons.cls('mdi:person;color=#0069b5'),
        disabled: !objs[0],
      });
      //return [];
      return items;
    },
  },
];
```

Die Einstellung `disabled: !objs[0]` führt dazu, dass das Icon nur aktiv wird, wenn der Benutzer einen Eintrag im Explorer ausgewählt hat, wie hier gezeigt:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/878e98f0-1cc1-11ef-b611-005056aa0ecc)

```auto
OCR: Dateien, Eigene Dateien, Mail, Demo, Willkommen.pdf, Einstieg, agorum, cor, Verwaltung, Vertrieb, Projekte, Informationen, Entwicklung, Beschreibung, Betreff
```

Aktivieren eines Icons nur bei aktiver Auswahl

#### Hauptmenü-Icon ergänzen

Sie können mit einem Skript nach folgendem Muster ein Hauptmenü-Icon ergänzen, etwas das Icon ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABwAAAAZCAYAAAAiwE4nAAACbklEQVRIS82WXUhTYRjHf3Obm1ubzlFtFSYaRN1YSon0dRMh2G0gUQhFF9WN99FVdNGN2U23IUEUURQkSNSNJCLSkkbLgkzZxtSc5swc+6r3uHnaaTsflEnPzYFzHp7f+3++3mP6IYwNNNN/BczmYH4FlpKwkoZ0VjsVVjNUWcFlh9oqMFeU+qsqjC3BTOLvcr3VDX6XMkYJMCmUTC3kFa2HSYp3esAunpIpgBLsU1wtdTmWEou8n4wTSf12lEoHTfVe6tw2CnEVDlKqG715qAL4Yba8snQ0xMX7nwkktRvaZndzofMw57aXFk9SuntLEVC9ZjPc6B3lwbLBBDu3cae7maYy7lJNVxVK3RiMqQWcoPt6iKCnhhavRXaaic0RxMVxv01+txxfYHihhmtX2uhQCbcK/CJOH/2qDQwfaOPRCVGIgvXfe8ZV9hI43SC/+/j8JZ2jDn3ghGiUhJi18pZXuK7Ad9NaQ/0PgGNRrYbIA0esVjwWk+yYSqWYx4Kv8ldH5jJpZtO1+ik1Ahw02KTg1QcaSelghY39DWJPTcd58005j7ZNbo74YHwiQSRnAGikaSZbWnnSvhnGhmnuF11WZEc7TtK7D0IDLzjz2qmvUHssCoNv8dFzqo7wQICbkYwC6N2xi552B48fvuVpRn3w5V2qPfiig6NBuu5OMa5zPWF2cv7sMS6XWW1rJ5R3qe51lF2kr2+IWzGxlspYtb+Rvq491IlFrWbyaltzUFve0vfw0CsujXxHXaSJ+taD3D5UXZZXsrwlL+3ryfBclDiqXk9r0A27gIuPpltTA4IN/WIUx9nQnygDAv7I5Sfh5nCLRtJCDgAAAABJRU5ErkJggg==):

```auto
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

exports.settings = user => [
  {
    name: 'agorum.doc.test.override',

    mainMenuOverride: (items, objs) => {
      console.log('main menu override called', items, objs);
      items.push({
        type: 'agorum.button',
        tooltip: 'Test-Aktion im Hauptmenü',
        icon: 'aguila-icon directions_subway',
      });
      //return [];
      return items;
    },
  },
];
```

#### Öffnen eines externen E-Mail-Programms bei bestimmten Benutzern

In diesem Beispiel wird für bestimmte Benutzer anstelle der eingebauten E-Mail-Anzeige ein externes E-Mail-Programm geöffnet. Dazu wird geprüft, ob der Benutzer eine bestimmte ACL hat (in diesem Fall *ACLDemo*) und für Benutzer mit dieser ACL der externe E-Mail-Client geöffnet.

```auto
/* global sca */

let icons = require('/agorum/roi/customers/agorum.icons/js/icons');
let objects = require('common/objects');
let beans = require('common/beans');

exports.settings = user => {
  let redirectMailOpen = objects(sca.asUser(user)).mayDiscover('ACLDemo');

  return [
    {
      name: 'agorum.doc.test.override',

      openOverride: (items, objs) => {
        console.log('openOverride', redirectMailOpen, items);

        if (redirectMailOpen) {
          /*
          let isMail = items.some(
            item => item.name === '_mail' || item.name === '_mailDraft' || item.name === 'agorum.mail.open'
          );
          */
          let isMail = objs.every(obj => beans.selected(obj, '[classname=/MailObject|AMailMail/]'));

          if (isMail) {
            return [
              {
                name: '_openClient',
              },
            ];
          }
        }

        return items;
      },
    },
  ];
};
```

#### open-Aktionen verhindern

Sie können durch die Verwendung von openOverride jegliche open-Aktionen verhindern, etwa um Fallbacks bei Ordnern zu verhindern.

```auto
exports.settings = user => [
  {
    name: 'agorum.doc.test.override',
    openOverride: (items, objs) => {
      console.log('open override called', items, objs);
      // keine Aktion ausführen
      return [{}];
    },
  },
];
```

### Parameter

* * *

| Parameter | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| items | Menü-Items mit entsprechenden Einstellungen | Array von Items |
| objects | Das Array der agorum core-Objekte, die durch den Explorer selektiert wurden | Array von Objekten |
| parent | Das zugehörige parent-Objekt, von dem das Kontextmenü geöffnet wurde (optional). | parent Objekt |

Für die möglichen Angaben zu den Items siehe [agorum core aguila](#).

