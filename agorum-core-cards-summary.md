# agorum core cards - Übersicht summary

## agorum core cards

*agorum core cards* verwenden Sie, wenn Sie größere Informationsmengen, etwa Suchergebnislisten, übersichtlich und flexibel darstellen möchten. *agorum core cards* teilt die Informationen innerhalb von Suchergebnislisten in kleinere Teile auf, die jeweils ein cardlet verwaltet. Jedes cardlet biete diverse Funktionen zum Steuern dieser einzelnen Informationen und deren Darstellung.

Grundlage von *agorum core cards* ist das Widget *agorum.cards.view*, das die Verwaltung von cardlets übernimmt und diese auf einem darunterliegenden *agorum.cardView* darstellt.

Ein grundlegendes Verständnis von *aguila* wird vorausgesetzt.

### Einführung

* * *

| Thema | Beschreibung | Link |
| --- | --- | --- |
| Einführung | Einführung in agorum core cards, Unterschiede und Ähnlichkeiten mit aguila. | Einführung in agorum core cards |
| Elemente einer card | Diese Dokumentation enthält eine Referenz aller Standard-Elemente von agorum core cards. | agorum core cards-Elemente |

### Widgets

* * *

| Widget | Beschreibung | Link |
| --- | --- | --- |
| agorum.cards.view | Dieses Widget bildet den Kern von agorum core cards und enthält diverse Funktionen, mit denen Sie den Inhalt Ihrer cards bearbeiten. | agorum.cards.view |
| agorum.cards.list | Dieses Widget verwendet eine agorum.cards.view, um Objektlisten anzuzeigen. | agorum.cards.list |

### Cardlets

* * *

| cardlet | Beschreibung | Link |
| --- | --- | --- |
| agorum.object | Dieses cardlet stellt jeweils ein Objekt (referenziert über den Parameter id) dar und verwendet decorators, um die Erzeugung des cardlets übersichtlich und modular zu halten. | agorum.object |

### JavaScript-Bibliotheken

* * *

| JavaScript-Bibliothek | Beschreibung | Link |
| --- | --- | --- |
| agorum.cards/js/decorators | Diese JavaScript-Bibliothek dient zur Unterstützung der Entwicklung von decorators und enthält Funktionen, mit denen Sie Elemente in einem gegebenen cardlet finden und ändern können. | JavaScript-Bibliothek agorum.cards/js/decorators |
| agorum.cards/js/cards | Diese JavaScript-Bibliothek dient zur Unterstützung der Entwicklung von cardlets und decorators. | JavaScript-Bibliothek agorum.cards/js/cards |

### Entwicklung

* * *

| Thema | Beschreibung | Link |
| --- | --- | --- |
| Eigene cardlets | Sie können einen eigenen cardlet-Typ erstellen, etwa wenn Sie Teile einer Ansicht wiederverwenden möchten oder wenn eine eigene Ereignisbehandlung erforderlich ist. | Eigene cardlets erstellen |
| Eigene decorators | Im Rahmen von Projektanforderungen, etwa das Darstellen weiterer Daten für Objekte oder das Ausblenden bestehender, können Sie eigene decorators einbinden. | Eigene decorators erstellen |
| Beispiele | Beispiele zu agorum core cards | agorum.cards - Beispiele |

## Einführung in agorum core cards

*agorum core cards* verwenden Sie, wenn Sie größere Informationsmengen, etwa Suchergebnislisten, übersichtlich und flexibel darstellen möchten. *agorum core cards* teilt die Informationen innerhalb von Suchergebnislisten in kleinere Teile auf, die jeweils ein cardlet verwaltet. Jedes cardlet bietet diverse Funktionen zum Steuern dieser einzelnen Informationen und deren Darstellung.

