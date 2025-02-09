# Übersicht - agorum.composite.form summary

## agorum.composite.form

Mit der *aguila*\-Bibliothek *agorum.composite.form* können Sie Form-Elemente wie Eingabefelder oder Auswahlboxen zusammenstellen, um so etwa Aktendeckel oder Eingabemasken umzusetzen.

Die Bibliothek enthält Funktionen wie eine automatische Validierung, das Laden von Datenquellen bei Auswahlboxen sowie das Umschalten zwischen Bearbeitungs- und Ansichtsmodus.

### Allgemein

* * *

| Thema | Beschreibung | Link |
| --- | --- | --- |
| Grundlagen | Beispiel zur Verwendung der Bibliothek. | Grundlegende Verwendung |
| Validierung | Validierungsfunktionen der form-Elemente. | Validierung |
| Häufig verwendete Utils | Eine Sammlung häufig verwendeter Utils im Zusammenhang mit agorum core form. | Utils |

### form-Typen

* * *

*elements* bündelt das System in *form*. Sie können diverse elements zu einer Einheit zusammenfassen und als Ganzes verwenden.

| Thema | Beschreibung | Link |
| --- | --- | --- |
| basic | basic ist die grundlegende form und enthält element-Widgets. | basic |
| metadata-basic | metadata basiert auf basic und erweiterte diese form um die Möglichkeit, Metadaten automatisch zu laden und zu speichern. | metadata-basic |
| metadata-collection | Mit dieser form können Sie metadata collections (Sammlungen von Metadaten) verwenden. | metadata-collection |
| metadata-edit | metadata-edit basiert auf metadata-basic und ergänzt das Laden und Speichern von Metadaten um eine komplette Steuerung der Maske über diverse Schaltflächen. | metadata-edit |
| edit | edit bietet dieselben Steuerungselemente wie metadata-edit, mit dem Unterschied, dass Sie das Speichern und Laden selbst implementieren und somit steuern können, was beim Speichern und Laden passiert. | edit |

### element-Typen

* * *

Enthält die einzelnen *elements* in einer form. Diese enthalten die Logik zur Darstellung und Validierung von Feldern.

| Thema | Beschreibung | Link |
| --- | --- | --- |
| Grundlegende Eigenschaften | Eigenschaften, die alle elements gemeinsam haben. | Grundlegende Eigenschaften |
| boolean | Stellt ein Ja-/Nein-Feld als Checkbox dar. | boolean |
| button | Stellt ein button-element dar. | button |
| date | Stellt ein Datumselement dar, das viele Darstellungsoptionen enthält, um etwa Datum + Uhrzeit oder nur Datum einzugeben und darzustellen. | date |
| emailAddress | E-Mail-Adressen eingeben und wählen. | emailAddress |
| grid | Präsentiert in Spalten angeordnete Felder. Dieses Element enthält umfangreiche Darstellungs- und Bearbeitungsfunktionen für die dargestellten Felder. | grid |
| html | HTML-Inhalte anzeigen und editieren. | html |
| label | Definiert Labels für Basis-Widgets, die kein Label besitzen. | label |
| list | Stellt eine Liste von Werten dar. Dieses Element enthält umfangreiche Darstellungs- und Bearbeitungsfunktionen für die Werte einer Liste. | list |
| mailEditor | Stellt eine konfigurierbare E-Mail-Maske dar. | mailEditor |
| Metadatum | Wird lediglich ein Metadaten-Name übergeben, so ermittelt agorum core automatisch das passende Element und lädt alle Eigenschaften aus der Metadaten-Definition. | Metadatum |
| number | Stellt ein Zahlen-Eingabefeld dar, sowohl für Integer- als auch für Dezimal-Zahlen. | number |
| objectPicker | Stellt ein Eingabefeld mit Picker zur Auswahl eines Objekts dar, entweder über die Suche oder über eine Ordnerauswahl. | objectPicker |
| objects | Stellt eine konfigurierbare Maske zur Verwaltung und Auswahl von Objekten dar. | objects |
| picker | Stellt ein Eingabefeld mit einem Widget dar, das sich öffnet, wenn ein Benutzer eine Trigger-Schaltfläche anklickt. | picker |
| select | Stellt eine Auswahlbox für einzelne oder multiple Werte (Combobox, Tokenbox) dar. Das Laden und Darstellen von Auswahl-Werten aus Datenquellen wird dabei automatisch unterstützt. | select |
| splitGrid | Präsentiert Felder in Spalten und teilt (splittet) Positionen einer Rechnung auf. | splitGrid |
| splitList | Stellt eine Liste von Feldern dar und teilt (splittet) Positionen einer Rechnung auf. | splitList |
| text | Stellt ein ein- oder mehrzeiliges Textfeld dar, das monospace (gleichbleibender Abstand von Buchstaben) und Passwort unterstützt. | text |

### Erweiterung

* * *

Sie können *agorum.composite.form* um eigene Element*\-*Typen erweitern.

| Thema | Beschreibung | Link |
| --- | --- | --- |
| Interner Aufbau von element | Beschreibung der Factory zur Erzeugung eigener Element-Typen. | Interner Aufbau |

## agorum.composite.form - Grundlegende Verwendung

### Die Bestandteile

* * *

Eine Oberfläche besteht aus zwei Elementen:

* der form
* den darin enthaltenen Elementen (text, date, ...)

Die *form* bündelt die Elemente zu einer Einheit.

**Beispiel**

Dieses Beispiel erstellt eine basic-form mit zwei enthaltenen Text-Elementen.

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 300,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Text 1',
      validation: [
        {
          required: true
        }
      ]
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField2',
      label: 'Text 2'
    },
    {
      name: 'ag_tags'
    }

  ],
  readOnly: false

});

form;
```

* Das erste Text-Element wurde als *required* definiert (Pflichtfeld).
* Das zweite Text-Element ist optional.
* Das dritte Element *ag\_tags* ist ein definiertes Metadatum. Hier ermittelt *agorum.composite.form* automatisch die korrekte Darstellungs- und Eingabeform basierend auf den Einstellungen des Metadatums.

Die umliegende *form* mit dem Namen *basicForm* ist somit eine Oberfläche, bestehend aus drei Feldern. Sie können über die basic-form alle Parameter steuern.

**Hinweis**: Die folgenden Abschnitte beschreiben die grundlegende Funktionsweise. Zur Beschreibung der einzelnen Parameter von *agorum.composite.form.basic* siehe [agorum.composite.form - basic](#).

### In den Ansichtsmodus umschalten

* * *

```auto
form.down('basicForm').readOnly = true;
```

### Die Validierung abfragen

* * *

Das folgende Beispiel ermittelt, ob alle Eingaben valide sind:

```auto
let valid = form.down('basicForm').valid;
```

Wenn ja, erhalten Sie *true* zurück, ansonsten *false*.

### Funktionen

* * *

#### set

**Ab welcher Version verfügbar?**

• *agorum core* 9.3.0

Setzt Parameter und Werte direkt.

Verwenden Sie *set* bevorzugt vor *form.down* (siehe [Werte setzen](#WerteSetzen)), um Werte direkt zu setzen.

**Verwendung**

```auto
form.set(path, propertyValue);

// Beispiel
form.set('textField1.value', 'Ein Wert');
```

**Parameter**

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| path | Definiert den Pfad zum Element inklusive Parameter (etwa value, hidden, readOnly), von wo aus das System die Funktion aufruft. Befindet sich das Element textField1 etwa direkt unter form, lautet der Pfad dazu textField1 (relativ zu form gesehen). | Werte von tiefer verschachtelten Elementen setzen (Listen) // setzt den Wert für column1 in Zeile 0 in Liste listField1: form.set('listField1\[0\].column1.value', 'Wert für Liste, Zeile 0, Spalte column1'); Parameter setzen (hidden, readOnly) // Deaktiviert das Feld in column1 in Zeile 0 in Liste listField1: form.set('listField1\[0\].column1.disabled', true); path kann entweder in Punkt und Array \[\] Notation erfolgen, wie in den obigen Beispielen, oder Sie können path als Array definieren. Das ist notwendig, wenn der Namen eines Parameters einen Punkt oder \[\] besitzt. Obige Beispiele als Array geschrieben // setzt den Wert für column1 in Zeile 0 in Liste listField1: form.set(\[ 'listField1', 0, 'column1', 'value' \], 'Wert für Liste, Zeile 0, Spalte column1'); // Deaktiviert das Feld in column1 in Zeile 0 in Liste listField1: form.set(\[ 'listField1', 0, 'column1', 'disabled' \], true); |

#### get

**Ab welcher Version verfügbar?**

• *agorum core* 9.3.0

Liest Parameter und Werte direkt.

Verwenden Sie *get* bevorzugt vor *form.down* (siehe [Werte lesen](#WerteLesen)), um Werte direkt zu lesen.

**Verwendung**

```auto
let value = form.get(path);

// Beispiel: holt den Wert von textField1
let value = form.get('textField1.value');
```

**Parameter**

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| path | Definiert den Pfad zum Element inklusive Parameter (etwa value, hidden, readOnly), von wo aus das System die Funktion aufruft. Befindet sich das Element textField1 etwa direkt unter form, lautet der Pfad dazu textField1 (relativ zu form gesehen). | Werte von tiefer verschachtelten Elementen lesen (Listen) // holt den Wert für column1 in Zeile 0 in Liste listField1: let value = form.get('listField1\[0\].column1.value'); Parameter lesen (hidden, readOnly) // liest den Status von disabled vom Feld in column1 in Zeile 0 in Liste listField1: let disabled = form.get('listField1\[0\].column1.disabled'); path kann entweder in Punkt und Array \[\] Notation erfolgen, wie in den obigen Beispielen, oder Sie können path als Array definieren. Das ist notwendig, wenn der Namen eines Parameters einen Punkt oder \[\] besitzt. Obige Beispiele als Array geschrieben // holt den Wert für column1 in Zeile 0 in Liste listField1: let value = form.get(\[ 'listField1', 0, 'column1', 'value' \]); // liest den Status von disabled vom Feld in column1 in Zeile 0 in Liste listField1: let disabled = form.get(\[ 'listField1', 0, 'column1', 'disabled' \]); |

#### Werte setzen

**Hinweis**: Verwenden Sie ab *agorum core* 9.3.0 die Funktion [set](#set), um Werte zu setzen, da Sie bei *form.down* einige Besonderheiten beachten müssen.

**Verwendung**

```auto
form.down('basicForm').value = {
  textField1: 'Wert 1',
  textField2: 'Wert 2'
};
```

**Werte direkt auf die jeweiligen Elemente setzen**

```auto
...
  items: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Text 1',
      value: 'Wert 1'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField2',
      label: 'Text 2',
      value: 'Wert 2'
    }
  ]
...
```

#### Werte lesen

**Hinweis**: Verwenden Sie ab *agorum core* 9.3.0 die Funktion [get](#get), um Werte zu lesen, da Sie bei *form.down* einige Besonderheiten beachten müssen.

**Verwendung**

```auto
let values = form.down('basicForm').value;
```

**Ergebnis (Beispiel)**

```auto
{
  textField1: 'Wert 1',
  textField2: 'Wert 2'
}
```

### aguila-Widgets verwenden

* * *

Sie können die einzelnen Elemente mit *aguila*\-Widgets mischen, sodass Sie die einzelnen Felder nach Wunsch anordnen können.

**Textfelder durch [agorum.hbox](#) nebeneinander darstellen**

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 600,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      type: 'agorum.hbox',
      items: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'textField1',
          label: 'Text 1',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'textField2',
          label: 'Text 2',
          flexible: true
        }
      ]
    },
    {
      name: 'ag_tags'
    }

  ],
  readOnly: false

});

form;
```

### Elemente ohne form verwenden

* * *

Sie können Elemente ohne *form* verwenden, wenn Sie keine *form* benötigen, um mehrere Elemente zu einer Einheit zu bündeln, sondern nur die Funktionen des Elements verwenden möchten.

**Beispiel**

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  width: 600,
  height: 300,
  type: 'agorum.vbox',

  items: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Text 1'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField2',
      label: 'Text 2'
    }
  ]
});

widget;
```

## agorum.composite.form - Validierung

Mit einer Validierung können Sie Benutzereingaben anhand von Vorgaben einschränken und einen Benutzer darauf hinweisen, was er einzugeben hat. Eine Validierung können Sie entweder an ein Element oder auf eine ganze *form* setzen.

* Setzen Sie eine Validierungsdefinition (validation) auf die *form*, mischt das System deren Definitionen mit den validation-Definitionen der Elemente. Das System verhält sich dann so, als wenn die Validierung bei jedem Element gesetzt werden würde.
* Das System zeigt einen *errorText* beim jeweiligen Element an und verdeutlicht die fehlerhafte Eingabe durch eine rote Markierung.

### Validierungsdefinition

* * *

* Sie setzen die Validierungsdefinition (*validation*) per Parameter auf das Element oder die *form*.
* Die Validierung definiert, wann der eingegebene Wert eines Elements gültig ist und erlaubt so die Prüfung auf Korrektheit des eingegebenen Werts.
* Sie können mehrere Arten der Validierung übergeben.

Das System prüft bei jeder Werteänderung des Elements oder beim Ändern der Validerungsdefinitionen auf diese Validierung. Schlägt sie fehl, dann:

* setzt das System den Parameter *valid* auf *false*
* markiert das System das Element rot (abhängig von *showError*)
* zeigt das System per Mouse-Over den jeweiligen Fehlertext an (abhängig von *showError*)

Die Validierung ist ein Array mit mehreren möglichen Definitionen. Das System kann mehrere Verhalten nacheinander prüfen, und Sie können im Hinweistext genau differenzieren. So können Sie statt einer komplexen RegEx, die alles abprüft, zwei einzelne formulieren. Dadurch ist zum einen die Formulierung der regulären Ausdrücke einfacher, zum anderen zeigt das System so zu jeder RegEx einen speziellen Hinweis an.

* Jede Definition enthält einen Fehlertext ([errorText](#errorText)) und einen Parameter (etwa [regex](#regex)).
* Definieren Sie den optionalen *errorText* nicht, erzeugt das System eine Standard-Fehlermeldung.

### Beispiel einer Oberfläche

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/a9a41f00-e8b6-11ec-bc0b-005056aa0ecc)

```auto
OCR: Mail, marta.mueller.com, Keine Mail
```

Beispiel

#### Skript zur Oberfläche

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'e-Mail',
      validation: [
        {
          regex: '/.*@.*\\..*/i', // Achtung, stark vereinfacht!
          errorText: 'Keine gültige E-Mail'

        },
        {
          required: true
        }
      ]
    }
  ]
});

form;
```

### Parameter

* * *

#### required

| Wert | Beschreibung |
| --- | --- |
| true | Prüft, ob der Benutzer einen Wert gesetzt oder eingegeben hat. Verhindert etwa, dass der Benutzer das Feld vergisst und nichts eingibt. |
| false | Prüft NICHT, ob der Benutzer einen Wert gesetzt oder eingegeben hat. |

**Beispiel**

```auto
{
  required: true
}
```

#### errorText

Definiert eine Fehlermeldung.

Definieren Sie keine Fehlermeldung, lautet die Fehlermeldung *Feld darf nicht leer sein*.

**Beispiel**

```auto
{
  errorText: 'Keine gültige E-Mail'
}
```

#### maxLength

**Ab welcher Version verfügbar?**• *agorum core* 9.5.1

Beschränkt die Menge der einzugebenden Zeichen.