Grundlage von *agorum core cards* ist das Widget [agorum.cards.view](#), das die Verwaltung von cardlets übernimmt und diese auf einem darunterliegenden *agorum.cardView* darstellt.

Diese Dokumentation zeigt im Folgenden einen Überblick über die Funktionsweise von *agorum core cards*, insbesondere im Vergleich zu *aguila*.

Ein grundlegendes Verständnis von *aguila* wird vorausgesetzt.

### Ähnlichkeiten mit aguila

* * *

Der Aufbau ist modular. Analog zu den Widgets von *aguila* definieren Sie cardlets, die Sie an anderer Stelle wiederverwenden können. Ein cardlet kann sich wiederum aus weiteren cardlets zusammensetzen.

Erzeugt das System eine cardlet-Instanz, ruft es einen registrierter cardlet-Handler auf, der für die Konstruktion verantwortlich ist, vergleichbar mit den Konstruktoren von *aguila*.

Eingebaute cardlet-Typen können Sie als Basiskomponenten verwenden (als Elemente bezeichnet).

### Unterschiede zu aguila

* * *

**Events werden jeweils vom ersten umgebenden cardlet behandelt**

Das System propagiert ein Event automatisch aufwärts, ausgehend von dem cardlet, von dem es erzeugt wurde, bis es behandelt wird. Danach stoppt diese Propagierung automatisch.

* Wird ein Event von keinem cardlet-Handler behandelt, wird es stattdessen auf dem Widget [agorum.cards.view](#) ausgelöst.
* Wird ein Event von einem cardlet-Handler erzeugt, so kann es nicht von diesem selbst behandelt werden.

Wenn ein cardlet-Handler ein cardlet / Element selbst erzeugt hat (es also selbst „kennt“), ist er für die Behandlung von Events zuständig, die von diesen ausgehen. Im Gegensatz zu aguila sind hier auch cardlets voneinander isoliert, die auf demselben Element aufbauen.

**Beispiel**

```auto
top level: {
  type: 'sample.a',
  name: 'a'
}

cardlet sample.a: {
  type: 'sample.b',
  name: 'b'
}

cardlet sample.b: {
  type: 'agorum.vertical',
  name: 'vrt',
  items: [
    {
      type: 'sample.c',
      name: 'c1'
    },
    {
      type: 'sample.c',
      name: 'c2'
    }
  ]
}

cardlet sample.c: {
  type: 'agorum.button'
  name: 'btn',
  text: 'Test'
}
```

* sample.c behandelt Events, die von *btn* ausgehen.
* sample.b behandelt Events, die von *vrt*, *c1* und *c2* ausgehen.
* sample.a behandelt Events, die von *b* ausgehen und sieht insbesondere nicht Events, die von dem zugrundeliegenden cardlet *vrt* ausgehen.
* Events, die von *a* ausgehen, leitet das System als *aguila*\-Events auf dem agorum.cards.view-Widget weiter.

**Kein impliziter Kontext durch cardlet-Konstruktor**

Event-Handler müssen *cx.meta* als expliziten Kontext verwenden, um Informationen zwischenzuspeichern. cardlet-Handler werden nur einmalig als Bibliothek eingebunden und nicht für jedes zugehörige cardlet neu erzeugt.

**cardlet-Ha****ndler werden nicht im UI-Thread aufgerufen**

Die Funktionen *build()* und *event()* werden außerhalb des UI-Threads aufgerufen und müssen daher etwa nicht *aguila.fork()* verwenden, um IO-Operationen durchzuführen. Dafür muss stattdessen umgekehrt *aguila.enter()* verwendet werden, um direkt auf die UI zuzugreifen (meistens nicht nötig).

## agorum core cards – Elemente

Diese Dokumentation enthält eine Referenz aller Standard-Elemente von *agorum core cards*.

Mit diesen Elementen bauen Sie die *cards* auf.

### Übersicht aller Container-Elemente

* * *

| Element | Beschreibung |
| --- | --- |
| agorum.card | Erstellt eine card und kann zum Anordnen von Elementen in einer cards-Struktur verwendet werden. Enthaltene Elemente werden vertikal angeordnet. |
| agorum.horizontal | Erstellt eine horizontale Anordnung von Elementen. |
| agorum.vertical | Erstellt eine vertikale Anordnung von Elementen. |
| agorum.display.group | Stellt Elemente gruppiert dar. Das System verteilt die Gruppen dabei je nach verfügbarer Breite automatisch auf mehrere Spalten. |
| agorum.button | Erstellt eine interaktive Schaltfläche. |
| agorum.text | Zeigt einen Text in einer card an. |
| agorum.img | Zeigt ein Bild in einer card an. |
| agorum.chip | Erstellt ein Chip-Element. Ein Chip ist eine kompakte Komponente, die zum Ausdruck von Schlüsselwörtern, Filtern oder Aktionen verwendet werden kann. |
| agorum.separator | Erstellt einen visuellen Trenner zwischen Elementen in einer card. |
| agorum.badge | Erstellt ein Abzeichen. Ein Abzeichen ist eine kleine Komponente, die zum Anzeigen von Zahlen, Status oder Markierungen verwendet wird. |
| agorum.display | Stellt Daten in Textform dar. |
| agorum.object | Stellt ein agorum core-Objekt dar. |

### Allgemeine Eigenschaften für alle Elemente

* * *

Folgende Eigenschaften gelten für alle Elemente und werden bei den jeweiligen Elementen nicht nochmals definiert.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| type | Definiert den Typ des Elements, etwa agorum.text. | Zeichenkette |
| name | Definiert den Namen des Elements, um es später ansprechen zu können oder bei einem Event zu wissen, welches Element welches Event ausgelöst hat. | Zeichenkette |
| flex | Definiert die Flexibilität des Elements in Bezug auf die Größenanpassung. Wenn etwa 2 Elemente nebeneinander liegen und das erste Element die Eigenschaft flex=1 besitzt und das zweite flex=2, verbraucht das erste Element 1⁄3 und das zweite Element 2⁄3 der verfügbaren Breite. In einem horizontalen Container bezieht sich die Angabe auf die Breite. In einem vertikalen Container bezieht sich die Angabe auf die Höhe. | Numerischer Wert |
| size | Vertikaler Container Definiert die Höhe des Elements in Pixeln. Horizontaler Container Definiert die Breite des Elements in Pixeln. | Numerischer Wert |
| width | Definiert die feste Breite des Elements in Pixeln. | Numerischer Wert |
| height | Definiert die feste Höhe des Elements in Pixeln. | Numerischer Wert |
| minSize | Vertikaler Container Definiert die minimale Höhe des Elements in Pixeln. Horizontaler Container Definiert die minimale Breite des Elements in Pixeln. | Numerischer Wert |
| maxSize | Vertikaler Container Definiert die maximale Höhe des Elements in Pixeln. Horizontaler Container Definiert die maximale Breite des Elements in Pixeln. | Numerischer Wert |
| minWidth | Definiert die minimale Breite des Elements in Pixeln. | Numerischer Wert |
| maxWidth | Definiert die maximale Breite des Elements in Pixeln. | Numerischer Wert |
| minHeight | Definiert die maximale Breite des Elements in Pixeln. | Numerischer Wert |
| maxHeight | Definiert die maximale Höhe des Elements in Pixeln. | Numerischer Wert |
| pointer | true Stellt den Mauszeiger als Zeiger dar, wenn der Benutzer über das Element fährt. false (Standard) Stellt den Mauszeiger nicht als Zeiger dar, wenn der Benutzer über das Element fährt. | siehe Spalte Beschreibung |
| interactive | true Benutzer können das Element anklicken, das Element löst ein Event aus. false (Standard) Benutzer können das Element nicht anklicken. | siehe Spalte Beschreibung |
| tooltip | Definiert ein Tooltip für das Element. Der Tooltip erscheint, wenn der Benutzer mit der Maus über das Element fährt. | Zeichenkette |
| borderless | true Entfernt den Rahmen eines Elements, sofern das Element einen Rahmen besitzt. false (Standard) Belässt den Rahmen eines Elements, sofern das Element einen Rahmen besitzt. | siehe Spalte Beschreibung |

### Allgemeine Eigenschaften für Container-Elemente

* * *

Folgende Eigenschaften gelten für alle Container-Elemente, etwa:

* agorum.card
* agorum.horizontal
* agorum.vertical
* agorum.display.group

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| padding | Definiert die Größe des Innenabstands des Containers zu seinen Kind-Elementen in Pixeln. | 's' = 4 'm' = 8 'l' = 12 'xl' = 16 Beispiel zum Verwenden von padding siehe Beispiel |
| spacing | Definiert die Größe der Abstände der Elemente innerhalb des Containers in Pixeln. | 'none' = 0 's' = 4 'm' = 8 'l' = 12 'xl' = 16 Beispiel zum Verwenden von spacing siehe Beispiel |
| items | Enthält ein Array der Kind-Elemente für dieses Container-Element. | Array aus weiteren Elementen |

#### Beispiel

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 800,
  items: [
    {
      type: 'agorum.spacer',
      height: 10,
    },
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let card = (num, spacing, padding) => ({
  type: 'agorum.card',
  minWidth: 200,
  flex: 1,
  spacing: spacing,
  padding: padding,
  items: [
    {
      type: 'agorum.button',
      text: 'Button 1 ' + num,
    },
    {
      type: 'agorum.button',
      text: 'Button 2 ' + num,
    },
  ],
});

let sample = {
  type: 'agorum.horizontal',
  spacing: 'xl',
  wrap: true,
  items: [card(1, 'none', 'none'), card(2, 's', 's'), card(3, 'm', 'm'), card(4, 'l', 'l'), card(5, 'xl', 'xl')],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/034a7cc0-4aea-11ee-a4a5-005056aa0ecc)

```auto
OCR: Button 1 1, Button 2 1, Button 1 4, Button 2 4, Button 1 2, Button 2 2, Button 1 5, Button 2 5, Button 1 3, Button 2 3
```

Beispiel zu *padding* und *spacing*

### agorum.card

* * *

Dieses Element:

* erstellt eine *card*
* kann zum Anordnen von Elementen in einer *cards*\-Struktur verwendet werden
* unterstützt verschiedene Eigenschaften zum Steuern des Aussehens und Verhaltens der *card*

*agorum.card* ist meist die Grundlage für eine *card*. Sie können auch eine *card* in *cards* verschachteln und Unterelemente darstellen.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| Container-Eigenschaften | siehe Allgemeine Eigenschaften für Container-Elemente | – |
| mark | Definiert die Markierungsfarbe der card und zeigt einen Farbbalken links an der card an. | 'primary', 'secondary', 'tertiary', 'success', 'warning', 'danger', 'dark', 'medium', 'light', 'transparent', 'disabled' |
| selectable | true Benutzer können die card wählen. Sinnvoll, wenn mehrere cards gewählt werden können. false (Standard) Benutzer können die card nicht wählen. | siehe Spalte Beschreibung |
| badges | Definiert die Abzeichen, die in der card rechts oben erscheinen. | Array von agorum.bade-Elementen |

#### Beispiel

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      type: 'agorum.spacer',
      height: 10,
    },
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  mark: 'success',
  spacing: 'm',
  padding: 's',
  interactive: true,
  pointer: true,
  minWidth: 200,
  height: 100,
  badges: [
    {
      type: 'agorum.badge',
      color: 'primary',
      text: 'New',
      name: 'new',
    },
  ],
  items: [
    {
      type: 'agorum.text',
      text: 'Hello, world!',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/976e5700-4892-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.card.js (Test), Hello, world!, - x, New, agorum.card.js, Test, Hello, world, New
```

Beispiel zu *agorum.card*

Dieses Beispiel zeigt eine *card*, die das Element *agorum.text* enthält.

Die *card*:

* besitzt eine minimale Breite von 200 Pixel und eine Höhe von 100 Pixeln
* besitzt eine grüne Markierung (success), einen mittleren Abstand (m) zwischen den Elementen und einen kleinen Innenabstand (s)
* zeigt ein Badge mit *New* an
* ist interaktiv und zeigt den Mauszeiger als Zeiger an, wenn er über die *card* fährt

### agorum.vertical

* * *

Dieses Element:

* erstellt eine vertikale Anordnung von Elementen
* kann zum Anordnen von Elementen in einer Spalte in einem *cards*\-Layout verwendet werden
* und unterstützt verschiedene Eigenschaften zum Steuern des Layouts und Verhaltens der Elemente

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| Container-Eigenschaften | siehe Allgemeine Eigenschaften für Container-Elemente | – |

#### Beispiel 1

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.vertical',
      spacing: 'm',
      flex: 1,
      minWidth: 100,
      items: [
        {
          type: 'agorum.text',
          text: 'Text 1',
        },
        {
          type: 'agorum.text',
          text: 'Text 2',
        },
        {
          type: 'agorum.text',
          text: 'Text 3',
        },
        {
          type: 'agorum.text',
          text: 'Text 4',
        },
      ],
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/3cd9cb10-4894-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.vertical.js (Test), Text 1, Text 2, -, Text 3, Text 4, agorum.vertical.js, Test, Text, Text, Text, Text
```

Beispiel 1 *zu agorum.vertical*

Dieses Beispiel zeigt eine *card*, die das Element *agorum.vertical* enthält und vier Textelemente untereinander innerhalb des Elements anzeigt.

#### Beispiel 2

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      spacing: 'm',
      flex: 1,
      minWidth: 100,
      items: [
        {
          type: 'agorum.vertical',
          flex: 1,
          items: [
            {
              type: 'agorum.text',
              text: 'Text 1',
            },
            {
              type: 'agorum.text',
              text: 'Text 2',
            },
          ],
        },
        {
          type: 'agorum.vertical',
          flex: 2,
          items: [
            {
              type: 'agorum.text',
              text: 'Text 3',
            },
            {
              type: 'agorum.text',
              text: 'Text 4',
            },
          ],
        },
      ],
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/de6e3bf0-4894-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.vertical.js (Test), Text 1, Text 2, Text 3, Text 4, -, agorum.vertical.js, Test, Text, Text, Text, Text
```

Beispiel 2 zu *agorum.vertical*

Dieses Beispiel zeigt eine *card*, die das Element *agorum.horizontal* und innerhalb des Elements zwei weitere *agorum.vertical*\-Elemente enthält.

* Das erste *agorum.vertical*\-Element hat einen *flex*\-Wert von 1.
* Das zweite *agorum.vertical*\-Element hat einen *flex*\-Wert von 2 und nimmt doppelt so viel Platz ein wie das erste *agorum.vertical*\-Element.
* Jedes *agorum.vertical*\-Element enthält zwei Textelemente.

### agorum.horizontal

* * *

Dieses Element:

* erstellt eine horizontale Anordnung von Elementen
* kann zum Anordnen von Elementen in einer Zeile in einem *cards*\-Layout verwendet werden
* unterstützt verschiedene Eigenschaften zum Steuern des Layouts und Verhaltens der Elemente

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| Container-Eigenschaften | siehe Allgemeine Eigenschaften für Container-Elemente | – |
| wrap | true Verschiebt Kind-Elemente des Containers automatisch in die nächste Zeile, wenn die Kind-Elemente nicht mehr nebeneinander passen. false (Standard) Verschiebt keine Kind-Elemente. | siehe Spalte Beschreibung |

#### Beispiel

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      spacing: 'm',
      flex: 1,
      minWidth: 100,
      wrap: true,
      items: [
        {
          type: 'agorum.text',
          text: 'Text 1',
        },
        {
          type: 'agorum.text',
          text: 'Text 2',
        },
        {
          type: 'agorum.text',
          text: 'Text 3',
        },
        {
          type: 'agorum.text',
          text: 'Text 4',
        },
      ],
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/a52edc30-4896-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.horizontal.js (Test), Text 1, Text 2, Text 3, Text 4
```

Beispiel zu *agorum.horizontal*

Dieses Beispiel zeigt eine *card*, die das Element *agorum.horizontal* und innerhalb des Elements vier Textelemente enthält.

Das Element besitzt mehrere Eigenschaften zum Steuern des Verhaltens:

| Eigenschaft | Beschreibung |
| --- | --- |
| spacing | m stellt den Abstand zwischen den Elementen ein. |
| flex | 1 ermöglicht es dem Element, flexibel in seiner Größe zu sein. |
| minWidth | 100 stellt die minimale Breite des Elements ein. |
| wrap | true ermöglicht es den Elementen, auf die nächste Zeile zu springen, wenn nicht genug Platz in der aktuellen Zeile vorhanden ist. |

### agorum.button

* * *

Dieses Element:

* erstellt eine interaktive Schaltfläche
* unterstützt verschiedene Eigenschaften zum Steuern des Aussehens und Verhaltens der Schaltfläche

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| text | Definiert den Text der Schaltfläche. Wenn Sie keinen Text angeben, erscheint nur das Symbol aus der Eigenschaft icon. | Zeichenkette |
| html | Definiert alternativ zur Eigenschaft text den HTML-Text der Schaltfläche. Wenn Sie diese Eigenschaft nicht angeben, erscheint nur das Symbol aus der Eigenschaft icon. | Zeichenkette |
| color | Definiert die Farbe der Schaltfläche. | 'primary', 'secondary', 'tertiary', 'success', 'warning', 'danger', 'dark', 'medium', 'light', 'transparent', 'disabled' |
| icon | Definiert das zu verwendende Symbol, etwa ionicon:alert. Wenn Sie diese Eigenschaft nicht angeben, erscheint nur der Text oder HTML-Text aus den Eigenschaften text oder html. | Alle Icon-Definitionen, die Sie über die Aktion Icon erstellen definieren können. |
| size | Definiert die Größe des verwendeten Symbols (Eigenschaft icon) und die Schriftgröße der Eigenschaften text und html. | 's' = 12 (Icon), 10 (Schrift) 'm' (Standard) = 14 (Icon), 12 (Schrift) 'l' = 16 (Icon), 14 (Schrift) 'xl' = 18 (Icon), 16 (Schrift) Beispiel zum Verwenden von Größen siehe Beispiel 2 |
| weight | normal (Standard) Stellt den Text normal dar. light Stellt den Text dünner dar. bold Stellt den Text fetter dar. | siehe Spalte Beschreibung |

#### Beispiel 1

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.button',
      text: 'Primary',
      color: 'primary',
      size: 'm',
      weight: 'bold',
      icon: 'ionicon:checkmark',
      name: 'primaryButton',
    },
    {
      type: 'agorum.button',
      text: 'Secondary',
      color: 'secondary',
      size: 's',
      weight: 'normal',
      icon: 'ionicon:close',
      name: 'secondaryButton',
    },
    {
      type: 'agorum.button',
      text: 'Success',
      color: 'success',
      size: 'l',
      weight: 'light',
      icon: 'ionicon:alert',
      name: 'successButton',
    },
  ],
};

widget.down('cardView').replace(sample);

widget.down('cardView').on('elementClicked', name => console.log('Button clicked:', name));

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/cf1060d0-4898-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.button.js, Test, Primary, Secondary, Success
```

Beispiel zu *agorum.button*

Dieses Beispiel zeigt drei Schaltflächen mit je unterschiedlichen Eigenschaften.

Ein Event-Handler wird hinzugefügt, der den Namen der geklickten Schaltfläche in der Konsole ausgibt.

#### Beispiel 2

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.button',
      icon: 'ionicon:document;color=white',
      text: 'Default is m',
    },
    {
      type: 'agorum.button',
      icon: 'ionicon:document;color=white',
      text: 'Size s',
      size: 's',
    },
    {
      type: 'agorum.button',
      icon: 'ionicon:document;color=white',
      text: 'Size m',
      size: 'm',
    },
    {
      type: 'agorum.button',
      icon: 'ionicon:document;color=white',
      text: 'Size l',
      size: 'l',
    },
    {
      type: 'agorum.button',
      icon: 'ionicon:document;color=white',
      text: 'Size xl',
      size: 'xl',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/741dcba0-4ae5-11ee-a4a5-005056aa0ecc)

```auto
OCR: Groessen_agorum.button.js, Test, Default, Size, Size, Size, Size
```

Beispiel zum Verwenden von Größen

### agorum.text

* * *

Dieses Element:

* zeigt Text in einer *card* an
* unterstützt verschiedene Eigenschaften zum Steuern des Aussehens und Verhaltens des Textes

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| text | Definiert den Text. | Zeichenkette |
| html | Definiert alternativ zur Eigenschaft text den HTML-Text. | Zeichenkette |
| weight | normal (Standard) Stellt den Text normal dar. light Stellt den Text dünner dar. bold Stellt den Text fetter dar. | siehe Spalte Beschreibung |
| align | start Richtet den Text linksbündig aus. center Richtet den Text mittig aus. end Richtet den Text rechtsbündig aus. | siehe Spalte Beschreibung |
| ellipsis | start Zeigt Ellipsen (…) am Anfang an, wenn der Text zu lang ist. end Zeigt Ellipsen (…) am Ende an, wenn der Text zu lang ist. Hinweis: Wenn Sie diese Eigenschaft nicht angeben, setzt das System den Wert null und fügt weder am Anfang noch am Ende Ellipsen an. | siehe Spalte Beschreibung |
| size | Definiert die Schriftgröße der Eigenschaften text und html. | 's' = 12 (Icon), 10 (Schrift) 'm' (Standard) = 14 (Icon), 12 (Schrift) 'l' = 16 (Icon), 14 (Schrift) 'xl' = 18 (Icon), 16 (Schrift) Beispiel zum Verwenden von Größen siehe Beispiel 2 |

#### Beispiel 1

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.text',
      text: 'Hello, world!',
      size: 'm',
      weight: 'bold',
      align: 'center',
      name: 'myText',
    },
    {
      type: 'agorum.text',
      text: 'This is a long text that will be cut off at the end.',
      size: 's',
      weight: 'normal',
      align: 'start',
      ellipsis: 'end',
      name: 'myLongText',
    },
    {
      type: 'agorum.text',
      text: 'This is a long text that will be cut off at the start.',
      size: 'l',
      weight: 'light',
      align: 'end',
      ellipsis: 'start',
      name: 'myLongTextStart',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/3f10a410-489b-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.text.js (Test), Hello, world!, This is a long text that will be cut off at the..., ... that will be cut off at the start., agorum.text.js, Test, Hello, world, This, long, text, that, will, cut, off, the, ..., ..., that, will, cut, off, the, start
```

Beispiel zu *agorum.text*

Dieses Beispiel zeigt drei Textelemente mit je unterschiedlichen Eigenschaften.

* Der erste Text besitzt eine mittlere Größe, eine fette Gewichtung und ist zentriert.
* Der zweite Text besitzt eine kleine Größe, eine normale Gewichtung, ist linksbündig und zeigt Ellipsen am Ende an, wenn der Text abgeschnitten wird.
* Der dritte Text besitzt eine große Größe, eine leichte Gewichtung, ist rechtsbündig und zeigt Ellipsen am Anfang an, wenn der Text abgeschnitten wird.

#### Beispiel 2

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.text',
      text: 'Default is m',
    },
    {
      type: 'agorum.text',
      text: 'Size s',
      size: 's',
    },
    {
      type: 'agorum.text',
      text: 'Size m',
      size: 'm',
    },
    {
      type: 'agorum.text',
      text: 'Size l',
      size: 'l',
    },
    {
      type: 'agorum.text',
      text: 'Size xl',
      size: 'xl',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/7babb4f0-4ae9-11ee-a4a5-005056aa0ecc)

```auto
OCR: Default is m, Size s, Size m, Size l, Size xl, Groessen_agorum.text.js, Test, Default, Size, Size, Size, Size
```

Beispiel zum Verwenden von Größen

### agorum.separator

* * *

Dieses Element erstellt einen visuellen Trenner zwischen Elementen.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| color | Definiert die Farbe der Trennlinie. | 'primary', 'secondary', 'tertiary', 'success', 'warning', 'danger', 'dark', 'medium', 'light', 'transparent', 'disabled' |