* Sie können *maxLength* und [minLength](#minLength) entweder gemeinsam oder jeweils einzeln verwenden.
* Verwenden Sie den Parameter [errorText](#errorText), um eine Fehlermeldung auszugeben, wenn ein Benutzer diese Menge überschreitet.

**Beispiel**

```auto
// maximal 10 Zeichen
{
  maxLength: 10,
  errorText: 'Zu viele Zeichen'
}
```

#### minLength

**Ab welcher Version verfügbar?**• *agorum core* 9.5.1

Verlangt eine Mindestmenge von Zeichen, die ein Benutzer eingeben muss.

* Sie können *minLength* und [maxLength](#maxLength) entweder gemeinsam oder jeweils einzeln verwenden.
* Verwenden Sie den Parameter [errorText](#errorText), um eine Fehlermeldung auszugeben, wenn ein Benutzer diese Menge unterschreitet.

**Beispiel**

```auto
// mindestens 3 Zeichen
{
  minLength: 3,
  errorText: 'Zu wenige Zeichen'
}
```

#### regex

Erwartet einen regulären Ausdruck in Form eines Strings.

* Das System prüft diesen Ausdruck bei Eingabe des Benutzers oder bei Änderung von *value*, etwa ('/(w\*)\[0-9\]+/').
* Sie können einen Parameter übergeben, wenn Sie den regulären Ausdruck in Schrägstriche hüllen (ein führender und endender Schrägstrich (/)) etwa regex: '/(w\*)\[0-9\]+/ig'. Dadurch erstellt das System den regulären Ausdruck mit den Parametern *i* und *g*.
* Sie können eine Schreibweise ohne Schrägstriche verwenden, etwa regex: '(w\*)\[0-9\]+'.
* Verwenden Sie den Parameter [errorText](#errorText), um eine Fehlermeldung auszugeben, wenn der reguläre Ausdruck nicht stimmt.

**Beispiel**

```auto
{
  regex: '/^([A-Z])\\w+/',
  errorText: 'Bitte mit Großbuchstaben beginnen.'

}
```

Dieser reguläre Ausdruck erwartet ein Wort, das mit mindestens einem Großbuchstaben beginnt.

* Übergeben Sie den regulären Ausdruck als String.
* Escapen Sie \\ mit \\\\.
* Das System prüft reguläre Ausdrücke nur, wenn das Feld auch einen Wert besitzt.
* Das System führt keine Prüfung durch, wenn der Parameter [required](#required) auf *false* steht, weil definiert ist, dass das Feld nicht belegt sein muss.

#### script (JavaScript)

Sie können über ein Skript eine Validierung für das jeweilige Feld durchführen. Dazu erzeugen und registrieren Sie das Skript.

Das Skript muss die Funktion *validate* enthalten.

**Wichtig**: Das System ruft diese Funktion jedes Mal synchron auf:

* für jedes Element, wenn sich das jeweilige Element ändert

* für jedes Element einer Form, wenn Sie die Funktion auf form-Ebene definiert haben

Führen Sie keine langlaufenden Operationen durch, weil sonst die Oberfläche langsamer arbeitet.

**Das Skript in der MetaDb registrieren**

1. Öffnen Sie auf der Startseite von *agorum core* **Smart Assistant**.
2. Wählen Sie links im Menü **Root Ordner**.
3. Öffnen Sie diesen **Ordner** (Beispiel):

    ```auto
    /agorum/roi/customers/tstforms/js/form/validation/
    ```

4. Legen Sie diese **JavaScript-Datei** an (Beispiel):

    ```auto
    validate-script.js
    ```

5. Klicken Sie mit der rechten Maustaste auf die **JavaScript-Datei**.
6. Wählen Sie im Kontextmenü **agorum core template manager > Register form validation**.**Ergebnis**: Sie haben das Validierungsskript registriert. Es erhält im obigen Beispiel den Namen *tstforms.testValidation*.

**Inhalt des Validierungsskripts**

**Möglichkeit 1: Das Skript gibt true / false zurück**

Diese Funktion erhält als Parameter das Element (widget) und den Wert (value).

Die Funktion:

* gibt *true* bei einem gültigen Wert zurück
* gibt *false* bei einem ungültigen Wert zurück

Beispiel für einen Zahlenwert, der zwischen 10 und 20 liegen muss:

```auto
/**
 * validate if given value is between 10 and 20
 */
function validate(element, value) {
  if (value && value >= 10 && value <= 20) {
    return true;
  }

  return false;
}

// export function
module.exports = {
  validate: validate
};
```

Geben Sie in der Definition des Elements das Skript sowie den Parameter [errorText](#errorText), den der Benutzer sehen soll, wenn die Validierung fehlschlägt, so an:

```auto
{
  script: 'tstforms.testValidation',
  errorText: 'Der angegebene Wert muss zwischen 10 und 20 liegen.'
}
```

**Möglichkeit 2: Das Skript gibt eine Fehlermeldung zurück**

Diese Möglichkeit ist ähnlich der [Möglichkeit 1](#MoeglichkeitEins), mit dem Unterschied, dass das Skript selbst Fehlermeldungen produzieren kann, die der Benutzer dann je nach Fall sieht.

***Beispiel***

```auto
/**
 * validate if given value is between 10 and 20
 */
function validate(element, value) {

  if (!value) {
    return 'Der Wert des Felds "' + element.name + '" muss belegt sein.';
  }

  if (!(value >= 10 && value <= 20)) {
    return 'Der Wert des Felds "' + element.name + '" muss zwischen 10 und 20 liegen.';
  }

  return true;
}

// export function
module.exports = {
  validate: validate
};
```

* Sie müssen den Parameter [errorText](#errorText) in der Definition nicht definieren, da der Text bereits aus dem Skript kommt.
* Ist eine Skript-Validierung aktiv, ignoriert das System den Parameter [required](#required), sodass das Skript die Möglichkeit hat, sich darum kümmern zu können.

**Parameter an das Validierungsskript übergeben**

Sie können optional Parameter übergeben, um das Skript von außen zu steuern.

***Beispiel***

```auto
/**
 * validate if given value is between parameters.from and parameters.to
 */
function validate(element, value, parameters) {

  parameters = parameters || {};

  if (!parameters.from || !parameters.to) {
    throw new Error('Fehlende Parameter: from und to müssen belegt sein.');
  }

  if (!value) {
    return 'Hier muss was rein: ' + element.name;
  }

  if (value && !(value >= parameters.from && value <= parameters.to)) {
    return 'Der Wert muss zwischen ' + parameters.from + ' und ' + parameters.to + ' liegen: ' + element.name;
  }

  return true;
}

// export function
module.exports = {
  validate: validate
};
```

**Element definieren**

```auto
validation: [
  {
    script: 'tstforms.testValidation',
    parameters: {
      from: 1,
      to: 100
    }
  }
]
```

### Validierung außerhalb des Elements

* * *

Sie können die Validierung auf form-Ebene, d. h. außerhalb des jeweiligen Elements, durchführen. Dies kann etwa erfolgen, wenn sich der Wert auf form-Ebene geändert hat. So beachtet das System auch mehrere Elemente bei einer Validierung.

#### Beispiel 1

```auto
form.on('valueChanged', () => {
  //Prüfen, ob textField1 mit einem "a" beginnt
  if (form.value.textField1 && !form.value.textField1.startsWith('a')) {
    //Wenn textField1 nicht mit einem a beginnt, belege textField1 mit einer Fehlermeldung
    form.error = {
      textField1: 'Der Text muss mit einem a beginnen.'
    };
  }
  else {
  // Um die Fehlermeldung wieder zu entfernen, setze form.error zurück
    form.error = {};
  }
});
```

#### Beispiel 2 mit agorum.composite.form.element.list

```auto
.
.

    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      maxItems: 5,
      label: 'Test',
      showAppend: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'locale',
          label: 'Sprache[_<Land>[_<Variante>]]',
          flexible: true,
          validation: [
            {
              required: true
            }
          ]
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'text',
          label: '_agorum.messages.manager.js.messagemanager.filekey.label',
          flexible: true,
          validation: [
            {
              required: true
            }
          ]
        }

      ]
    },

.
.
.
.

form.on('input', input => {
  if (input.name === 'locale') {
    // Prüfen, ob Eingabe okay
    let lookupData = localeHandler.read(input.value, {lookup:true});
    if (lookupData && lookupData[0]) {
      // Wenn okay, dann errorText wieder zurücksetzen
      form.set(['listField', input.index, 'locale', 'error' ], null);
    }
    else {
      // errorText setzen und durch form.validate anzeigen lassen
      form.set(['listField', input.index, 'locale', 'error' ], 'Fehlerhafte Eingabe ...');
      form.validate();
    }
  }
});
```

## agorum.composite.form - Utils

Dies ist eine Sammlung häufig verwendeter Utils aus dem Bereich *form*.

### Übersicht über Utils

* * *

#### alert

Zeigt eine Nachricht an (siehe [agorum.composite - message](#)).

#### alertHtml

Zeigt eine Nachricht im HTML-Format an (siehe [agorum.composite - message](#)).

#### confirm

Zeigt eine Nachricht mit Bestätigungs-Schaltfläche an (siehe [agorum.composite - message](#)).

#### folderPicker

Definiert eine Objektauswahl über Ordner.

* Sie erhalten das Widget des Fensters zurück.
* siehe [Parameter zu „folderPicker“](#folderPicker)

**Beispiel**

```auto
let formUtils = require('/agorum/roi/customers/agorum.composite.form/js/utils/form-utils');

let baseFolder = null;
let folder = null;
let width = 800;
let height = 600;
let selectors = [
  '[isFolder=true]'
];

let widget = formUtils.folderPicker(baseFolder, folder, selected => {
  console.log('selected object', selected);
}, width, height, selectors);
```

#### searchPicker

Definiert eine Objektauswahl über Suche.

* Sie erhalten das Widget des Fensters zurück.
* siehe [Parameter zu „searchPicker“](#searchPicker)

**Beispiel**

```auto
let formUtils = require('/agorum/roi/customers/agorum.composite.form/js/utils/form-utils');

let searchParameters = {
  query: 'hallo',
  additionalBaseQuery: 'isfolder:true',
  filterCollapsed: true,
  settingName: 'inbox-all',
  detailsWidget:  {
    type: 'agorum.composite.details',
    width: 600
  }
};

let width = 800;
let height = 600;
let selectors = [
'[isFolder=true]'
];

let widget = formUtils.searchPicker(searchParameters, selected => {
  console.log('selected object', selected);
}, width, height, selectors);
```

#### Parameter zu „folderPicker“

| Parameter | Beschreibung |
| --- | --- |
| baseFolder | Definiert den Startordner, ab dem der Baum der Ordnerauswahl erscheint. Die Startordner der aktiven smart assistant-Konfiguration gelten, wenn Sie nichts angeben. |
| folder | Öffnet den definierten Ordner. |
| selected | Dient als Callback und übergibt das gewählte agorum core-Objekt als Parameter. |
| width | (optional) Definiert die Breite des Fensters. |
| height | (optional) Definiert die Höhe des Fensters. |
| selectors | Ab welcher Version verfügbar? • agorum core 9.2.3 Definiert Selektoren, um die Auswahl der Objekte einzuschränken. Die Schaltfläche OK aktiviert sich erst, wenn auf jedes der gewählten Objekte mindestens einer dieser Selektoren passt. |

#### Parameter zu „searchPicker“

| Parameter | Beschreibung |
| --- | --- |
| searchParameters | (optional) Steuert eine dahinterliegende information center-Suche. Sie können alle Parameter aus agorum.composite.acic und agorum.composite.search.filterResultDetails verwenden. |
| selected | Dient als Callback und übergibt das gewählte agorum core-Objekt als Parameter. |
| width | (optional) Definiert die Breite des Fensters. |
| height | (optional) Definiert die Höhe des Fensters. |
| selectors | Ab welcher Version verfügbar? • agorum core 9.2.3 Definiert Selektoren, um die Auswahl der Objekte einzuschränken. Die Schaltfläche OK aktiviert sich erst, wenn auf jedes der gewählten Objekte mindestens einer dieser Selektoren passt. |

## agorum.composite.form.basic

Dieses Widget bietet alle Basisfunktionen einer *form*:

* Bearbeitungsmaske
* Ansichtsmaske
* Eingabe/ Werte validieren
* Werte setzen /holen

### Einfaches Beispiel

* * *

Das folgende Beispiel erstellt eine Maske mit zwei Eingabefeldern.

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 300,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Text 1'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField2',
      label: 'Text 2'
    }

  ]
});

form;
```

### Komlexes Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 300,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Text 1'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField2',
      label: 'Text 2'
    }

  ],
  readOnly: false,
  validation: [
    {
      required: true
    }
  ],
  value: {
    textField1: 'Wert 1',
    textField2: 'Wert 2'
  },
  showError: 'always',
  error: {
    textField1: 'Error darstellen für textField1'
  }
});

form;
```

### Parameter

* * *

#### type

Definiert den Typ und lautet immer *agorum.composite.form.basic*.

#### name

Definiert einen eindeutigen Namen für diese *form*.

#### manualConfig

| Wert | Beschreibung |
| --- | --- |
| true | Übernimmt KEINE Form Element-Definitionen aus der Metadaten-Definition, wenn der Name eines Elements mit dem Namen eines definierten Metadatums übereinstimmt. |
| false (Standard) | Übernimmt Form Element-Definitionen aus der Metadaten-Definition, wenn der Name eines Elements mit dem Namen eines definierten Metadatums übereinstimmt. |

Dieser Parameter können Sie auf Element-Ebene definieren.

#### labelWidth

Definiert optional die Breite der jeweiligen Labels der in dieser *form* enthaltenen Elemente.

Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.labelWidth = 150; // Standard: 100
```

#### labelPosition

**Ab welcher Version verfügbar?**• *agorum core* 9.2.3

Definiert die Position des Labels.

Sie können diesen Parameter nachträglich ändern.

| Wert | Beschreibung |
| --- | --- |
| left (Standard) | Das Label ist links vom Feld. |
| top | Das Label ist über dem Feld. |

**Hinweis**: Wenn Sie *labelPosition* auf Element-Ebene definieren möchten, dürfen Sie auf form-Ebene kein *labelPosition* setzen, weil das System *labelPosition* auf Element-Ebene mit der Einstellung der *form* überschreibt.

**Beispiel**

```auto
form.labelPosition = 'top';
```

#### elements

Definiert ein Array von Elementen, die das System in dieser *form* verwendet.

**Beispiel**

Ein Element kann auch nur aus dem Namen eines Metadatums bestehen. Dann ermittelt *agorum.composite.form* automatisch alle Parameter aus der Metadaten-Definition zur korrekten Darstellung des Felds:

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 300,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      name: 'ag_tags'
    },
    {
      name: 'user_ag_tags'
    }

  ]
});

form;
```

Sie können diesen Parameter nachträglich ändern.

```auto
form.elements = [
  {

    name: 'ag_tags'
  }
];
```

#### readOnly

| Wert | Beschreibung |
| --- | --- |
| true | Der Ansichtsmodus erscheint. |
| false (Standard) | Der Bearbeitungsmodus erscheint. |

**Hinweis**: Wenn Sie *readOnly* auf Element-Ebene definieren möchten, dürfen Sie auf form-Ebene kein *readOnly* setzen, weil das System *readOnly* sonst auf Element-Ebene mit der Einstellung der *form* überschreibt.

**Beispiel**

```auto
form.readOnly = true; // Ansichtsmodus einschalten
```

#### validation

Enthält ein Array von [Validierungsdefinitionen](#) für alle Elemente in dieser *form*.

* Die Validierung können Sie auch bei den einzelnen Elementen definieren.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.validation = [
  {

    required: true
  }
];
```

#### value

Definiert eine Map von Werten zum Setzen und Auslesen der Werte der einzelnen Elemente in der *form*.

Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.value = {

  ag_tags: [ 'Tag 1', 'Tag 2' ]
};
```

#### showError

Steuert das Anzeigeverhalten von Fehlermeldungen bei den einzelnen Elementen.

Sie können diesen Parameter nachträglich ändern.

| Wert | Beschreibung |
| --- | --- |
| deferred (Standard) | Zeigt die Fehlermeldung erst, wenn der Benutzer etwas ändert und die Validierung daraufhin fehlschlägt. |
| always | Zeigt die Fehlermeldung sofort an, wenn die Validierung fehlschlägt. |
| never | Zeigt keine Fehlermeldung an. |

**Beispiel**

```auto
form.showError = 'always';
```

#### error

Setzt eigene Fehlermeldungen an die jeweiligen Elemente, etwa wenn ein Skript eine Validierung durchführt.

**Beispiel**

```auto
form.on('valueChanged', () => {
  if (form.value.textField1 && !form.value.textField1.startsWith('a')) {
    form.error = {
      textField1: 'Der Text muss mit einem a beginnen'
    };
  }
  else {
    form.error = {};
  }
});
```

Dieses Beispiel prüft bei Änderung der Werte in der *form*, ob das Feld *textField1* mit einem *a* beginnt. Wenn nicht, setzt das System eine Fehlermeldung auf das Feld.

**Hinweis**: Das Setzen eines errors zeigt nicht sofort einen Fehler an. Dieser verändert lediglich den Parameter *valid*. Soll direkt der Fehler erscheinen, setzen Sie *showError* etwa auf *always*.​​​​​​

#### disabled

Deaktiviert alle Elemente dieser *form*.

* Die Elemente sind noch sichtbar, können aber nicht verwendet werden (ausgegraut).
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.disabled = true;
```

#### valid

| Wert | Beschreibung |
| --- | --- |
| true | Alle Felder sind gültig. |
| false | Ein oder mehrere Felder sind ungültig. |

Verwenden Sie diesen Parameter, um zu prüfen, ob alle Eingaben korrekt sind, bevor ein Benutzer Eingaben in einer Oberfläche speichert.

### Events (on)

* * *

#### focused

Löst aus, wenn das System ein Element der *form* fokussiert.

* Das System übergibt als Parameter ein Objekt, das Informationen zum auslösenden Element enthält.
* Die übergebene Struktur (im Beispiel *info*) ist wie folgt aufgebaut:

```auto
{
  name: 'name des elements',
  path: [  'name-des-haupt-elements', 'weitere untergeordnete', 'name-des-elements' ]
}
```

| Parameter | Beschreibung |
| --- | --- |
| name | Definiert den Namen des ursprünglich auslösenden Elements. |
| path | Definiert den gesamten Pfad zu dem auslösenden Element als Array aus Sicht der form. |

**Beispiel**

```auto
form.on('focused', info => {
  console.log('focused', info);
});
```

**Beispiel bei einem list-element mit der Spalte „col1“**

Das list-element selbst trägt den Namen *list1*:

```auto
{
  name: 'col1',
  index: 0,
  path: [  'list1', 0, 'col1' ]
}
```

In der Liste *list1* wurde die 1te Zeile (0) in der Spalte *col1* fokussiert (selbige Struktur gilt auf für die nachfolgenden Events *blurred* und *action*).

#### blurred

Löst aus, wenn das System ein Element der *form* defokussiert.

* Das System übergibt als Parameter ein Objekt, das Informationen zum auslösenden Element enthält.
* Struktur siehe Parameter [focused](#Focused)

**Beispiel**

```auto
form.on('blurred', info => {
  console.log('blurred', info);
});
```

#### action

Löst aus, wenn ein Benutzer das Element *button* oder *menuItem* der *form* aklickt.

* Das System übergibt als Parameter ein Objekt, das Informationen zum auslösenden Element enthält.
* Struktur siehe Parameter [focused](#Focused)
* Die action-Events folgender Standard-*aguila*\-Widgets lösen ebenfalls das *actionEvent* auf *form*\-Ebene aus, sofern diese sich unterhalb der Elemente befinden und einen Namen besitzen (*agorum.button* oder *agorum.menuItem*).

#### validChanged

Löst aus, wenn eine Eingabe erfolgt und sich dadurch der Status von *valid* ändert.

* Das System übergibt als Parameter den neuen Wert von *valid*.
* *valid* ist dann *true*, wenn alle in der *form* enthaltenen Elemente auch *true* sind und umgekehrt.

#### valueChanged

Löst aus, wenn sich ein oder mehrere Werte der *form*\-Elemente ändern.

* Das System übergibt als Parameter den neuen Wert von *value*.
* *value* enthält eine map, die die Werte aller Elemente der *form* enthält.

#### input

Löst aus, wenn ein Benutzer einen Wert in einem Feld ändert. Dieses Event ist einfacher zu verwenden als [valueChanged](#ValueChanged).

Das System übergibt als Parameter eine Struktur mit den Informationen, was sich geändert hat.

**Beispiel**

Als Parameter übergibt das System diese Struktur:

```auto
{
  value: 'current value',      // aktueller Wert des Felds
  oldValue: 'previous value',  // Wert vor der Änderung
  name: 'name-of-element',     // Name des auslösenden Elements
}
```

Der Inhalt dieser Struktur kann je nach verwendetem Element variieren. Das Element [list](#) gibt hier etwa noch weitere Informationen mit.

#### elementsChanged

Löst aus, wenn sich *elements* ändert.

Das System übergibt den neuen Wert von *elements*, also eine Liste der neuen *elements*.

#### readOnlyChanged

Löst aus, wenn eine Änderung im Bearbeitungs-/ oder Ansichtsmodus stattfindet.

Das System übergibt als Parameter den neuen Wert von *readOnly*.

#### labelWidthChanged

Löst aus, wenn sich der Parameter [labelWidth](#LabelWidth) ändert.

Das System übergibt als Parameter den neuen Wert von *labelWidth*.

#### validationChanged

Löst aus, wenn sich die validation-Definition ändert.

Das System übergibt als Parameter den neuen Wert von *validation*.

#### showErrorChanged

Löst aus, wenn sich der Parameter [showError](#ShowError) ändert.

Das System übergibt als Parameter den neuen Wert von *showError*.

#### errorChanged

Löst aus, wenn sich der Parameter [error](#Error) ändert.

Das System übergibt als Parameter den neuen Wert von *error*.

### Events (fire)

* * *

####  focus

Fokussiert das angegebene Element.

Das System fokussiert das erste Element der *form*, wenn Sie kein Element angeben.

**Beispiel**

```auto
// erstes element
form.fire('focus');

// oder mit element
form.fire('focus', 'name-des-elements');
```

### Funktionen

* * *

#### validate()

Führt eine Validierung aller darunterliegenden Elemente durch, gibt das Ergebnis *true* oder *false* zurück und stellt eventuell aufgetretene Fehler einmalig visuell dar, unabhängig von der aktuell gesetzten Einstellung *showError*.

#### dump

**Ab welcher Version verfügbar?**• *agorum core* 10.1.0

Gibt den internen Zustand aller Elemente innerhalb dieser *form* zurück.

Sie debuggen damit, welche Felder innerhalb der *form* welchen Zustand besitzen, etwa wann welche Felder dazu führen, dass eine *form* nicht valide ist.

**Beispiel**

```auto
console.log(form.dump());
```

## agorum.composite.form.metadataBasic

Dieses Widget basiert auf [agorum.composite.form.basic](#) und erbt davon alle Eigenschaften.

Sie können mithilfe des Widgets:

* die Werte für die einzeln definierten Elemente automatisch laden (über den Parameter [id](#id))
* Metadaten speichern

### Parameter

* * *

Alle Parameter in [agorum.composite.form.basic](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### type

Der type ist immer *agorum.composite.form.metadataBasic*.

#### id

Lädt die Metadaten des dahinterliegenden Objekts und setzt die Werte auf die definierten Elemente der form.

**Beispiel**

```auto
form.id = objects.find('/agorum/roi/Files/Demo').ID;
```

**Werte zurücksetzen**

Um die Werte neu zu laden, setzen Sie den Parameter *id* zurück:

```auto
form.id = null;
form.id = testObject.ID;
```

### Events (on)

* * *

Alle Events in [agorum.composite.form.basic](#) gelten. Zusätzlich gelten die folgenden Events.

#### saved

Löst aus, sobald das Event (fire) [save](#save) abgeschlossen ist.

* Damit steuern Sie etwa den Status von Schaltflächen oder schließen das Fenster.
* Das Event enthält keine Parameter.

#### failed

Löst aus, wenn beim Event (fire) [save](#save) ein Fehler auftritt.

Das System übergibt als Parameter die Fehlermeldung.

#### idChanged

Löst aus, wenn sich der Parameter [id](#id) geändert hat.

Das System übergibt als Parameter die neue Id.

### Events (fire)

* * *

#### save

Speichert die *form* und löst das Event *save* aus.

**Beispiel**

```auto
form.fire('save');
```

### Komplettes Beispiel

* * *

Das folgende Beispiel enthält die komplette Steuerung des Speichervorgangs mit den Schaltflächen *save*, *edit* und *cancel*.

Das System:

* erstellt eine Oberfläche mit den Metadaten *ag\_tags* (globale Tags) und *user\_ag\_tags* (Benutzertags)
* lädt vom Ordner */agorum/roi/Files/Demo* die beiden Metadaten automatisch und speichert diese Metadaten wieder auf den Ordner

```auto
let aguila = require('common/aguila');
let objects = require('common/objects');

// a test folder, to load and save the metadata to
let testObject = objects.find('/agorum/roi/Files/Demo');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.metadataBasic',

  docked: {
    top: {
      type: 'agorum.toolbar',
      border: true,
      items: [
        {
          type: 'agorum.button',
          name: 'save',
          text: 'Save'
        },
        {
          type: 'agorum.button',
          name: 'cancel',
          text: 'Cancel'
        },
        {
          type: 'agorum.button',
          name: 'edit',
          text: 'Edit',
          disabled: true
        }
      ]
    }
  },

  // the metadata, that should be edited
  // all settings are loaded from the metadata definition
  elements: [
    {
      name: 'ag_tags'
    },
    {
      name: 'user_ag_tags'
    }

  ]
});

let saveBtn = form.down('save');
let editBtn = form.down('edit');
let cancelBtn = form.down('cancel');

saveBtn.on('clicked', () => {
  // save
  form.fire('save');

  // set form to view mode
  form.readOnly = true;

  // switch button states

  saveBtn.disabled = true;
  cancelBtn.disabled = true;
  editBtn.disabled = false;
});

cancelBtn.on('clicked', () => {
  // reload original data
  form.id = null;
  form.id = testObject.ID;

  // set form to view mode
  form.readOnly = true;

  // switch button states

  saveBtn.disabled = true;
  cancelBtn.disabled = true;
  editBtn.disabled = false;
});

editBtn.on('clicked', () => {
  // set form to edit mode
  form.readOnly = false;

  // switch button states
  saveBtn.disabled = false;
  cancelBtn.disabled = false;
  editBtn.disabled = true;
});

// load a sample object
form.id = testObject.ID;

form;
```

## agorum.metadata.collection.form

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.8

Mit dieser form verwenden Sie [metadata collections](#) (Sammlungen von Metadaten). Dadurch können Sie mehrere Elemente auf einmal angeben. Die metadata collections können Sie etwa für Rechnungen verwenden.

*agorum.metadata.collection.form* erbt alle [grundlegenden Eigenschaften](#) von *agorum.composite.form.element*.

### Einfaches Beispiel

* * *

Dieses Beispiel zeigt eine Oberfläche, die eine metadata collection verwendet:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/dca7d8e0-4205-11ec-805f-005056aa0ecc)

```auto
OCR: test-md-collection.js (Test), Test string*, Test long*, Test double*, Test boolean*, Rechnungsnumme, test, collection.js, Test, Test, string, Test, long, Test, double, Test, boolean, Rechnungsnumme
```

Einfaches Beispiel

**Skript**

```auto
let aguila = require('common/aguila');

aguila.create({
  type: 'agorum.metadata.collection.form',
  usage: 'form_no_date',
  collection: 'test_metadata_collection_06'
});
```

Die im Beispiel verwendete metadata collection finden Sie unter [Beispiele für die metadata-collection.yml](#).

### Komplexeres Beispiel

* * *

Dieses Beispiel zeigt eine Oberfläche, die weitere forms verwendet:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/1a72a240-4206-11ec-805f-005056aa0ecc)

```auto
OCR: Beispiel_metadata_collection_neu.js (Test), Beschreibung*, Test string*, Test date*, Test long*, Test double*, Test boolean*, Rechnungsnummer*, Rechnungsdatum, Ende, Beispiel_metadata_collection_neu.js, Test, Tragen Sie hier die entsprechenden Werte ein, Beschreibung, Test string, Test date, Test long, Test double, Test boolean, Rechnungsnummer, Rechnungsdatum, Ende
```

Komplexeres Beispiel

**Skript**

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.composite.form.repeater',
  labelPosition: 'top',
  elements:  [
    // form für Anweisung und Beschreibung
    {
      type: 'agorum.composite.form.basic',
      elements: [
        {
          type: 'agorum.textDisplay',
          text: 'Tragen Sie hier die entsprechenden Werte ein:'
        },

        {
          type: 'agorum.composite.form.element.text',
          label: 'Beschreibung',
          name: 'description'
        }
      ]
    },
    // collection form für die Rechnungs-Metadaten
    {
      type: 'agorum.metadata.collection.form',
      usage: 'form',
      collection: 'test_metadata_collection_06'

    },
    // form für Buttons
    {
      type: 'agorum.composite.form.basic',
      elements: [
        {
          type: 'agorum.spacer',
          height: 24
        },
        {
          type: 'agorum.hbox',
          items: [
            {
              type: 'agorum.spacer',
              flexible: true
            },
            {
              type: 'agorum.composite.form.element.button',
              name: 'finish',
              text: 'Ende',
              icon: 'aguila-icon check'
            }
          ]
        }
      ]
    }
  ]
});

widget.on('action', action => {
  console.log('button clicked', action);
});

widget.on('valueChanged', value => {
  console.log('resulting value', value);
});

widget;
```

Die im Beispiel verwendete metadata collection finden Sie unter [Beispiele für die metadata-collection.yml](#).

### Parameter

* * *

#### usage

Definiert die Art der metadata collection (Verwendungszweck).

* Nur eine spezifische Auswahl an Sammlungen steht zur Wahl.
* Sie können die metadata collection durch die Anwendung dieses Parameters erweitern oder einschränken.

Im [einfachen Beispiel](#EinfachesBeispiel) erscheinen etwa durch diesen Parameter die Datumsfelder in der Oberfläche nicht. Im [komplexeren Beispiel](#KomplexeresBeispiel) sind die Datumsfelder hingegen sichtbar.

**Beispiel 1**

```auto
usage: 'form', // die Standardsammlungen stehen zur Auswahl
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/c2316780-c07f-11ec-8945-005056aa0ecc)

```auto
OCR: test-md-collection.js (Test), Typ: Alle Datentypen, Beleg, Bericht, CRM Kollektion, Dokumentvorlage, Rechnung, Test Metadaten Sammlung 06, test-collection.js, Test, Typ, Alle, Datentypen, Beleg, Bericht, CRM, Kollektion, Dokumentvorlage, Rechnung, Test, Metadaten, Sammlung
```

Beispiel 1

**Beispiel 2**

```auto
usage: 'form_no_date', // nur die Sammlung Test Metadaten Sammlung 06 steht zur Auswahl
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/c34ce9a0-c07f-11ec-8945-005056aa0ecc)

```auto
OCR: test-md-collection.js (Test), Typ: Test Metadaten Sammlung 06, test collection.js, Test, Typ, Test, Metadaten, Sammlung
```

Beispiel 2

**Beispiel 3**

```auto
usage: '', // die Standardsammlungen stehen zur Auswahl, wenn Sie keine Angabe machen
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/c4256f50-c07f-11ec-8945-005056aa0ecc)

```auto
OCR: test-md-collection.js (Test), Typ: Alle Datentypen, Beleg, Bericht, CRM Kollektion, Dokumentvorlage, Rechnung, Test Metadaten Sammlung 06, test-collection.js, Test, Typ, Alle, Datentypen, Beleg, Bericht, CRM, Kollektion, Dokumentvorlage, Rechnung, Test, Metadaten, Sammlung
```

Beispiel 3

#### collection

Umgeht die Auswahl der metadata collections, sodass Sie die gewünschte metadata collection direkt angeben können.

Die Felder der metadata collection erscheinen direkt beim Ausführen.

```auto
collection:'test_metadata_collection_06'
```

### Optionale Parameter

* * *

* labelPosition
* labelWidth
* value
* valid
* disabled
* readOnly
* validation

Informationen zu den Parametern siehe [agorum.composite.form - basic](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(e9bbf870-9142-11e9-8702-005056aa0ecc\)&detailsId=e9bbf870-9142-11e9-8702-005056aa0ecc)

### Events

* * *

Alle Events unter [agorum.composite.form - basic](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(e9bbf870-9142-11e9-8702-005056aa0ecc\)&detailsId=e9bbf870-9142-11e9-8702-005056aa0ecc) gelten.

### Funktionen

* * *

#### validate()

Führt eine Validierung aller darunterliegenden Elemente durch und gibt das Ergebnis (true / false) zurück.

* Eventuell aufgetretene Fehler erscheinen einmalig, unabhängig von der aktuell gesetzten Einstellung *showError*.
* Ein Beispiel finden Sie unter [agorum.composite.form - Validierung](#).

## agorum.composite.form.metadataEdit

Dieses Widget:

* bietet eine Bearbeitungsmaske für Metadaten
* kümmert sich um das Validieren, Speichern und Laden der Daten
* bietet Schaltflächen zum Bearbeiten, Speichern und Abbrechen, um etwa Aktendeckel umzusetzen

### Verhalten

* * *

Eine Oberfläche mit den definierten Metadaten erscheint. Abhängig davon, ob die Oberfläche im Bearbeitungs- oder Ansichtsmodus ist (über den Parameter [readOnly](#readOnly)), steuert eine Toolbar die Zustände der Schaltflächen:

| Zustand | Beschreibung |
| --- | --- |
| Bearbeiten | Aktiv, wenn die Oberfläche im Ansichtsmodus ist und der Benutzer Schreibrechte auf das Objekt besitzt. |
| Speichern | Aktiv, wenn die Oberfläche im Bearbeitungsmodus ist. |
| Abbrechen | Aktiv, wenn die Oberfläche im Bearbeitungsmodus ist. |

Ändern sich Daten und klickt ein Benutzer auf *Abbrechen*, so weist das System den Benutzer darauf hin, dass sich Daten geändert haben und fragt, ob er sicher ist, abzubrechen. (Voraussetzung: Die verwendeten Elemente müssen als Metadaten definiert sein.)

### Beispiel

* * *

```auto
let aguila = require('common/aguila');
let objects = require('common/objects');

let form = aguila.create({
  type: 'agorum.composite.form.metadataEdit',
  width: 500,
  height: 500,
  toolbar: 'top',

  buttonsAlignment: 'end',
  readOnly: true,
  elements: [
    {
      name: 'ag_tags'
    },
    {
      name: 'user_ag_tags'
    }

  ]
});

// test
setImmediate(() => {
  form.id = objects.find('/agorum/roi/Files/Demo').ID;
});

form;
```

Dieses Beispiel lädt eine Oberfläche zur Bearbeitung der Metadaten *ag\_tags* und *user\_ag\_tags* auf dem Ordner */agorum/roi/Files/Demo* (Dateien/Demo).

### Parameter

* * *

Alle Parameter in [agorum.composite.form - metadata-basic](#) gelten. Zusätzlichen gelten die folgenden Parameter.

#### type

Der type ist immer *agorum.composite.form.metadataEdit*.

#### toolbar

Definiert, wo die Toolbar mit den Schaltflächen für *Bearbeiten*, *Speichern* und *Abbrechen* erscheint.

Sie können den Parameter nachträglich nicht ändern, er löst somit kein changed-Event aus.

| Wert | Beschreibung |
| --- | --- |
| top (Standard) | Oben am Fenster |
| bottom | Unten am Fenster |
| left | Linker Rand |
| right | Rechter Rand |

#### buttonsAlignment

Definiert, wie die Schaltflächen in der Toolbar ausgerichtet sind.

Sie können den Parameter nachträglich nicht ändern, er löst somit kein changed-Event aus.

| Wert | Beschreibung |
| --- | --- |
| start | Toolbar ist oben / unten = Schaltflächen links angeordnet Toolbar rechts / links = Schaltflächen oben angeordnet |
| end | Toolbar ist oben / unten = Schaltflächen rechts angeordnet Toolbar rechts / links = Schaltflächen unten angeordnet |

#### id

Definiert die ID des Objekts, von dem das System die Metadaten lädt oder speichert.

#### elements

Definiert ein Array von Elementen, die das System in dieser *form* verwendet.

**Beispiel**

```auto
form.elements = [
  {

    name: 'ag_tags'
  }
];
```

#### readOnly

| Wert | Beschreibung |
| --- | --- |
| true | Aktiviert den Ansichtsmodus. |
| false (Standard) | Aktiviert den Bearbeitungsmodus. |

**Beispiel**

```auto
form.readOnly = true;
```

Sie können den Parameter nachträglich ändern.

### Events

* * *

Alle Events in [agorum.composite.form - metadata-basic](#) gelten.

## agorum.composite.form.edit

Dieses Element bietet dieselben Steuerungselemente für Oberflächen wie [metadataEdit](#), mit dem Unterschied, dass Sie das Speichern und Laden selbst implementieren und somit steuern können, was beim Speichern und Laden passiert. Dies ist etwa für Bearbeitungsoberflächen von Objekten geeignet, die nicht auf Metadaten basieren.

Damit können Sie etwa Oberflächen umsetzen, um Benutzer anzulegen oder andere Objekte zu steuern.

### Verhalten

* * *

Das System zeigt eine Oberfläche mit den definierten Metadaten an. Abhängig davon, ob die Oberfläche im Bearbeitungs- oder Ansichtsmodus ist (über den Parameter *readOnly* einstellbar), steuern Sie in einer Toolbar die Zustände der Schaltflächen:

| Zustand | Beschreibung |
| --- | --- |
| Bearbeiten | Aktiv, wenn die Oberfläche im Ansichtsmodus ist und der Benutzer Schreibrechte auf das Objekt besitzt. |
| Speichern | Aktiv, wenn die Oberfläche im Bearbeitungsmodus ist. |
| Abbrechen | Aktiv, wenn die Oberfläche im Bearbeitungsmodus ist. |

Ändert ein Benutzer Daten und klickt auf die Schaltfläche *Abbrechen*, so erhält der Benutzer einen Hinweis, dass sich Daten geändert haben. Er muss dann das Abbrechen nochmals bestätigen.

### Grundgerüst

* * *

Dieses Beispiel zeigt das Grundgerüst für die eigene Bearbeitungsoberfläche. Ein vollständiges Beispiel zur Bearbeitung / Erstellung eines Benutzers finden Sie unter [Beispiel: Benutzer erstellen/ändern](#BenutzerErstellenAendern).

#### Skript zum Grundgerüst

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  type: 'agorum.composite.form.edit',
  properties: [
    'id'
  ],
  width: 500,
  height: 500,
  toolbar: 'top',
  validation: [
    {
      required: true
    }
  ],

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'userName',
      label: 'Name'
    }

  ]
});

form.on('idChanged', () => {
  if (form.id !== null) {
    // load information and set to form.value ...

    // ....
  }

  // tell that the load is finished
  form.fire('loaded');
});

form.on('save', () => {
  // save event, save the data
  // ....

  // tell, that the save has finished
  form.fire('saved');
});

form;
```

### Parameter

* * *

Alle Parameter in [metadataEdit](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### type

Der type ist immer *agorum.composite.form.edit*.

#### value

Setzt die Werte des jeweils definierten Elements *form*.

* Das System übernimmt nur die Werte, für die ein entsprechendes Element existiert.
* Lädt es etwa die Werte über [metadata.load](#), filtert es alle undefinierten Werte raus.

#### id

Definiert die Id als Property, sodass das System über das Event [idChanged](#idChanged) auf die Änderung der *id* hört und dort dann die Lade-Funktion implementiert.

### Events

* * *

Alle Events in [metadataEdit](#) gelten. Zusätzlich gelten die folgenden Events.

#### idChanged

Löst aus, sobald Sie den Parameter [id](#id) setzen. Das eigene Widget reagiert dann und lädt alle notwendigen Daten.

**Beispiel**

```auto
form.on('idChanged', () => {
  if (form.id !== null) {
    // load information and set to form.value ...

    // ....
  }

  // tell that the load is finished
  form.fire('loaded'); // zwingend notwendig
});
```

**Hinweis:** Klickt ein Benutzer auf die Schaltfläche *Bearbeiten*, setzt das System die [id](#id) kurzzeitig auf null und dann wieder auf den ursprünglichen Wert der id, damit die Daten beim Wechsel in den Bearbeitungsmodus neu laden. Das System ruft dabei das Event *idChanged* zweimal auf:

* einmal mit id = null

* einmal mit id = Wert

Wenn Sie bei *id = nul*l etwas verändern und einen fork verwenden, achten Sie auf diesen Umstand des zweimaligen Aufrufens, da sonst Seiteneffekte entstehen und 2 parallele Threads versuchen, die UI-Elemente zu verändern. Das [Beispiel zu idChanged](#idChangedBeispiel) fragt daher explizit ab, ob *id !== null* ist.

#### save

Löst aus, sobald ein Benutzer auf der Oberfläche auf *Speichern* klickt und alle Daten valide sind. Hiermit implementieren Sie das eigene Speichern.

**Beispiel**

```auto
form.on('save', () => {
  // save event, save the data
  // ....

  // tell, that the save has finished
  form.fire('saved'); //zwingend notwendig
});
```

#### canceled

**Ab welcher Version verfügbar?**

• *agorum core* 9.2.3

Löst aus, sobald ein Benutzer auf der Oberfläche auf *Abbrechen* klickt.

Verwenden Sie dieses Event, um das umliegende Fenster zu schließen, wenn es sich um eine Neuanlage handelt.

**Beispiel**

```auto
form.on('canceled', () => {
  if (!form.id) {
    form.form.close();
  }
});
```

### Beispiel: Benutzer erstellen /ändern

* * *

```auto
let aguila = require('common/aguila');
let objects = require('common/objects');

/**
 * sample for creating a custom edit form for a user, simplified, but functional, for demonstrating
 */
let form = aguila.create({
  type: 'agorum.composite.form.edit',
  properties: [
    'id'
  ],
  width: 500,
  height: 500,
  toolbar: 'top',
  readOnly: true,
  validation: [
    {
      required: true
    }
  ],

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'userName',
      label: 'Name'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'givenName',
      label: 'Vorname'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'familyName',
      label: 'Nachname'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'mail',
      label: 'E-Mail',
      validation: [
        {
          regex: '/^.*@.*\\..*',
          errorText: 'E-Mail Adresse falsch'
        }
      ]
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'password',
      label: 'Passwort',
      password: true
    }

  ]
});

let userName = form.down('userName');
let password = form.down('password');

form.on('idChanged', () => {
  if (form.id !== null) {
    // load information

    aguila.fork(() => {
      let user = objects.find(form.id);
      let iup = user.infoUserProfile;

      return {
        userName: user.name,
        givenName: iup.givenName,
        familyName: iup.familyName,
        mail: user.emailAddresses ? user.emailAddresses.join(';') : ''
      };
    }).then(data => {
      // set values to the form
      form.value = data;

      // tell, that load has finished
      form.fire('loaded');
    });
  }
  else {
    // tell, that load has finished
    form.fire('loaded');
  }

  prepareForm();
});

function prepareForm() {
  if (form.id) {
    // id, so in update mode, password is optional
    password.validation = [
      {
        required: false
      }
    ];
  }
  else {
    // no id, so in create mode, password is require
    password.validation = [
      {
        required: true
      }
    ];
    form.readOnly = false;
  }
}

// Ab agorum core 9.2.3
form.on('canceled', () => {
  // close form, on abort, when no ID is given
  if (!form.id) {
    form.form.close();
  }
});

form.on('save', () => {
  aguila.fork(() => {
    if (form.id !== null) {
      // update
      let otherUser = objects.tryFind('user:' + form.value.userName);
      if (otherUser && otherUser.ID !== form.id) {
        throw new Error('Es existiert bereits ein anderer Benutzer mit demselben Namen');
      }

      let data = {
        name: form.value.userName,
        password: form.value.password,
        admin: false,
        givenName: form.value.givenName,
        familyName: form.value.familyName,
        language: 'de',
        emailAddresses: form.value.mail.split(';').map(v => v.trim())
      };

      // filter out, values, that are not set, cause update of user, does not like empty values
      for (let k in data) {
        if (data[k] === null || data[k] === undefined) delete data[k];
      }

      let user = objects.update('user', objects.find(form.id), data);

      return user.ID;
    }
    else {
      // create
      if (objects.tryFind('user:' + form.value.userName)) {
        throw new Error('user ist bereits vorhanden');
      }

      let user = objects.create('user', {
        name: form.value.userName,
        password: form.value.password,
        path: '',
        admin: false,
        givenName: form.value.givenName,
        familyName: form.value.familyName,
        language: 'de',
        emailAddresses: form.value.mail.split(';').map(v => v.trim())
      });

      return user.ID;
    }
  }).then(id => {
    // set the id to the form (for newly created user)
    form.id = id;

    // tell, that the save has finished
    form.fire('saved');
  }).catch(err => {
    // something went wrong, tell that the save has failed
    form.fire('failed', '' + err);

    // throw the error further for displaying
    throw err;
  });
});

setImmediate(() => {
  // test: load data of demo user, if a new user should be created, just comment out the next line.

  form.id = objects.find('user:demo').ID;

  prepareForm();
});

form;
```

## agorum.composite.form.element - Grundlegende Eigenschaften

Eine *form* besteht aus Elementen. Dies sind die jeweiligen Eingabe-/ Ansichtselemente der Oberfläche. Verschiedene Typen existieren, etwa Text, Auswahlbox, Datum.

All diese Elemente haben gemeinsame Grundeigenschaften.

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 300,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Text 1',
      readOnly: null,
      value: 'Wert 1',
      placeholder: 'Bitte einen Text eingeben',
      error: 'Eine Fehlermeldung',
      validation: [
        {
          required: true
        }
      ]
    }

  ]
});

form;
```

### Parameter

* * *

#### type

Definiert den Typ des Elements, etwa *agorum.composite.form.element.text*.

Das System wählt automatisch das Text-Element, wenn Sie keinen *type* definieren.

#### name

Definiert den eindeutigen Namen des Elements.

* Das System ermittelt den Typ anhand der Metadaten-Definition, wenn *name* ein bekanntes Metadatum ist.
* Die jeweiligen Metadaten-Definitionen können Sie in der Element-Definition überschreiben.
* Setzen Sie *manualConfig=true*, wenn Sie dieses Verhalten für dieses Element komplett deaktivieren möchten.

#### manualConfig

Verhindert, dass das System Form-Element-Definitionen aus der Metadaten-Definition übernimmt, wenn der Name eines Elements mit dem Namen eines definierten Metadatums übereinstimmt.

Setzen Sie dazu *manualConfig=true* (Standard: false).

#### label

Definiert den Text / das Label vor dem Element*.*

**Beispiel**

```auto
form.down('textField1').label = 'Neues Label';
```

Sie können diesen Wert nachträglich ändern.

#### labelWidth

Definiert die Breite des Labels vor dem Element (Standard: 100).

Sie können diesen Wert nachträglich ändern.

**Beispiel**

```auto
form.down('textField1').labelWidth = 150;
```

#### labelPosition

**Ab welcher Version verfügbar?**• *agorum core* 9.2.3

| Wert | Beschreibung |
| --- | --- |
| left (Standard) | Das Label erscheint links vom Feld. |
| top | Das Label erscheint über dem Feld. |

**Hinweis**: Auf einer umliegenden *form* darf keine labelPosition-Definition vorhanden sein, wenn Sie die *labelPosition* auf Element-Ebene direkt definieren möchten.

**Beispiel**

```auto
form.down('textField1').labelPosition = 'top';
```

Sie können diesen Wert nachträglich ändern.

#### fieldBorder

**Ab welcher Version verfügbar?**• *agorum core* 9.2.3

Definiert den border-Parameter innerhalb eines Elements.

* Sie können so etwa die border eines html-Elements innen deaktivieren, aber außen (border-Parameter) beibehalten.
* Sie können diesen Wert nachträglich ändern.

**Beispiel**

```auto
form.down('textField1').fieldBorder = false;
```

#### readOnly

| Wert |  Beschreibung |
| --- | --- |
| false (Standard) | Das System steuert den Bearbeitungs- oder Ansichtsmodus über die umliegende form. Das Element befindet sich im Bearbeitungsmodus, wenn keine form existiert. |
| true | Das Element ist immer im Ansichtsmodus, unabhängig vom Zustand der umliegenden form. |

**Beispiel**

```auto
form.down('textField1').readOnly = true;
```

Sie können diesen Wert nachträglich ändern.

#### value

Definiert den vorbelegten Wert des Elements.

* Das System überschreibt den hier definierten Wert, wenn Sie einen Wert über die *form* setzen.
* Sie können diesen Parameter über die umliegende *form* setzen (siehe [Werte setzen](#) und [Werte lesen](#)).
* Sie können diesen Wert nachträglich ändern.

**Beispiel**

```auto
form.down('textField1').value = 'Neuer Wert';
```

#### placeholder

Definiert einen Platzhalter-Text, wenn das Element leer ist.

Sie können diesen Wert nachträglich ändern.

**Beispiel**

```auto
form.down('textField1').placeholder = 'Neuer placeholder';
```

#### error

Definiert eine Fehlermeldung auf dem Element.

* Sie können eine solche Fehlermeldung etwa bei einer Prüfung über JavaScript, etwa bei [valueChanged](#valueChanged) setzen, wenn die Standard-Validierungen nicht ausreichen.
* Sie können diesen Parameter über die umliegende *form* setzen (siehe [Werte setzen](#) und [Werte lesen](#)).

**Hinweise**:

* Das Setzen eines errors zeigt nicht sofort einen Fehler an. Der error verändert lediglich den Parameter *valid*.

* Setzen Sie etwa *showError = 'always'*, wenn der Fehler direkt erscheinen soll.

**Beispiel**

```auto
form.down('textField1').error = 'Neue Fehlermeldung';
```

Sie können diesen Wert nachträglich ändern.

#### showError

Steuert das Anzeigeverhalten von Fehlermeldungen des Elements.

Sie können diesen Parameter über die umliegende *form* setzen (siehe [Werte setzen](#) und [Werte lesen](#)).

| Wert | Beschreibung |
| --- | --- |
| deferred (Standard) | Zeigt die Fehlermeldung erst, wenn der Benutzer etwas ändert und die Validierung daraufhin fehlschlägt. |
| always | Zeigt die Fehlermeldung sofort an, wenn die Validierung fehlschlägt. |
| never | Zeigt keine Fehlermeldungen an. |

#### validation

Definiert die Validierung für dieses Element.

* Im Sonderfall von *required* hat die Definition auf dem Element selbst Vorrang gegenüber der validation-Definition auf der *form* (siehe [agorum.composite.form - Validierung](#)).
* Sie können diesen Parameter über die umliegende *form* setzen (siehe [Werte setzen](#) und [Werte lesen](#)).
* Sie können diesen Wert nachträglich ändern.

**Beispiel**

```auto
form.down('textField1').validation = [
  {
    required: false
  }
];
```

#### disabled

| Wert | Beschreibung |
| --- | --- |
| true | Deaktiviert das Element. Das Element ist sichtbar, aber ausgegraut. Der Benutzer kann es nicht verwenden. |
| false (Standard) | Aktiviert das Element, sodass der Benutzer es verwenden kann. |

**Beispiel**

```auto
form.down('textField1').disabled = true;
```

Sie können diesen Wert nachträglich ändern.

#### valid

Ermittelt, ob die eingestellten Validierungen auf dem Element korrekt sind.

* Wenn das System innerhalb des Events [valueChanged](#valueChanged) auf *valid* geprüft wird, so kann es sein, dass *valid* noch nicht korrekt ist, da intern die Validierung noch nicht erfolgt ist.
* Verwenden Sie die Funktion *setImmediate*, um den Code am Ende der Verarbeitungskette auszuführen.

**Beispiel**

```auto
form.on('valueChanged', () => {
  console.log('Valid ggf. noch falsch: ' + form.valid);
  setImmediate(() => {
      console.log('Valid ist jetzt korrekt: ' + form.valid);
  });
});
```

### Funktionen

* * *

#### set

**Ab welcher Version verfügbar?**• *agorum core* 9.3.0

Setzt Parameter und Werte direkt (siehe [set](#)).

**Beispiel**

```auto
// Beispiel einen Wert setzen
form.set('textField1.value', 'Ein Wert');

// Beispiel Feld disablen
form.set('textField1.disabled', true);
```

#### get

**Ab welcher Version verfügbar?**• *agorum core* 9.3.0

Liest Parameter und Werte direkt aus (siehe [get](#)).

**Beispiel**

```auto
// Beispiel einen Wert lesen
let value = form.get('textField1.value');

// Beispiel Feld disabled Status lesen
let disabled = form.get('textField1.disabled');
```

### Events (on)

* * *

#### labelChanged

Ändert den Parameter [label](#label).

Das System übergibt als Parameter den neuen Wert von *label*.

#### labelWidthChanged

Ändert den Parameter [labelWidth](#labelWidth).

Das System übergibt als Parameter den neuen Wert von *labelWidth*.

#### validChanged

Löst aus, wenn eine Eingabe erfolgt und sich dadurch der Status von [valid](#valid) ändert.

Das System übergibt als Parameter den neuen Wert von *valid*.

#### valueChanged

Löst aus, wenn sich ein oder mehrere Werte der Form-Elemente ändern.

Das System übergibt als Parameter den neuen Wert von [value](#value).

**Tipp**: Verwenden Sie das Event [input](#input), wenn Sie ausschließlich auf Änderungen von Benutzereingaben reagieren möchten.

#### readOnlyChanged

Ändert den Bearbeitungs-/Ansichtsmodus.

Das System übergibt als Parameter den neuen Wert von [readOnly](#readOnly).

#### validationChanged

Ändert die validation-Definition.

Das System übergibt als Parameter den neuen Wert von [validation](#validation).

#### showErrorChanged

Ändert den Parameter [showError](#showError).

Das System übergibt als Parameter den neuen Wert von *showError*.

#### errorChanged

Ändert den Parameter [error](#error).

Das System übergibt als Parameter den neuen Wert von *error*.

#### placeholderChanged

Ändert den Parameter [placeholder](#placeholder).

Das System übergibt als Parameter den neuen Wert von *placeholder*.

#### input

Löst aus, wenn ein Benutzer einen Wert in einem Feld ändert.

* Das Event ist einfacher zu verwenden als [valueChanged](#valueChanged).
* Der Parameter *data* enthält folgende Informationen:

| Wert | Beschreibung | Beispiel |
| --- | --- | --- |
| path | Definiert den Pfad des Elements als Array, in der eine Änderung stattgefunden hat. | Inhalt von path bei einem Texfeld \[ 'nameDesElements' \] (aus Sicht der form) Beispiel bei Listen \[ 'nameDerListe', row, 'column' \], also zum Beispiel: \[ 'listField1', 0, 'column1' \] Sie erhalten hier genaue Information darüber, wo die Eingabe des Benutzers stattgefunden hat. Allgemeines Beispiel form.on('input', data => { let path = data.path; let value = data.value; let oldValue = data.oldValue; let name = data.name; }); |

### Events (fire)

* * *

#### focus

Fokussiert das Element.

**Beispiel**

```auto
form.down('textField1').fire('focus');
```

## agorum.composite.form.element.boolean

Dieses Element stellt eine Checkbox dar und zeigt im Textmodus den Wert *Ja* oder *Nein* an.

*agorum.composite.form.element.boolean* erbt alle Grundeigenschaften von [element](#).

### Beispiel

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/155ba310-18e1-11ef-b4fe-005056aa0ecc)

```auto
OCR: Checkbox 1: Text hinter der Checkbox, Checkbox 2: Text hinter der Checkbox, Checkbox: Text hinter der Checkbox, Checkbox: Text hinter der Checkbox
```

Checkbox-Beispiele

#### Skript zur Oberfläche

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      type: 'agorum.composite.form.element.boolean',
      name: 'checkBox1',
      label: 'Checkbox 1',
      value: true,
      text: 'Text hinter der Checkbox',
    },
    {
      type: 'agorum.composite.form.element.boolean',
      name: 'checkBox2',
      label: 'Checkbox 2',
      value: false,
      text: 'Text hinter der Checkbox',
    },
  ],
});

form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### value

| Wert | Beschreibung |
| --- | --- |
| true | Angehakt |
| false | Nicht angehakt |

Wenn *validation.required = true* ist und die Checkbox ist nicht angehakt, ist automatisch *valid=false*. Die Box erscheint dann rot markiert.

```auto
{
      type: 'agorum.composite.form.element.boolean',
      name: 'checkBox3',
      label: 'Checkbox 3',
      value: false,
      text: 'Text hinter der Checkbox',
      validation: [
        {
          required: true,
        },
      ],
    },
```

#### text

Definiert den Text hinter der Checkbox.

* Sie können den Parameter nachträglich ändern.
* Der Text erscheint nur im Bearbeitungsmodus.

**Beispiel**

```auto
form.down('checkBox1').text = 'Neuer Text';
```

### Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gelten die folgenden Events.

#### textChanged

Löst aus, wenn sich der Parameter [text](#Text) ändert.

Das System übergibt als Parameter den neuen Wert von *text*.

## agorum.composite.form.element.button

Dieses Element stellt eine Schaltfläche dar und löst ein action-Event aus.

* Die Schaltfläche erscheint nur im Bearbeitungsmodus.
* Bei *readOnly=true* erscheint die Schaltfläche NICHT.

*agorum.composite.form.element.button* erbt alle Grundeigenschaften von [element](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      type: 'agorum.composite.form.element.button',
      name: 'button1',
      text: 'Ein Button',
      label: 'Ein label'

    }
  ]
});

form.on('action', data => {
  console.log('action - name des Buttons:', data.name);
  console.log('action - data:',             data);
});

form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### label

Definiert das Label der Schaltfläche.

Sie können den Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('button1').label = 'Neues label';
```

#### text

Definiert den Text der Schaltfläche.

Sie können den Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('button1').text = 'Neuer Text';
```

#### icon

Definiert das Icon der Schaltfläche.

Sie können den Parameter nachträglich ändern.

**Beispiel mit Standard-Icon**

```auto
form.down('button1').icon = 'aguila-icon ac_unit';
```

**Beispiel mit erstelltem Icon**

Über die Aktion [Icon erstellen](#) können Sie eigene Icons definieren. Diese können Sie ebenfalls hier verwenden:

```auto
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');
// ...
form.down('button1').icon = icons.cls('agorum:agorum-logo;color=#0069b5');
```

#### readOnlyHidden

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Schaltfläche aus, sofern Sie den readOnly-Modus gesetzt haben. |
| false | Blendet die Schaltfläche ein. |

Für Schaltflächen gedacht, die den Wert eines Formulars ändern, etwa eine Schaltfläche, die den Wert eines anderen Felds zurücksetzt.

### Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gelten die folgenden Events.

#### action

Löst aus, wenn ein Benutzer die Schaltfläche anklickt.

* Verwenden Sie die Schaltfläche innerhalb einer *form*, so löst auf Ebene der *form* ebenfalls ein [action](#)\-Event aus.
* Das System übergibt dann als Parameter den Namen der Schaltfläche.

**Beispiel**

```auto
form.on('action', data => {
  console.log('action - name des Buttons', data.name);
});
```

## agorum.composite.form.element.date

Dieses Element stellt ein Eingabefeld für Datum / Uhrzeit dar.

*agorum.composite.form.element.date* erbt alle Grundeigenschaften von [element](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      type: 'agorum.composite.form.element.date',
      name: 'dateField1',
      label: 'Datum 1',
      value: new Date()
    },
    {
      type: 'agorum.composite.form.element.date',
      name: 'dateField2',
      label: 'Datum 2',
      precision: 'minute',
      value: new Date()
    },
    {
      type: 'agorum.composite.form.element.date',
      name: 'dateField3',
      label: 'Datum 3',
      value: new Date(),
      format: 'de|dd. MMMM yyyy',
      readOnly: true
    },

    {

      type: 'agorum.composite.form.element.date',
      name: 'dateField4',
      label: 'Datum 4',
      value: new Date(),
      format: 'de|dd. MMMM yyyy HH:mm',
      precision: 'minute',

      readOnly: true
    }
  ]
});

form;
```

### Parameter

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### value

Übergibt ein Date-Objekt und gibt es gleichzeitig zurück.

**Beispiel**

```auto
form.down('dateField1').value = new Date();
```

#### precision

Definiert die Art der Eingabe und Anzeige.

* Sie können diesen Parameter nachträglich ändern.
* *precision* kontrolliert, wie das Datum als Wert zur Verfügung steht.

**Mögliche Werte für „precision“**

| Wert | Beschreibung |
| --- | --- |
| day (Default) | Zeigt ein eingegebenes Datum an. Das System stellt die Stunde auf 12 und die Minute, Sekunde und Millisekunde auf 0, da bei der Angabe eines reinen Datums das System davon ausgeht, dass das Datum in jeder Zeitzone gleichermaßen gilt. |
| hour | Zeigt ein eingegebenes Datum + Stunde an. Das System stellt die Minuten, Sekunden und Millisekunden automatisch auf 0. |
| minute | Zeigt ein eingegebenes Datum + Stunde + Minute an. |
| second | Zeigt ein eingegebenes Datum + Stunde + Minute + Sekunde an. |
| millisecond | Zeigt ein eingegebenes Datum + Stunde + Minute + Sekunde + Millisekunde an. |

**Beispiel**

```auto
form.down('dateField1').precision = 'minute';
```

#### format

Übergibt für die Anzeige ein eigen definiertes Format.

* Sie können diesen Parameter nachträglich ändern.
* Die Anzeige orientiert sich automatisch am Parameter *precision* und an der Sprache des Benutzers, wenn Sie kein Format definieren.
* Im Standard verwendet das System für die Formatierung die Sprache des Benutzers.
* Sie können die Sprache überschreiben, indem Sie die Sprache vor das Format stellen und mit | trennen:

```auto
de|dd. MMMM yyyy
```

**Beispiel**

```auto
form.down('dateField1').format = 'dd.MM.yyyy';
```

**Weitere Formate**

* dd.MM.yyyy (01.01.2019)
* de|dd. MMMM yyyy (01. Januar 2019) – *de* steht für deutsche Ausgabe.
* dd.MM.yyyy HH:mm:ss (01.01.2019 12:50:00)

Informationen zu dieser Formatierung siehe [https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)

### Events

* * *

Alle Events in [element](#) gelten.

#### precisionChanged

Löst aus, wenn sich der Parameter [precision](#Precision) ändert.

Als Parameter übergibt das System die neue *precision*.

#### formatChanged

Löst aus, wenn sich der Parameter [format](#Format) ändert.

Als Parameter übergibt das System das neue *format*.

## agorum.composite.form.element.emailAddress

Dieses Element dient der Eingabe und Auswahl von [E-Mail-Adressen](#). Sie können es über Parameter in Verhalten und Darstellung anpassen. Außerdem bietet es eine Validierung der eingetragene()n E-Mail-Adresse(n) an. Diese Validierung können Sie nicht abstellen oder ändern, Sie können die Validierung aber um eigene Validierungen erweitern.

*agorum.composite.form.element.emailAddress* erbt alle Grundeigenschaften von [element](#).

### Verwendung

* * *

```auto
let aguila = require('common/aguila');
let widget = aguila.create({
  type: 'agorum.composite.form.basic',
  width: 400,
  elements: [
    {
      type: 'agorum.composite.form.element.emailAddress',
      label: 'E-Mail Adresse',
      name: 'email',
      addressType: 'recipient',
      value: ['roi@agorumcore.com', 'demo@agorumcore.com']
    }
  ]
});
widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/2dc64310-79f1-11ec-bb53-005056aa0ecc)

```auto
OCR: E-Mail Adresse: roi@agorumcore.com, demo@agorumcore.com
```

Beispiel einer grafischen Oberfläche

### Parameter

* * *

#### dataSource

Erwartet einen MetaDb-Pfad als String zu der gewünschten *dataSource,* die das System für die Auswahl von E-Mail-Adressen verwendet.

* Verwenden Sie diesen Parameter, wenn die Datenquelle bereits bekannt ist und Sie sie nicht dynamisch zusammenstellen, etwa beim Einsatz einer CSV-Datei oder dem Zugriff auf externe Datenbanken und Systeme.
* Sie müssen keinen Lookup implementieren, da das Element mit der Einstellung *textIsValue* arbeitet.
* Die *dataSource* muss den gleichen Wert für *text* und *value* zur Verfügung stellen.

**Beispiel**

```auto
form.down('email').dataSource = 'MAIN_MODULE_MANAGEMENT/....';
```

#### data

Erwartet ein Array aus Objektdefinitionen als Datenbasis für die Auswahl der E-Mail-Adresse in diesem Element.

* Das Array besteht aus einer Objektdefinition mit den Keys *text* und *value*.
* Die Werte für *text* und *value* müssen jeweils gleich sein, da das Element so eingestellt ist, dass *textIsValue* eingeschaltet ist (siehe [Beispiele](#dataBeispiele)).

**Beispiele**

```auto
let data = [
  {
    value: 'name@domain.de',
    text: 'name@domain.de'
  },
  {
    value: 'name2@domain.de',
    text: 'name2@domain.de'
  }
];
```

```auto
form.down('email').data = [
  {
    value: 'name@domain.de',
    text: 'name@domain.de'
  },
  {
    value: 'name2@domain.de',
    text: 'name2@domain.de'
  }
];
```

#### addressType

Steuert das Verhalten des Elements.

**Parameter**

Sie können dem Parameter diese Werte als String übergeben:

| Parameter | Beschreibung |
| --- | --- |
| Keinen Wert / Parameter nicht angegeben | Das Element stellt sich als einfaches Eingabefeld dar.  Wählen Sie diesen Wert, wenn das System eine E-Mail-Adresse abfragen soll. In das Eingabefeld kann der Benutzer jede E-Mail-Adresse eintragen. |
| recipient | Das Element stellt sich als Mehrfachauswahl dar. Wählen Sie diesen Wert, wenn das System eine Auswahl an E-Mail-Adressen anbieten soll. In die Mehrfachauswahl kann der Benutzer mehrere E-Mail-Adressen eintragen oder aus verfügbaren E-Mail-Adressen in agorum core wählen. |
| sender | Das Element stellt sich als Einfachauswahl dar. Wählen Sie diesen Wert, wenn das System eine Auswahl an E-Mail-Adressen des Benutzers anbieten soll. In die Einfachauswahl kann der Benutzer jede E-Mail-Adresse eintragen oder aus seinen E-Mail-Adressen wählen, die in seinem Benutzer definiert sind. |

**Beispiel**

```auto
form.down('email').addressType = 'sender';
```

#### multi

Steuert bei der Definition einer eigenen *dataSource* oder einer eigenen *data*\-Struktur, ob das Element eine Mehrfach- oder eine Einfachauswahl zur Verfügung stellt.

* Wenn Sie weder *data* noch *dataSource* definieren, so entsteht ein leeres Multi-Auswahlfeld ohne Datenquelle. Ein Benutzer kann dann E-Mail-Adressen eingeben. Bei allen anderen Parametern gibt das Element die Darstellung selbst vor.
* Im Standard steht der Wert auf *false*.
* Sie können den Parameter nachträglich ändern:

```auto
form.down('email').multi = true;
```

**Beispiel**

```auto
{
  data: [
    {
      value: 'entry-1',
      text: 'Eintrag 1'
    },
    {
      value: 'entry-2',
      text: 'Eintrag 2'
    }
  ],
  multi: true
}
```

#### restricted

**Ab welcher Version verfügbar?**• *agorum core* 10.0.10

| Wert | Beschreibung |
| --- | --- |
| true | Beschränkt die Eingabe auf die Werte der jeweiligen Datenquelle. |
| false (Standard) | Beschränkt die Eingabe nicht auf die Werte der jeweiligen Datenquelle. |

**Beispiel**

```auto
restricted: true
```

### Events

* * *

Bis auf die Changed-Events existieren keine weiteren Events.

## agorum.composite.form.element.grid

Dieses Element dient zur Darstellung von Werten und Eingabefeldern in nach Spalten angeordneten Listen. Sie können damit:

* jede andere Art von Element innerhalb der Liste verwenden
* Benutzeraktionen für Positionen der Liste festlegen, damit Benutzer die Positionen bearbeiten, verschieben, duplizieren oder löschen können
* beliebig lange Listen mit Scrollbalken darstellen

*agorum.composite.form.element.grid* erbt alle Grundeigenschaften von [element](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#/14e22220-e915-11e9-a3bc-005056aa0ecc/59fc0790-abdf-11ee-ab59-005056aa0ecc).

### Unterschiede zwischen list und grid

* * *

Die beiden Möglichkeiten zur Oberflächengestaltung, `agorum.composite.form.element.grid` und `agorum.composite.form.element.list`, unterscheiden sich darin, wie Benutzer die Informationen anzeigen lassen und bearbeiten können.

| Verhalten | agorumcomposite.form.element.list | agorum.composite.form.element.grid |
| --- | --- | --- |
| Anzeige von vielen Posten | limitierte Anzeige von Posten auf einer Seite, Blättern auf andere Seiten | Anzeige weiterer Werte durch Scrollen |
| Spaltenanzeige | feste Spaltenanzeige aller Spalten | auswählbare Spaltenanzeige, beschränkt auf angezeigte Spalten |
| Bearbeitung der editierbaren Felder | Bearbeitung in der Listenansicht | Bearbeitung in der Anzeige eines Postens, der durch Doppelklicken ausgewählt wird (Detailansicht) |
| Anzeige von Validierungshinweisen | Anzeige in der Listenansicht bei der Bearbeitung, keine Anzeige für die gesamte Liste | Anzeige in der Detailansicht bei der Bearbeitung, Hervorhebung in der Listenansicht bei fehlerhaften Einträgen |

**Tipp:** Sie können *list* meistens einfach durch *grid* ersetzen. Nur Parameter und Funktionen, die sich auf das Seitenblättern und das direkte Bearbeiten in der Listenansicht beziehen, sind bei *grid* nicht verfügbar.

### Beispiel einer Oberfläche

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/6da08be0-0887-11ef-916e-005056aa0ecc)

```auto
OCR: Test,Spalte,Spalte,Spalte,Spalte,Spalte,Spalte,Spalte,Value1_0,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_1,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_2,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_3,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_4,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_5,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_6,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_7,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_8,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_9,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_10,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Value1_11,02.05.2024,Wert,Das,ist,ein,Beispieltext,20.520,24,Volunt,Destin,Deianielbout,20.520.21
```

Beispiel einer Oberfläche

Ein Doppelklick auf eine Position (Zeile) öffnet folgende Ansicht:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/5e607950-0888-11ef-916e-005056aa0ecc)

```auto
OCR: Test, Spalte, Spalte, Spalte, Spalte, Spalte, Spalte, Value1_0, bitte, 02.05.2024, Wert, Das, ist, ein, Beispieltext, Spalte, Spalte, Spalte, 1-1, von, 20520,24
```

Detailansicht einer Position

Ein fehlerhafter Eintrag wird wie folgt in der Detailansicht angezeigt, in diesem Beispiel nach Herauslöschen des erforderlichen Texts in Spalte 1:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/ae8e5960-0bb7-11ef-85c8-005056aa0ecc)

```auto
OCR: Test, Spalte, Spalte, Spalte, Spalte, bitte, 06.05.2024, von, Spalte, Wert, Spalte, Das ist ein Beispieltext, Spalte, Spalte, Spalte, 20520,24
```

Anzeige eines fehlerhaften Eintrags in der Detailansicht

Ein fehlerhafter Eintrag wird wie folgt in der Listenansicht angezeigt, in diesem Beispiel nach Herauslöschen des erforderlichen Texts in Spalte 1 in der Detailansicht:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/ae7ea1f0-0bb7-11ef-85c8-005056aa0ecc)

```auto
OCR: 06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,06.05.2024,Wert,Das ist ein Beispieltext,20.520,24,05.05.2004,Wort,Das ist ein Raienialtout,30.530
```

Anzeige eines fehlerhaften Eintrags in der Listenansicht

#### Skript zur Oberfläche

```auto
let aguila = require('common/aguila');

// fill test values
let testValue = [];
for (let i = 0; i < 100; i++) {
  testValue.push({
    col1: {
      type: 'custom',
      value: 'Value1_' + i,
      hidden: false,
    },
    user_ag_tags: null,
    col2: null,
    col3: {
      type: 'custom',
      value: new Date(),
    },
    col4: 'value1',
    col5: 'Das ist ein Beispieltext.',
    col6: {
      type: 'custom',
      icon: 'aguila-icon local_airport',
    },
    col7: {
      type: 'custom',
      value: '+',
    },
    col8: {
      type: 'custom',
      value: 20520.24,
    },
  });
}

let form = aguila.create({
  width: 1200,
  height: 600,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.grid',
      name: 'listField',
      // showError: 'always',
      // readOnly: true,
      label: 'Test',
      // showAppend: true,
      // showRowDelete: true,
      // showRowMove: true,
      // hideHeader: true,
      // tableWidth: 2000,

      // general actions

      actions: {
        duplicate: true,
        setColumnValues: true,
      },
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Spalte 1',
          flexible: true,
          hidden: false,
          width: 100,

          actions: {
            setColumnValues: false,
          },

          validation: [
            {
              required: true,
            },
          ],
        },
        {
          // use of metadata
          type: 'agorum.composite.form.element.text',
          name: 'user_ag_tags',
          label: 'Spalte 2',
          width: 100,
        },
        {
          // boolean sample
          type: 'agorum.composite.form.element.boolean',
          name: 'col2',
          label: 'Spalte 3',
          width: 100,
          text: 'Ja, bitte',
          readOnlyHidden: true,
        },
        {
         // date sample
          type: 'agorum.composite.form.element.date',
          name: 'col3',
          label: 'Spalte 4',
          width: 134,
        },
        {
         // select sample
          type: 'agorum.composite.form.element.select',
          name: 'col4',
          label: 'Spalte 5',
          restricted: true,
          data: [
            {
              value: 'value1',
              text: 'Wert 1',
            },
            {
              value: 'value2',
              text: 'Wert 2',
            },
            {
              value: 'value3',
              text: 'Wert 3',
            },
            {
              value: 'value4',
              text: 'Wert 4',
            },
          ],
          width: 134,
        },
        {
         // textDisplay sample
          type: 'agorum.textDisplay',
          name: 'col5',
          label: 'Spalte 6',
          width: 200,
          required: true,
        },
        {
         // button with icon sample
          type: 'agorum.composite.form.element.button',
          name: 'col6',
          label: 'Spalte 7',
          icon: 'aguila-icon drive_eta',
          width: 54,
        },
        {
         // button with text sample
          type: 'agorum.composite.form.element.button',
          name: 'col7',
          label: 'Spalte 8',
          value: 'Y',
          readOnlyHidden: true,
          width: 54,
        },
        {
          // number sample
          type: 'agorum.composite.form.element.number',
          name: 'col8',
          label: 'Spalte 9',
          width: 104,
          format: ',000.00',
          calculator: true,
        },
      ],
      value: testValue,
    },
  ],
});

form
  .down('listField')
  .on('action', data => {
    console.log('action', data);
  })
  .on('itemDeleted', data => {
    console.log('deleted', data);
  })
  .on('itemMoved', data => {
    console.log('moved', data);
  });

form;
```

### grid Parameter

* * *

Zusätzlich zu den Parametern von [element](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#/14e22220-e915-11e9-a3bc-005056aa0ecc/59fc0790-abdf-11ee-ab59-005056aa0ecc) können Sie folgende Parameter verwenden:

| Parameter | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| actions | Definiert Aktionen auf Zeilenebene, die ein Benutzer im Kontextmenü ausführen kann. Die Aktionen können global für grid angegeben werden oder auf template-Ebene pro Spalte. | Siehe actions Parameter |
| compactHeader | Stellt den Header in der Detailansicht in einer kompakten Form dar. Nur die Symbole für Vor und Zurück sowie die Anzeige der angezeigten Elemente auf der rechten Seite existieren, um Platz zu sparen. | Boolescher Wert, Standardwert: false |
| OCR: Test, Spalte, Spalte, Spalte, Spalte, Spalte, Spalte, Spalte, Spalte, Spalte, Value1\_1, bitte, 02.05.2024, Wert, Das ist ein Beispieltext, 20520,24, von Detailansicht mit kompaktem Header |
| hideHeader | Ausblenden der Kopfzeile mit den Spaltennamen in der Detailansicht | Boolescher Wert, Standardwert: false |
| OCR: Test, Value1\_1, bitte, 02.05.2024, Wert, Das ist ein Beispieltext, 20520,24 Detailansicht mit ausgeblendeter Kopfzeile |
| label | Angezeigter Name (Label) der Grid-Liste. Die Anzeige führt dazu, dass das System das grid-Element genauso eingerückt darstellt wie andere Elemente in einer form, wenn die Standardeinstellungen verwendet werden. | Zeichenkette |
| showAppend | Blendet das Symbol + zum Hinzufügen von neuen Positionen ein.   OCR: Bitte gib mir den OCR-Text, den ich zusammenfassen soll. Ich werde dann: | Boolescher Wert, Standardwert: false |
| showRowDelete | Blendet das Symbol Zeile löschen in der Listenansicht im Kontextmenü und in der Detailansicht ein, wodurch Benutzer eine Position aus der Liste löschen können.   OCR: Bitte gib mir den OCR-Text, den ich zusammenfassen soll. Ich werde dann: | Boolescher Wert, Standardwert: false |
| showRowMove | Blendet die Symbole zum Verschieben von Einträgen in der Listenansicht im Kontextmenü und in der Detailansicht ein, wodurch Benutzer Elemente in der Liste verschieben können.   OCR: Bitte gib den OCR-Text ein, den ich zusammenfassen soll. Ich werde dann: | Boolescher Wert, Standardwert: false |
| template | Definiert die Darstellung der jeweiligen Spalten einer Zeile in der Tabelle. Darin enthalten sind form-Elemente oder aguila-widgets. Sie können alle Parameter von element oder aguila-widget verwenden. Sie können durch die Angabe von actions die Standardeinstellungen von actions der Grid-Liste pro Spalte überschreiben. Definieren Sie mindestens eine Spalte als flexible=true und andere Spalten mit einer festen width, sodass die Liste sinnvoll die gesamte Breite verwendet. Das System lädt alle Angaben für die Darstellung aus der Metadaten-Definition, wenn name ein definiertes Metadatum ist. Sie können weitere Parameter definieren, die dann die Parameter aus der Metadaten-Definition überschreiben oder ergänzen. Sie können zu Spalten, die sich automatisch aus einer metadata-list-Definition ergeben, noch weitere eigene Spalten hinzuzufügen. | Hinweis: Die Spalte name darf nicht mit einem \_ (Unterstrich) beginnen. Diese Schreibweise ist ausschließlich für interne Zwecke reserviert. |
| value | Übergibt die Werte für die Grid-Liste als Array mit map-Einträgen, die zu der Definition in template passen müssen. | Array Hinweis: Alle Werte befinden sich im Speicher und verbrauchen somit RAM. |

#### actions Parameter

| Parameter | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| duplicate | Aktiviert die Aktion Zeile duplizieren im Kontextmenü in der Listenansicht und in der Detailansicht, mit der Benutzer die aktuelle Zeile in der Liste kopieren können. Das System übernimmt die Zustände der Zellen, etwa disabled, readOnly, hidden.   OCR: Bitte gib den OCR-Text ein, den ich zusammenfassen soll. Ich werde dann: | Boolescher Wert, Standardwert: false |
| setColumnValues | Aktiviert das Vererben von Werten einer Spalte nach oben, unten oder in beide Richtungen. Das System übernimmt nur die Werte, nicht die Zustände wie disabled, readOnly, hidden.   OCR: Wert nach oben vererben, Wert nach unten vererben, Wert auf die gesamte Spalte anwenden | Boolescher Wert, Standardwert: false |

### grid Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gelten die folgenden Events.

| Event | Beschreibung | Hinweise |
| --- | --- | --- |
| action | Löst aus, wenn ein Benutzer auf ein Symbol innerhalb der Grid-Liste klickt. | Das System übergibt als Parameter diese Struktur:  { name: 'col1', // Spaltenname index: 0, // Position in der Liste (bezogen auf alle Werte) path: \[ 0, 'col1' \] // Pfad zum auslösenden Element } |
| changed | Löst aus, wenn ein Benutzer einen Wert in einem Feld ändert und das Feld verlässt. Dieses Event löst erst aus, sobald der Benutzer mit seiner Eingabe fertig ist. Bei grid löst das changed-Event unterschiedlich aus: Für das jeweils geändert Feld in einer Spalte und Zeile. Für die ganze grid, wenn ein Benutzer eine neue row zur Liste hinzufügt oder löscht. Für weitere Informationen zu changed siehe agorum.composite.form.element - Grundlegende Eigenschaften | Das System übergibt als Parameter diese Struktur:  { value: 'current value', // aktueller Wert des Felds index: 0, // Index der Zeile, in der die Änderung stattfand name: 'col1', // Name des auslösenden Elements // ist nicht belegt beim input-Event für die Zeile oder ganze grid path: \[ 0, 'col1' \] // Pfad zum auslösenden Element } |
| input | Löst aus, wenn ein Benutzer einen Wert in einem Feld ändert.  Bei grid löst das input-Event unterschiedlich aus: Für die Spalte selbst. Hier enthalten value und oldValue den Wert der geänderten Spalte. Für die ganze Zeile. Hier enthalten value und oldValue den Wert der gesamten Zeile, in der die Änderung stattfand. Für die ganze grid. Hier enthalten value und oldValue den Wert der gesamten Liste. Für weitere Informationen zu input siehe agorum.composite.form.element - Grundlegende Eigenschaften | Das System übergibt als Parameter diese Struktur:  { value: 'current value', // aktueller Wert des Felds oldValue: 'previous value', // Wert vor der Änderung index: 0, // Index der Zeile, in der die Änderung stattfand name: 'col1', // Name des auslösenden Elements // ist nicht belegt beim input-Event für die Zeile oder ganze grid path: \[ 0, 'col1' \] // Pfad zum auslösenden Element } |
| itemAppended | Löst aus, wenn ein Benutzer ein Element zu der Grid-Liste hinzufügt. | Das System übergibt als Parameter diese Struktur:  { item: \[ ... \], // der Wert der neuen Zeile index: 99, // Position in der Liste (bezogen auf alle Werte der Liste), zu der das Element hinzugefügt wurde } |
| itemDeleted | Löst aus, wenn ein Benutzer ein Element der Grid-Liste löscht. | Das System übergibt als Parameter diese Struktur:  { item: \[ ... \], // der Wert dieser Zeile index: 0 // Position in der Liste (bezogen auf alle Werte der Liste), in der das Element zuvor war } |
| itemMoved | Löst aus, wenn ein Benutzer ein Element der Grid-Liste verschiebt. | Das System übergibt als Parameter diese Struktur:  { item: \[ ... \], // der Wert dieser Zeile fromIndex: 0, // Position in der Liste (bezogen auf alle Werte der Liste), bevor das Element verschoben wurde toIndex: 1 // Position nach dem Verschieben } |
| valueChanged | Löst aus, wenn sich mindestens ein Wert innerhalb der Listen-Werte ändert. Das System übergibt als Parameter den neuen Wert von value, d. h. das gesamte Array der Grid-Liste. Tipp: Sie können mit dem Event input gezieltere Informationen darüber erhalten, was der Benutzer in der Liste geändert hat. | Innerhalb von valueChanged können Sie die value der form oder des Elements nicht ändern, da ansonsten eine Endlosschleife die Folge wäre. Sofern dies dennoch notwendig ist, ändern Sie den Wert über setImmediate. Ignorieren Sie dann zwingend das darauffolgende valueChanged-Event, etwa mit einem Flag oder durch Prüfung des Values auf Änderung. |

### grid Funktionen

* * *

Für weitere Informationen zu den Funktionen set und get siehe [list Funktionen](#).

## agorum.composite.form.element.html

Mit diesem form-Element zeigen Sie HTML-Inhalte an, sodass Benutzer diese HTML-Inhalte editieren können. Um HTML editieren oder HTML-Inhalte darstellen zu können, setzen Sie den Parameter *value*.

*agorum.composite.form.element.html* erbt alle Grundeigenschaften von [element](#).

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/43417500-22bd-11ed-b442-005056aa0ecc)

```auto
OCR: test.js, Test, Hello, World, For, ..., Stil
```

form-Element

### Verwendung

* * *

```auto
let aguila = require('common/aguila');
let widget = aguila.create({
  type: 'agorum.composite.form.basic',
  width: 600,
  height: 400,
  elements: [
    {
      type: 'agorum.composite.form.element.html',
      flexible: true,
      value: '<p>Hello World</p>'
    }
  ]
});
widget;
```

### Parameter

* * *

#### value

Stellt den HTML-Inhalt der Komponente dar, den ein Benutzer bearbeiten kann und angezeigt bekommt.

#### flexible

| Wert | Beschreibung |
| --- | --- |
| true | Berechnet die Höhe und Breite des Elements dynamisch. Das Element verwendet den kompletten zur Verfügung gestellten Platz des übergeordneten Widgets/ Fensters. |
| false | Berechnet die Höhe und Breite des Elements nicht dynamisch. |

Das System gibt eine Mindesthöhe von 150 Pixeln vor, wenn Sie den Parameter nicht setzen.

**Beispiel zu true**

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/43417500-22bd-11ed-b442-005056aa0ecc)

```auto
OCR: test.js, Test, Hello, World, For, ..., Stil
```

Parameter *flexible* auf *true*

**Beispiel zu false**

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/44245af0-22bd-11ed-b442-005056aa0ecc)

```auto
OCR: test.js, Test, ..., Stil, Hello, World
```

Parameter *flexible* auf *false*

#### security

**Ab welcher Version verfügbar?**

• *agorum core* 9.2.3

Stellt diverse Sicherheitsstufen für die Anzeige des HTML-Inhalts ein.

| Wert | Beschreibung |
| --- | --- |
| none (Standard) | Gibt den Inhalt so wieder, wie er ist. Achtung: Sicherheitslücken durch schädliches HTML möglich. Verwenden Sie nur HTML-Inhalt, dem Sie auch vertrauen. |
| sanitized | Bereinigt den Inhalt von bösartigem Code und Tags. Das System zeigt den Inhalt danach direkt an. |
| isolated | Zeigt den Inhalt in einem iFrame an, filtert zusätzlich schädlichen Code heraus und zeigt den Inhalt in einem isolierten Bereich an, der keinen Zugriff auf das Hauptfenster besitzt. Dies ist etwa für die Anzeige von HTML-E-Mails notwendig, da diese oftmals über Stylesheets Anzeigen ändern, die ansonsten Auswirkungen auf die gesamte agorum core-Weboberfläche hätten. |

#### cls

Definiert ein Style-Set für den Parameter [value](#value), das das System anzeigt.

* Sie können CSS-Klassennamen übergeben, die Sie zuvor *agorum core* zur Verfügung gestellt haben.
* Sie können mehrere Klassennamen mit einem Leerzeichen voneinander trennen.

#### disableDefaultLinkHandling

| Wert | Beschreibung |
| --- | --- |
| true | Deaktiviert das Standardverhalten bei einem Klick auf einen agorum core-Link in einem HTML. |
| false (Standard) | Das System ruft bei einem Klick auf den Link die Open-Aktion aus dem agorum core smart assistant konfigurator auf und beim Rechtsklick das Kontextmenü. |

Sie können den Wert nur bei der Initialisierung des Widgets definieren.

**Beispiel**

```auto
<a action="open" class="agorum-editor-link" href="#" uuid="df4c1a20-a711-11e9-bb06-02420a0a0007">test linked.html</a>
```

#### linkCls

Übergibt ein Array von Strings, die Link-Klassen von HTML-Links enthalten, auf die Sie Klick-Events erhalten möchten.

* Sie können damit Links im HTML definieren, auf die Sie im Widget reagieren können.
* Das System gibt automatisch alle Attribute des Links zurück.
* Sie können den Wert nur bei der Initialisierung des Widgets definieren.

**Beispiel**

```auto
<a action="open" class="my-link" href="#" uuid="df4c1a20-a711-11e9-bb06-02420a0a0007">test linked.html</a>
```

Wenn Sie bei *linkCls* die Klasse *my-link* definieren, so erhalten Sie die Events:

* [linkClicked](#events)
* [linkRightClicked](#events)
* [linkDblClicked](#events)

Das System löst die Events nur im Ansichtsmodus des Elements aus, im Bearbeitungsmodus stehen diese nicht zur Verfügung.

**Klassen festlegen**

```auto
let aguila = require('common/aguila');
let widget = aguila.create({
  type: 'agorum.composite.form.basic',
  width: 400,
  height: 400,
  readOnly: true,
  elements: [
    {
      type: 'agorum.composite.form.element.html',
      name: 'htmlElement',
      linkCls: [
        'my-link'
      ],
      flexible: true,
      value: '<a action="open" class="my-link" href="#" uuid="df4c1a20-a711-11e9-bb06-02420a0a0007">test linked.html</a>'
    }
  ]
});

widget.down('htmlElement').on('linkClicked', link => {
  console.log('link clicked', link);
});

widget.down('htmlElement').on('linkRightClicked', link => {
  console.log('link right-clicked', link);
});

widget.down('htmlElement').on('linkDblClicked', link => {
  console.log('link double-clicked', link);
});

widget;
```

### Funktionen

* * *

#### insert

**Ab welcher Version verfügbar?**

• *agorum core* 9.2.3

Ermöglicht es Benutzern, HTML-Code an die Stelle des Cursors im Editor einzufügen.

Der Editor muss sich im Bearbeitungsmodus befinden.

**Beispiel**

```auto
widget.down('htmlElement').insert('<b>Beispieltext</b>');
```

### Events

* * *

#### linkClicked

Löst aus, wenn ein Benutzer auf einen Link im HTML klickt, dessen *class* einer der definierten Klassen innerhalb von [linkCls](#linkCls) entspricht.

Sie erhalten als Übergabe-Parameter folgende Struktur zurück:

```auto
{
  linkCls: 'cls-Angabe, wie in linkCls definiert',
  weitere: '....'
}
```

| Parameter | Beschreibung |
| --- | --- |
| linkCls | Definiert die Klasse des Links, auf den ein Benutzer geklickt hat. |
| weitere... | Enthält alle weiteren Attribute des Links, etwa die UUID oder action, sofern beim Link definiert. |

#### linkRightClicked

Löst aus, wenn ein Benutzer auf einen Link im HTML mit der rechten Maustaste klickt.

Ansonsten identisch zum Event [linkClicked](#events)

#### linkDblClicked

Löst aus, wenn ein Benutzer auf einen Link im HTML doppelklickt.

Ansonsten identisch zum Event [linkClicked](#events)

## agorum.composite.form.element.label

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.10

Dieses Element stellt ein Label dar. Sie können es etwa in Kombination mit Widgets verwenden, die kein Label besitzen.​​​​​​

*agorum.composite.form.element.label* erbt alle Grundeigenschaften von [element](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    // Sample: label on top, bevore vbox
    {
      type: 'agorum.composite.form.element.label',
      label: 'Label 1',
      labelPosition: 'top'
    },
    {
      type: 'agorum.vbox',
      border: true,
      height: 100
    },
    {
      type: 'agorum.hbox',
      items: [
        // Sample: label on left side before vbox
        {
          type: 'agorum.composite.form.element.label',
          label: 'Label 2'
        },
        {
          type: 'agorum.vbox',
          border: true,
          flexible: true,
          height: 100
        }
      ]
    },
    // text element has builtin label
    {
      type: 'agorum.composite.form.element.text',
      label: 'Label 3'
    },
    // text element has builtin label
    {
      type: 'agorum.composite.form.element.text',
      label: 'Label 4',
      labelPosition: 'top'
    }
  ]
});

form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten bis auf *value*.

### Events

* * *

Alle Events in [element](#) gelten.

## agorum.composite.form.element.list

Dieses Element stellt eine Liste von Werten dar. Sie können damit:

* jede andere Art von Element innerhalb der Liste verwenden
* Positionen der Liste verschieben
* Positionen der Liste löschen
* beliebig lange Listen mit Blätter-Funktion darstellen
* Aktions-Schaltflächen innerhalb der Listenpositionen verwenden
* das Element im Zusammenhang mit Metadaten-Definitionen verwenden

Sie können das list-Element ebenfalls mit *metadata-edit* verwenden, wenn es ein Metadatum vom Typ *list* ist.

*agorum.composite.form.element.list* erbt alle Grundeigenschaften von [element](#).

Zum Suchen nach einem list-Metadatum siehe [Suchsyntax in Solr verwenden](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

// fill test values
let testValue = [];
for (let i=0;i<100;i++) {
  testValue.push({
    col1: {
      type: 'custom',
      value: 'Value1_' + i,
      hidden: false
    },
    user_ag_tags: null,
    col2: 'Value2_' + i,
    col3: {
      type: 'custom',
      value: new Date()
    },
    col4: 'value1',
    col5: 'This is a sample text',
    col6: {
      type: 'custom',
      icon: 'aguila-icon local_airport'
    },
    col7: {
      type: 'custom',
      value: '+'
    }
  });
}

let form = aguila.create({
  width: 1200,
  height: 600,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      // showError: 'always',
      // readOnly: true,
      maxItems: 5,
      label: 'Test',
      // hideNavigation: true,
      // showAppend: true,
      // showRowDelete: true,
      // showRowMove: true,
      // hideHeader: true,
      // tableWidth: 2000,

      // actions is ab agorum core 9.5.0 verfügbar
      actions: {
        duplicate: true,
        setColumnValues: true
      },
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Spalte 1',
          flexible: true,
          hidden: false,

          // actions is ab agorum core 9.5.0 verfügbar
          actions: {
            setColumnValues: false
          },

          validation: [
            {
              required: true
            }
          ]
        },
        {
          // use of metadata
          name: 'user_ag_tags',
          width: 100
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'col2',
          label: 'Spalte 2',
          width: 100
        },
        {
          type: 'agorum.composite.form.element.date',
          name: 'col3',
          label: 'Spalte 3',
          width: 200
        },
        {
          type: 'agorum.composite.form.element.select',
          name: 'col4',
          label: 'Spalte 4',
          restricted: true,
          data: [
            {
              value: 'value1',
              text: 'Wert 1'
            },
            {
              value: 'value2',
              text: 'Wert 2'
            }
          ],
          width: 200
        },
        {
          type: 'agorum.textDisplay',
          name: 'col5',
          width: 100
        },
        {
          type: 'agorum.composite.form.element.button',
          name: 'col6',
          icon: 'aguila-icon drive_eta',
          readOnlyHidden: true,
          width: 34
        },
        {
          type: 'agorum.composite.form.element.button',
          name: 'col7',
          value: 'Y',
          readOnlyHidden: true,

          width: 34
        }

      ],
      value: testValue
    }
  ]
});

form.down('listField').
on('focused', data => {
  console.log('focused', data);
}).
on('blurred', data => {
  console.log('blurred', data);
}).
on('action', data => {
  console.log('action', data);
}).
on('itemDeleted', data => {
  console.log('deleted', data);
}).
on('itemMoved', data => {
  console.log('moved', data);
});

form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### maxItems

Definiert die maximale Anzahl gleichzeitig dargestellter Zeilen (Standard: 5).

* Verwenden Sie einen kleinen Wert für diesen Parameter, da das System ansonsten zu viele Informationen gleichzeitig darstellt und die Performance negativ beeinflusst.
* Sie können ab *agorum core* 9.3.0 den Wert 0 setzen, damit die Liste dynamisch wächst und ein Benutzer sie nicht blättern muss, etwa bei kleineren Listen, bei denen ein Benutzer nicht mehr als 10 Werte erwartet (schnelle initiale Darstellung bei kleinen Mengen und Entfall der Navigationsbuttons und Positions-Anzeige, was Platz einspart).

**Beispiel**

```auto
form.down('listField').maxItems = 10;
```

#### hideHeader

| Wert | Beschreibung |
| --- | --- |
| true | Blendet den Header der Liste aus. |
| false (Standard) | Blendet den Header der Liste ein. |

**Beispiel**

```auto
form.down('listField').hideHeader = true;
```

Sie können diesen Parameter nachträglich ändern.

#### compactHeader

**Ab welcher Version verfügbar?**• *agorum core* 9.3.0

| Wert | Beschreibung |
| --- | --- |
| true | Stellt den Header in einer kompakten Form dar. Nur die Symbole für Vor und Zurück sowie die Anzeige der angezeigten Elemente auf der rechten Seite existieren, um Platz zu sparen. |
| false (Standard) | Stellt den Header NICHT kompakt dar. |

**Beispiel**

```auto
form.down('listField').compactHeader = true;
```

Sie können diesen Parameter nachträglich ändern.

#### hideNavigation

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Navigation der Liste aus. Benutzer können dann nicht mehr zu Werten navigieren, die nicht sichtbar sind. |
| false (Standard) | Blendet die Navigation der Liste ein. |

**Beispiel**

```auto
form.down('listField').hideNavigation = true;
```

Sie können diesen Parameter nachträglich ändern.

#### showAppend

| Wert | Beschreibung |
| --- | --- |
| true | Blendet das Symbol + zum Hinzufügen von neuen Elementen ein. |
| false (Standard) | Blendet das Symbol + zum Hinzufügen von neuen Elementen aus. |

**Beispiel**

```auto
form.down('listField').showAppend = true;
```

**Einträge programmatisch hinzufügen**

```auto
form.down('listField').value = form.down('listField').value.concat([
  {
    col1: 'Wert 1',
    col2: 'Wert 2',
    // ...
  },
  {
    // ...
  }
]);
```

Sie können diesen Parameter nachträglich ändern.

#### showRowDelete

| Wert | Beschreibung |
| --- | --- |
| true | Blendet das Symbol Löschen bei den jeweiligen Listeneinträgen ein, wodurch Benutzer Elemente aus der Liste löschen können. |
| false (Standard) | Blendet das Symbol Löschen bei den jeweiligen Listeneinträgen aus. |

**Beispiel**

```auto
form.down('listField').showRowDelete = true;
```

Sie können diesen Parameter nachträglich ändern.

#### showRowMove

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Symbole zum Verschieben von Einträgen der Liste ein, wodurch Benutzer Elemente in der Liste verschieben können. |
| false (Standard) | Blendet die Symbole zum Verschieben von Einträgen der Liste aus. |

**Beispiel**

```auto
form.down('listField').showRowMove = true;
```

Sie können diesen Parameter nachträglich ändern.

#### label

Stellt das Label (Bezeichnung) vorn an der Liste dar, sodass das System das list-Element genauso eingerückt darstellt wie andere Elemente in einer *form.*

Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('listField').label = 'Liste';
```

#### tableWidth

Definiert die innere Breite der Tabelle in der Liste.

* Die Liste verwendet im Standard die volle Breite des Fensters (Standard: null).
* Eine Scrollbar entsteht, wenn Sie eine Breite definieren, die größer ist als die Listenbreite, um viele Spalten in der Tabelle sinnvoll darzustellen.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('listField').tableWidth = 2000;
```

#### page

Springt zur jeweiligen Listenposition.

* Enthält die Liste etwa zehn Werte und *maxItems=5*, dann bedeutet *page=1*, dass das System auf die Seite 2 springt und die Elemente 6–10 darstellt.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('listField').page = 1;
```

#### actions

**Ab welcher Version verfügbar?**• *agorum core* 9.5.0

Definiert Aktionen auf Zeilenebene, die ein Benutzer per rechter Maustaste aufrufen kann.

| Wert | Beschreibung |
| --- | --- |
| duplicate=true/false (Standard: false) | Aktiviert die Aktion Duplizieren, mit der Benutzer die aktuelle Zeile in der Liste kopieren können. Das System übernimmt die Zustände der Zellen, etwa disabled, readOnly, hidden. |
| setColumnValues=true/false (Standard: false) | Aktiviert das Vererben von Werten einer Spalte nach oben, unten oder in beide Richtungen. Das System übernimmt nur die Werte, nicht die Zustände wie disabled, readOnly, hidden. |

* Sie können beide Werte auf [template](#template)\-Ebene pro Spalte definieren.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('listField').actions = {
  duplicate: true,
  setColumnValues: true
};
```

| Parameter | Beschreibung/Beispiel |
| --- | --- |
| template | siehe Abschnitt template |
| value | siehe Abschnitt value |

#### template

Definiert die Darstellung der jeweiligen Spalten einer Zeile in der Tabelle. Darin enthalten sind normale form-Elemente oder *aguila*\-widgets.

**Beispiel**

```auto
...
{
  // use of metadata
  name: 'user_ag_tags',
  width: 100,               // Wenn Sie keine width oder kein flexible definieren, steht width im Standard auf 80 (ab agorum core 9.5.1)
  label: 'Tags',            // Überschreibt das Label des Metadatums user_ag_tags
  hidden: false,            // Mit hidden=true blenden Sie die Spalte aus
  readOnlyHidden: false,    // Mit readOnlyHidden=true blenden Sie die Spalte im readOnly-Modus aus

  actions: {

    setColumnValues: false
  }
}
...
```

**Hinweis**: Die Spalte *name* darf nicht mit einem \_ beginnen. Diese Schreibweise ist ausschließlich für interne Zwecke reserviert.

* Das System lädt alle Angaben für die Darstellung aus der Metadaten-Definition, wenn *name* ein definiertes Metadatum ist.
* Sie können weitere Parameter definieren, die dann die Parameter aus der Metadaten-Definition überschreiben oder ergänzen.
* Sie können alle Parameter von Element oder widget verwenden.
* Sie können ab *agorum core* 9.5.0 durch die Angabe von [actions](#actions) die Standardeinstellungen von *actions* der Liste pro Spalte überschreiben.
* Sie können ab *agorum core* 9.5.1 zu Spalten, die sich automatisch aus einer metadata-list*\-*Definition ergeben, noch weitere eigene Spalten hinzuzufügen.
* Definieren Sie mindestens eine Spalte als *flexible=true* und andere Spalten mit einer festen *width*, sodass die Liste sinnvoll die gesamte Breite ausnutzt.

**Parameter nachträglich ändern**

```auto
form.down('listField').template: [
  {
    type: 'agorum.composite.form.element.text',
    name: 'col1',
    label: 'Spalte 1',
    flexible: true,
    validation: [
      {
        required: true
      }
    ]
  },
  {
    // use of metadata
    name: 'user_ag_tags',
    width: 100
  }
];
```

**Die Reihenfolge der Spalten aus der Metadaten-Definition steuern**

Das System übernimmt die Spalten aus der Metadaten-Definition, wenn Sie das list-Element mit einem Metadatum vom *type=list* initialisieren, in einer willkürlichen Reihenfolge.

Sie können die Reihenfolgen aller definierten Spalten mit einem zusätzlichen Parameter steuern. Alle nicht definierten fügt das System in unbestimmter Reihenfolge hinten an:

1. Das Metadatum *tst\_rechnungsposition* beinhaltet etwa die Felder *number*, *description* und *net*.
2. Sie definieren die yml-Datei:

    ```auto
    -tst_rechnungsposition:
      displayName: Rechnungspositionen
      list:
        number:
          displayName: Nummer
          type: long

        description:
          displayName: Bezeichnung
          type: string

        net:
          displayName: Nettobetrag
          type: double
    ```

3. Sie initialisieren das list-Element:

    ```auto
    let form = aguila.create({
      width: 1200,
      height: 600,
      type: 'agorum.composite.form.basic',
      elements: [
        {
          name: 'tst_rechnungsposition'
        }
      ]
    });
    ```

    **Ergebnis**: Eine Liste mit den Spalten *number*, *description* und *net* in willkürlicher Reihenfolgende entsteht.
4. Beeinflussen Sie die Reihenfolge etwa so:Sie müssen nicht alle Spalten angeben, sondern nur diejenigen, deren Reihenfolge Ihnen wichtig ist.

    ```auto
    let form = aguila.create({
      width: 1200,
      height: 600,
      type: 'agorum.composite.form.basic',
      elements: [
        {
          name: 'tst_rechnungsposition',
          template: [
            {
              name: 'number'
            },
            {
              name: 'description'
            },
            {
              name: 'net'
            }
          ]
        }
      ]
    });
    ```

#### value

Übergibt die Werte für die Liste als Array mit map-Einträgen, die zu der Definition in [template](#template) passen müssen.

**Hinweise**: Alle Werte befinden sich im Speicher und verbrauchen somit RAM.

**Beispiel**

```auto
form.down('listField').value = [{
  col1: {
    type: 'custom',
    value: 'Value1_' + i,
    hidden: false
  },
  user_ag_tags: null,
  col2: 'Value2_' + i,
  col3: {
    type: 'custom',
    value: new Date()
  },
  col4: 'value1',
  col5: 'This is a sample text',
  col6: {
    type: 'custom',
    icon: 'aguila-icon local_airport'
  },
  col7: {
    type: 'custom',
    value: '+'
  }
}];
```

**Ein Widget in der Spalte steuern**

Im Standard übergeben Sie nur *Spaltenname=Wert*, sodass das System die Spalte mit dem Namen *col1* mit dem Wert *Wert 1* belegt, etwa:

```auto
// ...
{
  col1: 'Wert 1'
}
// ...
```

Sie können die jeweiligen Widgets in der Spalte steuern, indem Sie eine map mit dem *type=custom* übergeben. Dadurch können Sie jede Art von Parameter an das dahinterliegende Widget übertragen. So können Sie etwa die Icons von *buttons* verändern oder einen Wert in der jeweiligen Zeile ausblenden. Der Parameter *value* enthält dann den eigentlichen Wert:

```auto
// ...
col6: {
  type: 'custom',
  icon: 'aguila-icon local_airport',
  readOnly: true,
  // oder alle weitern Properties des dahinterliegenden Widgets
}
// ...
```

**Hinweise**:

* Bis *agorum core* 9.5.0: Sie erhalten die Werte genauso zurück, wie Sie sie auch gesetzt haben. Das nutzende Programm muss dann also selbstständig die korrekten Werte aus dieser Struktur wieder auslesen.

* Ab *agorum core* 9.5.1: Sie erhalten bei allen Rückgaben der Werte (*valueChanged*, *input*, *get*/*set*) den eigentlichen *value*. Das bedeutet, Sie müssen in den verarbeitenden Programmen nicht mehr darauf achten.

#### Spezielle Werte für die Symbole

Für die Symbole zum Verschieben und Löschen von Einträgen existieren spezielle vordefinierte Spaltennamen. Dadurch können Sie die Symbole auf Positionsebene ebenfalls ausblenden.

| Spaltenname | Beschreibung |
| --- | --- |
| \_up | Eintrag nach oben verschieben |
| \_down | Eintrag nach unten verschieben |
| \_delete | Eintrag löschen |

**Das Symbol „Löschen“ für eine Zeile ausblenden**

```auto
form.down('listField').value = [{
  // ....
  _delete: {
    type: 'custom',
    hidden: true
  }
}];
```

### Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gelten die folgenden Events.

#### pageChanged

Löst aus, wenn ein Benutzer innerhalb der Liste navigiert.

Das System übergibt als Parameter den neuen Wert von [page](#page).

#### valueChanged

Löst aus, wenn sich mindestens ein Wert innerhalb der Listen-Werte ändert.

Das System übergibt als Parameter den neuen Wert von [value](#value), d. h. das gesamte Array der Liste.

**Hinweis**: Innerhalb von *valueChanged* können Sie die *value* der *form* oder des Elements nicht ändern, da ansonsten eine Endlosschleife die Folge wäre. Sofern dies dennoch notwendig ist, ändern Sie den Wert über *setImmediate*. Ignorieren Sie dann zwingend das darauffolgende valueChanged-Event, etwa mit einem Flag oder durch Prüfung des Values auf Änderung.

**Tipp**: Sie können ab *agorum core* 9.3.0 mit dem Event [input](#input) gezieltere Informationen darüber erhalten, was sich vom Benutzer in der Liste geändert hat. Zudem können Sie direkt mit [set](#set) und [get](#get) Werte setzen und lesen.

#### focused

Löst aus, wenn ein Benutzer ein Element innerhalb der Liste fokussiert.

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{
  name: 'col1',        // Name der Spalte
  index: 0,            // Position in der Liste (bezogen auf alle Werte)
  path: [ 0, 'col1' ]  // Pfad zum auslösenden Element
}
```

#### blurred

Löst aus, wenn ein Benutzer ein Element innerhalb der Liste nicht mehr fokussiert.

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{
  name: 'col1',        // Name der Spalte
  index: 0,            // Position in der Liste (bezogen auf alle Werte)
  path: [ 0, 'col1' ]  // Pfad zum auslösenden Element
}
```

#### input

**Ab welcher Version verfügbar?**• *agorum core* 9.3.0

Löst aus, wenn ein Benutzer einen Wert in einem Feld ändert.

Dieses Event ist einfacher zu verwenden als [valueChanged](#valueChanged).

Bei *list* löst das input-Event unterschiedlich aus:

* Für die Spalte selbst. Hier enthalten *value* und *oldValue* den Wert der geänderten Spalte.
* Für die ganze Zeile. Hier enthalten *value* und *oldValue* den Wert der gesamten Zeile, in der die Änderung stattfand.
* Für die ganze *list*. Hier enthalten *value* und *oldValue* den Wert der gesamten Liste.

Details zu *input* siehe [agorum.composite.form - element - Grundlegende Eigenschaften](#)

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{
  value: 'current value',      // aktueller Wert des Felds
  oldValue: 'previous value',  // Wert vor der Änderung
  index: 0,                    // Index der Zeile, in der die Änderung stattfand
  name: 'col1',                // Name des auslösenden Elements
                               // ist nicht belegt beim input-Event für die Zeile oder ganze list
  path: [ 0, 'col1' ]          // Pfad zum auslösenden Element
}
```

#### action

Löst aus, wenn ein Benutzer auf ein Symbol innerhalb der Liste klickt.

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{

  name: 'col1',        // Name der Spalte
  index: 0,            // Position in der Liste (bezogen auf alle Werte)
  path: [ 0, 'col1' ]  // Pfad zum auslösenden Element
}
```

#### itemDeleted

Löst aus, wenn ein Benutzer ein Element der Liste löscht.

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{
  item: [ ... ],  // Der Wert dieser Zeile
  index: 0        // Position in der Liste (bezogen auf alle Werte der Liste), in der das Element zuvor war
}
```

#### itemMoved

Löst aus, wenn ein Benutzer ein Element der Liste verschiebt.

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{
  item: [ ... ],   // Der Wert dieser Zeile
  fromIndex: 0,    // Position in der Liste (bezogen auf alle Werte der Liste), bevor das Element verschoben wurde
  toIndex: 1       // Position nach dem Verschieben
}
```

#### itemAppended

Löst aus, wenn ein Benutzer ein Element der Liste hinzufügt.

**Beispiel**

Das System übergibt als Parameter diese Struktur:

```auto
{
  item: [ ... ],   // Der Wert der neuen Zeile
  index: 99,       // Position in der Liste (bezogen auf alle Werte der Liste), zu der das Element hinzugefügt wurde
}
```

**Werte nach dem Hinzufügen anreichern**

```auto
let listField = form.down('listField');

listField.on('itemAppended', data => {
  let value = listField.value;
  value[data.index] = {
    col3: {
      type: 'custom',
      value: new Date()
    },
    col6: {
      type: 'custom',
      icon: 'aguila-icon local_airport'
    },
    col7: {
      type: 'custom',
      value: '+'
    }
  };
  listField.value = listField.value.concat([]);

});
```

### Funktionen

* * *

**Hinweis**: Verwenden Sie ab *agorum core* 9.3.0 [set](#set), [get](#get) und [input](#input) anstelle von *value=*, *valueChanged* oder *.value*.

#### set

**Ab welcher Version verfügbar?**• *agorum core* 9.3.0

Setzt Parameter und Werte.

**Beispiel**

```auto
let listField = form.down('listField');

// Beispiel einen Wert setzen
listField.set('[0].col1.value', 'Ein Wert');

// Beispiel Feld disablen
listField.set('[0].col1.disabled', true);
```

**Beispiel bei Listen**

Bei Listen legt das System die Zeile, wenn sie noch nicht existiert, automatisch an und füllt alle bis dahin noch nicht vorhandenen auf.

Wenn eine Liste etwa noch keine Werte besitzt, belegt das System mit *set* die 10. Zeile. In diesem Falle füllt es alle 9 davor liegenden mit leeren Zellen auf und setzt entsprechend die 10. Zeile:

```auto
let listField = form.down('listField');

listField.set('[10].col1.value', 'Ein Wert');
```

**Eine komplette Zeile setzen**

```auto
let listField = form.down('listField');

listField.set('[0].value', {
  col1: 'Wert 1',
  col2: 'Wert 2'
});
```

**Eine komplette Liste setzen**

```auto
let listField = form.down('listField');

listField.set('value', [
  {
    col1: 'Wert 1.1',
    col2: 'Wert 1.2'
  },
  {
    col1: 'Wert 2.1',
    col2: 'Wert 2.2'
  }
]);
```

#### get

**Ab welcher Version verfügbar?**• *agorum core* 9.3.0

Liest Parameter und Werte direkt.

**Beispiel**

```auto
let listField = form.down('listField');

// Beispiel einen Wert lesen aus der ersten Zeile und Spalte col1
let value = listField.get('[0].col1.value');

// Beispiel Feld disabled Status lesen
let disabled = listField.get('[0].col1.disabled');
```

Das System wirft einen Fehler, wenn es eine nicht existierende Zeile ausliest.

**Eine komplette Zeile lesen**

```auto
let listField = form.down('listField');

let row = listField.get('[0].value');
```

**Eine komplette Liste lesen**

```auto
let listField = form.down('listField');

let list = listField.get('value');
```

**Hinweis**: Bis *agorum core* 9.5.0 speicherte die Liste intern die Werte teilweise anders ab. Dies gilt ausschließlich für ein *get* auf Zeilen oder die ganze Liste. D. h. dass das System bei *value* nicht unbedingt direkt den *value* zurückliefert, sondern folgende Struktur:

```auto
let value = {
  type: 'custom',
  value: 'Der eigentliche Wert',
  disabled: true
};
```

Eine Zelle kann nicht nur einen Wert haben, sondern auch andere Zustände speichern, etwa *disabled* oder *hidden* oder jedes andere Property.

Möchten Sie etwa über die ganze Liste iterieren und benötigen Sie dabei den *value* der jeweiligen Zelle, verwenden Sie dieses Skript:

```auto
listField.get('value').forEach((row, index) => {
  let value = listField.get([ 'value', index, 'name-of-column', 'value' ]);
});
```

Sie müssen die „rohen“ internen Strukturen beibehalten, wenn Manipulationen auf der ganzen Liste stattfinden sollen, da ansonsten Informationen wie *disabled* verloren gehen.

### Weitere Beispiele

* * *

#### Eine Spalte in Abhängigkeit einer anderen Spalte ändern

Dieses Beispiel stellt eine Liste mit 3 Spalten dar. Ändern sich die ersten beiden Spalten, so berechnet das System in der letzten Spalte die Summe und stellt diese dar.

```auto
let aguila = require('common/aguila');

// create a basic form with a list, with 3 columns
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.number',
          name: 'number1',
          label: 'Number 1',
          width: 60,
        },
        {
          type: 'agorum.composite.form.element.number',
          name: 'number2',
          label: 'Number 2',
          width: 60,
        },
        {
          type: 'agorum.composite.form.element.number',
          name: 'result',
          disabled: true,
          label: 'Sum',
          flexible: true
        }
      ],
      // add empty row
      value: [{}]
    }
  ]
});

// get event on user change
form.on('input', data => {
  // when either number1 or number2 is changed, build sum
  // path will look like this: [ 'listField', row, column ]: for example: [ 'listField', 0, 'number1' ]

  if (data.name === 'number1' || data.name === 'number2') {
    // row is second part in path
    let row = data.path[1];

    // get number 1
    let number1 = form.get([ 'listField', row, 'number1', 'value' ]);
    let number2 = form.get([ 'listField', row, 'number2', 'value' ]);

    // build sum and set to result column
    if (number1 !== undefined && number2 !== undefined) {
      let sum = number1 + number2;
      form.set([ 'listField', row, 'result', 'value' ], sum);
    }
  }
});

form;
```

#### Eine Zeile hinzufügen

Dieses Beispiel fügt eine Zeile am Ende der Liste hinzu.

```auto
let aguila = require('common/aguila');

// create a basic form with a list, with 3 columns
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.button',
      name: 'append',
      value: 'Append a row'
    },
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Column 1',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'col2',
          label: 'Column 2',
          flexible: true
        }
      ]
    }
  ]
});

form.on('action', data => {
  // append button is clicked
  if (data.name === 'append') {
    // append a row
    let rows = form.get('listField.value') || [];
    let index = rows.length;

    let newRow = {
      col1: 'This is row: ' + index,
      col2: 'it has been appended'
    };

    form.set([ 'listField', index, 'value' ], newRow);
  }
});

form;
```

#### Eine Zeile löschen

Dieses Beispiel löscht eine Zeile. Der Benutzer kann über ein Symbol immer die erste Zeile löschen.

```auto
let aguila = require('common/aguila');

// create a basic form with a list, with 3 columns
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.button',
      name: 'delete',
      value: 'Delete first row'
    },
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Column 1',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'col2',
          label: 'Column 2',
          flexible: true
        }
      ],
      value: [
        {
          col1: {
            type: 'custom',
            value: 'Value 1',
            disabled: true
          },
          col2: {
            type: 'custom',
            value: 'Value 2'
          }
        }
      ]
    }
  ]
});