#### Beispiel

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.text',
      text: 'Text above the separator',
    },
    {
      type: 'agorum.separator',
      color: 'danger',

    },
    {
      type: 'agorum.text',
      text: 'Text below the separator',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/19a408f0-489d-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.separator.js (Test), Text above the separator, Text below the separator, agorum.separator.js, Test, Text, above, the, separator, Text, below, the, separator
```

Beispiel zu *agorum.separator*

Dieses Beispiel zeigt eine *card*, die zwei Textelemente und einen Separator enthält.

Der Separator dient als visueller Trenner zwischen den beiden Textelementen.

### agorum.chip

* * *

Dieses Element erstellt ein Chip-Element.

Ein Chip ist eine kompakte Komponente, die zum Ausdruck von Schlüsselwörtern, Filtern oder Aktionen verwendet werden kann.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| text | Definiert den Text des Chips. Wenn Sie diese Eigenschaft nicht angeben, erscheint nur das Symbol aus der Eigenschaft icon. | Zeichenkette |
| html | Definiert alternativ zur Eigenschaft text den HTML-Text. | Zeichenkette |
| color | Definiert die Farbe des Chips. | 'primary', 'secondary', 'tertiary', 'success', 'warning', 'danger', 'dark', 'medium', 'light', 'transparent', 'disabled' |
| icon | Definiert das zu verwendende Symbol, etwa ionicon:alert. Wenn Sie diese Eigenschaft nicht angeben, erscheint nur der Text oder HTML-Text aus den Eigenschaften text oder html. | Alle Icon-Definitionen, die Sie über die Aktion Icon erstellen definieren können. |
| size | Definiert die Größe des verwendeten Symbols (Eigenschaft icon) und die Schriftgröße der Eigenschaften text und html. | 's' = 12 (Icon), 10 (Schrift) 'm' (Standard) = 14 (Icon), 12 (Schrift) 'l' = 16 (Icon), 14 (Schrift) 'xl' = 18 (Icon), 16 (Schrift) Beispiel zum Verwenden von Größen siehe Beispiel 2 |
| weight | normal (Standard) Stellt den Text normal dar. light Stellt den Text dünner dar. bold Stellt den Text fetter dar. | siehe Spalte Beschreibung |

#### Beispiel 1

```auto
let aguila = require('common/aguila');
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.chip',
      text: 'Keyword',
      color: 'primary',
      size: 'm',
      icon: 'ionicon:checkmark',
      name: 'keywordChip',
    },
    {
      type: 'agorum.chip',
      text: 'Filter',
      color: 'secondary',
      size: 's',
      icon: 'ionicon:filter',
      name: 'filterChip',
    },
    {
      type: 'agorum.chip',
      text: 'Action',
      color: 'danger',
      size: 'l',
      icon: 'ionicon:flash',
      name: 'actionChip',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/723bb6a0-489f-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.chip.js, Test, Keyword, Filter, Action
```

Beispiel zu *agorum.chip*

Dieses Beispiel zeigt drei Chip-Elemente mit je unterschiedlichen Eigenschaften:

* Das erste Chip-Element besitzt die Farbe *primary*, eine mittlere Größe und ein Häkchen-Symbol.
* Das zweite Chip-Element besitzt die Farbe *secondary*, eine kleine Größe und ein Filter-Symbol.
* Das dritte Chip-Element besitzt die Farbe *danger*, eine große Größe und ein Blitz-Symbol.

#### Beispiel 2

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.chip',
      icon: 'ionicon:document;color=white',
      text: 'Default is m',
    },
    {
      type: 'agorum.chip',
      icon: 'ionicon:document;color=white',
      text: 'Size s',
      size: 's',
    },
    {
      type: 'agorum.chip',
      icon: 'ionicon:document;color=white',
      text: 'Size m',
      size: 'm',
    },
    {
      type: 'agorum.chip',
      icon: 'ionicon:document;color=white',
      text: 'Size l',
      size: 'l',
    },
    {
      type: 'agorum.chip',
      icon: 'ionicon:document;color=white',
      text: 'Size xl',
      size: 'xl',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/a69bc030-4ae7-11ee-a4a5-005056aa0ecc)

```auto
OCR: Groessen_agorum.chip.js (Test), Default is m, Size s, Size m, Size I, Size xl, Groessen_agorum.chip.js, Test, Default, Size, Size, Size, Size
```

Beispiel zum Verwenden von Größen

### agorum.img

* * *

Dieses Element:

* zeigt ein Bild in einer *card*
* unterstützt verschiedene Eigenschaften zum Steuern des Aussehens und Verhaltens des Bilds

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| src | Definiert das anzuzeigende Bild als: URL ein in agorum core abgelegtes Bild ein inline eingebettetes Bild Ein in agorum core abgelegtes Bild Verwenden Sie folgende URL-Angabe: '/api/rest/object/embed/\[ID, UUID, Pfad\]' | Zeichenkette |
| content | Übergibt alternativ zur Eigenschaft src das Bild als Inhalt, etwa die XML-Struktur einer SVG-Datei. | Zeichenkette |

#### Beispiel

```auto
let aguila = require('common/aguila');
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.img',
      content: icons.get('ionicon:document'),
      size: 40,
      name: 'documentIcon',
    },
    {
      type: 'agorum.img',
      src: '/api/rest/object/embed/432667f0-45bd-11ee-82e4-02420a0a000b',
      minWidth: 100,
      minHeight: 100,
      name: 'myImageWithId',
    },
    {
      type: 'agorum.img',
      src: '/api/rest/object/embed/%2FHome%2Froi%2FMyFiles%2Fcard%2Fsamples%2Fresources%2Fa-image.jpg',
      minWidth: 100,
      minHeight: 100,
      name: 'myImageWithPath',
    },
    {
      type: 'agorum.img',
      src: 'data:image/gif;base64,R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7////wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7',
      minWidth: 32,
      minHeight: 32,
      name: 'inlineImage',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/2f1a0b90-48c4-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.img.js (Test), *, -, agorum.img.js, Test
```

Beispiel zu agorum.img

Dieses Beispiel zeigt vier Bilder:

* Das erste Bild ist ein Symbol, das von der Funktion *icons.get* als SVG-XML abgerufen wird und eine Größe von 40 Pixeln besitzt.
* Das zweite Bild ist eine Bilddatei, die über die *agorum core*\-API mit der UUID geladen wird und eine minimale Breite und Höhe von jeweils 100 Pixeln besitzt.
* Das dritte Bild wurde mit der *agorum core*\-API und einem Pfad geladen.
* Zusätzlich wurde ein viertes Bild als Inline-Grafik hinzugefügt, die als Base64-codierte GIF-Datei definiert ist und eine minimale Breite und Höhe von jeweils 100 Pixeln besitzt.

### agorum.badge

* * *

Dieses Element erstellt ein Abzeichen an einer *card* in der rechten oberen Ecke.

Ein Abzeichen ist eine kleine Informationsfläche, die Text und / oder Symbole anzeigen kann.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| text | Definiert den Text des Badges. Wenn Sie diese Eigenschaft nicht angeben, erscheint nur das Symbol aus der Eigenschaft icon. | Zeichenkette |
| html | Definiert alternativ zur Eigenschaft text den HTML-Text. | Zeichenkette |
| color | Definiert die Farbe des Badges. | 'primary', 'secondary', 'tertiary', 'success', 'warning', 'danger', 'dark', 'medium', 'light', 'transparent', 'disabled' |
| icon | Definiert das zu verwendende Symbol, etwa ionicon:alert. Wenn Sie diese Eigenschaft nicht angeben, erscheint nur der Text oder HTML-Text aus den Eigenschaften text oder html. | Alle Icon-Definitionen, die Sie über die Aktion Icon erstellen definieren können. |
| content | Übergibt alternativ zur Eigenschaft icon das Bild als Inhalt, etwa die XML-Struktur einer SVG-Datei. | Zeichenkette |

#### Beispiel

```auto
let aguila = require('common/aguila');
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      type: 'agorum.spacer',
      height: 10,
    },
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  badges: [
    {
      type: 'agorum.badge',
      text: 'New',
      color: 'primary',
      content: icons.get('ionicon:checkmark'),
      name: 'newBadge',
    },
    {
      type: 'agorum.badge',
      text: 'Warning',
      color: 'warning',
      icon: 'ionicon:alert',
      name: 'warningBadge',
    },
    {
      type: 'agorum.badge',
      text: 'Error',
      color: 'danger',
      icon: 'ionicon:close',
      name: 'errorBadge',
    },
  ],
  items: [
    {
      type: 'agorum.text',
      text: 'Hello, world!',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/958c07d0-48a5-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.badge.js, Test, Hello world, New Warning, Error
```

Beispiel zu *agorum.badge*

Dieses Beispiel zeigt drei Abzeichen mit je unterschiedlichen Eigenschaften:

* Das erste Abzeichen besitzt den Text *New*, die Farbe *primary* und ein Häkchen-Symbol.
* Das zweite Abzeichen besitzt den Text *Warning*, die Farbe *warning* und ein Warnsymbol.
* Das dritte Abzeichen besitzt den Text *Error*, die Farbe *danger* und ein Schließen-Symbol.

### agorum.object

* * *

Dieses Element stellt ein *agorum core*\-Objekt dar, um etwa Informationen über ein bestimmtes *agorum core*\-Objekt anzuzeigen.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| id | Definiert die agorum core-ID des darzustellenden Objekts. | Zeichenkette |
| level | Definiert das Detaillevel der anzuzeigenden Informationen. Um den Wert aus der Konstanten LEVELS der JavaScript-Bibliothek agorum.cards/js/decorators zu erhalten, verwenden Sie folgenden Code: let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators'); decorators.LEVEL.MAXIMUM | MINIMUM, SMALL, REDUCED, DEFAULT, MAXIMUM |

#### Beispiel

```auto
let aguila = require('common/aguila');
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.object',
      id: '/agorum/roi/Files',
      level: decorators.LEVEL.MAXIMUM, // MINIMUM, SMALL, REDUCED, DEFAULT, MAXIMUM
      interactive: true,
      minWidth: 200,
      name: 'agorumObject',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/dbba1340-48a6-11ee-a4a5-005056aa0ecc)

```auto
OCR: agorum.object.js (Test), Dateien, 14 Objekte, Root/agorum/roi, 29.12.2004 08:47, agorum.object.js, Test, Dateien, Objekte, Root, agorum, roi, 29.12.2004, 08:47
```

Beispiel zu *agorum.object*

Dieses Beispiel zeigt eine *card*:

* die das Element *agorum.object* enthält
* ein *agorum core*\-Objekt darstellt, das durch seine ID identifiziert wird
* interaktiv ist und eine minimale Breite von 200 Pixeln besitzt.

Die Detailstufe der angezeigten Informationen ist auf das Maximum (4) gesetzt.

### agorum.display.group

* * *

Dieses Element stellt eine Anzeigegruppe dar, die zum Anzeigen von zusammengehörigen Inhalten verwendet wird.

* Mehrere Anzeigegruppen können nebeneinander dargestellt werden, wenn genügend Platz vorhanden ist, ansonsten wird auf die nächste Zeile umgebrochen.
* Innerhalb einer Anzeigegruppe können Sie Labels und Werte definieren, um zusammengehörige Informationen darzustellen. Dabei können verschiedene Datentypen verwendet werden, etwa Text, Zahlen, Daten und Objekte, die das System entsprechend sinnvoll rendert.
* Wenn Sie bei den Unterelementen keinen *type* angeben, setzt das System alle Elemente unterhalb von *agorum.display.group* auf den Typ *agorum.display*.
* Objekt-IDs löst das System automatisch auf und stellt sie als anklickbare Links dar, die auf das jeweilige *agorum core*\-Objekt verweisen. Dies ermöglicht eine intuitive Interaktion mit den dargestellten Informationen.
* Die Breite der Labels und der einzelnen Abschnitte können Sie anpassen, um die Darstellung der Anzeigegruppe zu optimieren.
* Jede Anzeigegruppe wird durch ein leeres Element *''* abgetrennt. Dadurch entstehen mehrere Spalten, die automatisch nebeneinander dargestellt werden, sofern genug Platz vorhanden ist.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| Container-Eigenschaften | siehe Allgemeine Eigenschaften für Container-Elemente | – |
| labelWidth | Definiert die Breite der Labels. | Numerische Angabe Standard 100 |
| sectionWidth | Definiert die Breite einer Sektion für jeden Block. Passen mehrere Sektionen von der Breite her nebeneinander, stellt das System diese nebeneinander dar, ansonsten untereinander. | Numerische Angabe Standard 300 |
| items | Definiert die Elemente, die in der Anzeigegruppe erscheinen. Enthält ein Eintrag im Array den Wert '', definiert das den Beginn einer neuen Sektion. | Array von Elementen |

#### Beispiel

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.display.group',
      labelWidth: 80, // width of labels, default 100
      sectionWidth: 200, // width of a section for each block. Default is 300
      items: [
        // First column of display group
        {
          type: 'agorum.vertical',
          size: 12,
        },
        {
          type: 'agorum.display', // optional type-definition, cause default type is agorum.display
          label: 'Name',
          value: 'John Doe',
        },
        {
          label: 'Email',
          value: 'john.doe@example.com',
        },
        {
          label: 'Phone',
          value: '+1-202-555-0179',
        }, // blank item, makes new column in display group
        '',

        // Second column of display group
        {
          type: 'agorum.vertical',
          size: 12,
        },
        {
          label: 'Label 1',
          value: 'Text 1',
        },
        {
          label: 'Date',
          value: new Date(),
        },
        {
          label: 'Number',
          value: 1.5,
        },
        {
          label: 'Object', // object: looks up the agorum core object and displays a link. The text is the displayName of the object
          object: 'user:demo',
        },
        {
          label: 'Array', // also arrays of values are possible
          value: ['Value 1', 'Value 2'],
        },
        {
          label: 'Object Array',
          items: [{ object: 'user:demo' }, { object: 'user:roi' }],
        },
      ],
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/e5062eb0-48a7-11ee-a4a5-005056aa0ecc)

```auto
OCR: John Doe,Text 1,john.doe@example.com,01.09.2023,+1-202-555-0179,1,50,demo demo (demo),Value 1, Value 2,demo demo (demo),roi (roi), - x
```

Beispiel zu *agorum.display.group*

Dieses Beispiel zeigt das Element *agorum.display.group*, das innerhalb des Elements verschiedene Arten von Elementen anzeigt, darunter:

* Text
* Datum
* Zahl
* Objekt
* Arrays von Werten und Objekten.

Leere Elemente werden verwendet, um neue Zeilen in der Anzeigegruppe zu erstellen.

### agorum.display

* * *