let listField = form.down('listField');

form.on('action', data => {
  // delete button is clicked
  if (data.name === 'delete') {
    // delete first row
    let rows = form.get('listField.value') || [];

    if (rows.length > 0) {
      // remove first row
      rows.shift();
    }

    // set new rows to the list
    form.set([ 'listField', 'value' ], rows);
  }
});

listField.on('valueChanged', () => {
  // check, amount of rows, if no row is present,

  // disable the delete button, otherwise enable it
  let rows = form.get('listField.value') || [];
  form.set('delete.disabled', rows.length === 0);
});

form;
```

#### Eine Zeile kopieren

Dieses Beispiel fügt zwischen 2 Zeilen eine neue Zeile ein, wenn der Benutzer ein Symbol anklickt, und übernimmt die Werte aus der geklickten Zeile.

```auto
let aguila = require('common/aguila');

// create a basic form with a list, with 3 columns
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Column 1',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'col2',
          label: 'Column 2',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.button',
          name: 'copy',
          label: 'Copy',
          value: 'Copy row'
        }
      ],
      value: [
        {
          col1: {
            type: 'custom',
            value: 'Value 1',
            disabled: true
          },
          col2: {
            type: 'custom',
            value: 'Value 2'
          }
        }
      ]
    }
  ]
});

let listField = form.down('listField');

form.on('action', data => {
  // copy button is clicked
  if (data.name === 'copy') {
    let rows = form.get('listField.value') || [];

    // path will look like this: [ 'listField', row, column ]:

    // for example: [ 'listField', 0, 'number1' ]
    // row is second part in path
    let row = data.path[1];

    // clone this row and add it behind
    let newRow = rows[row];
    rows.splice(row + 1, 0, newRow);

    // set new rows to the list
    form.set([ 'listField', 'value' ], rows);
  }
});

form;
```

#### Eine Zeile zwischen 2 Listen transferieren

Dieses Beispiel stellt 2 Listen dar. Per Symbol kann der Benutzer eine Zeile von der einen in die andere Liste verschieben.

```auto
let aguila = require('common/aguila');

// create a basic form with a list, with 3 columns
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    // list 1
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField1',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Column 1',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'col2',
          label: 'Column 2',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.button',
          name: 'move',
          label: 'Move',
          value: 'Move to other list'
        }
      ]
    },

    // list 2
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField2',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Column 1',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.text',
          name: 'col2',
          label: 'Column 2',
          flexible: true
        },
        {
          type: 'agorum.composite.form.element.button',
          name: 'move',
          label: 'Move',
          value: 'Move to other list'
        }
      ]
    }
  ]
});