Dieses Element gibt einen Wert formatiert mit Label aus und wird zumeist in Kombination mit dem Element [agorum.display.group](#agorum.display.group) verwendet.

* Sie können verschiedene Datentypen verwenden, etwa Text, Zahlen, Daten und Objekte, die das System entsprechend sinnvoll rendert.
* Objekt-IDs löst das System automatisch auf und stellt sie als anklickbare Links dar, die auf das jeweilige *agorum core*\-Objekt verweisen. Dies ermöglicht eine intuitive Interaktion mit den dargestellten Informationen.

| Eigenschaft | Beschreibung | Mögliche Werte |
| --- | --- | --- |
| Allgemeine Eigenschaften | siehe Allgemeine Eigenschaften für alle Elemente | – |
| labelWidth | Definiert die Breite der Labels. | Numerische Angabe Standard 100 |
| label | Definiert das Label, das neben dem Wert erscheint. | Zeichenkette |
| value | Definiert den anzuzeigenden Wert, etwa eine Zahl oder ein Date-Objekt. | Anzuzeigender Wert als JavaScript-Objekt |
| object | Definiert alternativ zur Eigenschaft value ein agorum core-Objekt in Form einer id, etwa UUID, ID oder einen Pfad. | Zeichenkette |

#### Beispiel

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.display',
      label: 'Name',
      labelWidth: 100,
      value: 'John Doe',
    },
    {
      type: 'agorum.display',
      label: 'Email',
      value: 'john.doe@example.com',
    },
    {
      type: 'agorum.display',
      label: 'Phone',
      value: '+1-202-555-0179',
    },
    {
      type: 'agorum.display',
      label: 'Label 1',
      value: 'Text 1',
    },
    {
      type: 'agorum.display',
      label: 'Date',
      value: new Date(),
    },
    {
      type: 'agorum.display',
      label: 'Number',
      value: 1.5,
    },
    {
      type: 'agorum.display',
      label: 'Object', // object: looks up the agorum core object and displays a link. The text is the displayName of the object
      object: 'user:demo',
    },
    {
      type: 'agorum.display',
      label: 'Array', // also arrays of values are possible
      value: ['Value 1', 'Value 2'],
    },
    {
      type: 'agorum.display',
      label: 'Object Array',
      items: [{ object: 'user:demo' }, { object: 'user:roi' }],
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

Das Beispiel definiert eine Reihe von *agorum.display*\-Elementen innerhalb einer [agorum.card](#agorum.card). Diese Elemente dienen dazu, verschiedene Arten von Informationen anzuzeigen:

| Information | Beschreibung |
| --- | --- |
| Name, Email, Phone, Label 1, Date, Number | Diese Elemente zeigen einfache Werte an, etwa: einen Namen eine E-Mail-Adresse eine Telefonnummer einen Text ein Datum eine Zahl Jedes Element hat ein Label und einen Wert. |
| Object | Dieses Element zeigt einen Link zu einem agorum core-Objekt an. Der Text ist der displayName des Objekts, im Beispiel das Objekt user:demo. |
| Array | Dieses Element kann ein Array von Werten anzeigen, im Beispiel die Werte Value 1 und Value 2. |
| Object Array | Dieses Element kann ein Array von Objekten anzeigen, im Beispiel die Objekte user:demo und user:roi. |

### Diverse Beispiele

* * *

#### Alle Elemente auf einer card

**Hinweis**: Die Bilder im folgenden Beispiel verweisen teilweise auf UUIDs, die in Ihrem System nicht vorhanden sind. Um die Bilder anzeigen zu können, laden Sie ein Bild in Ihr System und ersetzen Sie die UUIDs im Code.

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 800,
  items: [
    {
      type: 'agorum.spacer',
      height: 10,
    },
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let attachment = num => ({
  type: 'agorum.card',
  padding: 's',
  flex: 1,
  minWidth: 200,
  name: 'attachment-' + num,
  interactive: true,
  pointer: true,
  tooltip: 'test',
  items: [
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.img',
          icon: 'ionicon:document',
          size: 40,
        },
        {
          type: 'agorum.vertical',
          flex: 1,
          items: [
            {
              type: 'agorum.text',
              text: 'Attachment ' + num,
              weight: 'bold',
            },
            {
              type: 'agorum.text',
              text: '100kb',
              size: 's',
            },
          ],
        },
      ],
    },
  ],
});

let sample = {
  type: 'agorum.card',
  mark: 'warning',
  spacing: 'xl',
  badges: [
    {
      type: 'agorum.badge',
      text: 'text + icon',
      icon: 'ionicon:heart',
      color: 'primary',
      name: 'text-icon',
    },
    {
      type: 'agorum.badge',
      text: 'longer text',
      color: 'warning',
      name: 'long-text',
    },
    {
      type: 'agorum.badge',
      text: '1',
      color: 'danger',
      name: 'priority-1',
    },
    {
      type: 'agorum.badge',
      color: 'success',
      icon: 'ionicon:checkmark',
      name: 'seen',
    },
    {
      type: 'agorum.badge',
      color: 'success',
      text: '✓',
      name: 'seen2',
    },
  ],
  items: [
    {
      type: 'agorum.vertical',
      spacing: 'm',
      items: [
        {
          type: 'agorum.horizontal',
          spacing: 'm',
          items: [
            {
              type: 'agorum.img',
              icon: 'agorum:rounded-square-5;color=#b1b1b1|agorum:folder;scale=.8;color=#ffd61c',
              size: 40,
              name: 'icon',
            },
            {
              type: 'agorum.horizontal',
              spacing: 'm',
              flex: 1,
              minWidth: 140,
              items: [
                {
                  flex: 1,
                  minWidth: 160,
                  type: 'agorum.text',
                  html: 'align center Line 1<br>Line 2<br>Line 3',
                  align: 'center',
                  weight: 'bold',
                },
                {
                  type: 'agorum.text',
                  text: 'dd.MM.yyyy HH:mm',
                  weight: 'normal',
                  align: 'end',
                },
              ],
            },
            {
              type: 'agorum.vertical',
              mark: 'primary',
              flex: 1,
              minWidth: 100,
              items: [
                {
                  type: 'agorum.text',
                  html: 'flex 1<br>minWidth 100',
                },
              ],
            },
            {
              type: 'agorum.card',
              mark: 'primary',
              flex: 2,
              minWidth: 200,
              items: [
                {
                  type: 'agorum.text',
                  html: 'flex 2<br>minWidth 200',
                },
              ],
            },
            {
              type: 'agorum.card',
              mark: 'primary',
              flex: 3,
              items: [
                {
                  type: 'agorum.text',
                  text: 'flex 3',
                },
                {
                  type: 'agorum.card',
                  mark: 'danger',
                  name: 's',
                  spacing: 's',
                  items: [
                    {
                      type: 'agorum.text',
                      text: 'spacing s',
                    },
                    {
                      type: 'agorum.button',
                      text: 'xxxx',
                      name: 'xxxx-s',
                    },
                  ],
                },
                {
                  type: 'agorum.card',
                  mark: 'danger',
                  spacing: 'm',
                  items: [
                    {
                      type: 'agorum.text',
                      text: 'spacing m',
                    },
                    {
                      type: 'agorum.button',
                      text: 'xxxx',
                      name: 'xxxx-m',
                    },
                  ],
                },
                {
                  type: 'agorum.card',
                  mark: 'danger',
                  spacing: 'l',
                  items: [
                    {
                      type: 'agorum.text',
                      text: 'spacing l',
                    },
                    {
                      type: 'agorum.button',
                      text: 'xxxx',
                      name: 'xxxx-l',
                    },
                  ],
                },
                {
                  type: 'agorum.card',
                  mark: 'danger',
                  spacing: 'xl',
                  items: [
                    {
                      type: 'agorum.text',
                      text: 'spacing xl',
                    },
                    {
                      type: 'agorum.button',
                      text: 'xxxx',
                      name: 'xxxx-xl',
                    },
                  ],
                },
              ],
            },
          ],
        },
      ],
    },
    {
      type: 'agorum.separator',
    },
    {
      type: 'agorum.horizontal',
      spacing: 's',
      items: [
        {
          type: 'agorum.chip',
          size: 's',
          text: 'Chip 1 (s)',
          icon: 'ionicon:person',
          name: 'chip-1',
        },
        {
          type: 'agorum.chip',
          text: 'Chip 2',
          icon: 'ionicon:person',
          name: 'chip-2',
          color: 'success',
        },
        {
          type: 'agorum.chip',
          text: 'Chip 3',
          icon: 'ionicon:person',
          name: 'chip-3',
          color: 'warning',
        },
        {
          type: 'agorum.chip',
          text: 'Chip 4',
          icon: 'ionicon:person',
          name: 'chip-4',
          color: 'danger',
        },
      ],
    },
    {
      type: 'agorum.text',
      text: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.',
      weight: 'normal',
    },
    {
      type: 'agorum.text',
      text: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.',
      weight: 'normal',
      width: 200,
      ellipsis: 'end',
    },
    {
      type: 'agorum.text',
      text: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.',
      weight: 'normal',
      ellipsis: 'end',
    },
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.img',
          name: 'medium-icon',
          icon: 'ionicon:heart',
          size: 50,
        },
        {
          type: 'agorum.img',
          name: 'large-icon',
          icon: 'ionicon:person|agorum:circle;slot=bottom-left;color=orange|ionicon:flash;slot=bottom-left;color=white;scale=.8',
          size: 100,
        },
        {
          type: 'agorum.img',
          name: 'small-image',
          src: 'data:image/gif;base64,R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7////wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7',
          size: 16,
        },
        {
          type: 'agorum.img',
          name: 'square-image',
          src: '/api/rest/object/embed/432667f0-45bd-11ee-82e4-02420a0a000b',
          size: 100,
        },
        {
          type: 'agorum.img',
          name: 'small-image',
          src: '/api/rest/object/embed/432667f0-45bd-11ee-82e4-02420a0a000b',
          minWidth: 148.97579,
          minHeight: 100,
        },
        {
          type: 'agorum.img',
          name: 'large-image',
          src: '/api/rest/object/embed/432667f0-45bd-11ee-82e4-02420a0a000b',
          minWidth: 100,
          width: 800,
          height: 537,
        },
      ],
    },
    {
      type: 'agorum.separator',
    },
    {
      type: 'agorum.object',
      id: '432667f0-45bd-11ee-82e4-02420a0a000b',
      name: 'agorum-object-card',
      level: 4, // 0=MINIMUM, 1=SMALL, 2=REDUCED, 3=DEFAULT, 4=MAXIMUM
      interactive: true,
      minWidth: 200,
    },
    {
      type: 'agorum.separator',
    },
    {
      type: 'agorum.horizontal',
      wrap: true,
      items: [attachment(1), attachment(2), attachment(3), attachment(4)],
    },
  ],
};

widget.down('cardView').replace(sample);

widget
  .down('cardView')
  .on('elementClicked', name => console.log('clicked', name))
  .on('elementRightClicked', name => console.log('right clicked', name))
  .on('elementDblClicked', name => console.log('dbl clicked', name));

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/47aab0f0-48c5-11ee-a4a5-005056aa0ecc)

```auto
OCR: Alle_Elemente.js,Test,align,center,Line,dd.MM.yyyy,flex,Line,Line,minWidth,100,flex,minWidth,200,flex,spacing,spacing,spacing,spacing,text,icon,longer,text,XXXX,XXXX,XXXX,XXXX,Chip,Chip,Chip,Chip,Lorem ipsum dolor sit amet consetetur sadipscing elitr sed diam nonumy eirmod tempor invidunt labore dolore magna aliquyam erat sed diam voluptua vero eos accusam justo duo dolores rebum,Stet clita kasd gubergren sea takimata sanctus est,Lorem ipsum dolor sit amet,Lorem ipsum dolor sit amet consetetur sadipscing elitr sed diam nonumy eirmod tempor invidunt labore dolore magna aliquyam erat sed diam voluptua vero eos accusam justo duo dolores rebum,Stet clita kasd gubergren sea takimata sanctus est,Lorem ipsum dolor sit amet,Lorem ipsum dolor sit amet consetetur sadipscing elitr sed diam nonumy eirmod tempor invidunt labore dolore magna aliquyam erat sed diam voluptua vero eos accusam justo duo dolores rebum,Stet clita kasd gubergren sea takimata sanctus est,...,JPG,Kimi Raikkonen_2006_test.jpg,192,9,Eigene Dateien,card,samples,resources,Home,roi,Eigene Dateien,card,samples,resources,Root,Home,roi,Eigene Dateien,card,samples,resources,Attachment,100kb,Attachment,100kb,Fires,Emirates,Emirates,Attachment,Attachment,100kb,100kb,28.08,18:09
```

Alle Elemente in einer *card*

Dieses Beispiel demonstriert die Verwendung aller Elemente, zeigt verschiedene Möglichkeiten zur Gestaltung von *cards* und enthält mehrere *agorum.card*\-Elemente, einige davon in anderen *cards* eingebettet.

Jede *card* besitzt:

* Abzeichen
* Text
* Bilder
* Chips
* Trennlinien
* Objekte
* Anzeigegruppen.
* interaktive Schaltflächen und horizontale Layouts mit Wrap.

Die Anzeigegruppe zeigt verschiedene Datentypen an, Objekte löst das System automatisch auf und macht sie anklickbar.

Event-Handler existieren, die auf Klicks auf Elemente reagieren.

#### Adress-card

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.img',
          src: '/api/rest/object/embed/432667f0-45bd-11ee-82e4-02420a0a000b',
          minWidth: 100,
          minHeight: 100,
          name: 'personImage',
        },
        {
          type: 'agorum.display.group',
          labelWidth: 80,
          sectionWidth: 200,
          items: [
            {
              label: 'Name',
              value: 'John Doe',
            },
            {
              label: 'Address',
              value: '123 Main St, Anywhere, USA',
            },
            {
              label: 'Phone',
              value: '+1-202-555-0179',
            },
            {
              label: 'Email',
              value: 'john.doe@example.com',
            },
          ],
        },
      ],
    },
    {
      type: 'agorum.button',
      text: 'Contact',
      color: 'primary',
      size: 'm',
      weight: 'bold',
      icons: 'ionicon:mail',
      name: 'contactButton',
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/a6ead8b0-48c5-11ee-a4a5-005056aa0ecc)

```auto
OCR: Name: John Doe, Address: 123 Main St, Anywhere, USA, Phone: +1-202-555-0179, Email: john.doe@example.com, Contact
```

Adress-card

#### Elemente rechtsbündig ausrichten

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 600,
  items: [
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let sample = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.vertical',
      flex: 1,
      items: [
        {
          type: 'agorum.text',
          text: 'Some text',
        },
        // use a vertical, to create a spacer between the text and the buttons
        {
          type: 'agorum.vertical',
          height: 10,
        },
        {
          type: 'agorum.horizontal',
          spacing: 'm',
          items: [
            // use a flex vertical to align the buttons on the right side
            {
              type: 'agorum.vertical',
              flex: 1,
            },
            {
              type: 'agorum.button',
              text: 'Button 1',
              name: 'button1',
            },
            {
              type: 'agorum.button',
              text: 'Button 2',
              name: 'button2',
            },
            {
              type: 'agorum.button',
              text: 'Button 3',
              name: 'button3',
            },
          ],
        },
      ],
    },
  ],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/1bf96240-48ab-11ee-a4a5-005056aa0ecc)

```auto
OCR: Rechtsbuendiges_Ausrichten.js, Test, Some, text, Button, Button, Button
```

Elemente rechtsbündig ausrichten