form.on('action', data => {
  // move button is clicked
  if (data.name === 'move') {
    // path will look like this: [ 'listField', row, column ]:

    // for example: [ 'listField', 0, 'number1' ]

    // find out what the source list is an what the target list
    let listName = data.path[0];

    let srcList;
    let dstList;

    if (listName === 'listField1') {
      srcList = 'listField1';
      dstList = 'listField2';
    }
    else {
      srcList = 'listField2';
      dstList = 'listField1';
    }

    // get rows from source and destination list
    let rowsSrc = form.get([ srcList, 'value' ]) || [];
    let rowsDst = form.get([ dstList, 'value' ]) || [];

    // row is second part in path
    let srcRow = data.path[1];

    // remove it from the srcList
    let removedRow = rowsSrc.splice(srcRow, 1);

    // append it to the destinatino list
    rowsDst = rowsDst.concat(removedRow);

    // set back the new rows to the source and destination lists
    form.set([ srcList, 'value' ], rowsSrc);
    form.set([ dstList, 'value' ], rowsDst);
  }
});

form;
```

#### Werten in Zeilen trimmen

Dieses Beispiel iteriert über Listen-Elemente und liest Werte darin aus, sodass Sie diese verändern können.

```auto
let aguila = require('common/aguila');

// create a basic form with a list, with 3 columns
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.button',
      name: 'trim',
      value: 'Trim values in list'
    },
    {
      type: 'agorum.composite.form.element.list',
      name: 'listField',
      showAppend: true,
      showRowMove: true,
      showRowDelete: true,
      template: [
        {
          type: 'agorum.composite.form.element.text',
          name: 'col1',
          label: 'Column 1',
          flexible: true
        }
      ],
      value: [
        {
          col1: '   Value 1   '
        }
      ]
    }
  ]
});