* Das erste Element ist ein Textelement ([agorum.text](#agorum.text)), das den Text *Some text* anzeigt.
* Ein weiteres vertikales Layout mit einer Höhe von 10 Pixeln folgt, das als Abstandshalter dient und einen Abstand zwischen dem Text und den nachfolgenden Elementen erzeugt.
* Das letzte Element ist ein horizontales Layout ([agorum.horizontal](#agorum.horizontal)), das die Elemente von links nach rechts anordnet. Innerhalb dieses Layouts sind vier Elemente definiert: ein vertikales Layout und drei Schaltflächen.
* Das vertikale Layout im horizontalen Layout dient dazu, die drei Schaltflächen an die rechte Seite des *card*\-Layouts zu schieben. Das Layout besitzt die Eigenschaft *flex=1* und füllt dadurch den verfügbaren Platz vor den Schaltflächen aus.
* Die drei Schaltflächen ([agorum.button](#agorum.button)) besitzen jeweils einen Text (*Button 1*, *Button 2* und *Button 3*) sowie einen Namen, der dem Text entspricht. Diese Namen können Sie verwenden, um auf die Schaltflächen in anderen Teilen des Codes zu verweisen.

#### Mehrere cards dynamisch nebeneinander anzeigen

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.vbox',
  background: 'dark',
  width: 800,
  items: [
    {
      type: 'agorum.spacer',
      height: 10,
    },
    {
      name: 'cardView',
      type: 'agorum.cards.view',
    },
  ],
});

let card = num => ({
  type: 'agorum.card',
  minWidth: 300,
  flex: 1,
  badges: [
    {
      type: 'agorum.badge',
      text: new Date().toLocaleString(),
      color: 'primary',
      name: 'dateBadge-' + num,
    },
  ],
  items: [
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.img',
          icon: 'ionicon:document',
          size: 40,
          name: 'icon-' + num,
        },
        {
          type: 'agorum.text',
          text: 'Card ' + num,
          weight: 'bold',
          name: 'headline-' + num,
        },
      ],
    },
    {
      type: 'agorum.text',
      html: '<p>This is the content of card ' + num + '.</p>',
      name: 'content-' + num,
    },
  ],
});

let sample = {
  type: 'agorum.horizontal',
  spacing: 'xl',
  wrap: true,
  items: [card(1), card(2), card(3), card(4), card(5), card(6)],
};

widget.down('cardView').replace(sample);

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/342e5310-48ac-11ee-a4a5-005056aa0ecc)

```auto
OCR: Mehrere_Cards_dynamisch.js (Test), September 1, 2023 11:43:56 AM CEST, Card 1, Card 2, This is the content of card 1., September 1, 2023 11:43:56 AM CEST, Card 3, - x, September 1, 2023 11:43:56 AM CEST, This is the content of card 2., September 1, 2023 11:43:56 AM CEST, Card 4, This is the content of card 3., This is the content of card 4., September 1, 2023 11:43:56 AM CEST, Card 5, September 1, 2023 11:43:56 AM CEST, Card 6, This is the content of card 5., This is the content of card 6.
```

Mehrere *cards* dynamisch nebeneinander anzeigen

Dieses Beispiel zeigt ein horizontales Layout, das ein Array von sechs *cards* enthält.

* Das System verwendet die Eigenschaft *wrap*, damit *cards* automatisch in die nächste Zeile springen, wenn der Platz in der aktuellen Zeile nicht mehr ausreicht.
* Jede *card* besitzt eine minimale Breite von 300 Pixeln.

## agorum.cards.view

Dieses Widget bildet den Kern von *agorum core cards* und enthält diverse Funktionen, mit denen Sie den Inhalt Ihrer cards erzeugen und bearbeiten.

### Verwendung

* * *

Dieses Widget zeigt etwa eine Liste von *agorum.object-cardlets* an:

```auto
let aguila = require('common/aguila');
let objects = require('common/objects');

let widget = aguila.create({
  type: 'agorum.cards.view',
  scrolling: true,
  background: 'light',
  width: 600,
  height: 800
});

aguila
.fork(() => objects.find('home:MyFiles').items().map(item => item.UUID))
.then(ids => {
  widget.replace({
    type: 'agorum.vertical',
    items: ids.map(id => ({
      type: 'agorum.object',
      id: id,
      name: id,
      selectable: true
    }))
  });
});

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/28618cb0-2ed8-11ef-8dc6-005056aa0ecc)

```auto
OCR: agorum.object, cardlets.js, Test, TXT, test1.txt, 149,0, Eigene Dateien, tmp, 18.01, 18:56, TXT, test2.txt, 87,5, Eigene Dateien, tmp, agorum.object, cardlets.js, 584 Byte, Eigene Dateien, tmp, 22.01, 08:45, vor min
```

Darstellung einer Liste von *agorum.object-cardlets*

### Parameter

* * *

#### scrolling

| Wert | Beschreibung |
| --- | --- |
| true | Blendet Scrollbalken ein, wenn die Höhe des Inhalts die Höhe des Widgets übersteigt. |
| false (Standard) | Scrollbalken aus, wenn die Höhe des Inhalts die Höhe des Widgets übersteigt. |

#### selection

Enthält ein Array mit den *name*\-Attributen aller aktuell selektierten Elemente.

* Ändert sich dieser Parameter, ändert sich auch die dargestellte Selektion.
* Das System kann ein Element nur selektieren, wenn es die Eigenschaft *name* besitzt und der Parameter *selectable* auf *true* gesetzt ist.

### Events

* * *

Sie können neben den fest definierten Ereignissen auf diesem Widget cardlet-Ereignisse auslösen, wenn diese nicht schon von cardlet-Handlern behandelt wurden.

#### more

Löst aus, sobald das System das Widget mit [scrolling: true](#scrolling) erzeugt hat und sich die Scrollposition dem unteren Ende nähert.

Verwenden Sie diesen Event, um dynamisch weitere Einträge einer größeren Liste nachzuladen und hinzuzufügen.

### Funktionen

* * *

#### Allgemeines zu Modifikator-Funktionen

Modifikator-Funktionen ([remove](#remove), [replace](#replace), [insert](#insert), [append](#append)) erwarten unter anderem eine Folge von Namen als Parameter, um das Basiselement für die jeweilige Modifikation anzugeben. Hierbei wird jeweils das erste passende Element über eine Breitensuche gewählt. Geben Sie keinen Namen an, spricht das System immer das oberste Element an (root element).

Wird hier etwa die Kombination 'list', 'item2' als Parameter angegeben, wird ausgehend vom obersten Element zunächst nach einem Element mit dem Namen *list* gesucht, dann von dort aus weiter ein Element mit dem Namen *item2*. Das gefundene Element ist dann das Basiselement für die Modifikation, im Fall von [remove](#remove) würde dieses also entfernt werden.

#### more()

Weist das Widget an, das Ereignis wieder freizugeben, sodass es erneut ausgelöst werden kann, wenn das gleichnamige Ereignis *more* bereits ausgelöst wurde und aktuell unterdrückt wird.

Für dynamisch nachladende Listen ergibt sich folgender Ablauf:

1. Liste erzeugen und initiale Einträge darstellen.
2. Sobald das Ereignis *more* ausgelöst wird, weitere Einträge erzeugen und darstellen. Abbrechen, wenn keine weiteren Einträge vorhanden sind.
3. Die Funktion *more()* aufrufen.
4. Zurück zu 2.

#### reset()

Setzt die horizontale und vertikale Scrollposition des Widgets zurück auf den Anfang.

#### remove(name, ...)

Entfernt das referenzierte Basiselement.

```auto
view.remove('list', '12345');
```

#### replace(name, ..., def)

Ersetzt das referenzierte Basiselement durch das über *def* beschriebene cardlet.

```auto
view.replace('list', '12345', {
  type: 'agorum.object',
  name: '12345',
  id: '12345'
});
```

#### insert(name, ..., def)

Fügt dem referenzierten Basiselement das über *def* beschriebene cardlet als Unterelement hinzu.

```auto
view.insert('list', {
  type: 'agorum.object',
  name: '12345',
  id: '12345'
});
```

#### append(name, ..., def)

Fügt hinter dem referenzierten Basiselement das über *def* beschriebene cardlet hinzu.

Führen Sie diese Änderung nicht auf dem äußersten Element (root-Element) durch.

```auto
view.append('list', '12344', {
  type: 'agorum.object',
  name: '12345',
  id: '12345'
});
```

## agorum.cards.list

Dieses Widget verwendet eine [agorum.cards.view](#), um Objektlisten anzuzeigen.

* Das System erzeugt für jedes darzustellende Objekt ein cardlet des Typs *agorum.object* und setzt dessen Eigenschaft *id* auf die UUID des Objekts.
* Die Suche verwendet dieses Widget etwa für die Anzeige von Suchergebnissen.
* Das System lädt bei umfangreichen Listen zunächst nur die ersten Einträge und blendet erst nach dem Scrollen weitere Einträge ein.

### Verwendung

* * *

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.cards.list',
  query: 'inpath:${ID:/agorum/roi/Files}'
});

widget;
```

### Parameter

* * *

Das Widget reicht alle Parameter an die erzeugten agorum.object-cardlets weiter.

**Hinweis**: Setzen Sie bei diesem Widget zwingend einen der folgenden Parameter:

* id

* ids

* query

#### id

Stellt den Inhalt eines Ordners in einer Liste dar, indem Sie diesen Parameter auf die ID des Ordners setzen.

#### ids

Stellt die zugehörigen Objekte in einer Liste dar, indem Sie diesen Parameter auf ein Array aus IDs setzen.

#### query

Stellt das Suchergebnis in einer Liste dar, indem Sie diesen Parameter auf eine Suchanfrage setzen.

#### sort

Legt die Sortierung der Objekte in der Liste fest.

Das Widget erwartet ein Array in diesem Format:

```auto
[
  {
    property: 'property',
    descending: true/false
  }
]
```

**Werte für Parameter „descending“**

| Wert | Beschreibung |
| --- | --- |
| true | Sortiert die Objekte des Parameters property in absteigender Reihenfolge. |
| false (Standard) | Sortiert die Objekte des Parameters property in aufsteigender Reihenfolge. |

Geben Sie mehrere Sortierungen an, sortiert das System diese nach ihrer Reihenfolge absteigend.

#### readOnly

| Wert | Beschreibung |
| --- | --- |
| true | Verbietet eine Ablage per Drag-and-drop und bei statischen Listen die Aktionen Einfügen und Entfernen (letzteres nur möglich, sofern Sie den Parameter id gesetzt haben). |
| false (Standard) | Erlaubt eine Ablage per Drag-and-drop. |

#### selection

Enthält ein Array mit den UUIDs aller aktuell selektierten Objekte.

Ändert sich dieser Parameter, ändert sich auch die dargestellte Selektion.

#### loading

Ist automatisch *true*, während die Liste erstmalig oder nachträglich lädt.

#### lastSeen

Stellt eine Trennlinie zwischen Objekten dar, die zeitlich vor oder nach einem gegebenen Zeitpunkt liegen.

* Sie können diesen Parameter in Kombination mit dem Parameter [sort](#sort) verwenden.
* Das System sortiert nach einer Datums-/Uhrzeit-Eigenschaft (etwa *lastModifyDate*).
* Das System setzt einen Zeitstempel im UNIX-Format (wie es von *Date.getTime()* zurückgeliefert wird) für diesen Parameter.

**Beispiel für eine Suchliste mit einer Trennlinie am 04.12.2022 um 00:00**

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.cards.list',
  query: 'inpath:${ID:/agorum/roi/Files}',
  lastSeen: new Date(2022, 11, 4).getTime(),
  sort: [
    {
      property: 'lastModifyDate',
      descending: true
    }
  ]
});

widget;
```

## agorum.object

Dieses cardlet stellt jeweils ein Objekt (referenziert über den Parameter *id*) dar und verwendet [decorators](#), um die Erzeugung des cardlets übersichtlich und modular zu halten. Die decorators erzeugen Stück für Stück die anzuzeigende Element-Struktur.

### Verwendung

* * *

Das cardlet erzeugen Sie im Regelfall im Rahmen des Widgets [agorum.cards.list](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(c220c1d0-763e-11ed-8901-005056aa0ecc\)&detailsId=c220c1d0-763e-11ed-8901-005056aa0ecc) automatisch. Sie können es jedoch für ein einzelnes Objekt gezielt darstellen, etwa in der Details-Ansicht für einige Objekttypen.

**Beispiel für die Verwendung zur Darstellung des Ordners „/agorum/roi/Files“**

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.cards.view',
  scrolling: true,
  background: 'light',
  width: 600,
  height: 800
});

widget.replace({
  type: 'agorum.object',
  id: '/agorum/roi/Files'
});

widget;
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/3587ae00-2ed9-11ef-8dc6-005056aa0ecc)

```auto
OCR: agorum.object-cardlets-Files.js (Test), Dateien, 16 Objekte, Root/agorum/roi, 29.12.2004 08:47, agorum.object, cardlets, Files.js, Test, Dateien, Objekte, Root, agorum, roi, 29.12.2004, 08:47
```

Darstellung des Ordners „/agorum/roi/Files“

### Automatische Aktualisierung

* * *

Ändern Sie ein Objekt, erzeugt das System alle agorum.object-cardlets neu, die dieses Objekt aktuell darstellen. Das gilt auch dann, wenn diese cardlets als Teil eines größeren cardlets dargestellt werden, etwa die Attachments eines Workflows oder das Hauptobjekt, an dem eine Notiz hängt.

## JavaScript-Bibliothek agorum.cards/js/decorators

Diese JavaScript-Bibliothek dient zur Unterstützung der Entwicklung von [decorators](#) und enthält Funktionen, mit denen Sie Elemente in einem gegebenen cardlet finden und ändern können.

### Verwendung

* * *

Diese Bibliothek binden Sie stets am Anfang eines Skripts ein:

```auto
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');
```

### Funktionen

* * *

#### down

Sucht innerhalb einer cardlet-Definition nach einem Element mit dem gegebenen Namen und gibt dieses zurück.

**Syntax**

```auto
let element = decorators.down(cardlet, name);
```

**Parameter**

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| cardlet | Definiert die cardlet-Definition, in der das System sucht. | ja |
| name | Definiert den Namen des Elements, nach dem das System sucht. | ja |

**Beispiel**

```auto
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');

let cardlet = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.text',
          name: 'test',
          text: 'Test-Element'
        }
      ]
    }
  ]
};

let element = decorators.down(cardlet, 'test');

element;
```

#### with

Sucht innerhalb einer cardlet-Definition nach einem Element mit dem gegebenen Namen und ruft die übergebene Funktion mit diesem als Parameter auf.

Das System ruft die Funktion nicht auf, wenn es kein passendes Element findet.

**Syntax**

```auto
let element = decorators.with(cardlet, name, fn);
```

**Parameter**

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| cardlet | Definiert die cardlet-Definition, in der das System sucht. | ja |
| name | Definiert den Namen des Elements, nach dem das System sucht. | ja |
| fn | Definiert die Funktion, die das System mit dem gefundenen Element aufruft. | ja |

**Beispiel**

```auto
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');