form.on('action', data => {
  // trim button is clicked
  if (data.name === 'trim') {
    // iterate through all values and trim them
    // (remove spaces before an after the string)

    // get rows
    let rows = form.get('listField.value') || [];

    // we need to iterate through all row-items and get
    // each value directly, cause in list, the value
    // can be substructured with information like disabled, etc ...

    rows.forEach((row, index) => {
      // get value and trim it
      let value = form.get([ 'listField', index, 'col1', 'value' ]).trim();

      // set value back
      form.set([ 'listField', index, 'col1', 'value' ], value);
    });
  }
});

form;
```

## agorum.mail.element.editor

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.7

Dieses Element stellt einen E-Mail-Editor dar, den Sie beliebig anpassen können.

*agorum.mail.element.editor* erbt alle [grundlegende Eigenschaften](#) von element.

### Beispiel eines E-Mail-Editors

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/3bc43960-3e3f-11ec-8fd4-005056aa0ecc)

```auto
OCR: form.element.mailEditor.js, Test, Ein Text, Von roi@agorumcore.com, demo@agorum.com, Betreff Hier den Betreff eingeben, Kopie, Blindkopie BCC, For ..., Stil Geben Sie hier einen Text
```

Beispiel eines E-Mail-Editors

#### Skript zum E-Mail-Editor

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  type: 'agorum.composite.form.basic',
  width: 800,
  height: 800,
  labelPosition: 'top',
  elements: [
    {
      type: 'agorum.composite.form.element.text',
      label: 'Ein Text'
    },
    {
      type: 'agorum.mail.element.editor',
      name: 'mailEditor',
      height: 400,
      deactivated: [
        /*
        'to',
        'cc',
        'bcc',
        'replyTo',
        'subject',
        'body',
        */
      ],
      removed: [
        'replyTo',
        'attachments'
      ],
      value: {
        from: 'roi@agorumcore.com',
        to: [ 'demo@agorum.com' ],
        subject: 'Hier den Betreff eingeben',
        body: 'Geben Sie hier einen Text an'
      }
    }
  ]
});

form;
```

### Felder und Werte anpassen

* * *

| Feld | Bezeichnung in der E-Mail-Maske | Beschreibung |
| --- | --- | --- |
| from | Von: | Absender |
| to | An\*: | Empfänger |
| cc | Kopie (CC) | Kopie (CC) |
| bcc | Blindkopie (BCC) | Blindkopie (BCC) |
| replyTo | Antwort an: | Antwort an |
| subject | Betreff\*: | Betreff der E-Mail |
| body | \- | E-Mail-Textfeld |
| attachments | \- | Anhänge (Array von IDs) |

**Hinweis:** Sie können zu den bereits vorhandenen Feldern weitere Felder hinzufügen. Im oben aufgeführten [Beispiel](#BeispielEMailEditor) ist etwa ein zusätzliches Textfeld angegeben.

### Parameter

* * *

#### deactivated

Definiert Felder, die in der E-Mail-Maske nicht verändert werden können.

**Beispiel**

```auto
deactivated: {
  'cc',
  'bcc'
}
```

#### removed

Definiert Felder, die in der E-Mail-Maske nicht erscheinen.

**Beispiel**

```auto
removed: {
  'cc',
  'bcc'
}
```

#### value

Definiert vordefinierte Werte für bestimmte Felder.

**Beispiel**

```auto
value: {
  from: 'roi@agorumcore.com'
}
```

## agorum.composite.form - element - Metadatum

Existiert für ein Element bereits eine Metadaten-Definition (*name* muss dem Namen des Metadatums entsprechen), dann lädt das System alle Eigenschaften aus der Metadaten-Definition.

Ist dies nicht gewünscht, kann durch die Eigenschaft *manualConfig=true* am Element dieses Verhalten deaktiviert werden.

### Beispiel einer Oberfläche

* * *

Dieses Beispiel erstellt eine Oberfläche mit den Metadaten *ag\_tags* (Globale Tags) und *user\_ag\_tags* (Benutzer Tags):

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/eb10b980-e8b1-11ec-bc0b-005056aa0ecc)

```auto
OCR: Sonstiges/sonstiges.js (Test), Globale Tags*, Benutzer-Tags: Sonstiges, sonstiges.js, Test, Globale Tags, Benutzer Tags
```

Beispiel einer Oberfläche

Die Metadaten müssen Sie zuvor definiert haben (siehe [Metadaten mit YML definieren (metadata.yml)](#) und [Metadaten Designer konfigurieren](#)).

**Skript zur Oberfläche**

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      name: 'ag_tags'
    },
    {
      name: 'user_ag_tags'
    }

  ]
});

form;
```

### Eigenschaften überschreiben

* * *

Sie können die Eigenschaften innerhalb der Definition des jeweiligen Elements aus der Metadaten-Definition überschreiben.

**Beispiel**

Dieses Beispiel überschreibt den Parameter *label* des jeweiligen Elements. Die Überschreibung funktioniert mit jeder weiteren Eigenschaft eines Elements (siehe [agorum.composite.form - element - Grundlegende Eigenschaften](#)).

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      name: 'ag_tags',
      label: 'Tags'
    },
    {
      name: 'user_ag_tags',
      label: 'Meine Tags'
    }

  ]
});

form;
```

## agorum.composite.form.element.number

Dieses Element stellt ein Zahlen-Eingabefeld dar.

*agorum.composite.form.element.number* erbt alle [grundlegenden Eigenschaften](#) von element.

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      type: 'agorum.composite.form.element.number',
      name: 'numberField1',
      label: 'Nummer 1',
      calculator: true,
      value: 123.456,
      precision: 2
    },
    {
      type: 'agorum.composite.form.element.number',
      name: 'numberField2',
      label: 'Nummer 2',
      value: 123,
      integer: true
    },
    {
      type: 'agorum.composite.form.element.number',
      name: 'numberField3',
      label: 'Nummer 3',
      value: 1234567.891,
      format: ',000.00',
      readOnly: true
    }
  ]
});

form;
```

### Parameter

* * *

Alle [Parameter](#) in element gelten. Zusätzlich gelten die folgenden Parameter.

#### calculator

**Ab welcher Version verfügbar?**• *agorum core* 10.0.8

Erzeugt einen [Taschenrechner](#taschenrechner) im gewählten Element.

Sie können den Taschenrechner über die Tastatur und über die Maus verwenden.

| Parameter | Beschreibung |
| --- | --- |
| true | Aktiviert den Taschenrechner. |
| false (Standard) | Deaktiviert den Taschenrechner. |

#### precision

Definiert die Anzahl der Nachkommastellen zwischen 0 und 100, die ein Benutzer eingeben kann und die erscheinen.

* Möglich sind Zahlen zwischen 0 und 100 (Standard: 2).
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('numberField1').precision = 3;
```

#### format