let cardlet = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.text',
          name: 'test',
          text: 'Test-Element'
        }
      ]
    }
  ]
};

decorators.with(cardlet, 'test', element => {
  // ...
});
```

#### remove

Entfernt innerhalb einer cardlet-Definition ein Element mit dem gegebenen Namen.

**Hinweis**: Das System markiert das zu entfernende Element lediglich als solches und entfernt es erst in einem späteren Schritt, nachdem alle decorators ausgeführt wurden, um die Performance nicht zu beeinträchtigen.

**Syntax**

```auto
decorators.remove(cardlet, name);
```

**Parameter**

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| cardlet | Definiert die cardlet-Definition, die das System ändert. | ja |
| name | Definiert den Namen des Elements, das das System entfernt. | ja |

**Beispiel**

```auto
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');

let cardlet = {
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      items: [
        {
          type: 'agorum.text',
          name: 'test',
          text: 'Test-Element'
        }
      ]
    }
  ]
};

decorators.remove(cardlet, 'test');
```

#### state

Ruft ein Objekt ab, in dem ein decorator Zustandsinformationen hinterlegen kann, die erhalten bleiben, auch wenn das zugehörige agorum.object-cardlet neu erzeugt wird.

**Syntax**

```auto
let state = decorators.state(def, key, defaults);
```

**Parameter**

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| def | Definiert die agorum.object-cardlets-Definition, die decorators als Parameter erhalten. | ja |
| key | Definiert eine eindeutige Bezeichnung für das Zustandsobjekt. | ja |
| defaults | Definiert eine Vorbelegung, die das System verwendet, wenn das Zustandsobjekt initial erzeugt wird. | nein |

**Beispiel**

```auto
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');

module.exports = (cardlet, object, def) => {
  let state = decorators.state(def, 'my.decorator.state', {
    expanded: false
  });

  if (state.expanded) {
    // ...
  }
};
```

**Verwendung**

Das zurückgelieferte Zustandsobjekt wird typischerweise an ein cardlet weitergereicht, das vom decorator erzeugt wird und das dieses verwendet, um seinen Zustand bei Neuerstellung beizubehalten. Das hier verwendete Pfadanzeige-cardlet hinterlegt etwa, ob der Benutzer es aktuell aufgeklappt hat oder nicht.

#### text, html, defaultText, defaultHtml

Diese Funktionen vereinfachen die Arbeit mit den beiden Attributen *text* und *html*, die von cardlets angeboten werden, die Text darstellen, etwa *agorum.text* oder *agorum.button*.

**Syntax**

```auto
decorators.text(cardlet, name, fn);
decorators.html(cardlet, name, fn);
decorators.defaultText(cardlet, name, fn);
decorators.defaultHtml(cardlet, name, fn);
```

**Parameter**

Die Parameter dieser Funktionen verhalten sich analog zu denen der Funktion [with](#with). Lediglich der Rückgabewert der Funktion *fn* wird zusätzlich verwendet, um den Wert des Attributs (*text* oder *html*) festzulegen.

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| cardlet | Definiert die cardlet-Definition, in der das System sucht. | ja |
| name | Definiert den Namen des Elements, nach dem das System sucht. | ja |
| fn | Definiert die Funktion, die das System mit dem gefundenen Element aufruft. Der Rückgabewert dieser Funktion wird als Wert des zu setzenden Attributs verwendet. | ja |

**Funktionsweise**

| Funktion | Beschreibung |
| --- | --- |
| text | Setzt den Wert des Attributs text und löscht das Attribut html, sofern dieses vorhanden ist. |
| html | Setzt den Wert des Attributs html und löscht das Attribut text, sofern dieses vorhanden ist. |
| defaultText | Setzt den Wert des Attributs text, sofern weder text noch html bisher einen Wert besitzen. |
| defaultHtml | Setzt den Wert des Attributs html, sofern weder text noch html bisher einen Wert besitzen. |

**Beispiel**

```auto
decorators.text(cardlet, 'title', () => 'Neuer Titel im Text-Format');

decorators.html(cardlet, 'title', () => 'Neuer Titel im <strong>HTML</strong>-Format');

decorators.defaultText(cardlet, 'subject', () => 'Kein Betreff');

decorators.defaultText(cardlet, 'subject', () => '<em>Kein Betreff</em>');
```

## JavaScript-Bibliothek agorum.cards/js/cards

Diese JavaScript-Bibliothek dient zur Unterstützung der Entwicklung von cardlets und [decorators](#).

### Verwendung

* * *

Diese Bibliothek binden Sie stets am Anfang eines Skripts ein:

```auto
let cards = require('/agorum/roi/customers/agorum.cards/js/cards');
```

### Funktionen

* * *

#### eventHandler

Erzeugt einen standardisierten Ereignis-Handler, der als Funktion *event* eines cardlet-Handlers verwendet werden kann.

Der Cardlet-Handler nimmt alle einkommenden Ereignisse des cardlets entgegen und leitet sie an je Zielelement und Ereignistyp registrierte Funktionen weiter.

**Syntax**

```auto
let event = cards.eventHandler();
```

Das zurückgegebene Objekt *event* bietet folgende Funktionen:

**path**

Leitet die Registrierung einer Funktion als Handler für ein spezifisches Ereignis ein.

***Syntax***

```auto
event.path(<path>).on(<type>, <handler>);
```

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| path | Definiert eine Folge von Zeichenketten-Parametern, die einschränken, auf welche Zielelemente der Handler reagiert. Der Handler wird nur aufgerufen, wenn der Pfad bis zu einem Element all diese Namen enthält (siehe Eigene cardlets erstellen). | nein |
| type | Definiert den Namen des Ereignistyps, auf den der Handler reagiert. | ja |
| handler | Definiert die Funktion, die als Handler registriert werden soll und für passende Ereignisse aufgerufen wird. | ja |

Tritt ein passendes Ereignis ein, ruft das System die Handler-Funktion mit dem cardlet-Kontext (siehe [Eigene cardlets erstellen](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(157bef80-3ff3-11ed-9c7e-005056aa0ecc\)&detailsId=157bef80-3ff3-11ed-9c7e-005056aa0ecc)) und dem (optionalen) Parameter des Ereignisses auf.

Beispiel für einen Schaltflächen-Handler, der auf Ereignisse des Typs *elementClicked* unterhalb des Pfads *\[ 'buttons', 'ok' \]* reagiert:

```auto
event.path('buttons', 'ok').on('elementClicked', (cx, param) => {
  // ...
});
```

**link**

Definiert Link-Typen. HTML-Hyperlinks und interaktive Elemente gelten als Links, deren Namen diesem Schema entsprechen:

```auto
<Link-Typ>:<Link-Parameter>
```

* Der Link-Typ ist eine Zeichenkette, die aus Kleinbuchstaben und Punkten bestehen darf.
* Bei Verwendung von HTML-Hyperlinks dürfen die Link-Parameter nur Zeichen enthalten, die in HTML-Attributen erlaubt sind.
* Bei Bedarf kann die Funktion *escape* der Bibliothek [common/html](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(1c511b50-d59d-11e9-a4ef-005056aa0ecc\)&detailsId=1c511b50-d59d-11e9-a4ef-005056aa0ecc) verwendet werden.

Folgende Link-Typen sind vordefiniert:

| Link-Typ | Beschreibung |
| --- | --- |
| object:<id/ref> | Verweist auf ein agorum-Objekt und bietet das Kontextmenü (Rechtsklick) und Öffnen-Aktion (Linksklick) an. |
| action:<action>:<parent>:<id1>:<id2>:... | Führt bei einem Linksklick die als action angegebene Aktion mit den als parent und idX angegebenen Objekten als folder und objects aus. |
| call:<service>:<args> | Ruft bei einem Linksklick den als service registrierten Dienst mit den Argumenten args auf. |

**Weitere Link-Typen definieren**

Sie können über die Funktion *link* weitere Link-Typen definieren, die innerhalb des aktuellen cardlets unterstützt werden sollen.

***Syntax***

```auto
event.link(<type>, <handler>);
```

| Parameter | Beschreibung | Pflicht |
| --- | --- | --- |
| type | Definiert den Namen des Link-Typs, auf den der Handler reagiert. | ja |
| handler | Definiert die Funktion, die das System als Handler registriert und für passende Links aufruft. | ja |

Klickt ein Benutzer einen derart registrierter Link an, ruft das System den hier registrierten Handler mit dem cardlet-Kontext (siehe [Eigene cardlets erstellen](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(157bef80-3ff3-11ed-9c7e-005056aa0ecc\)&detailsId=157bef80-3ff3-11ed-9c7e-005056aa0ecc)), dem Link-Parameter und dem Namen der verwendeten Maustaste (left, right oder middle) auf.

Beispiel für einen Link-Handler, der auf Links des Typs agorum.log reagiert:

```auto
event.link('agorum.log', (cx, params, button) => {
  console.log('agorum.log', params, button);
});
```

Beispiel für die Verwendung eines Links in HTML:

```auto
<a name="agorum.log:Hallo Welt!">Test-Link</a>
```

Beispiel für die Verwendung eines Links in einem Element:

```auto
{
  type: 'agorum.chip',
  name: 'agorum.log:Hallo Welt!',
  text: 'Test-Link'
}
```

Beispiel für einen Objekt-Link in HTML:

```auto
Hier ist das gesuchte <a name="object:13bc3565-2a2e-4764-b9ec-e61944a3ac73">Dokument</a>.
```

#### link

Erstellt einen Objekt-Link aus einem Objekt, einer Objekt-ID oder einer Objektreferenz.

**Syntax**

```auto
let name = cards.link(<object/id/ref>);
```

**Parameter**

Sie können als Parameter *object/ref* entweder direkt ein agorum-Objekt übergeben oder eine Beschreibung eines agorum-Objekts in Form einer Objektreferenz. Letzteres verwenden Sie, wenn weder das zugehörige Objekt noch eine ID davon vorliegt, aber etwa eine Beschreibung, die in einer Indexsuche verwendet werden kann, um das Objekt zu finden. In diesem Fall wird das referenzierte Objekt erst bei Betätigung des Links gesucht, um unnötige Verzögerungen bei der Darstellung des cardlets zu vermeiden.

Für die Auflösung solcher Objektreferenzen sind resolver zuständig. Mitgeliefert ist der resolver *agorum.search*, der eine Objektreferenz per Indexsuche ermöglicht.

Ein Beispiel für die Verwendung einer Objektreferenz mit resolver *agorum.search* wäre:

```auto
cards.link({
  resolver: 'agorum.search',
  query: 'identifier:Lieferantenakte lieferantennummer:123456'
});
```

Bei einem Rechtsklick auf einen solchen Link würde die Lieferantenakte mit Lieferantennummer 123456 gesucht und deren Kontextmenü angezeigt werden.

**Rückgabewerte**

Sie erhalten eine Zeichenkette zurück, die Sie als Name eines HTML-Hyperlinks oder als Name eines Elements verwenden können.

#### resolve

Löst die übergebene Objektreferenz in eine Objekt-ID (typischerweise die UUID des Objekts) auf.

Diese Funktion ist hauptsächlich für die interne Anwendung bei agorum gedacht.

**Syntax**

```auto
let id = cards.resolve(<ref>);
```

**Parameter**

Übergeben Sie als Parameter die Objektreferenz, wie sie für einen Link verwendet werden könnte.

**Rückgabewerte**

Sie erhalten den Rückgabewert des aufgerufenen resolvers, im Regelfall die UUID des gefundenen Objekts.

## Eigene cardlets erstellen

Sie können einen eigenen cardlet-Typ erstellen, etwa wenn Sie Teile einer Ansicht wiederverwenden möchten oder wenn eine eigene Ereignisbehandlung erforderlich ist.

### cardlet-Handler

* * *

Ein cardlet-Handler ist eine JavaScript-Bibliothek, die die Funktionen *build* und *event* exportiert.

#### build

Das System ruft diese Funktion auf, wenn ein [agorum.cards.view](#)\-Widget ein cardlet des zugehörigen Typs darstellen soll.

* Die Funktion erhält als Parameter ihre zu erzeugenden cardlets und die Definition, die zur Erstellung verwendet wurde.
* Die Funktion erwartet als Rückgabewert das erstellte cardlet.

```auto
let build = (cx, def) => {
  // ...
};
```

**cx**

Sie können den cardlet-Kontext in der build-Funktion dazu verwenden, um Informationen über den inneren Zustand des cardlets zu hinterlegen, die später für die Verarbeitung von Events notwendig sind.

In folgendem Beispiel würde das System etwa für ein aufklappbares cardlet die Information speichern, ob das cardlet gerade geöffnet oder geschlossen ist:

```auto
cx.meta = {
  expanded: false
};
```

**Hinweis**: Sie können ausschließlich das Feld *meta* des Kontexts zur Speicherung von Zustandsinformationen verwenden.

**def**

Übergibt zusätzliche Parameter, die für deren Darstellung relevant sind.

#### event

Das System ruft diese Funktion auf, wenn ein Ereignis innerhalb des cardlets ausgelöst und noch nicht von einem anderen handler behandelt wurde.

Die Funktion erhält als Parameter:

* den cardlet-Kontext
* den Namen des Ereignis-Typs
* den relativen Pfad zu dem Element, auf dem das Ereignis ausgelöst wurde
* einen eventuellen Parameter, der zu diesem Ereignis gehört

```auto
let event = (cx, type, path, param) => {
 // ...
};
```

**Tipp**: Verwenden Sie die JavaScript-Bibliothek [agorum.cards/js/cards](#), um gezielt auf bestimmte Ereignisse von bestimmten Elementen zu reagieren.

**cx**

Sie können den cardlet-Kontext in der event-Funktion neben dem Zugriff auf das Feld *meta* dazu verwenden, um das cardlet selbst zu ändern und eigene Ereignisse auszulösen (siehe [cardlet-Kontext](#cx)).

**type**

Übergibt den Namen des Ereignis-Typs.

Zur Übersicht der Standard-Ereignistypen siehe [Standard-Ereignisse](#type)

**path**

Enthält ein Array aus den Namen aller benannten Elemente ab dem cardlet selbst bis zu dem Zielelement des Ereignisses.

```auto
{
  type: 'agorum.card',
  items: [
    {
      type: 'agorum.horizontal',
      name: 'buttons',
      items: [
        {
          type: 'agorum.button',
          name: 'ok',
          text: 'OK'
        },
        {
          type: 'agorum.button',
          name: 'cancel',
          text: 'Cancel'
        }
      ]
    }
  ]
}
```

Ein Klick auf die OK-Schaltfläche dieses cardlets würde diesen Pfad zur Folge haben:

```auto
[ 'buttons', 'ok' ]
```

**param**

Übergibt weitere Daten über das ausgelöste Ereignis.

### cardlet-Kontext

* * *

Das System übergibt den Funktionen *build* und *event* jeweils als erster Parameter den cardlet-Kontext. Während dieser in der build-Funktion nur verwendet werden kann, um Zustandsinformationen im Feld *meta* zu hinterlegen, existieren in der event-Funktion weitere Möglichkeiten.

#### Allgemein

Die Modifikator-Funktionen *remove*, *replace*, *insert* und *append* erwarten jeweils einen (optionalen) Pfad als die ersten n-Parameter, der das Zielelement dieser Modifikation adressiert.

Geben Sie den Pfad nicht an, bezieht sich die Modifikation auf das gesamte cardlet, zu dem dieser Kontext gehört.

**Beispiel für die Adressierung eines Unterelements**

```auto
cx.replace('buttons', 'ok', {
  type: 'agorum.button',
  name: 'ok',
  text: 'OK'
});
```

**Beispiel für die Adressierung des gesamten cardlets**

```auto
cx.append({
  type: 'agorum.display',
  text: 'Neuer Text'
});
```

#### remove

Entfernt ein Element aus der cardlet-Struktur.

```auto
cx.remove(<path>);
```

#### replace

Entfernt ein Element aus der cardlet-Struktur und ersetzt es durch ein neues.

```auto
cx.replace(<path>, <def>);
```

#### append

Fügt dem Zielelement ein neues Unterelement hinzu.

```auto
cx.append(<path>, <def>);
```

#### insert

Fügt ein neues Element vor dem Zielelement ein.

```auto
cx.insert(<path>, <def>);
```

#### fire

Löst ein benutzerdefiniertes Ereignis aus, das von einem übergeordneten cardlet-Handler behandelt werden kann.

```auto
cx.fire(<type>, <param>);
```

**Hinweis**: Der auslösende cardlet-Handler kann ein derart ausgelöstes Ereignis nicht selbst behandeln, sondern propagiert es strikt aufwärts.

### Standard-Ereignisse

* * *

#### elementClicked, elementRightClicked, elementMiddleClicked, elementDblClicked

Löst aus, sobald ein Benutzer auf Elemente klickt, die Sie als *interactive: true* oder *selectable: true* definiert haben.

#### linkClicked, linkRightClicked, linkMiddleClicked, linkDblClicked

Löst aus, sobald ein Benutzer auf Links innerhalb von Elementen des Typs *agorum.text* klickt, die ein name-Attribut besitzen.

**Beispiel für einen Link**

```auto
<a name="link-name">Link-Text</a>
```

#### inserted

Löst aus, sobald das System das cardlet in die Gesamtstruktur eingefügt hat.

* Das cardlet erhält als Parameter die eindeutige ID des cardlets.
* Sie können das Ereignis höchstens einmal pro cardlet auslösen.

**Hinweis**: Nachdem ein cardlet durch die build-Funktion erstellt wurde, kann einige Zeit vergehen, bis die zugehörige cardlet-Struktur vollständig erstellt ist und das System dieses cardlet in die für den Benutzer sichtbare Struktur einhängt. Es ist auch möglich, dass ein cardlet erzeugt, aber niemals verwendet wird, weil die darin angezeigten Daten bereits veraltet sind und schon eine neue Ansicht erzeugt wird.

#### ejected

Löst aus, sobald das System ein cardlet aus der sichtbaren Struktur entfernt, entweder direkt auf cardlet-Ebene oder durch Zerstörung des umgebenden Widgets.

* Das cardlet erhält als Parameter die eindeutige ID des cardlets.
* Sie können das Ereignis höchstens einmal pro cardlet auslösen.

### Einen cardlet-Handler anlegen und registrieren

Siehe [cards cardlet registrieren](#).

### Einen cardlet-Handler implementieren

* * *

Zur Illustration der Konzepte der vorherigen Abschnitte folgt ein Beispiel für einen cardlet-Handler mit internem Zustand (Anzahl Klicks auf *OK*), Ereignisbehandlung, Modifikationen und selbst ausgelösten Ereignissen:

```auto
let cards = require('/agorum/roi/customers/agorum.cards/js/cards');