Definiert das Anzeigeformat der Zahl und überschreibt im Anzeigemodus die Definition von [precision](#precision).

* Der Parameter gilt nicht für den Bearbeitungsmodus.
* In der Definition ist ein Komma das Tausendertrennzeichen und der Punkt das Dezimaltrennzeichen.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('numberField1').format = ',000.00';
```

**Die Sprache für das Format wählen**

Das System verwendet im Standard die Sprache des Benutzers für die Formatierung. Sie können diese Sprachen überschreiben, indem Sie die Sprache vor das Format voranstellen und mit | trennen:

```auto
form.down('numberField1').format = 'en|,000.00';
```

**Weitere Beispiele**

* 0 = keine Nachkommastellen
* 0.00 = 2 Nachkommastellen
* 0.0000 = 4 Nachkommastellen
* ,000 = zeigt Tausendertrennzeichen und keine Nachkommastellen
* ,000.00 = zeigt Tausendertrennzeichen und 2 Nachkommastellen
* 0.#### = Maximal 4 Nachkommastellen, Nullen rechts werden weggelassen
* ,000.00 € = Schreibt die Zahl und nach der Zahl noch €etwa 25.132,40 €.

#### integer

| Parameter | Beschreibung |
| --- | --- |
| true | Die Zahl ist eine Ganzzahl. |
| false (Standard) | Das System verwendet Dezimalzahlen (im Standard mit zwei Nachkommastellen, sofern nicht anders definiert). |

**Beispiel**

```auto
form.down('numberField1').integer = true;
```

Sie können diesen Parameter nachträglich ändern.

#### increment

Definiert die Schrittzahl, die das System hoch- oder runterzählt, wenn ein Benutzer beim Eingabefeld auf die Pfeile klickt oder die Pfeiltasten verwendet (Standard: 1).

Sie können beliebige dezimale Werte definieren, auch negative (kehrt die Richtung um).

**Beispiel**

```auto
form.down('numberField1').increment = 0.5;
```

Sie können diesen Parameter nachträglich ändern.

### Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gelten die folgenden Events.

#### precisionChanged

Löst aus, wenn sich der Parameter [precision](#precision) ändert.

Das System übergibt als Parameter den neuen Wert von *precision*.

#### integerChanged

Löst aus, wenn sich der Parameter [integer](#integer) ändert.

Das System übergibt als Parameter den neuen Wert von *integer*.

#### formatChanged

Löst aus, wenn sich der Parameter [format](#format) ändert.

Das System übergibt als Parameter den neuen Wert von *format*.

#### incrementChanged

Löst aus, wenn sich der Parameter [increment](#increment) ändert.

Das System übergibt als Parameter den neuen Wert von *increment*.

### Den Taschenrechner verwenden

* * *

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.8

Der Taschenrechner (über den Parameter [calculator](#calculator) steuerbar) erscheint rechts neben dem entsprechenden Label / Eingabefeld in Form des Symbols ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAWCAYAAADafVyIAAAA70lEQVRIDd1Vuw2DQAy96bILE1AwRpagS0MRIVGlpKY3dAhWQC9yIAGdbYEUkyLFFT4sv499OEzThHEc0XUdiMjtcE2uHfq+dysaExyGASG+9IzZFQOgwTUrEJICIXugZuvKao6TAmnJVio5isUGQI2Ui79OhRsR6vz+AbjkDYhkjqbeAFgZz2w3jN+KNqrWHDkkNoAiV2O4d2cDLJ6v7BbPfRRIf517oEyI7xTJZu15bX23e3Buk0+36PQm/8VDE01WHprIkdN3eIrkQ5PFtFE9DCB/194AB+yIFbRt+4OVyYuZ9zKjxQy+iXkfc+0n91wRHhjEtlgAAAAASUVORK5CYII=).

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/82bee1c0-357b-11ec-86a3-005056aa0ecc)

```auto
OCR: samples, numbers, sample.js, Test, Lesen, Schreiben, Integer, Double, Wert, setzen, Eingabe, Zahl, Geben Sie eine Zahl ein, Nachkommastelle, Text
```

Anzeige des Taschenrechners

#### Eingabemöglichkeiten

Geben Sie in das Feld daneben (hier: Nummer 1) eine Zahl ein und klicken Sie auf das Symbol, übernimmt das System die Zahl direkt in den Taschenrechner:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/0e3bce20-357c-11ec-86a3-005056aa0ecc)

```auto
OCR: samples, numbers, sample.js, Test, Lesen, Schreiben, Integer, Double, Wert, setzen, Eingabe, Zahl, Geben Sie eine Zahl ein, Nachkommastelle, Text
```

Übernommene Zahl in Taschenrechner

Addieren Sie etwa zur 55 die Zahl 10 hinzu und klicken auf *Übernehmen*, setzt das System das Ergebnis automatisch in das Feld daneben:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/d1448490-357f-11ec-86a3-005056aa0ecc)

```auto
OCR: samples, numbers, sample.js, Test, Lesen, Schreiben, Integer, Double, Wert setzen, Eingabe, Zahl, Nachkommastelle, Text
```

Addierte Zahl im Taschenrechner

#### Bearbeitungsmöglichkeiten

Im Taschenrechner existieren neben den angezeigten Zahlen und Zeichen folgende Bearbeitungsmöglichkeiten in Form von Symbolen.

| Symbol | Beschreibung | Beispiel |
| --- | --- | --- |
|  | Löscht die angezeigte Ziffer. | Aus 55 wird 5. |
|  | Löscht alle bereits getätigten Eingaben. | – |
|  | Erzeugt ein Eingabefeld für Ziffern /Zeichen. Die Ziffern / Zeichen können Sie entweder direkt eingeben oder kopierte Zahlen und Zeichen einfügen, um so eine direkte Berechnung durchzuführen. Klicken Sie auf Übernehmen, damit das System das Ergebnis automatisch ausrechnet und es in das Feld setzt. | – |

#### Bedienung per Tastatur

| Abgebildetes Zeichen im Taschenrechner | Taste auf Tastatur |
| --- | --- |
| % | % |
| C | c |
| < | Backspace |
| / | / (Ziffernblock) |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 0 | 0 |
| +/- | p |
| , | . oder , |
| \= | \= oder Enter Enter schließt den Taschenrechner und übernimmt den Wert. |
| ESC | ESC Schließt den Editor, ohne den Wert zu übernehmen. |
|  | e Aktiviert das Eingabefeld für Ziffern und Zeichen. Enter schließt das Feld wieder und übernimmt die Ziffern / Zeichen, ohne den Taschenrechner zu schließen. |

#### Beispiele für Rechenoperatoren

Das System führt jeden Rechenoperator sofort auf die Eingabe aus (keine Punkt- vor Strichrechnung).

| Eingabe in Taschenrechner | Beschreibung | Ergebnis |
| --- | --- | --- |
| 16 +19% | Zählt 19 % zu 16 hinzu. | 19.04 |
| 300 \* 19% | Rechnet 19 % von 300. | 57 |
| 200 - 19% | Zieht 19 % von 200 ab. | 162 |
| 119 / 1.19 | Rechnet 119 Brutto in Netto (Brutto -> Netto - MwSt-Satz = 19 %). | 100 |
| 100 - 200\*2 | Rechnet 100–200 und nimmt dann \*2. | \-200 |
| 200 / 10% | 200 / (10 % -> 0,1) = 200/0.1 = 2000 | 2000 |
| 123/0 | Teilt 123 durch 0. | Bei Klick auf = erscheint eine Fehlermeldung. Bei Klick auf Enter übernimmt das System den Wert 0 in das Eingabefeld. |

## agorum.composite.form.element.objectPicker

Dieses Element stellt ein Text-Eingabefeld mit einer Schaltfläche zur Auswahl eines *agorum core*\-Objekts dar. Sie können dabei entweder eine Ordnerauswahl oder die Suche verwenden.

*agorum.composite.form.element.objectPicker* erbt alle Grundeigenschaften von [element](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  elements: [
    {
      type: 'agorum.composite.form.element.objectPicker',
      // value: '/agorum/roi/Files/Demo',
      name: 'picker1',
      label: 'Objektauswahl',
      // displayProperty: 'anyFolderPath',  // UUID, name, ID, anyFolderPath
      // valueProperty: 'ID',               // UUID, name, ID, anyFolderPath
      pickerType: 'search',                 // search, folder
      // baseFolder: '/agorum',             // start folder
      // searchParameters: {}               // parameters for search
      pickerWidth: 1000,                    // width of picker window
      pickerHeight: 1000                    // height of picker window
    }
  ]
});
form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### pickerType

| Wert | Beschreibung |
| --- | --- |
| folder | Öffnet eine Ordnerübersicht zur Auswahl. |
| search | Öffnet die Suche zur Auswahl. |

**Beispiel**

```auto
form.down('picker1').pickerType = 'search';
```

* Sie können diesen Parameter nachträglich ändern.
* Das System übernimmt bei *pickerType=folder* den Wert aus dem Eingabefeld und versucht, den Ordner an dieser Stelle zu öffnen.

#### pickerWidth, pickerHeight

Definiert optional die Breite und Höhe des Explorer-/Suchfensters, wenn ein Benutzer auf die Schaltfläche zum Auswählen klickt.

* Das System definiert die optimale Breite und Höhe automatisch, wenn Sie diesen Parameter nicht angeben.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('picker1').pickerWidth = 800;
form.down('picker1').pickerHeight = 600;
```

#### valueProperty

Definiert das Attribut, das das System zurückgibt, wenn ein Benutzer ein Objekt auswählt.

* Der Wert steht als *value* des Elements zur Verfügung.
* Sie können diesen Parameter nachträglich ändern.
* Sie können alle *agorum core*\- Attribute verwenden.

**Beispiele**

* name
* UUID (Standard)
* ID
* anyFolderPath
* description

```auto
form.down('picker1').valueProperty = 'UUID';
```

#### displayProperty

Definiert das Attribut, das das System zur Anzeige verwendet.

* Sie können diesen Parameter nachträglich ändern.
* Sie können alle *agorum core*\-Attribute verwenden.

**Beispiele**

* name
* UUID
* ID
* anyFolderPath (Standard)
* description

```auto
form.down('picker1').displayProperty = 'anyFolderPath';
```

Wenn *displayProperty* kein ID-Attribut ist, deaktiviert sich die Eingabe des Felds. Der Benutzer kann dann nur noch über den Picker ein Objekt wählen.

ID-Attribute sind:

* ID
* UUID
* anyFolderPath

Die Anzeige bei *anyFolderPath* ist abhängig von der Einstellung *baseFolder*.

#### baseFolder

Definiert optional den Startordner, ab dem der Baum der Ordnerauswahl erscheint.

* Die Startordner der aktiven *agorum core* *smart assistant-*Konfiguration gelten, wenn Sie nichts angegeben.
* Der Parameter beeinflusst den Startordner bei *pickerType='folder'* und die Suche bei *pickerType='search'*.
* Bei *'folder'* erscheint der Verzeichnisbaum erst ab diesem Ordner.
* Bei der Suche sucht das System nur Objekte unterhalb dieses Ordners.
* Die Angabe von *baseFolder* hat Einfluss auf die Anzeige, wenn Sie *displayProperty='anyFolderPath'* verwenden.
* Das System wählt bei Auswahl eines Objekts den bestmöglichen Startordner und übersetzt diesen. Die interne Ordnerangabe */agorum/roi/Files/Demo* führt etwa zu *Dateien/Demo*.
* Das System beachtet bei der Eingabe in das Feld die baseFolder-Einstellungen. Der Benutzer kann nur das eingeben, was laut Anzeige funktioniert. Intern legt das System dabei *value* stets korrekt gemäß *valueProperty* ab (im Standard als UUID).
* Eingaben, die nicht korrekt sind, invalidieren das Eingabefeld mit dem Text *Objekt nicht gefunden*.
* Sie können diesen Parameter nachträglich ändern.

**Hinweise**:

* Das System mischt den *baseFolder* mit der grundlegenden Suchkonfiguration. D. h. die Suchkonfiguration muss so eingestellt sein, dass der in *baseFolder* angegebene Startordner in der Suchkonfiguration enthalten ist.

* Der zuletzt gewählte Name gilt (aus der Suche), wenn Sie bei *searchParameters* keinen *settingName* mitgeben.

* Definieren Sie entweder *settingName*, etwa mit *ac\_all*, oder geben Sie eine eigene Konfiguration per *settings* mit (siehe [agorum.composite.search.filterResultDetails](#)).

**Beispiel**

```auto
form.down('picker1').baseFolder = '/agorum/roi/workspace';
```

#### searchParameters

Definiert optional und nur bei *pickerType=search* die komplette Konfiguration der Suche und gibt sie mit, um die Suche zu steuern.

* Sie können diesen Parameter nachträglich ändern.
* Alle Einstellungen von [agorum.composite.acic](#) und [agorum.composite.search.filterResultDetails](#) gelten.

**Beispiel**

```auto
form.down('picker1').searchParameters = {
  query: 'hallo',
  additionalBaseQuery: 'isfolder:true',
  filterCollapsed: true,
  settingName: 'inbox-all',
  detailsWidget:  {
    type: 'agorum.composite.details',
    width: 600
  }
};
```

* Das System lädt ab *agorum core* 9.2.3 im Standard für die Suche das Widget *agorum.composite.acic*.
* Sie können der Suche hier keine eigene Filterkonfiguration mitgeben, jedoch den widget-type.

**Eigenen Filter mitgeben**

```auto
form.down('picker1').searchParameters = {
  type: 'agorum.composite.search.filterResultDetails',
  filter: [ ... jetzt kann ein Filter definiert werden ... ],
  // ... weitere Parameter für filterResultDetails
};
```

#### selectors

**Ab welcher Version verfügbar?**• *agorum core* 9.2.3

Definiert Selektoren, die prüfen, ob das gewählte Objekt mit dem definierten Selektor übereinstimmt.

Die Schaltfläche *Ok* zur Übernahme des Objekts aktiviert sich erst, wenn einer der Selektoren greift (Beispiele für Selektoren siehe [Selektoren](#)).

**Beispiel**

```auto
// Entweder es ist ein Ordner oder der Name lautet Demo:
form.down('picker1').selectors = [
  '[isFolder=true]',
  '[name=Demo]'
];
```

### Events

* * *

Alle Events in  [element](#) gelten

## agorum.composite.form.element.objects

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.8

Dieses Element stellt ein Fenster zum Wählen von Objekten in *agorum core* dar. Durch das Wählen der Objekte stellen Sie eine Liste zusammen, die Sie etwa für einen Workflow verwenden können. Die gewählten Objekte fügen Sie über eine Ordnerstruktur, eine Suche oder per Drag-and-drop in das Auswahlfenster ein.

*agorum.composite.form.element.objects* erbt alle [grundlegenden Eigenschaften](#) von element.

Einen Workflow zu diesem Element finden Sie unter [Workflow „Attachments über ein UI hinzufügen und entfernen“](#).

### Beispiel einer Oberfläche

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/443e22a0-3e3e-11ec-8fd4-005056aa0ecc)

```auto
OCR: form.element.objects.js, Test, Name, Beschreibung, Betreff, Zuletzt von, 1-0, von
```

Oberfläche zum Wählen von Objekten

#### Skript zur Oberfläche

```auto
let aguila = require('common/aguila');

let form = aguila.create({

  type: 'agorum.composite.form.basic',
  width: 800,
  height: 600,
  labelPosition: 'top',
  elements: [
    {
      type: 'agorum.composite.form.element.objects',
      name: 'objects',
      height: 200,
      listConfig: 'Standard',
      allowedNames: [ // ab agorum core 10.2.2
        '\\.pdf$',
        '\\.doc$',
        '\\.docx$'
      ],
      // allowMove: true, // ab agorum core 10.2.2
      // listReadOnly: true,
      // hideRemove: true,
      /*
      texts: {
        selectSearch: 'Ordner suchen',
        selectFolder: 'Ordner auswählen',

        removeSelection: 'Ordner löschen',
        upload: 'Lokale Dateien hochladen' // ab agorum core 10.2.2
      },
      */
      /*
      icons: {
        selectSearch: 'aguila-icon https',
        // selectFolder: 'aguila-icon https',
        // removeSelection: 'aguila-icon https',
        // upload: 'aguila-icon file_upload' // ab agorum core 10.2.2
      },
      */
      searchConfig: {
        additionalBaseQuery: 'isfolder:true',
        filterCollapsed: true,
        settingName: 'inbox-all',
        detailsWidget:  {
          type: 'agorum.composite.details',
          width: 600
        },
        //pickerWidth: 800,
        //pickerHeight: 600

      },
      folderConfig: {
        selectors: [
        '[isFolder=true]',
        '[name=Demo]'

        ],
        startFolder: '/agorum/roi/workspace',
        // baseFolder: '/',
        //pickerWidth: 500,

        //pickerHeight: 400

      },
      uploadConfig: { // ab agorum core 10.2.2
        browse: true, // Button für lokalen Dateiupload anzeigen
        drop: true // Drag-and-drop auf die Liste ermöglichen
      }
    }
  ]
});

form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### form

Legt das Aussehen des Auswahlfensters fest.

Sie können das zu verwendende Design, die Höhe, Breite und die Labelposition angeben.

**Beispiel**

```auto
let form = aguila.create({

  type: 'agorum.composite.form.basic',

  width: 800,

  height: 600,

  labelPosition: 'top',
```

#### type

Definiert, dass es sich um ein Element handelt.

Sie können die Anzeige des Fensters mit *name* und *height* anpassen.

**Beispiel**

```auto
type: 'agorum.composite.form.element.objects',

name: 'objects',

height: 200,
```

#### listReadOnly

| Wert | Beschreibung |
| --- | --- |
| true | Drag-and-drop und Entfernen sind NICHT möglich. |
| false | Drag-and-drop und Entfernen sind möglich. |

#### hideRemove

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Schaltfläche Löschen ein. |
| false | Blendet die Schaltfläche Löschen aus. |

#### allowMove

**Ab welcher Version verfügbar?**

• *agorum core* 10.2.2

| Wert | Beschreibung |
| --- | --- |
| true | Blendet zwei Schaltflächen ein, mit denen der Benutzer die markierten Objekte innerhalb der Liste nach oben oder unten verschieben kann. |
| false | Blendet die Schaltflächen aus. |

#### pickerWidth, pickerHeight

Definiert optional die Breite und Höhe des Suchfensters oder der Ordnerübersicht, wenn ein Benutzer auf die Schaltfläche zum Wählen klickt.

* Das System definiert automatisch eine optimale Breite und Höhe, wenn Sie keine Werte angeben.
* Sie können die Breite und Höhe des Suchfensters unabhängig von der Breite und Höhe der Ordnerübersicht einstellen.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
pickerWidth = 800;
pickerHeight = 600;
```

#### allowedNames

**Ab welcher Version verfügbar?**

• *agorum core* 10.2.2

Definiert reguläre Ausdrücke erlaubter Namen als String.

* Sie müssen die regulären Ausdrücke codieren ( *\\* mit etwa *\\\\*).
* Das System vergleicht die regulären Ausdrücke Case-sensitiv.
* Das System gibt eine entsprechende Meldung aus und formt das Element um in *valid=false*, wenn eine hinzugefügte Datei hinzukommt und keines der Suchmuster von *allowedNames* passt.

**Beispiel**

```auto
allowedNames: [
  '\\.pdf$',
  '\\.doc$',
  '\\.docx$'
],
```

#### texts

Passt optional den Text an, der erscheint, sobald die Maus über eine der folgenden Schaltflächen fährt:

* Suche
* Ordner-Auswahl
* Löschen
* Upload

**Beispiel**

```auto
texts: {

   selectSearch: 'Ordner suchen',

   selectFolder: 'Ordner auswählen',

   removeSelection: 'Ordner löschen',
​​​​​​   upload: 'Lokale Dateien hochladen'
```

#### icons

Passt optional die Symbole der folgenden Schaltflächen an:

* Suche
* Ordner-Auswahl
* Löschen
* Upload

Zum Anpassen der Symbole in der Oberfläche siehe [Symbole anpassen](#SymboleAnpassen).

**Beispiel**

```auto
icons: {

  selectSearch: 'aguila-icon https',

  selectFolder: 'aguila-icon add',

  removeSelection: 'aguila-icon https',
  upload: 'aguila-icon file_upload'
```

#### searchConfig

Definiert optional die Parameter für die Suche nach Elementen, die ein Benutzer zur Liste hinzufügen kann.

* Die Schaltfläche zum Suchen erscheint nicht, wenn Sie *searchConfig* nicht definiert haben.
* Beispiel siehe [Beispiel einer Oberfläche](#beispiel)

Zu *searchConfig* existieren weitere Parameter:

***additionalBaseQuery***

| Wert | Beschreibung |
| --- | --- |
| isfolder:true | Der Benutzer darf nur nach der angegebenen Objektart suchen. |
| isfolder:false | Der Benutzer darf nach allem außer der angegebenen Objektart suchen. |

***filterCollapsed***

| Wert | Beschreibung |
| --- | --- |
| true | Blendet den Filter auf der linken Seite ein. |
| false | Blendet den Filter auf der linken Seite aus. |

***settingName***

Definiert, welcher Filter bei der Suche zuerst erscheint.

Der zuletzt verwendete Filter des Benutzers erscheint als Erstes, wenn Sie nichts angeben.

**Tipp**: Verwenden Sie die Funktion [Search query builder](#) in der Kopfleiste, um den *settingName* Ihrer *agorum core information center*\-Filterkonfigurationen zu erhalten.

Beispiel:

```auto
settingName: 'inbox-all',
```

***detailsWidget***

Passt die Detailansicht auf der rechten Seite an.

```auto
detailsWidget:  {

  type: 'agorum.composite.details', // Typ der Detailansicht

  width: 600 // Breite der Detailansicht
},
```

***pickerWidth, pickerHeight***

Definiert optional die Breite und Höhe des Suchfensters oder der Ordnerübersicht, wenn ein Benutzer auf die Schaltfläche zum Wählen klickt.

* Das System definiert automatisch eine optimale Breite und Höhe, wenn Sie keine Werte angeben.
* Sie können die Breite und Höhe des Suchfensters unabhängig von der Breite und Höhe der Ordnerübersicht einstellen.
* Sie können diesen Parameter nachträglich ändern.

Beispiel:

```auto
pickerWidth = 800;
pickerHeight = 600;
```

#### folderConfig

Definiert die Parameter für die Auswahl einer Datei aus der Ordner- / Baum-Auswahl.

* Die Schaltfläche für die Ordner-Auswahl erscheint nicht, wenn Sie *searchConfig* nicht definiert haben.
* Der Parameter beeinflusst den Startordner bei *folderConfig* und bei *searchConfig*`.`

* Bei *'folder'* erscheint der Verzeichnisbaum erst ab diesem Ordner.
* Das System beachtet bei der Eingabe in das Feld die baseFolder-Einstellungen. Der Benutzer kann nur das eingeben, was laut Anzeige funktioniert.
* Das System wählt bei Auswahl eines Objekts den bestmöglichen Startordner und übersetzt diesen. Die interne Ordnerangabe */agorum/roi/Files/Demo* führt etwa zu *Dateien/Demo*.
* Eingaben, die nicht korrekt sind, invalidieren das Eingabefeld mit dem Text *Objekt nicht gefunden*.
* Sie können diesen Parameter nachträglich ändern.
* Beispiel siehe [Beispiel einer Oberfläche](#beispiel)

**Hinweise**:

* Der zuletzt gewählte Name gilt (aus der Suche), wenn Sie bei *searchParameters* keinen *settingName* mitgeben.

* Definieren Sie entweder *settingName*, etwa mit *ac\_all*, oder geben Sie eine eigene Konfiguration per *settings* mit (siehe [agorum.composite.search.filterResultDetails](#)).

Zu *folderConfig* existieren weitere Parameter:

***pickerWidth, pickerHeight***

Definiert optional die Breite und Höhe des Suchfensters oder der Ordnerübersicht, wenn ein Benutzer auf die Schaltfläche zum Wählen klickt.

* Das System definiert automatisch eine optimale Breite und Höhe, wenn Sie keine Werte angeben.
* Sie können die Breite und Höhe des Suchfensters unabhängig von der Breite und Höhe der Ordnerübersicht einstellen.
* Sie können diesen Parameter nachträglich ändern.

Beispiel:

```auto
pickerWidth = 800;
pickerHeight = 600;
```

***selectors***

Definiert [Selektoren](#) für die Prüfung, ob das gewählte Objekt mit den Selektoren übereinstimmt.

Die Schaltfläche *Ok* zur Übernahme des Objekts aktiviert sich erst, wenn einer der Selektoren greift.

Beispiel:

```auto
selectors: [

'[isFolder=true]',

'[name=Demo]'

],
```

***startFolder***

Definiert, in welchem Ordner Sie sich befinden, wenn sich der Picker öffnet.

Beispiel:

```auto
startFolder: '/agorum/roi/workspace',
```

***baseFolder (optional)***

Definiert den Basisordner, ab dem der Baum beginnt.

* Die Anzeige ab dem Basisordner gilt, wenn Sie *baseFolder* angeben.
* Wenn Sie nichts angeben, gelten die Startordner der aktiven *agorum core smart assistant*\-Konfiguration.
* Die Angabe von *baseFolder* hat Einfluss auf die Anzeige, wenn Sie *displayProperty='anyFolderPath'* verwenden.

**Hinweise**:

* Das System mischt den *baseFolder* mit der grundlegenden Suchkonfiguration. D. h. die Suchkonfiguration muss so eingestellt sein, dass der in *baseFolder* angegebene Startordner in der Suchkonfiguration enthalten ist

* Der *baseFolder* muss innerhalb des angegebenen Bereichs des *startFolders* liegen, wenn Sie einen *startFolder* angegeben haben.

Beispiel:

```auto
baseFolder = 'home:MyFiles';
```

#### uploadConfig

**Ab welcher Version verfügbar?**

• *agorum core* 10.2.2

| Wert | Beschreibung |
| --- | --- |
| browse: true | Blendet die Schaltfläche zum Hochladen von Dateien ein. |
| browse: false (Standard) | Blendet die Schaltfläche zum Hochladen von Dateien aus. |
| drop: true | Ermöglicht Drag-and-drop auf die Liste. |
| drop: false | Ermöglicht KEIN Drag-and-drop auf die Liste. |

#### selectors

Definiert [Selektoren](#) für die Prüfung, ob das gewählte Objekt mit den Selektoren übereinstimmt.

Die Schaltfläche *Ok* zur Übernahme des Objekts aktiviert sich erst, wenn einer der Selektoren greift.

**Beispiel**

```auto
selectors: [

'[isFolder=true]',

'[name=Demo]'

],
```

#### detailsWidget

Passt die Detailansicht auf der rechten Seite an.

```auto
detailsWidget:  {

  type: 'agorum.composite.details', // Typ der Detailansicht

  width: 600 // Breite der Detailansicht
},
```

### Symbole anpassen

* * *

1. Öffnen Sie im Hauptmenü über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACQAAAAWCAYAAACosj4+AAAAp0lEQVRIDe2WPQqAMAyFczyv4nG8i4O7c+9QuvcMT4JESmjQQdMKLYQmWd7H6w8hAMg5I6WEGGOTYG1m4EWctALRusxCLZ3RQMxCutm6/hFQ2DHNK+g2NizhvcdgO9QdkP4CLsB3HdF31nZoAJ330MUhIoIOfVRSuwCxWAkk4rXdDUigahBlzxWoFLbyAWQ5I/3nDul/6aN6AMnRWHt/A1p3I2xvQ/4BfuHjRzE1j3IAAAAASUVORK5CYII=) **agorum core template manager** ​​​​​.
2. Wählen Sie **Icon selection**.
3. Klicken Sie das gewünschte **Symbol** an.
4. Kopieren Sie den **Text**, der oben im Feld erscheint.
5. Fügen Sie den kopierten **Text** anstelle der momentan verwendeten Symbol-Bezeichnung in das Skript ein.

### Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gilt das folgende Event.

#### selectionChanged

Löst aus, wenn ein Benutzer ein oder mehrere Objekte in der Liste wählt.

Sie erhalten deren UUID in einem Array zurück.

**Beispiel 1**

Dieses Skript erzeugt ein einfaches Widget mit einer Datei-Liste des persönlichen Verzeichnisses des aktuellen Benutzers und gibt es zurück.

```auto
let aguila = require('common/aguila');
let objects = require('common/objects');

let folder = objects.find('home:/');

let attachments = aguila.create({
  name: 'attachments',
  type: 'agorum.composite.form.element.objects',
  id: folder.ID,
});

attachments;
```

**Beispiel 2**

Dieses Skript reagiert auf alle Events einer Explorer-Liste und protokolliert es in der Konsole.

```auto
let aguila = require('common/aguila');
let objects = require('common/objects');

let folder = objects.find('home:/');

let attachments = aguila.create({
  name: 'attachments',
  type: 'agorum.composite.form.element.objects',
  id: folder.ID,
  pageSize: 10,
});

/**
 * Listen to all events and print the values to the console
 */
attachments.on('valueChanged', value => {
  console.log('Valued Changed', value);
});

attachments.on('configChanged', configName => {
  console.log('Config Changed', configName);
});

attachments.on('groupChanged', group => {
  console.log('Group Changed', group);
});

attachments.on('idChanged', id => {
  console.log('ID Changed', id);
});

attachments.on('idsChanged', ids => {
  console.log('IDs Changed', ids);
});

attachments.on('pageChanged', page => {
  console.log('Page Changed', page);
});

attachments.on('pageSizeChanged', pageSize => {
  console.log('Page Size Changed', pageSize);
});

attachments.on('queryChanged', queryString => {
  console.log('Query Changed', queryString);
});

attachments.on('sortChanged', sort => {
  console.log('Sort Changed', sort);
});

attachments.on('selectionChanged', selection => {
  console.log('Selection Changed', selection);
});

attachments;
```

## agorum.composite.form.element.picker

Dieses Element stellt ein Text-Eingabefeld dar und zeigt ein Widget an, um weitere Informationen zu laden. Die Trigger-Schaltfläche neben dem Eingabefeld öffnet ein Widget.

*agorum.composite.form.element.picker* erbt alle grundlegenden Eigenschaften von [element](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

// the widget that should show, when clicking on the trigger
let pickerWidget = {
  type: 'agorum.vbox',
  width: 400,
  height: 400,
  items: [
    {
      type: 'agorum.textInput',
      label: 'A text',
      name: 'aText'
    },
    {
      type: 'agorum.button',
      text: 'Set value',
      name: 'aButton'
    }
  ]
};

// the form
let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',
  readOnly: true,
  showError: 'always',
  docked: {
    top: {
      type: 'agorum.toolbar',
      items: [
        {
          type: 'agorum.button',
          text: 'Switch readOnly',
          name: 'switchReadOnly'
        }
      ]
    }
  },
  elements: [
    {
      type: 'agorum.composite.form.element.picker',
      name: 'pickerField1',
      value: {
        value: 'This is a value',
        text: 'This is a text'
      },
      loose: false,
      label: 'Pickerfield 1',
      attached: pickerWidget,
      validation: [
        {
          required: true
        }
      ]
    }
  ]
});

let pf = form.down('pickerField1');
let switchReadOnly = form.down('switchReadOnly');

function initPickerEvents() {
  let pwText = form.down('aText');
  let aButton = form.down('aButton');

  // when the picker is in readOnly mode, there is no button, cause the
  // pickerWidget is not loaded
  if (aButton) {
    aButton.on('clicked', () => {
      form.value = {
        pickerField1: {
          value: pwText.value,
          text: pwText.value
        }
      };

      pf.fire('collapse');
    });
  }
}

// init picker events
initPickerEvents();

form.on('readOnlyChanged', () => {
  // when the pickerField changes to readOnly, reinit the events, cause the picker widget is recreated
  initPickerEvents();
});

pf.on('trigger', expanded => {
  console.log('trigger', expanded);
});

pf.on('expanded', () => {
  console.log('expanded');
});

pf.on('collapsed', () => {
  console.log('collapsed');
});

switchReadOnly.on('clicked', () => {
  form.readOnly = !form.readOnly;
});

form.on('valueChanged', v => {
  console.log('valueChanged', v);
});

form.on('validChanged', v => {
  console.log('validChanged', v);
});

form;
```

* Das Widget (hier *pickerWidget*) lädt nur dann, wenn das Element im Bearbeitungsmodus (*readOnly = false*) ist.
* Wechselt ein Benutzer zwischen der Bearbeitung und der Ansicht, verwirft das System das *pickerWidget* und die Events, die darauf gebunden sind.
* Das obige Beispiel reagiert auf *readOnlyChanged* und bindet die Events neu.

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### value

Definiert den Wert des Elements.

* Der Wert muss *text* und *value* enthalten.
* Sie müssen den Wert genau so übergeben, wie Sie ihn gesetzt haben.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('pickerField1').value= {
  text: 'Ein Text',
  value: 'Ein Wert'
};
```

#### attached

Übergibt das Widget, das erscheint, wenn ein Benutzer den Trigger anklickt.

* Dieser Parameter ist Pflicht.
* Sie können diesen Parameter nachträglich nicht ändern.
* Das übergebene Widget muss ein reines *aon* sein, kein erstelltes Widget.

**Beispiel**

```auto
// ...
{
  type: 'agorum.composite.form.element.picker',
  name: 'pickerField1',
  label: 'Pickerfield 1',
  attached: {
    type: 'agorum.vbox',
    width: 400,
    height: 400,
    items: [
      {
        type: 'agorum.textInput',
        label: 'A text',
        name: 'aText'
      },
      {
        type: 'agorum.button',
        text: 'Set value',
        name: 'aButton'
      }
    ]
  }
}
// ...
```

#### loose

| Wert | Beschreibung |
| --- | --- |
| true | Die Breite des pickerWidgets orientiert sich nicht automatisch an der Breite des Eingabefelds. Ein Benutzer kann die Breite manuell ändern. |
| false (Standard) | Die Breite des pickerWidgets orientiert sich automatisch an der Breite des Eingabefelds. |

#### disableTrigger

| Wert | Beschreibung |
| --- | --- |
| true | Deaktiviert das automatische Öffnen des pickerWidgets, sodass ein Benutzer die Steuerung manuell übernehmen kann. |
| false (Standard) | Aktiviert das automatische Öffnen des pickerWidgets. |

### Events (fire)

* * *

Ausgehende Events zum Element hin.

#### expand

Öffnet das Widget programmatisch (analog zum Klick auf den Trigger).

**Beispiel**

```auto
form.down('pickerField1').fire('expand');
```

#### collapse

Schließt das Widget programmatisch (analog zum Klick auf den Trigger).

**Beispiel**

```auto
form.down('pickerField1').fire('collapse');
```

### Events (on)

* * *

Elle Events in [element](#) gelten. Zusätzlich gelten die folgenden Events.

#### trigger

Löst aus, wenn ein Benutzer den Trigger anklickt, und gibt *true* (Widget wurde geöffnet) oder *false* (Widget wurde geschlossen) zurück.

**Beispiel**

```auto
form.down('pickerField1').on('trigger', expanded => {
  console.log('trigger', expanded);
});
```

#### expanded

Löst aus, wenn sich das Widget öffnet.

**Beispiel**

```auto
form.down('pickerField1').on('expanded', () => {
  console.log('expanded');
});
```

#### collapsed

Löst aus, wenn sich das Widget schließt.

**Beispiel**

```auto
form.down('pickerField1').on('collapsed', () => {
  console.log('collapsed');
});
```

#### key

Löst aus, wenn ein Benutzer eine Spezialtaste (alle Tasten außer Buchstaben / Zahlen) gedrückt hat, während sich der Tastaturfokus im Eingabefeld befindet, und gibt den Key-Code dieser Taste zurück.

**Beispiel**

Dieses Skript ermittelt die Key-Codes für die gewünschten Tasten.

```auto
form.down('pickerField1').on('key', number => {
  console.log('key number', number);
});
```

## agorum.composite.form.element.select

Dieses Element stell eine Auswahlbox zur Verfügung und unterstützt sowohl Einzel- als auch Mehrfachwerte.

*agorum.composite.form.element.select* erbt alle grundlegenden Eigenschaften von [element](#).

### Beispiel

* * *

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      type: 'agorum.composite.form.element.select',
      name: 'select1',
      label: 'Select 1',
      restricted: true,
      data: [
        {
          value: 'value1',
          text: 'Wert 1'
        },
        {
          value: 'value2',
          text: 'Wert 2'
        }
      ]
    },
    {
      type: 'agorum.composite.form.element.select',
      name: 'select2',
      label: 'Select 2',
      dataSource: 'MAIN_MODULE_MANAGEMENT/customers/D4wAddress/Data/d4w_address_data_country'
    }
  ]
});

form;
```

Dieses Beispiel verwendet am Ende die Standard-Datenquelle aus dem Address-Modul, um eine Länderauswahl (d4w\_address\_data\_country) anzuzeigen:

```auto
MAIN_MODULE_MANAGEMENT/customers/D4wAddress/Data/d4w_address_data_country
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten folgende Parameter.

#### placeholder

Definiert einen Platzhalter-Text für das select-Element mit einem einzelnen Wert (multi=false), den das System anzeigt, wenn das Element leer ist.

* Sie können diesen Parameter nicht für die Auswahl mehrerer Felder (multi=true) verwenden.
* Sie können diesen Parameter nachträglich ändern.

#### restricted

| Wert | Beschreibung |
| --- | --- |
| true | Erlaubt nur Werte aus der Datenquelle. |
| false (Standard) | Erlaubt das Eingeben von eigenen Werten, die nicht in der Datenquelle enthalten sind. |

**Beispiel**

```auto
form.down('select1').restricted = true;
```

#### multi

| Wert | Beschreibung |
| --- | --- |
| true | Ermöglicht die Auswahl mehrerer Werte (tokenbox). |
| false (Standard) | Ermöglicht die Auswahl eines einzelnen Werts. |

**Beispiel**

```auto
form.down('select1').multi = true;
```

Sie können diesen Parameter nachträglich ändern.

#### minChars

Definiert die Mindestanzahl einzugebender Zeichen, bevor das System in der Datenquelle sucht (Standard: 0).

* Das System verwendet den Wert der hinterlegten Datenquelle (dataSource), sofern vorhanden.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('select1').minChars = 2;
```

#### data

Definiert am Element eine Datenquelle.

* Der Aufbau besteht aus einem Array aus Einträgen, bestehend aus *value* und *text*, wobei *value* der Wert ist, der als Wert am Element sitzt und *text* zur Darstellung dient.
* Sie müssen entweder den Parameter *data* oder den Parameter [dataSource](#dataSource) setzen.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('select1').data = [
  {
    value: 'value1',
    text: 'Wert 1'
  },
  {
    value: 'value2',
    text: 'Wert 2'
  }
];
```

#### dataSource

Definiert eine in der MetaDb angelegte Datenquelle.

* Das System übernimmt bei Metadaten-Feldern die Datenquelle automatisch aus der Metadaten-Definition.
* Informationen zu Datenquellen siehe [Metadaten mit YML definieren (metadata.yml)](#) und [Beispiel-Datenquellen für DataHandler](#).

Die Datenquelle dient dazu, dem Benutzer aus einer Liste die richtigen Werte wählen zu lassen. Dabei ist der gewählte Wert (value) im Normalfall anders als der dem Benutzer angezeigte Wert (text). Das System zeigt etwa bei der Auswahl eines Benutzers den Benutzernamen an, aber der gewählte (hinterlegte) Wert ist die ID des Benutzers.Das Element *select* ist in der Lage, passend zum Wert den Text anzuzeigen. Dazu ist es notwendig, dass das System den Wert auch wieder zurückübersetzen kann, also vom Wert zum Text gelangt.Für die folgenden Standard-Datenquellen funktioniert dieser Vorgang automatisch:

* user-group (Auswahl für user, group oder beides: usergroup)
* csv
* search
* facet

* Ausnahmen bilden die Parameter [JavaScript](#javascript) und [jdbc](#jdbc).
* Sie müssen entweder den Parameter [data](#data) oder den Parameter *dataSource* setzen.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel 1 – eigene dataSource verwenden**

```auto
form.down('select1').dataSource = 'MAIN_MODULE_MANAGEMENT/customers/TESTPLUGIN/Data/test_datasource'
```

**Beispiel 2 – dataSource für user, group oder usergroup**

Die Einstellung, ob Sie Benutzer, Benutzergruppen oder beides wählen können, wird durch die *dataSourceParameter* bestimmt (siehe [DataHandler „user-group](#)“).

```auto
let objects = require('common/objects');
let groupname = 'GRP_myCompanyprefix_awesomeGroupname';

{
  type: 'agorum.composite.form.element.select',
  name: 'user',
  label: 'Select your User',
  dataSource: 'MAIN_MODULE_MANAGEMENT/customers/Standard/Data/user-group',
  dataSourceParameter: {
    searchUsers: true,   // default: false
    searchGroups: true,  // default: false

    //groupId: objects.find('group://' + groupname),  // only members within this group will be shown
  },
},
```

#### dataSourceParameter

Übergibt optional Parameter an den Datenquellen-Handler.

* Die Parameter kommen etwa bei einem JSHandler als *parameters* an.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('select1').dataSourceParameter = {
  param1: 'Wert 1',
  param2: 'Wert 2'
};
```

Im JavaScript-Handler können Sie folgendermaßen auf die Parameter zugreifen.

**Beispiel, wenn ein *agorum core smart assistant*\-Handler vorhanden ist**

```auto
acbasicarchive_aktearea.dataSourceParameter = {
  filter: {
    acbasicarchive_aktesection: value
  }
};
```

**Hinweis**: Bei csv-DataHandlern muss in der Spalte, nach der Sie filtern möchten, ein Wert enthalten sein, da das System die Filterung sonst nicht anwendet und die Zeile zurückgibt.

#### textIsValue

| Wert | Beschreibung |
| --- | --- |
| true | Text entspricht Wert, somit ist kein lookup-Handler notwendig. |
| false | Text ist ungleich Wert, somit ist ein lookup-Handler notwendig. |

**Beispiel**

```auto
form.down('select1').textIsValue = true;
```

Sie können diesen Parameter nachträglich ändern.

#### displayType

| Wert | Beschreibung |
| --- | --- |
| combo (Standard) | Erzeugt ein Auswahlmenü. |
| check | Stellt entweder Radiobuttons (multi=false) oder Checkboxen (multi=true) dar. Die Daten sind direkt wählbar, der Benutzer muss kein Auswahlmenü geöffnet haben.  Sie können hierdurch etwa durch einen DataHandler die Checkboxen definieren und müssen diese nicht einzeln bauen. Verwenden Sie check nur, wenn die Daten nicht durch Eingabe von Text gefiltert werden müssen oder die Datenmenge zu groß ist. |

**Beispiel**

```auto
let aon = {
  type: 'agorum.vbox',
  width: 300,
  items: [
    {
      type: 'agorum.composite.form.element.select',
      name: 'select2a',
      displayType: 'check',
      multi: true,
      // orientation: 'vertical',
      orientation: 'horizontal',
      data: [
        {
          text: 'text 1',
          value: 'value_1'
        },

        {
          text: 'text 2',
          value: 'value_2'
        }

      ]
    }
  ]
};
```

#### orientation

Steuert, wie das System die Checkboxen des Parameters [displayType](#displayType) darstellt.

Dieser Parameter funktioniert nur in Verbindung mit dem displayType *check*.

| Wert | Beschreibung |
| --- | --- |
| vertical (Standard) | Stellt die Checkboxen untereinander dar. |
| horizontal | Stellt die Checkboxen nebeneinander dar. |

#### dataSource: JavaScript

Für JavaScript-Datenquellen existiert eine spezielle Möglichkeit. Im Falle von lookup ruft das System diesen JavaScript-Handler auf, es lässt sich also nicht mit einer anderen Art von DataHandler für den lookup kombinieren.

Hier ruft das System den JS-Datahandler mit *parameters.lookup = true* auf. Das bedeutet, dass das System innerhalb des Skripts reagiert und den lookup durchführt.

**Beispiel**

```auto
/* global sc, query: true, parameters, command */

let objects = require('common/objects');

// only 'read' is supported
if (command !== 'read') {
  throw new Error('This data handler does not support the command "' + command + '"');
}

let parts = [
  'isfolder:true ${FOLDERPATH:/agorum/roi/Files}'
];

if (query && query.trim().length > 0) {
  if (parameters.lookup) {
    // lookup mode, search for uuid
    query = 'uuid:' + query;
  }
  else {

    // normal mode filter name by query
    query = '(name:(' + query.trim().split(' ').filter(f => f.trim().length > 0).join('* ') + '*))';
  }
}
else {
  query = '*';
}

parts.push(query);

objects
.query(parts.join(' '))
.limit(100)
.sort('name')
.search('name', 'uuid')
.rows
.map(function(row) {
  return {
    value: row.uuid,
    text: row.name
  };
});
```

* In dem obigen Beispiel führt das System eine Suche nach dem Ordnernamen ab */agorum/roi/Files* (Dateien) durch.
* Wählt ein Benutzer einen Ordner, speichert das System die UUID.
* Für ein lookup liefert das System als query die UUID und gibt den Namen des Ordners zurück.
* Das System liefert den *text* zu dem entsprechenden *value* (gegeben durch *query*) zurück, wenn *parameters.lookup = true* ist.
* Das System verwendet den DataHandler wie zuvor, wenn *lookup = false* ist.

#### jdbc

Sie müssen einen lookup-Handler definieren (siehe [Beispiel-Datenquellen für DataHandler](#)).

### Events

* * *

Alle Events in [element](#) gelten. Zusätzlich gelten folgende Events.

#### restrictedChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [restricted](#restricted).

#### multiChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [multi](#multi).

#### minCharsChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [minChars](#minChars).

#### dataChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [data](#data).

#### dataSourceChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [dateSource](#dataSource).

#### dataSourceParameterChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [dataSourceParameter](#dataSourceParameter).

#### textIsValueChanged

Löst aus, wenn sich die Eigenschaft ändert.

Das System übergibt als Parameter den neuen Wert von [textIstValue](#textIsValue).

## agorum.composite.form.element.splitGrid

Dieses Element stellt Positionen (Zeilen) in Listenform dar und erlaubt das Aufsplitten der Postionen, etwa für die Zuweisung von verschiedenen Kostenstelle bei der Kontierung.

Sie legen beim Erstellen einer *splitGrid*\-Oberfläche fest, welche Spalten (Felder) in der Oberfläche angezeigt werden und welche dieser Felder aufgesplittet werden. Dabei gibt es zwei Möglichkeiten, abhängig vom Typ des aufgesplitteten Felds:

* Zahlenbeträge können so aufgesplittet werden, dass sich die Gesamtsumme aus den aufgesplitteten Beträgen ergibt
* Textfelder können so aufgesplittet werden, dass die Beschreibung für jede aufgesplittete Zeile durch den Benutzer angepasst werden kann, etwa zum Eintragen unterschiedlicher Kostenstellen. Dabei kann der Wert der Ursprungsposition optional übernommen werden, wenn häufig keine Anpassung erforderlich ist.

**Achtung**: Sie benötigen zum Aufsplitten von Positionen mindestens ein eindeutiges Feld, das nicht aufgesplittet wird und nicht bearbeitet werden darf.

*agorum.composite.form.element.splitGrid* erbt alle grundlegenden Eigenschaften von [element](#).

### Unterschiede zwischen splitList und splitGrid

* * *

Die beiden Möglichkeiten zur Oberflächengestaltung, `agorum.composite.form.element.splitGrid` und `agorum.composite.form.element.splitList`, unterscheiden sich darin, wie Benutzer die Informationen anzeigen lassen und bearbeiten können.

| Verhalten | agorumcomposite.form.element.splitList | agorum.composite.form.element.splitGrid |
| --- | --- | --- |
| Anzeige von vielen Posten | limitierte Anzeige von Posten auf einer Seite, Blättern auf andere Seiten | Anzeige weiterer Werte durch Scrollen |
| Aufsplitten der Positionen | Aufsplitten in der Listenansicht | Aufsplitten in der Anzeige eines Postens, der durch Doppelklicken ausgewählt wird (Detailansicht) |
| Anzeige von Validierungshinweisen | Anzeige in der Listenansicht bei der Bearbeitung, keine Anzeige für die gesamte Liste | Anzeige in der Detailansicht bei der Bearbeitung, Hervorhebung in der Listenansicht bei fehlerhaften Einträgen |

**Tipp:** Sie können *splitList* meistens einfach durch *splitGrid* ersetzen, wenn Sie eine vorhandene *splitList* auf *splitGrid* umstellen wollen.

### Beispiel einer Oberfläche

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/0c1f4c40-0c41-11ef-85c8-005056aa0ecc)

```auto
OCR: 01,Position 1,10.00,100.00,1000.00,6.00,600.00,4353,4.00,400.00,4354,02,Position 2,20.00,50.00,1000.00,4356,01,Position 1,10.00,100.00,1000.00,6.00,600.00,4353,4.00,400.00,4354,02,Position 2,20.00,50.00,1000.00,4356,01,Position 1,10.00,100.00,1000.00,6.00,600.00,4353,4.00,400.00,4354,02,Position 2,20.00,50.00,1000.00,4356
```

Beispiel einer Oberfläche

#### Skript zur Oberfläche

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  type: 'agorum.composite.form.basic',
  name: 'form',
  labelPosition: 'top',
  elements: [
    {
      type: 'agorum.composite.form.element.splitGrid',
      name: 'splitGrid',
      disableSplit: false,
      showRowDelete: true,
      showAppend: true,
      copyDiffValues: false,
      template: [
        // Es muss mindestens ein festes Feld geben, das pro Position eindeutig ist, etwa eine Positionsnummer.
        {
          type: 'agorum.composite.form.element.text',
          label: 'Nummer',
          name: 'number',
          readOnly: true,
        },
        {
          type: 'agorum.composite.form.element.text',
          label: 'Beschreibung',
          name: 'description',
          readOnly: true,
        },
        {
          type: 'agorum.composite.form.element.number',
          label: 'Menge',
          name: 'quantity',
          // Der Wert dieser Spalte ergibt sich aus allen Summen der aufgesplitteten Werte dieser Spalte.
          split: 'sum',
        },
        {
          type: 'agorum.composite.form.element.number',
          label: 'Einzelpreis',
          name: 'net_price',
          readOnly: true,
        },
        {
          type: 'agorum.composite.form.element.number',
          label: 'Gesamtpreis',
          name: 'net_amount',
          readOnly: true,
          // Der Wert dieser Spalte ergibt sich aus allen Summen der aufgesplitteten Werte dieser Spalte.
          split: 'sum',
        },
        {
          type: 'agorum.composite.form.element.text',
          label: 'Kostenstelle',
          name: 'cost_center',
          // Der Wert dieser Spalte soll pro aufgesplitteter Position unterschiedlich sein.
          split: 'diff',
          validation: [
            {
              required: true,
            },
          ],
        },
      ],
    },
  ],
});

// Konsole vom Browser aufrufen, um Werte zu sehen
form.on('valueChanged', value => {
  console.log('values', value);
});

// Manuelle Erstellung von Testdaten
// Wichtig ist, dass die Bezeichnungen wie number / description dem name der splitGrid-Elementen entspricht.
// Dadurch können die Werte den entsprechenden Spalten zugeordnet werden.
// Die Namensgebung ist frei und kann beliebig angepasst werden.
setImmediate(() => {
  form.set('splitGrid.value', [
    {
      number: '01',
      description: 'Position 1',
      quantity: 10,
      net_price: 100,
      net_amount: 1000,
    },
    {
      number: '02',
      description: 'Position 2',
      quantity: 20,
      net_price: 50,
      net_amount: 1000,
    },
  ]);
});

form;
```

### splitGrid Parameter

* * *

Zusätzlich zu den Parametern von [element](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#/14e22220-e915-11e9-a3bc-005056aa0ecc/59fc0790-abdf-11ee-ab59-005056aa0ecc) können Sie folgende Parameter verwenden:

| Parameter | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| copyDiffValues | Steuert das Verhalten beim Aufsplitten von Positionen für Spalten, für die der split Parameter mit dem Wert diff gesetzt ist. Dient dazu, den Wert der Spalte, für die diff gesetzt ist, beim Aufsplitten in alle aufgeteilten Zeilen zu übernehmen. | Boolescher Wert, Standardwert: false |
| disableSplit | Blendet die Schaltfläche zum Splitten aus. | Boolescher Wert, Standardwert: false |
| label | Angezeigter Name (Label) der Grid-Liste. Optional. | Zeichenkette |
| readOnly | Dient zur Anzeige der Split-Liste im Lesemodus, wodurch das Aufsplitten der Positionen verhindert wird. | Boolescher Wert, Standardwert: false |
| showAppend | Blendet das Symbol + zum Hinzufügen von Zeilen in der Listenansicht und im Header der jeweiligen Position ein. OCR: Bitte gib mir den OCR-Text, den ich zusammenfassen soll. Ich werde dann: | Boolescher Wert, Standardwert: false |
| showRowDelete | Blendet das Symbol Zeile löschen in der Detailansicht ein, wodurch Benutzer komplette Positionen oder Aufteilungen löschen können. | Boolescher Wert, Standardwert: false |
| template | Definiert die Spalten einer Zeile. Darin enthalten sind form-Elemente oder aguila-Widgets. | Siehe template Parameter |

#### Parameter von form-Elementen in template

| Parameter | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| label | Angezeigter Name des Felds (der Spalte) | Zeichenkette |
| name | Eindeutiger Name | Hinweis: Die Spalte name darf nicht mit einem \_ (Unterstrich) beginnen. Diese Schreibweise ist ausschließlich für interne Zwecke reserviert. |
| readOnly | Dient zur Anzeige des Felds im Lesemodus, ohne dass eine Bearbeitung möglich ist. | Boolescher Wert, Standardwert: false Hinweis: Setzen Sie Spalten, die nicht gesplittet werden sollen, auf readOnly, um ungewollte Bearbeitung zu verhindern. |
| split | Legt fest, dass ein Feld gesplittet werden kann. Sie können Felder mit form-Element text oder number splitten. | 'sum': Der Wert dieser Spalte ergibt sich aus allen Summen der aufgesplitteten Werte dieser Spalte, etwa zur Aufteilung auf verschiedene Kostenstellen, ohne dass sich der Gesamtbetrag ändert. 'diff': Der Wert dieser Spalte soll pro aufgesplitteter Position unterschiedlich sein, etwa zur Angabe von verschiedenen Kostenstellen. |
| validation | Definiert die Validierung für dieses Feld. Sie benötigen die Validierung, wenn Sie nur vollständige Summen und die entsprechenden Kostenstellen akzeptieren möchten. Füllt ein Benutzer in der Bedienoberfläche beides nicht aus, wird eine Fehlermeldung ausgegeben. | validation: \[ { required: true } \] |

### splitGrid Events

* * *

Alle Events in [element](#) gelten.

## agorum.composite.form.element.splitList

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.8.

Dieses Element splittet Positionen. Das Splitten von Positionen setzen Sie für Rechnungen und die Kontierung, etwa für die Zuweisungen von verschiedenen Kostenstellen für eine Rechnungsposition.

*agorum.composite.form.element.splitList* erbt alle grundlegenden Eigenschaften von [element](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#/14e22220-e915-11e9-a3bc-005056aa0ecc/fed60ad0-929a-11e9-8702-005056aa0ecc).

### Beispiel: Oberfläche zum Aufteilen von Positionen

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/e0940020-3e34-11ec-8fd4-005056aa0ecc)

```auto
OCR: Nummer,split_list_11.js,Test,Beschreibung,Menge,Einzelpreis,Gesamtpreis,Kostenstelle,Position,Position,100,00,1000,00,600,00,200,00,200,00,50,00,1000,00,764,71,235,29
```

Oberfläche zum Aufteilen von Positionen

#### Funktionsweise der Oberfläche

Das folgende Video zeigt, dass eine Fehlermeldung auftritt, wenn der Hauptwert einer Position durch das Splitten nicht erreicht wird. Diese Fehlermeldung ist gewollt und tritt aufgrund des Parameters [validation](#validation) auf.

#### Skript zum Splitten von Positionen

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  type: 'agorum.composite.form.basic',
  name: 'form',
  labelPosition: 'top',
  elements: [
    {
      type: 'agorum.composite.form.element.splitList',
      name: 'splitList',
      disableSplit: false,
      showRowDelete: true,
      showAppend: true,
      template: [
        // Es muss mindestens ein festes Feld geben, das pro Position eindeutig ist, etwa eine Positionsnummer
        {
          type: 'agorum.composite.form.element.text',
          label: 'Nummer',
          name: 'number',
          readOnly: true
        },
        {
          type: 'agorum.composite.form.element.text',
          label: 'Beschreibung',
          name: 'description',
          readOnly: true
        },
        {
          type: 'agorum.composite.form.element.number',
          label: 'Menge',
          name: 'quantity',
          // Der Wert dieser Spalte ergibt sich aus allen Summen der aufgesplitteten Werte dieser Spalte
          split: 'sum'
        },
        {
          type: 'agorum.composite.form.element.number',
          label: 'Einzelpreis',
          name: 'net_price',
          readOnly: true
        },
        {
          type: 'agorum.composite.form.element.number',
          label: 'Gesamtpreis',
          name: 'net_amount',
          readOnly: true,
          // Der Wert dieser Spalte ergibt sich aus allen Summen der aufgesplitteten Werte dieser Spalte
          split: 'sum'
        },
        {
          type: 'agorum.composite.form.element.text',
          label: 'Kostenstelle',
          name: 'cost_center',
          // Der Wert dieser Spalte soll pro aufgesplitteter Position unterschiedlich sein
          split: 'diff',
          validation: [
            {
              required: true
            }
          ]
        }
      ]
    }
  ]
});

// Konsole vom Browser aufrufen, um Werte zu sehen
form.on('valueChanged', value => {
  console.log('values', value);
});

// Manuelle Erstellung von Testdaten
// Wichtig ist, dass die Bezeichnungen wie number / description dem name der splitListe-Elementen entspricht
// Dadurch können die Werte den entsprechenden Spalten zugeordnet werden.
// Die Namensgebung ist frei und kann beliebig angepasst werden.
setImmediate(() => {
  form.set('splitList.value', [
    {
      number: '01',
      description: 'Position 1',
      quantity: 10,
      net_price: 100,
      net_amount: 1000
    },
    {
      number: '02',
      description: 'Position 2',
      quantity: 20,
      net_price: 50,
      net_amount: 1000
    }
  ]);
});

form;
```

### Parameter

* * *

Alle Parameter in [element](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#/14e22220-e915-11e9-a3bc-005056aa0ecc/fed60ad0-929a-11e9-8702-005056aa0ecc) gelten. Zusätzlich gelten folgende Parameter.

#### labelPosition

| Wert | Beschreibung |
| --- | --- |
| top | Das Label ist über dem Feld. |
| left | Das Label ist links vom Feld. |

#### type

Definiert den type des Elements, etwa *agorum.composite.form.element.text.*

* Das System wählt automatisch das Text-Element, wenn Sie keinen *type* definieren.
* Das System ermittelt den *type* anhand der Metadaten-Definition, wenn *name* ein bekanntes Metadatum ist.

**Beispiel**

```auto
type: 'agorum.composite.form.element.text',
```

#### label

Definiert den Text / das Label vor dem Element*.*

**Beispiel**

```auto
label: 'Nummer',
```

#### name

Definiert die eindeutige Benennung des Elements.

**Beispiel**

```auto
name: 'number',
```

#### readOnly

Definiert optional, ob ein Element im Bearbeitungs- oder Ansichtsmodus ist.

| Wert | Beschreibung |
| --- | --- |
| false (Standard) | Das System legt den Bearbeitungs- oder Ansichtsmodus über die umliegende form. Das Element befindet sich im Bearbeitungsmodus, wenn keine form existiert. |
| true | Das Element ist immer im Ansichtsmodus, unabhängig vom Zustand der umliegenden form. |

#### split

Definiert optional, wie das System die Positionen aufteilt.

* Sie dürfen den Parameter in mindestens einer der Spalten nicht angeben. Dadurch erhalten Sie einen Anker (Kopfdaten), um die gesplitteten Informationen einer Position zuordnen zu können.
* Das System teilt die Positionen nicht auf, wenn Sie *split* nicht definieren, sondern setzt den Ursprungswert für jede betroffene Position.

| Wert | Beschreibung |
| --- | --- |
| sum | Teilt den Wert zwischen den Positionen anteilig auf. Das System prüft automatisch, ob die eingetragenen Werte der gesplitteten Positionen der Gesamtsumme entsprechen, wenn es sich dabei um eine Zahl handelt. Das System kopiert bei anderen Metadatentypen die ursprünglichen Einträge. split: 'sum' OCR: Gesamtpreis, 1000,00, 600,00, 200,00, 200,00, Gesamtpreis, 1000,00, 600,00, 200,00, 200,00 sum |
| diff | Die geteilten Positionen besitzen nach dem Splitten keinen Wert mehr, der Benutzer muss die unterschiedlichen Werte in der Bedienoberfläche manuell zuteilen. split: 'diff' OCR: Kostenstelle,1,2,Kostenstelle diff |

#### validation

Definiert die Validierung für das Element.

* Im Sonderfall von *required* hat die Definition auf dem Element selbst Vorrang gegenüber der [Definition](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#/14e22220-e915-11e9-a3bc-005056aa0ecc/e62b4990-92a0-11e9-8702-005056aa0ecc) *validation* auf der *form*.

* Sie benötigen das Validieren, wenn Sie nur vollständige Summen und die entsprechenden Kostenstellen akzeptieren möchten. Füllt ein Benutzer in der Bedienoberfläche beides nicht aus, verhindert das System das Fortfahren und gibt eine Fehlermeldung aus.

**Beispiel**

```auto
  validation: [
            {
              required: true
            }
          ]
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/cee99ae0-221f-11ed-b442-005056aa0ecc)

```auto
OCR: Kostenstelle, Element, darf nicht leer sein
```

validation

#### disableSplit

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Schaltflächen zum Splitten und Zusammenführen aus. |
| false (Standard) | Blendet die Schaltflächen zum Splitten und Zusammenführen ein. |

#### console.log

Definiert, was die Konsole (F12) bei Ausführung anzeigt.

**Beispiel**

```auto
console.log('values', value);
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/f445f770-221f-11ed-b442-005056aa0ecc)

```auto
OCR: Elemente, Konsole, Filtern, Standardlevel, Problem, values, Object, ausgeblendet
```

console.log

#### showRowDelete

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Schaltfläche zum Löschen im Header der jeweiligen Position ein. |
| false (Standard) | Blendet die Schaltfläche zum Löschen im Header der jeweiligen Position aus. |

#### showAppend

| Wert | Beschreibung |
| --- | --- |
| true | Blendet die Schaltfläche zum Hinzufügen im Header der Liste ein. |
| false (Standard) | Blendet die Schaltfläche zum Hinzufügen im Header der Liste aus. |

#### Parameter „split“

* Verwenden Sie den Parameter *split* an der richtigen Stelle.
* Verwenden Sie *split* nicht beim Element *splitList*, sondern bei den einzelnen Elementen *text* oder *number*.

```auto
...

  elements: [
    {
      type: 'agorum.composite.form.element.splitList',
      name: 'splitList',
      split: 'sum'
      template: [
        // Es muss mindestens ein festes Feld geben, das pro Position eindeutig ist, etwa eine Positionsnummer
...
        {
          type: 'agorum.composite.form.element.number',
          label: 'Menge',
          name: 'quantity',
          // Der Wert dieser Spalte ergibt sich aus allen Summen der aufgesplitteten Werte dieser Spalte.
          split: 'sum'
        },
...
```

* Geben Sie die vorgestellten Parameter pro Positionsspalte an.

* Jede Spalte ohne den Eintrag *split* bleibt als Anker (Kopfdaten) bestehen und ist nicht teilbar:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/cfa3cc60-42f2-11ec-805f-005056aa0ecc)

```auto
OCR: split_list_11.js,Test,Beschreibung,Menge,Nummer,Position,Einzelpreis,100,00,Gesamtpreis,Kostenstelle,1000,00,600,00,200,00,200,00
```

Beispiel: Nicht teilbare Einträge

* Damit das System die gesplitteten Informationen zu einer Position zuweisen kann und die Angaben des Benutzers nutzbar sind, verwenden Sie als Anker die Positionsnummer, da diese eindeutig ist.
* Das System fasst gleichnamige Werte eines Ankers als eine Position zusammen, was zu einer ungewollten Zusammenführung der Positionen führen kann. Setzen Sie daher zur Verwendung der Positionsnummer als Anker den Parameter [readOnly](#readOnly) ein. Durch diesen verhindern Sie eine ungewollte Bearbeitung der Positionsnummern.

Das folgende Video zeigt eine ungewollte Zusammenführung der Positionen. Es wird dieselbe Beschreibung *Konferenzraum klein* für zwei verschiedene Positionen ausgewählt. Dies führt dazu, dass das System die Mengen und Preise zusammenrechnet. Alle Angaben verschmelzen:

#### Weitere Parameter

Sie können weitere Parameter​​​​​ in das Skript einfügen (siehe [element.list](#)).

### Events

* * *

Alle Events in [agorum.composite.form - element - Grundlegende Eigenschaften](https://d4w.agorum.com/roiwebui/acds_module/overview2/index.html#) und in [agorum.composite.form - element - list](#) gelten.

## agorum.composite.form.element.text

Dieses Element stellt ein Text-Eingabefeld dar. Dabei sind diverse Eigenschaften möglich:

* Einzeiliger Text
* Mehrzeiliger Text
* Passwort
* monospace (gleichbleibender Buchstabenabstand)

*agorum.composite.form.element.text* erbt alle grundlegenden Eigenschaften von [element](#).

### Beispiel einer Oberfläche

* * *

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/d3277480-e8ac-11ec-bc0b-005056aa0ecc)

```auto
OCR: Textfeldoptionen, Textfeld 1: Wert 1, Textfeld 2: Wert 2.1, Wert 2.2, Textfeld 3: Wert 3.1, Wert 3.2, Textfeldoptionen, Textfeld: Wert, Textfeld: Wert, 2.1: Wert, 2.2: Wert, Textfeld: Wert, 3.1: Wert, 3.2: Wert, Textfeld
```

Beispiel einer Oberfläche

#### Skript zur Oberfläche

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 500,
  height: 300,
  type: 'agorum.composite.form.basic',

  elements: [
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField1',
      label: 'Textfeld 1',
      value: 'Wert 1'
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField2',
      label: 'Textfeld 2',
      value: 'Wert 2.1\nWert 2.2',
      textArea: true
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField3',
      label: 'Textfeld 3',
      value: 'Wert 3.1\nWert 3.2',
      textArea: true,
      monospace: true
    },
    {
      type: 'agorum.composite.form.element.text',
      name: 'textField4',
      label: 'Textfeld 4',
      value: 'Wert 3',
      password: true
    }
  ]
});

form;
```

### Parameter

* * *

Alle Parameter in [element](#) gelten. Zusätzlich gelten die folgenden Parameter.

#### textArea

| Wert | Beschreibung |
| --- | --- |
| true | Zeigt ein mehrzeiliges Textfeld an. |
| false (Standard) | Zeigt ein normales einzeiliges Textfeld an. |

**Beispiel**

```auto
form.down('textField1').textArea = true;
```

Sie können diesen Parameter nicht ändern.

#### monospace

| Wert | Beschreibung |
| --- | --- |
| true | Verwendet eine Schrift, die denselben Buchstabenabstand besitzt. |
| false (Standard) | Verwendet normale Schrift. |

* Dieser Parameter funktioniert nur zusammen mit *textArea=true*.
* Sie können diesen Parameter nachträglich ändern.

**Beispiel**

```auto
form.down('textField1').monospace = true;
```

#### password

| Wert | Beschreibung |
| --- | --- |
| true | Stellt einzelne Zeichen sowohl im Bearbeitungs- als auch im Ansichtsmodus durch \* dar. |
| false (Standard) | Zeigt normalen (Klar-)Text an. |

**Beispiel**

```auto
form.down('textField1').password = true;
```

Sie können diesen Parameter nachträglich ändern.

### Events

* * *

Alle Events in [element](#) gelten.

#### action

Löst aus, wenn ein Benutzer die Eingabe über die Tasten Strg+Enter oder Enter (nicht in mehrzeiligen Textfeldern) bestätigt*.*

Das System übergibt als Parameter ein Objekt, das den Pfad zum auslösenden Element und die Eigenschaft *submit:true* enthält.

#### textAreaChanged

Löst aus, wenn sich der Parameter [textArea](#textArea) ändert.

Das System übergibt als Parameter den neuen Wert von *textArea*.

#### monospaceChanged

Löst aus, wenn sich der Parameter [monospace](#monospace) ändert.

Das System übergibt als Parameter den neuen Wert von *monospace*.

#### passwordChanged

Löst aus, wenn sich der Parameter [password](#password) ändert.

Das System übergibt als Parameter den neuen Wert von *password*.

## agorum.composite.form-element - Interner Aufbau

Diese Dokumentation beschreibt den Rumpf eines Elements*.*

Sie müssen das Element als Widget registrieren, um es innerhalb einer *form* verwenden zu können.

```auto
/* global parameters, jshint unused: true */

let aguila = require('common/aguila');
let acfFactory = require('/agorum/roi/customers/agorum.composite.form/js/aguila/Libraries/form-factory-input');

let field;

// factory definition
let factoryData = acfFactory.elementInput({

  // pass parameters from widget to the factory
  parameters: parameters,

  // add custom properties
  properties: [
    'myProperty'
  ],

  // builder function for the edit-widget
  build: build,

  // optional builder function for the view-widget
  // if not defined, a normal textDisplay is used
  buildView: buildView,

  // view function for displaying the value as text (for readOnly mode)
  viewStringify: viewStringify,

  // optional handle for value conversions, before passing as value to the edit

  // widget of this element
  valueHandler: valueHandler
});

// get created widget
let formWidget = factoryData.widget;

// Add custom event listener: own properties + value
formWidget.on('myPropertyChanged', myProperty => {

  // do something ...
});

// view function for displaying the value as text (for readOnly mode)
// convert the value to a string, that should be used for displaying
// this function may also return a promise, that resolves with the value as

// parameter, if the value transformation is taking longer
function viewStringify(value) {
  return '' + value;
}

// build the edit field.
// has to return a widget
function build(properties) {
  // return a widget. This widget needs a property value
  // you can also create a widget containing multiple fields, but the

  // main widget itself
  // has to handle the value: e.g. a date time field, consisting of different

  // input fields should return and accept a date as value
  field = aguila.create({
    type: 'agorum.textInput',
    label: properties.label,
    value: properties.value
  });

  // if you have a flexible element, that has no own height, you have to

  // define flexible = true in the widget definition above

  return field;
}

// optional builder for the view widget
// if not defined, a normal textDisplay is used
function buildView(properties) {
  field = aguila.create({
    type: 'agorum.htmlDisplay',
    value: properties.value,
    flexible: true
  });

  return field;
}

// optional handler for value conversions, before passing as value to the edit

// widget of this element it returns either the converted value or a promise,

// that resolves with the value as parameter
let valueHandlerRun;
function valueHandler(value) {
  valueHandlerRun = {};
  let myRun = valueHandlerRun;

  return new Promise((resolve) => {
    aguila.fork(() => {
      // do something that takes long time
      return 'newValue...' + value;
    }).then(newvalue => {
      // resolve only the latest call to valueHandler, cause this is

      // threaded, it could be,
      // that this resolve is called multiple times
      if (myRun === valueHandlerRun) {

        resolve(newvalue);
      }
    });
  });
}

formWidget;
```