// build() and event handlers are called outside the UI thread
let build = (cx, def) => {
  // the cx.meta field is saved alongside the built cardlet and can be used in event handlers
  cx.meta = {
    count: 0
  };

  return {
    type: 'agorum.card',
    items: [
      {
        type: 'agorum.horizontal',
        items: [
          {
            type: 'agorum.img',
            icon: def.icon,
            size: 32
          },
          {
            type: 'agorum.display',
            name: 'display',
            text: def.text,
            size: 'l'
          }
        ]
      },
      {
        type: 'agorum.horizontal',
        name: 'buttons',
        items: [
          {
            type: 'agorum.button',
            name: 'ok',
            text: 'OK'
          },
          {
            type: 'agorum.button',
            name: 'cancel',
            text: 'Cancel'
          }
        ]
      }
    ]
  };
};

let event = cards.eventHandler();

event.path('buttons', 'ok').on('elementClicked', (cx, param) => {
  // increase the number of clicks
  ++cx.meta.count;

  // replace the OK button to change its text
  cx.replace('buttons', 'ok', {
    type: 'agorum.button',
    name: 'ok',
    text: 'OK (' + cx.meta.count + ')'
  });

  // fire an event that can be handled by the containing cardlet
  cx.fire('ok', cx.meta.count);
});

event.path('buttons', 'cancel').on('elementClicked', (cx, param) => {
  // reset the number of clicks
  cx.meta.count = 0;

  // replace the OK button to reset its text
  cx.replace('buttons', 'ok', {
    type: 'agorum.button',
    name: 'ok',
    text: 'OK'
  });

  // fire an event that can be handled by the containing cardlet
  cx.fire('cancel');
});

module.exports = {

  build: build,
  event: event

};
```

Registrieren Sie diesen cardlet-Handler etwa als *beispiel.paket.mein.cardlet*, können Sie ihn etwa in einem aguila-Skript verwenden:

```auto
let aguila = require('common/aguila');

let widget = aguila.create({
  type: 'agorum.cards.view',
  width: 400,
  height: 200
});

widget.replace({
  type: 'beispiel.paket.mein.cardlet',
  text: 'Beispieltext\nZeile 2',
  icon: 'mdi:warning;color=FireBrick'
});

widget
.on('ok', count => {
  console.log('ok', count);
})
.on('cancel', () => {
  console.log('cancel');
});

widget;
```

Das System leitet die durch das cardlet ausgelösten cardlet-Ereignisse *ok* und *cancel* automatisch inklusive ihrer Parameter als aguila-Ereignisse weiter, wenn sie nicht von einem cardlet-Handler behandelt werden.

## Eigene decorators erstellen

Zur Darstellung von Objekten verwendet *agorum core* an vielen Stellen cardlet-basierte Listen oder Ansichten. Für jedes darzustellende Objekt erzeugt das System ein cardlet des Typs *agorum.object*, das für die Anzeige dieses Objekts verantwortlich ist. Je nach Typ und Eigenschaften des Objekts kann diese unterschiedlich ausfallen, etwa sind bei einer E-Mail andere Daten interessant als bei einem Ordner.

Um die Darstellung von Objekten flexibel und erweiterbar gestalten zu können, greift das [agorum.object](#)\-cardlet auf decorators zurück, die sich um die Ermittlung und Anzeige der Daten kümmern. Ein decorator hat immer eine definierte Aufgabe, wie die Anzeige des Icons oder des Dateinamens.

*agorum core* liefert für viele Standard-Merkmale von Objekten bereits decorators mit. Im Rahmen von Projektanforderungen, etwa das Darstellen weiterer Daten für Objekte oder das Ausblenden bestehender, können Sie eigene decorators einbinden.

**Wichtig**: Achten Sie bei der Entwicklung von decorators auf die Performance. Ein einziger langsamer decorator kann die Darstellung von Listen stark verzögern, denn [agorum.object](#)\-cardlets können immer erst dargestellt werden, wenn alle decorators ihre Arbeit abgeschlossen haben. Tätigen Sie keine potenziell langsamen Operationen wie Suchen oder Zugriffe auf externe Datenquellen.

### Definition

* * *

Ein decorator ist eine JavaScript-Bibliothek, die eine einzelne Funktion exportiert. [agorum.object](#)\-cardlets rufen diese Funktion jedes Mal auf, wenn ein Objekt dargestellt werden soll, unabhängig vom Typ dieses Objekts.

```auto
module.exports = (cardlet, object, def) => {
  // ...
};
```

#### Parameter

| Parameter | Beschreibung |
| --- | --- |
| cardlet | Definiert das von den zuvor aufgerufenen decorators erzeugte cardlet. Der decorator führt ggf. nötige Modifikationen durch. |
| object | Definiert das Objekt, das das System darstellt. |
| def | Definiert die cardlet-Definition, die das System zur Erstellung des agorum.object-cardlets verwendet hat. Eventuell sind Parameter vorhanden, die die Darstellung beeinflussen. |

### Einen decorator anlegen und registrieren

* * *

siehe [cards decorator registrieren](#)

### Einen decorator implementieren

* * *

Der Aufbau eines decorators wird im Folgenden anhand des mitgelieferten icon-decorators beschrieben:

```auto
let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');
let icons = require('/agorum/roi/customers/agorum.icons/js/icons');

module.exports = (cardlet, object) => decorators.with(cardlet, 'icon', icon => icon.icon = icons.object(object).icon);
```

Das Beispiel verwendet neben der icons-Bibliothek die JavaScript-Bibliothek [agorum.cards/js/decorators](#), die Funktionen zum einfachen Einfügen, Ändern und Entfernen von Informationen in dem zu erstellende cardlet enthält.

Das Beispiel sucht das Element mit dem Namen *icon* und hinterlegt dort das von *icons.object()* ermittelte Objekt-Icon, sofern es gefunden wurde. Das Element selbst wurde dabei schon von einem vorhergehenden decorator erzeugt, der für das grundsätzliche Layout des cardlets verantwortlich ist.

Aktuell sind folgende Elemente für die Verwendung in decorators verfügbar:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| icon | agorum.img | Definiert das Icon, das für dieses Objekt erscheint. Im Standardfall handelt es sich hierbei um das Icon, das icons.object() zurückliefert. Ein abweichendes Icon kann dargestellt werden, etwa das Bild des Absenders für Notizen. Für eine indirekte Art, eine Objekt-card zu modifizieren und etwa ein Icon hinzuzufügen, siehe object icons registrieren. |
| title | agorum.text | Definiert eine Überschrift, die für dieses Objekt erscheint. Stellt im Standardfall den Parameter displayName des Objekts dar. |
| time | agorum.text | Definiert einen Zeitstempel, der für dieses Objekt erscheint. Im Standardfall wird der Zeitpunkt der letzten Änderung verwendet. |
| detail | agorum.text | Definiert einen kurzen Text, der wesentliche Eigenschaften des Objekts zusammenfasst. Beispiel Für Dateien erscheint die Größe, für E-Mails erscheinen Absender und Empfänger. |
| actions | Gruppe | Ist für Schnellaktionen reserviert, die Benutzer auf dem Objekt aus können. Beispiel Für Ordner wird eine Suche angeboten, die auf diesen Ordner beschränkt ist. |
| chips | Gruppe | Hinterlegt cardlets des Typs agorum.chip, die Sie etwa zur Anzeige von Benutzer-Tags verwenden können. |
| content | Gruppe | Stellt den Inhalt des Objekts oder ein Auszug davon dar. Die Darstellung variiert je nach Objekttyp. |
| location | Gruppe | Zeigt im Standard die Liste der Pfade an, unter denen das Objekt erreichbar ist. |
| super | Gruppe | Zeigt übergeordnete Objekte an, sofern vorhanden. Beispiel Zeigt bei einem E-Mail-Anhang die zugehörige E-Mail an. |
| sub | Gruppe | Zeigt untergeordnete Objekte an, sofern vorhanden. Beispiel Zeigt bei einer E-Mail die zugehörigen Anhänge an. |

**Hinweis**: Je nach Detailgrad der Darstellung existieren eventuell einzelne dieser Elemente nicht. Das System wählt etwa für dargestellte E-Mail-Anhänge eine kompaktere Ansicht ohne die Gruppen *content*, *super* und *sub*. Verwenden Sie daher zunächst die Funktion *decorators.with()*, um das Element zu suchen, das das System zur Anzeige verwenden soll. Existiert dieses nicht, kann der decorator teilweise oder vollständig übersprungen werden.

### Interaktivität

* * *

Da decorators im Gegensatz zu card-Handlern (siehe [Eigene cardlets erstellen](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(157bef80-3ff3-11ed-9c7e-005056aa0ecc\)&detailsId=157bef80-3ff3-11ed-9c7e-005056aa0ecc)) keine Ereignisbehandlung durchführen können, können Sie nicht direkt auf Benutzerinteraktion reagieren. Möchten Sie dennoch interaktive Elemente in einem [agorum.object](#)\-cardlet darstellen, existieren die folgenden Möglichkeiten.

#### Eigenes cardlet einbetten

Ein decorator kann zur Darstellung von interaktiven Elementen ein cardlet einbetten, das diese Funktion übernimmt. Das System stellt etwa die mitgelieferte Pfadanzeige auf diesem Weg dar.

#### Standard-Links verwenden

Neben den für alle cardlets verfügbaren Link-Typen wie *object* und *action* (siehe [JavaScript-Bibliothek agorum.cards/js/cards](/roiwebui/aguila_module/?type=agorum.composite.acic&settingName=inbox-all&filterCollapsed=true&detailsCollapsed=false&additionalBaseQuery=uuid:\(8b54c9e0-40c8-11ed-9c7e-005056aa0ecc\)&detailsId=8b54c9e0-40c8-11ed-9c7e-005056aa0ecc)) können Sie innerhalb von [agorum.object](#)\-cardlets zusätzlich Links des Typs *toggle* verwenden, die folgendermaßen funktionieren:

1. Der Link (etwa *toggle:my.test.value*) wird als name-Attribut eines Hyperlinks in einem agorum.text-cardlet oder als name-Eigenschaft eines interaktiven cardlets gesetzt.
2. Wenn ein Benutzer auf ein solches Element klickt, wird in der Definition des umgebenden agorum.object-cardlets der boolesche Wert des so benannten Schlüssels (im Beispiel *my.test.value*) invertiert und das cardlet neu erzeugt.
3. Der decorator kann jetzt auf den Wert dieses Schlüssels in der Definition reagieren und seine Darstellung anpassen.

Die mitgelieferten Adress-cardlets verwenden toggle-Links, um den Bearbeitungsmodus an- und abzuschalten.

## agorum.cards – Beispiele

### Aktionen und Objekte in cards aufrufen

* * *

Sie können Links und Schaltflächen in einem decorator oder cardlet definieren, sodass sich bei einem Klick ein *agorum core*\-Objekt öffnet oder eine *agorum core smart assistant*\-Aktion ausgelöst wird.

#### Links und Schaltflächen in einem decorator definieren

**Voraussetzungen**

* Sie haben die Dokumentation [Eigene decorators erstellen](#) gelesen.
* Sie haben ein [Projekt angelegt](#).

1. Öffnen Sie das **Projekt** im *agorum core explorer*.
2. Navigieren Sie in den Ordner **js**.
3. Erstellen Sie über das Kontextmenü ein neues **JS-Dokument**, etwa mit dem Namen **agorum-tests-cards-decorator-sample.js**.
4. Fügen Sie folgenden Code in das neue JS-Dokument ein:

    ```auto
    let objects = require('common/objects');
    let decorators = require('/agorum/roi/customers/agorum.cards/js/decorators');
    let html = require('common/html');

    // Funktion zur Erzeugung eines Links mit korrekt codiertem HTML
    let link = (text, name) => '<a name="' + html.escape(name) + '">' + html.escape(text) + '</a>';

    // Zu jedem Objekt soll in den Inhaltsbereich (content) etwas hinzugefügt werden
    module.exports = (cardlet, object) =>
      decorators.with(cardlet, 'content', content => {
        let document = objects.find('/agorum/roi/Files/Demo/Willkommen.pdf');
        let folder = objects.find('/agorum/roi/Files/Demo');

        // Falls es content bereits durch einen anderen decorator gibt, soll dahinter unser decorator eingefügt werden
        // Es werden diverse Links eingefügt
        content.items = (content.items || []).concat([
          {
            type: 'agorum.vertical',
            items: [
              {
                type: 'agorum.text',
                html: 'Hier ist ein <a href="https://www.agorum.com/" target="_blank">Link zu agorum</a>',
              },
              {
                type: 'agorum.text',
                html:
                  'Start einer agorum core-Aktion aus dem smart assistant: ' +
                  link('Details anzeigen', 'action:Detailsanzeigen::' + document.UUID),
              },
              {
                type: 'agorum.text',
                html: 'Öffnen-Aktion eines Objekts aufrufen: ' + link('Ordner anzeigen', 'object:' + folder.UUID),
              },
              {
                type: 'agorum.img',
                size: 14,
                icon: 'agorum:circle;color=#5696e8|ionicon:document-text;color=white;scale=0.7',
                interactive: true,
                pointer: true,
                tooltip: 'Hier klicken, um Details zu öffnen',
                name: 'action:Detailsanzeigen::' + document.UUID,
              },
            ],
          },
        ]);
      });
    ```

5. [Registrieren](#) Sie das neue JS-Dokument (decorator) über den *agorum core template manager*.
6. Öffnen Sie in einem neuen Browserfenster die **Suche** und führen Sie eine Suche über den Filter **Alles** aus.**Ergebnis**: Jedes Objekt zeigt im Inhalt die definierten Links und das Symbol an.

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/51b73660-5ee4-11ee-89c1-005056aa0ecc)

    ```auto
    OCR: PDF, Willkommen.pdf, 1.1, 113.9, Hier ist ein Link agorum Start einer agorum core Aktion aus dem smart assistant, Details anzeigen, Aktion eines Objektes aufrufen, Ordner anzeigen, Dateien, Demo VersioningWorkflow, 26.09, 08:55
    ```

    Links und Symbol im Inhalt eines Objekts

7. Klicken Sie auf die Links oder das Symbol.**Ergebnis**: Die entsprechenden Aktionen erscheinen.Auf diese Art können Sie jede beliebige Aktion aus dem *agorum core smart assistant*\-Konfigurator aufrufen, etwa auch Workflows starten oder Ähnliches.

#### Links und Schaltflächen in einem cardlet definieren

**Voraussetzungen**

* Sie haben die Dokumentation [Eigene cardlets erstellen](#) gelesen.
* Sie haben ein [Projekt angelegt](#).

**cardlet anlegen**

1. Öffnen Sie das **Projekt** im *agorum core explorer*.
2. Navigieren Sie in den Ordner **js**.
3. Erstellen Sie über das Kontextmenü ein neues **JS-Dokument**, etwa mit dem Namen **agorum-tests-cards-cardlets-links.js**.
4. Fügen Sie folgenden Code in das neue JS-Dokument ein:

    ```auto
    let cards = require('/agorum/roi/customers/agorum.cards/js/cards');
    let objects = require('common/objects');
    let html = require('common/html');

    // Name: agorum.tests.cards.agorumTestsCardsCardletsLinks

    // Funktion zur Erzeugung eines Links mit korrekt codiertem HTML
    let link = (text, name) => '<a name="' + html.escape(name) + '">' + html.escape(text) + '</a>';

    // cardlet definieren
    let build = (cx, def) => {
      cx.meta = {};

      let document = objects.find('/agorum/roi/Files/Demo/Willkommen.pdf');
      let folder = objects.find('/agorum/roi/Files/Demo');

      return {
        type: 'agorum.card',
        items: [
          {
            type: 'agorum.text',
            html: 'Hier ist ein <a href="https://www.agorum.com/" target="_blank">Link zu agorum</a>',
          },
          {
            type: 'agorum.text',
            html:
              'Start einer agorum core-Aktion aus dem smart assistant: ' +
              link('Details anzeigen', 'action:Detailsanzeigen::' + document.UUID),
          },
          {
            type: 'agorum.text',
            html: 'Öffnen-Aktion eines Objekts aufrufen: ' + link('Ordner anzeigen', 'object:' + folder.UUID),
          },
          {
            type: 'agorum.img',
            size: 14,
            icon: 'agorum:circle;color=#5696e8|ionicon:document-text;color=white;scale=0.7',
            interactive: true,
            pointer: true,
            tooltip: 'Hier klicken, um Details zu öffnen',
            name: 'action:Detailsanzeigen::' + document.UUID,
          },
        ],
      };
    };

    let event = cards.eventHandler();

    module.exports = {
      build: build,
      event: event,
    };
    ```

5. [Registrieren](#) Sie das neue JS-Dokument (cardlet) über den *agorum core template manager*.**Ergebnis**: Sie erhalten den Namen des cardlets.
6. Notieren Sie sich den Namen des cardlets, hier im Beispiel **agorum.tests.cards.agorumTestsCardsCardletsLinks**.Sie benötigen diesen Namen beim nachfolgenden Anlegen einer card-view.

**card-view anlegen**

Nachfolgend legen Sie eine card-view an, um das cardlet anzuzeigen.

1. Erstellen Sie im Ordner **js** des Projekts über das Kontextmenü den Ordner **aguila**.
2. Erstellen Sie im Ordner **aguila** ein neues JS-Dokument mit dem Namen **test-card.js**.
3. Fügen Sie folgenden Code in das neue JS-Dokument ein:

    ```auto
    let aguila = require('common/aguila');

    let widget = aguila.create({
      type: 'agorum.vbox',
      background: 'dark',
      width: 600,
      items: [
        {
          name: 'cardView',
          type: 'agorum.cards.view',
        },
      ],
    });

    let sample = {
      // replace with the name of your cardlet
      type: 'agorum.tests.cards.agorumTestsCardsCardletsLinks',
    };

    widget.down('cardView').replace(sample);

    widget;
    ```

    **Hinweis**: Fügen Sie bei *type* den notierten Namen des erstellten cardlets ein (siehe Schritt 6 unter [cardlet anlegen](#CardletAnlegenCardlet)).

4. Klicken Sie oben auf **Run**.**Ergebnis**: Ein Dialog öffnet sich, in dem die definierten Links und das Symbol erscheinen.

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/fb749f70-5ee5-11ee-89c1-005056aa0ecc)

    ```auto
    OCR: aguila, test, card.js, Test, Hier ist ein Link, agorum, Start einer agorum core Aktion aus dem smart assistant, Details anzeigen, Aktion eines Objektes aufrufen, Ordner anzeigen
    ```

    Links und Symbol im cardlet

5. Klicken Sie auf die Links oder das Symbol.**Ergebnis**: Die entsprechenden Aktionen erscheinen.Auf diese Art können Sie jede beliebige Aktion aus dem *agorum core smart assistant*\-Konfigurator aufrufen, etwa auch Workflows starten oder Ähnliches.

### Mithilfe der Schaltfläche „mehr“ weiteren Inhalt anzeigen

* * *

Sie können cardlets interaktiv steuern. Das folgende Beispiel zeigt, wie Sie in einem cardlet mit der „Mehr“-Schaltfläche weiteren Inhalt anzeigen.

**Voraussetzungen**

* Sie haben die Dokumentation [Eigene cardlets erstellen](#) gelesen.
* Sie haben ein [Projekt angelegt](#).

**cardlet anlegen**

1. Öffnen Sie das **Projekt** im *agorum core explorer*.
2. Navigieren Sie in den Ordner **js** und erstellen Sie über das Kontextmenü den neuen Ordner **cardlets**.
3. Erstellen Sie über das Kontextmenü ein neues **JS-Dokument**, etwa mit dem Namen **agorum-tests-cards-cardlets-more.js**.
4. Fügen Sie folgenden Code in das neue JS-Dokument ein:

    ```auto
    let cards = require('/agorum/roi/customers/agorum.cards/js/cards');
    let html = require('common/html');

    // Name: agorum.tests.cards.agorumTestsCardsCardletsMore

    // Funktion zur Erzeugung eines Links mit korrekt codiertem HTML
    let link = (text, name) => '<a name="' + html.escape(name) + '">' + html.escape(text) + '</a>';

    // cardlet definieren
    let draw = cx => {
      return {
        type: 'agorum.card',
        items: [
          {
            type: 'agorum.horizontal',
            items: [
              {
                type: 'agorum.text',
                html: 'Hier klicken, um mehr anzuzeigen: ' + link('Mehr', 'moreLink'),
                flex: 1,
              },
              {
                type: 'agorum.img',
                size: 14,
                icon: cx.meta.showMore ? 'mdi:expand-less' : 'mdi:expand-more',
                interactive: true,
                pointer: true,
                tooltip: 'Hier klicken, um mehr anzuzeigen',
                name: 'more',
              },
            ],
          },
          // show this only, if showMore=true
          cx.meta.showMore
            ? {
                type: 'agorum.text',
                html: 'Hier steht nun noch mehr!',
              }
            : null,
        ].filter(f => f), // empty element has to be filtered out
      };
    };

    // build the cardlet
    let build = (cx, def) => {
      // set initial meta information
      cx.meta = cx.meta || {};
      cx.meta.showMore = cx.meta.showMore || false;

      return draw(cx);
    };

    let event = cards.eventHandler();

    // click on more button
    event.path('more').on('elementClicked', (cx, param) => {
      cx.meta.showMore = !cx.meta.showMore;
      cx.replace(draw(cx));
    });

    // click on a link
    event.path().on('linkClicked', (cx, param) => {
      if (param === 'moreLink') {
        cx.meta.showMore = !cx.meta.showMore;
        cx.replace(draw(cx));
      }
    });

    module.exports = {
      build: build,
      event: event,
    };
    ```

5. [Registrieren](#) Sie das neue JS-Dokument (cardlet) über den *agorum core template manager*.**Ergebnis**: Sie erhalten den Namen des cardlets.
6. Notieren Sie sich den Namen des cardlets, hier im Beispiel **agorum.tests.cards.agorumTestsCardsCardletsMore**.Sie benötigen diesen Namen beim nachfolgenden Anlegen einer card-view.

**card-view anlegen**

Nachfolgend legen Sie eine card-view an, um das cardlet anzuzeigen.

1. Erstellen Sie im Ordner **js** des Projekts über das Kontextmenü den Ordner **aguila**.
2. Erstellen Sie im Ordner **aguila** ein neues JS-Dokument mit dem Namen **test-card.js**.
3. Fügen Sie folgenden Code in das neue JS-Dokument ein:

    ```auto
    let aguila = require('common/aguila');

    let widget = aguila.create({
      type: 'agorum.vbox',
      background: 'dark',
      width: 600,
      items: [
        {
          name: 'cardView',
          type: 'agorum.cards.view',
        },
      ],
    });

    let sample = {
      // replace with the name of your cardlet
      type: 'agorum.tests.cards.agorumTestsCardsCardletsLinks',
    };

    widget.down('cardView').replace(sample);

    widget;
    ```

    **Hinweis**: Fügen Sie bei *type* den notierten Namen des erstellten cardlets ein (siehe Schritt 6 unter [cardlet anlegen](#CardletAnlegenMehr)).

4. Klicken Sie oben auf **Run**.**Ergebnis**: Das cardlet öffnet sich im eingeklappten Zustand.

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/51e85bb0-5ee8-11ee-89c1-005056aa0ecc)

    ```auto
    OCR: aguila, test, card.js, Test, Hier klicken, mehr anzuzeigen, Mehr
    ```

    cardlet im eingeklappten Zustand

5. Klicken Sie auf **Mehr** oder oben rechts auf ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAABAUlEQVQoU82SIa6DQBRF70AIOBJWgEBTiwHDCkgQaCyiFSwD0Qo0GkHYAQIMtkgcG0BgCCHQ/2dSmrT8Js1XvckzM+/MvDt3yO1X+KfId8DUwbquIIQ8ijqi61txHMf2qJ7GbtsWWZZBlmX4vg9JkljTOI5IkgTDMMB1XWiatof7vsflfMG1ucKyLARBwJriOEZZljjoBxxPRyiKsoeXZUFVVcjzHF3XwbZtZqMoCqiqCsdxYJomeJ7fw3RlnmfUdY00TdE0DfOq6zo8z4NhGBAE4RHsn1HRCSgYRRFrDMOQHbDduNFvc6bjTtPE+kRRBH3lV72Ft2hYJPfoPoY/+bE/WCeS3Twm3icAAAAASUVORK5CYII=).**Ergebnis**: Das cardlet klappt sich aus.

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/51e28f50-5ee8-11ee-89c1-005056aa0ecc)

    ```auto
    OCR: aguila, test, card.js, Test, Hier klicken, mehr anzuzeigen, Mehr, Hier steht nun noch mehr
    ```

    cardlet im ausgeklappten Zustand

