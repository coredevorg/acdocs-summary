# Übersicht - agorum core JavaScript api summary

## Erste Zeile eines JavaScripts

Um Skripte in *agorum core* korrekt auszuführen, benötigt das System bestimmte globale Parameter. Diese tragen Sie in die erste Zeile des Skripts ein:

```auto
/* global sc, sca, object, data */
```

### Globale Parameter

* * *

Zwei stets verwendete Parameter lauten:

| Parameter | Erklärung |
| --- | --- |
| sc | Definiert die Session, mit der der Benutzer mit agorum core verbunden ist. |
| sca | Definiert die Session zur Nutzung als Administrator. |

### agorum core smart assistant konfigurator

* * *

**Hinweis**: Fokussieren Sie sich auf *objects* und benutzen Sie *folder* nicht mehr. Um auf einen *folder* zugreifen zu können, müssen Sie die Aktion auf der Baumstruktur im *agorum core smart assistant* ausführen. Andernfalls findet das System den *folder* nicht.

#### Element „Anlage“

**JavaScript (Initialisierung)**

```auto
/* global sc, sca, folder, objects */
```

**JavaScript (zuvor) und JavaScript (danach)**

```auto
/* global sc, sca, folder, data */
```

| Parameter | Erklärung |
| --- | --- |
| folder | Definiert das Ordner-Objekt des Ordners, auf dem ein Benutzer im agorum core explorer gerade positioniert ist. Hat ein Benutzer im Feld Zielordner ein Ordner eingegeben, ist folder dieser Zielordner. |
| objects | Definiert ein Objects-Array der Objekte, die im agorum core smart assistant zum Zeitpunkt der Ausführung markiert sind. |
| data | Definiert ein Objekt, das die Eingabewerte enthält. |

#### Element „Ablage“

**JavaScript (Initialisierung)**

```auto
/* global sc, sca, folder, objects */
```

**JavaScript (zuvor) und JavaScript (danach)**

```auto
/* global sc, sca, folder, objects, data */
```

#### Element „Suche“

**JavaScript**

```auto
/* global sc, sca, data */
```

#### Element „Server Aktion“

**JavaScript (Initialisierung)**

```auto
/* global sc, sca, folder, objects */
```

**JavaScript**

```auto
/* global sc, sca, folder, objects, data */
```

#### Element „Client Aktion“

**JavaScript (Initialisierung)**

```auto
/* global sc, sca, folder, objects */
```

**JavaScript**

```auto
/* global folderId, ids */
```

| Parameter | Erklärung |
| --- | --- |
| folderId | Definiert die ID des Ordners, der bei Aufruf der Aktion aktuell ist (als String). |
| ids | Enthält alle IDs als String-Array, die markiert waren, als die Aktion ausgeführt wurde. |

### CronJobs

* * *

Falls Sie ein JavaScript über einen CronJob starten möchten, muss innerhalb der ersten Zeile des Skripts Folgendes vorhanden sein:

```auto
/* global object */
```

### Workflows

* * *

Die folgende erste Zeile muss bei einem Skript vorhanden sein, das von einem Workflow verwendet wird:

```auto
/* global sc, sca, instance, token, outlets, parameters: true */
```

| Parameter | Erklärung |
| --- | --- |
| instance | Gilt global für alle Knoten, Verwendung etwa in instance.variables. Das System legt alle Variablen ab, die global zur Verfügung stehen. |
| token | Definiert den aktuellen Knoten, Verwendung etwa in token.variables. Enthält Variablen, die nur für den Token gelten. |
| outlets | Enthält die Keys der Transitions, Verwendung etwa beim Knoten fork. |
| parameters | Enthält die Werte, die Sie mit parameters übergeben. |

### API

* * *

Die folgende erste Zeile muss bei einem Skript vorhanden sein, das von der JS-/Rest-API verwendet wird:

```auto
/* global sc, sca, Packages, request */
```

| Parameter | Erklärung |
| --- | --- |
| request | Enthält Werte, die von außen / extern an das Skript mitgegeben werden. Beispiel Ein externes System ruft ein Skript in agorum core per API auf. Dieses externe System gibt Parameter mit, die das System unter request sammelt. |

### Aktive Ordner

* * *

Die folgende erste Zeile muss bei einem Skript vorhanden sein, das von einem *Aktiven Ordner* verwendet wird:

```auto
/* global folder, parameters */
```

| Parameter | Erklärung |
| --- | --- |
| folder | Definiert den Aktiven Ordner, den das Skript verwendet. |
| parameters | Enthält Parameter, die Sie übergeben. |

### Fileworkflow

* * *

Die folgende erste Zeile muss bei einem JavaScript vorhanden sein, das vom Fileworkflow verwendet wird:

```auto
/* global sc, folder, object, parameters */
```

| Parameter | Erklärung |
| --- | --- |
| sc | Admin SessionController, fileworkflow läuft immer als Administrator. |
| folder | Optional, es kann beim Fileworkflow Aufruf ein Startordner definiert werden. |
| object | Objekt, mit dem der Fileworkflow durchläuft. |
| parameters | Parameter, die im Fileworkflow in der Bedienoberfläche bei Parametern definiert werden. |

### ContentTask

* * *

Die folgende erste Zeile muss bei einem JavaScript vorhanden sein, das vom *Aktiven Ordner* verwendet wird:

```auto
/* global Packages, sc, object */
```

| Parameter | Erklärung |
| --- | --- |
| object | Enthält das Dokument, dessen Inhalt sich geändert hat, und wird dem Skript übergeben. |

### Best Practice-Tipps

* * *

#### new error

```auto
throw new error ('...')
```

Wenn Skripte in *agorum core* Fehler werfen, verwenden Sie *new Error*, um für die Fehlersuche den Stacktrace zur Verfügung zu haben.

## SessionController(sc)

Mithilfe dieser Java-Klasse fragen Sie diverse Kontexte zur Session des aktuell angemeldeten Benutzers ab.

Der SessionController ist eine Variable (sc), die in jedem Skript zur Verfügung steht.

### Syntax

* * *

Die Session des angemeldeten Benutzers ist als globale Variable verfügbar und trägt den Namen *sc*.

1. Definieren Sie diese Variable über die Angabe *global*, um sie zu verwenden:

    ```auto
    /* global sc */

    let value = sc.field;
    ```

Zusätzlich können Sie eine administrative Sitzung verwenden, indem Sie *sca* statt *sc* setzen.

* *sca* können Sie für Aktionen verwenden, für die der angemeldete Benutzer nicht berechtigt ist.
* Wenn Sie *sca* setzen, verwendet das System den Super-Administrator *roi*.

### Methoden

* * *

#### loginUser

Fragt den aktuell angemeldeten Benutzer der Session ab.

**Syntax*****Name des Benutzers***

```auto
let loginUser = sc.loginUser.name;
```

***ID des Benutzers***

```auto
let loginUser = sc.loginUser.ID;
```

**Parameter**

Zu dieser Methode existieren keine Parameter.

**Beispiele*****Name des Benutzers***

```auto
/* global sc */
let loginUser = sc.loginUser.name;
loginUser;
```

***ID des Benutzers***

```auto
/* global sc */
let loginUser = sc.loginUser.ID;
loginUser;
```

**Rückgabewerte**

Sie erhalten entweder den Namen oder die ID des aktuell angemeldeten Benutzers der Session zurück.***Name des Benutzers***

```auto
roi
```

***ID des Benutzers***

```auto
11000
```

**Verwendung**

Diese Methode verwenden Sie, wenn Sie den Namen oder die ID des aktuell angemeldeten Benutzers der Session erhalten möchten.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### loginUserUuid

Frag die UUID des aktuell angemeldeten Benutzers der Session ab.

**Syntax**

```auto
let loginUserUuid = sc.loginUserUuid;
```

**Parameter**

Zu dieser Methode existieren keine Parameter.

**Beispiel**

```auto
/* global sc */
let loginUserUuid = sc.loginUserUuid;
loginUserUuid;
```

**Rückgabewerte**

Sie erhalten die UUID des aktuell angemeldeten Benutzers der Session zurück.

```auto
714614d0-ce62-11e0-b47a-0800276e2399
```

**Verwendung**

Diese Methode verwenden Sie, wenn Sie die UUID des aktuell angemeldeten Benutzers der Session erhalten möchten.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### locale

Fragt die Spracheinstellung der Session ab.

**Syntax**

```auto
let locale = sc.locale;
```

**Parameter**

Zu dieser Methode existieren keine Parameter.

**Beispiel**

```auto
/* global sc */
let locale = sc.locale;
locale;
```

**Rückgabewerte**

Sie erhalten die Spracheinstellung der Session zurück. Es handelt sich dabei um ein [java.util.Locale](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html)\-Objekt.

```auto
"de"
```

**Verwendung**

Diese Methode verwenden Sie, wenn Sie die Spracheinstellung der Session erhalten möchten.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### adminEnabled

Fragt ab, ob sich die Session im Adminmodus oder im normalen Benutzermodus befindet.

**Syntax**

```auto
let adminEnabled = sc.adminEnabled;
```

**Parameter**

Zu dieser Methode existieren keine Parameter.

**Beispiel**

```auto
/* global sc */
let adminEnabled = sc.adminEnabled;
adminEnabled;
```

**Rückgabewerte**

Sie erhalten einen booleschen Wert zurück.

| Wert | Beschreibung |
| --- | --- |
| true | Die Session befindet sich im Adminmodus. |
| false | Session befindet sich im normalen Benutzermodus. |

**Verwendung**

Diese Methode verwenden Sie, um herauszufinden, ob sich die Session im Adminmodus oder im normalen Benutzermodus befindet.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### asAdmin()

Nimmt die aktuelle Sitzung und erzeugt einen temporären SessionController, bei dem der Adminmodus aktiviert ist.

**Syntax**

```auto
let asAdmin = sc.asAdmin();
```

**Parameter**

Zu dieser Methode existieren keine Parameter.

**Beispiel**

```auto
/* global sc */
let asAdmin = sc.asAdmin();

// objects-Bibliothek mit dieser neuen Session laden
let objectsAdmin = require('common/objects')(asAdmin);

// Mit der objects-Bibliothek als Admin weiterarbeiten, um etwa den Ordner "Testordner" unter "Eigene Dateien" des Benutzers zu erstellen
objectsAdmin = objectsAdmin.find('home:myFiles/Testordner:create');
```

**Rückgabewerte**

Diese Methode liefert keine Werte zurück.

**Verwendung**

Diese Methode verwenden Sie, wenn Sie etwas mit dem aktuell angemeldeten Benutzer durchführen wollen, dessen Rechte aber nicht ausreichen.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### asService()

Nimmt die aktuelle Sitzung und erzeugt einen temporären SessionController, bei dem der Servicemodus aktiviert ist.

Beim Servicemodus:

* verändert das System das *lastModifyDate* und den *lastModifier* nicht, wenn ein Objekt aktualisiert wird
* legt das System keine Historie an, wenn ein Objekt geändert wird
* erzeugt das System keine EventAssistance-Mitteilungen

**Syntax**

```auto
let asService = sc.asService();
```

**Parameter**

Zu dieser Methode existieren keine Parameter.

**Beispiel**

```auto
/* global sc */
let asService = sc.asService();

// objects-Bibliothek mit dieser neuen Session laden
let objectsService = require('common/objects')(asService);

// Mit der objects-Bibliothek im Servicemodus weiterarbeiten, um etwa einen Benutzer zu aktualisieren, ohne das lastModifyDate zu ändern.
objectsService = objectsService.update('user', objects.find('user:USERNAME'), {
  name: 'testuser',
  password: 'testpass',
  admin: false,
  givenName: 'Test',
  familyName: 'User',
  language: 'de',
  emailAddresses: [ 'testuser@agorum.com' ]
});
```

**Rückgabewerte**

Sie erhalten den erzeugten SessionController zurück.

```auto
4615452
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie mit Objekten arbeiten und wünschen, dass das System:

* beim Update eines Objekts das *lastModifyDate* und den *lastModifier* nicht verändert
* beim Ändern eines Dokuments keine Historie anlegt
* Im desk4web-Mitteilungssystem keine EventAssistance-Mitteilungen erzeugt

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### asUser(user)

Nimmt die aktuelle Sitzung und erzeugt einen temporären SessionController, bei dem das System den aktuellen Benutzer auf den angegebenen Benutzer ändert.

**Syntax**

```auto
let asUser = sc.asUser(user);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard-Wert | Weitere Informationen |
| --- | --- | --- | --- | --- |
| user | Definiert den Benutzer, mit dem Sie in der aktuellen Sitzung weiterarbeiten möchten. Wenn Sie den Benutzer anhand des Namens suchen wollen, verwenden Sie objects.find. | ja | – | Beispiel |

**Beispiel**

```auto
/* global sc */
let objects = require('common/objects');
let asUser = sc.asUser(objects.find('user:demo'));

// objects-Bibliothek mit dieser neuen Session laden
let objectsUser = require('common/objects')(asUser);

// Mit der objects-Bibliothek als Benutzer "demo" weiterarbeiten, um etwa den Ordner "Testordner" unter "Eigene Dateien" des Benutzers zu erstellen
objectsUser = objectsUser.find('home:myFiles/Testordner:create');
```

Für Beispiele zum Suchen von Objekten siehe JavaScript-Bibliothek [common/objects](#).

**Rückgabewerte**

Sie erhalten den erzeugten SessionController zurück.

```auto
4615452
```

**Verwendung**

Diese Methode verwenden Sie, wenn Sie etwa im Namen eines anderen Benutzers mit *agorum core* arbeiten möchten.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

#### getDirectoryUserFromEmailAddress

Fragt das Benutzerobjekt zu einer E-Mail-Adresse ab.

**Syntax**

```auto
let user = sc.getDirectoryUserFromEmailAddress('string');
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard-Wert | Weitere Informationen |
| --- | --- | --- | --- | --- |
| string | Definiert die E-Mail-Adresse. | ja | – | Beispiel |

**Beispiel**

```auto
/* global sc */
let user = sc.getDirectoryUserFromEmailAddress('demo@agorumcore.com');
user;
```

**Rückgabewerte**

Sie erhalten das Benutzerobjekt zurück, zu dem die angegebene E-Mail-Adresse zugeordnet ist.

```auto
1025764
```

**Verwendung**

Diese Methode verwenden Sie, wenn Sie zu einer E-Mail-Adresse den zugeordneten Benutzer erfahren möchten.

**Exceptions**

Zu dieser Methode existieren keine Exceptions.

### SessionController(sc) in Bibliotheken verwenden

* * *

Bibliotheken, die mit Objekten arbeiten (wie die JavaScript-Bibliothek [common/objects](#)), verwenden im Standard die global verfügbare Sitzung *sc* für ihre Operationen. Eine davon abweichende Sitzung verwenden Sie etwa folgendermaßen:

```auto
/* global sca */

let objects = require('common/objects')(sca);

let object = objects.find('/not/visible/to/current/user');
```

Dieses Beispiel verwendet abweichend die administrative Sitzung *sca*, um das Objekt */not/visible/to/current/user* zu finden, das der aktuell angemeldete Benutzer nicht sehen kann.

*sca* können Sie in diesen Bibliotheken verwenden:

* [common/data](#)
* [common/objects](#)
* [common/workflow](#)
* [common/workflows](#)
* [address/objects](#)
* [preview/objects](#)
* [adapter/objects](#)
* [mailfilter/objects](#)
* [filingassistant/service](#)
* common/permissions

## JavaScript-Bibliothek ac

Diese JavaScript-Bibliothek bietet generelle Hilfs-Funktionen.

### Verwendung

* * *

Sie benötigen die folgende Bibliothek, um diese JavaScript-Bibliothek verwenden zu können. Die Bibliothek geben Sie am Anfang des Skripts an.

```auto
let ac = require('ac');
```

### Funktionen

* * *

#### eq (equals)

Prüft, ob 2 Werte gleich sind mit angegebener Präzision.

**Syntax**

```auto
ac.eq(value1, value2, precision);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value1 | Definiert Wert 1 für den Vergleich. | Ja | – | Beispiel |
| value2 | Definiert Wert 2 für den Vergleich. | Ja | – |
| precision | Definiert die Nachkommastellen. | Nein | 2 |

**Beispiel**

```auto
let ac = require('ac');

ac.eq(123.44546, 123.45, 2);

// liefert "true" zurück
```

**Rückgabewerte**

Sie erhalten einen booleschen Wert zurück.

| Wert | Beschreibung |
| --- | --- |
| true | Wert 1 und Wert 2 sind identisch. |
| false | Wert 1 und Wert 2 sind nicht identisch. |

**Verwendung**

Diese Funktion verwenden Sie, um 2 Werte miteinander zu vergleichen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### format

Ruft die angegebene Formatierung auf.

* Intern verzweigt die Funktion, je nach Typ bei *value*.
* Das übergebene Format muss dem Typ von *value* entsprechen.

**Syntax**

```auto
ac.format(value, format);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value | Definiert den Wert, den das System formatiert. | Ja | – | Beispiel |
| format | Gibt die Formatierung an. | Ja | – |

**Beispiele**

***Datum formatieren***

```auto
let ac = require('ac');

ac.format(new Date(), 'dd.MM.yyyy');

// Liefert das aktuelle Datum zurück, etwa 19.05.2022.
```

In diesem Beispiel ruft das System intern die Funktion [formatDate](#formatDate) auf, da *value* ein Date ist.

***Zahlen formatieren***

```auto
let ac = require('ac');

ac.format(123.4, 'en|0.5');

// Liefert "123.5" zurück
```

In diesem Beispiel ruft das System intern die Funktion [formatNumber](#formatNumber) auf, da *value* eine Number ist.

**Rückgabewerte**

Das System gibt den angegebenen Wert formatiert zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie Werte formatieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### formatDate

Wandelt ein Datum in einen String mit angegebenem Format um.

* Die [Standard-Java-SimpleDateFormat-Angaben](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html) gelten.
* Für weitere Funktionen zur Datumsverarbeitung siehe [JavaScript-Bibliothek common/time](#)

**Syntax**

```auto
ac.formatDate(value, dateFormat);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value | Definiert den Wert, den das System umwandelt. | Ja | – | Beispiel |
| dateFormat | Definiert das Datumsformat für das Umwandeln. | Ja | – |

**Beispiel**

```auto
let ac = require('ac');

ac.formatDate(new Date(), 'dd.MM.yyyy');
```

**Rückgabewerte**

Sie erhalten das Datum als String zurück.

```auto
19.05.2022
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum als String benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### formatNumber

Wandelt eine Zahl in einen String um.

Die [Standard-Java-DecimalFormat-Angaben](https://docs.oracle.com/javase/8/docs/api/java/text/DecimalFormat.html) gelten.

**Syntax**

```auto
ac.formatNumber(number, 'language|DecimalFormat');
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| number | Definiert die Zahl, die das System in einen String umwandelt. | Ja | – | Beispiel |
| language|DecimalFormat | Definiert die Sprache des Formats inklusive Dezimal-Separator. | Nein | de |

**Beispiel**

```auto
let ac = require('ac');

ac.formatNumber(123.4, 'en|0.5');
```

**Rückgabewerte**

Sie erhalten die Zahl als String zurück.

```auto
123.5
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine Zahl als String benötigen.

**Exceptions**

Für diese Funktion existieren keine Exceptions.

#### formatString

Formatiert einen String.

**Syntax**

```auto
ac.formatString(String , x, y);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| String | Definiert den String an, den das System formatiert. | Ja | – | Beispiele |
| x | Definiert die Startposition des Strings. x beginnt ab 1. Wenn x negativ ist, beginnt das System von hinten, wobei -1 das letzte Zeichen ist. | Ja | – |
| y | Definiert die Endposition des Strings. y beginnt ab 1. Wenn y negativ ist, beginnt das System von hinten, wobei -1 das letzte Zeichen ist. | Ja | – |

**Beispiele**

***Beispiel 1***

```auto
let ac = require('ac');

ac.formatString('0123456789', '1');
```

Ergebnis:

```auto
'0'
```

***Beispiel 2***

```auto
let ac = require('ac');

ac.formatString('0123456789', '1,2');
```

Ergebnis:

```auto
'01'
```

***Beispiel 3***

```auto
let ac = require('ac');

ac.formatString('0123456789', '-1');
```

Ergebnis:

```auto
'9'
```

***Beispiel 4***

```auto
let ac = require('ac');

ac.formatString('0123456789', '-1,2');
```

Ergebnis:

```auto
'123456789'
```

***Beispiel 5***

```auto
let ac = require('ac');

ac.formatString('0123456789', '-1,-2');
```

Ergebnis:

```auto
'89'
```

**Rückgabewerte**

Sie erhalten den String im angegebenen Format zurück.

```auto
'0'
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String formatiert benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### ge (greater equal)

Prüft, ob Wert 1 größer oder gleich ist als Wert 2 mit angegebener Präzision.

**Syntax**

```auto
ac.ge(value1, value2, precision);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value1 | Definiert Wert 1 für den Vergleich. | Ja | – | Beispiel |
| value2 | Definiert Wert 2 für den Vergleich. | Ja | – |
| precision | Definiert die Nachkommastellen. | Nein | 2 |

**Beispiel**

```auto
let ac = require('ac');

ac.ge(123.44546, 123.45, 2);

// liefert "true" zurück
```

**Rückgabewerte**

Sie erhalten einen booleschen Wert zurück.

| Wert | Beschreibung |
| --- | --- |
| true | Wert 1 ist größer oder gleich Wert 2. |
| false | Wert 1 ist nicht größer oder gleich Wert 2. |

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie prüfen möchten, ob Wert 1 größer oder gleich ist als Wert 2.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### gt (greater than)

Prüft, ob Wert 1 größer ist als Wert 2 mit angegebener Präzision.

**Syntax**

```auto
ac.gt(value1, value2, precision);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value1 | Definiert Wert 1 für den Vergleich. | Ja | – | Beispiel |
| value2 | Definiert Wert 2 für den Vergleich. | Ja | – |
| precision | Definiert die Nachkommastellen. | Nein | 2 |

**Beispiel**

```auto
let ac = require('ac');

ac.gt(123.44546, 122.0, 2);

// liefert "true" zurück
```

**Rückgabewerte**

Sie erhalten einen booleschen Wert zurück.

| Wert | Beschreibung |
| --- | --- |
| true | Wert 1 ist größer als Wert 2. |
| false | Wert 1 ist nicht größer als Wert 2. |

**Verwendung**

Diese Funktion verwenden Sie, um zu prüfen, ob Wert 1 größer als Wert 2 ist.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### le (less equal)

Prüft, ob Wert 1 kleiner gleich ist als Wert 2 mit angegebener Präzision.

**Syntax**

```auto
ac.le(value1, value2, precision);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value1 | Definiert Wert 1 für den Vergleich. | Ja | – | Beispiel |
| value2 | Definiert Wert 2 für den Vergleich. | Ja | – |
| precision | Definiert die Nachkommastellen. | Nein | 2 |

**Beispiel**

```auto
let ac= require('ac');

ac.le(123.44546, 123.45, 2);

// liefert "true" zurück
```

**Rückgabewerte**

Sie erhalten einen booleschen Wert zurück.

| Wert | Beschreibung |
| --- | --- |
| true | Wert 1 ist kleiner oder gleich Wert 2. |
| false | Wert 1 ist nicht kleiner oder gleich Wert 2. |

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie prüfen möchten, ob Wert 1 kleiner oder gleich ist als Wert 2.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### lt (less than)

Prüft, ob Wert 1 kleiner ist als Wert 2 mit angegebener Präzision.

**Syntax**

```auto
ac.lt(value1, value2, precision);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value1 | Definiert Wert 1 für den Vergleich. | Ja | – | Beispiel |
| value2 | Definiert Wert 2 für den Vergleich. | Ja | – |
| precision | Definiert die Nachkommastellen. | Nein | 2 |

**Beispiel**

```auto
let ac = require('ac');

ac.lt(123.44546, 122.0, 2);

// liefert "false" zurück
```

**Rückgabewerte**

Sie erhalten einen booleschen Wert zurück.

| Wert | Beschreibung |
| --- | --- |
| true | Wert 1 ist kleiner als Wert 2. |
| false | Wert 1 ist nicht kleiner als Wert 2. |

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie prüfen möchten, ob Wert 1 kleiner ist als Wert 2.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseBoolean

Wandelt einen String in einen Boolean.

**Syntax**

```auto
ac.parseBoolean(String);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| String | Definiert den String, den das System umwandelt. | Ja | – | Beispiel |

**Beispiel**

```auto
let ac = require('ac');

ac.parseBoolean('true');
```

**Rückgabewerte**

Sie erhalten den String als Boolean zurück.

```auto
true
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String als Boolean benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseDate

Wandelt einen String mit angegebenem Format in ein Datum um.

* Die [Standard-Java-SimpleDateFormat-Angaben](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html) gelten.
* Die Standard-Zeitzone ist GMT.
* Für weitere Funktionen zur Datumsverarbeitung siehe [JavaScript-Bibliothek common/time](#)

**Syntax**

```auto
ac.parseDate(date, dateFormat, language);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| date | Definiert das Datum. | Ja | – | Beispiel |
| dateFormat | Definiert das Datumsformat für das Umwandeln. | Ja | – |
| language | Definiert, ob das System Monate etwa in Englisch oder Deutsch schreibt. Oct Okt October Oktober | Ja | – |

**Beispiel**

```auto
let ac = require('ac');

ac.parseDate('01.01.2018', 'dd.MM.yyyy','en');
```

**Rückgabewerte**

Sie erhalten den String als Datum formatiert zurück.

```auto
"2018-01-01T00:00:00.000Z"
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String als Datum benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseDouble

Wandelt einen String in eine double-Zahl.

**Syntax**

```auto
ac.parseDouble(String, language);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| String | Definiert den String, den das System umwandelt. | Ja | – | Beispiel |
| language | Definiert die Formatierung der Nachkommastellen. Für Komma 'de' Für Punkt 'en' | Ja | – |

**Beispiel**

```auto
let ac = require('ac');

ac.parseDouble('123.1','en');
```

**Rückgabewerte**

Sie erhalten den String als double-Zahl zurück.

```auto
123.1
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String als double-Zahl benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseFloat

Wandelt einen String in eine float-Zahl.

**Syntax**

```auto
ac.parseFloat(String, language);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| String | Definiert den String, den das System umwandelt. | Ja | – | Beispiel |
| language | Definiert die Formatierung der Nachkommastellen. Für Komma 'de' Für Punkt 'en' | Ja | – |

**Beispiel**

```auto
let ac = require('ac');

ac.parseDouble('123.1','en');
```

**Rückgabewerte**

Sie erhalten den String als float-Zahl zurück.

```auto
123.1
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String als float-Zahl benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseInt

Wandelt einen String in eine integer-Zahl.

**Syntax**

```auto
ac.parseInt(String);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| String | Definiert den String an, den das System umwandelt. | Ja | – | Beispiel |

**Beispiel**

```auto
let ac = require('ac');

ac.parseInt('123');
```

**Rückgabewerte**

Sie erhalten den String als integer-Zahl zurück.

```auto
123
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String als integer-Zahl benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseLong

Wandelt einen String in eine long-Zahl.

**Syntax**

```auto
ac.parseLong(String);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| String | Definiert den String, den das System umwandelt. | Ja | – | Beispiel |

**Beispiel**

```auto
let ac = require('ac');

ac.parseLong('123');
```

**Rückgabewerte**

Sie erhalten den String als long-Zahl zurück.

```auto
123
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String als long-Zahl benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### round

Rundet einen Wert anhand der übergebenen Präzision.

**Syntax**

```auto
ac.round(value, precision);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| value | Definiert den Wert, den das System rundet. | Ja | – | Beispiel |
| precision | Definiert die Nachkommastellen für das Runden. | Nein | 2 |

**Beispiel**

```auto
let ac = require('ac');

ac.round(123.44546, 2);
```

**Rückgabewerte**

Sie erhalten den gerundeten Wert zurück.

```auto
123.45
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen Wert runden möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### sum

Summiert die Werte einer bestimmten Spalte in einem Array von maps auf (siehe Funktion [toCSV](#toCSV)).

**Syntax**

```auto
ac.sum(rows, col);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| rows | Definiert ein Array von maps, das die Zeilenwerte enthält. | Ja | – | Beispiel |
| col | Definiert die Spalte, deren Werte das System aufsummiert, etwa die Spalte row2. | Ja | – |

**Beispiel**

```auto
let ac = require('ac');

let rows = [
  {
    row1: new Date(),
    row2: 1.5,
    row3: 'Eine Zeichenkette 1'
  },
  {
    row1: new Date('2018-01-01'),
    row2: 123.456,
    row3: 'Eine \nZeichenkette 2'
  }

];

ac.sum(rows, 'row2');
```

**Rückgabewerte**

Sie erhalten die aufsummierte Spalte zurück.

```auto
124.956
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie bestimmte Spalten aufsummieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### toCSV

Wandelt eine Array-Struktur in ein CSV-Format.

**Syntax**

```auto
ac.toCSV(rows, cols, colSeparator, rowSeparator, quoteCharacter);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| rows | Definiert ein Array von maps, das die Zeilenwerte enthält. | Ja | – | Beispiel |
| cols | Definiert die Spalten inklusive Formatierung. | Ja | – |
| colSeparator | Definiert den Spaltentrenner. | Nein | ; |
| rowSeparator | Definiert den Zeilentrenner. | Nein | /n |
| quoteCharacter | Definiert das Zeichen pro Wert. | Nein | " |

**Beispiel**

```auto
let ac = require('ac');

let cols = [
  'row1:dd.MM.yyyy',
  'row2:de|0.0',
  'row3'
];

let rows = [
  {
    row1: new Date(),
    row2: 1.5,
    row3: 'Eine Zeichenkette 1'
  },
  {
    row1: new Date('2018-01-01'),
    row2: 123.456,
    row3: 'Eine \nZeichenkette 2'
  }

];

ac.toCSV(rows, cols, ';', '\n', '"');
```

**Rückgabewerte**

Sie erhalten die Array-Struktur im CSV-Format zurück.

```auto
24.05.2022;1,5;Eine Zeichenkette 1
01.01.2018;123,5;"Eine
Zeichenkette 2"
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie diverse Spalten und Zeilen in das CSV-Format umgewandelt benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

## JavaScript-Bibliothek common/beans

Diese Bibliothek bietet Funktionen, mit denen Sie auf die API-Propertys von Objekten lesend und schreibend zugreifen können.

Eine Übersicht über die möglichen Property-Namen finden Sie im Modul *API-Dokumentation* in *agorum core*.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let beans = require('common/beans');
```

### Funktionen

* * *

#### get

Liest Attribute und Metadaten eines Objekts aus.

**Hinweis**: Diese Funktion ist veraltet. Verwenden Sie die JavaScript-Bibliothek [common-metadata](#). Sie unterstützt Entwickler mit Automatismen wie dem Konvertieren und Erkennen von Daten- und Vererbungstyp. Durch deren Verwenden vermeiden Sie später schwer zu korrigierende Inkonsistenzen.

**Beispiel**

```auto
// Nicht vererbtes Metadatum
let acmf_dokumentTyp = beans.get(object, '~acmf_dokumentTyp');

// Vererbtes Metadatum
let acmf_lieferantenName = beans.get(object, '~~acmf_lieferantenName[0]');
```

#### beans.get(object,'paths()')

Liefert ein Array mit allen Pfaden, die der Benutzer, der das Objekt geladen hat (object.sessionController), für dieses Objekt sieht.

*Path()* ist ein Pseudo-Attribut.

**Hinweis**: Das Objekt muss mit dem Benutzer geholt werden, der momentan angemeldet ist. Wurde es im Hintergrund von einem Administrator geholt, stimmen die Pfade nicht. In diesem Falle muss der Aufruf folgendermaßen erfolgen:

```auto
beans.get(objects.find(object), 'path()');
```

**Beispiel**

```auto
/* global sessionController */

let objects = require('common/objects');
let beans = require('common/beans');

let file = objects.find('14181094370011');
beans.get(file, 'paths()');
```

**Ergebnis**

```auto
[
  [
    {
      "displayName": "Home",
      "id": "10000"
    },
    {
      "displayName": "roi",
      "id": "10002"
    },
    {
      "displayName": "Eigene Dateien",
      "id": "1002330"
    },
    {
      "displayName": "tmp",
      "id": "1066572"
    },
    {
      "displayName": "14181094370011",
      "id": "14181095521165"
    },
    {
      "displayName": "Leitfaden-Ihr-Dokumentenmanagement-in-6-Schritten.pdf",
      "id": "14181094370011"
    }
  ],
  [
    {
      "displayName": "Root",
      "id": "9999"
    },
    {
      "displayName": "Home",
      "id": "10000"
    },
    {
      "displayName": "roi",
      "id": "10002"
    },
    {
      "displayName": "Eigene Dateien",
      "id": "1002330"
    },
    {
      "displayName": "tmp",
      "id": "1066572"
    },
    {
      "displayName": "14181094370011",
      "id": "14181095521165"
    },
    {
      "displayName": "Leitfaden-Ihr-Dokumentenmanagement-in-6-Schritten.pdf",
      "id": "14181094370011"
    }
  ],
  [
    {
      "displayName": "Eigene Dateien",
      "id": "1002330"
    },
    {
      "displayName": "tmp",
      "id": "1066572"
    },
    {
      "displayName": "14181094370011",
      "id": "14181095521165"
    },
    {
      "displayName": "Leitfaden-Ihr-Dokumentenmanagement-in-6-Schritten.pdf",
      "id": "14181094370011"
    }
  ]
]
```

**Tipp**: Wenn Sie unsicher sind, ob der Administrator das Objekt durch eine Funktion geholt hat, laden Sie das Objekt für den Aufruf nochmals. Erstellen Sie den Aufruf dafür folgendermaßen:

```auto
...
beans.get(objects.find(file), 'paths()');
```

#### beans.get(object, 'unc()')

Liefert einen unc-Pfad über einen vom Benutzer erreichbaren Share.

* Das System holt den Benutzer aus dem Objekt (object.sessionController).

* *unc()* ist ein Pseudo-Attribut.

Wenn das System etwa *null* als Host liefert, wurde das Objekt mit einem anderen internen Benutzer (etwa *Administrator*) geholt. Ändern Sie den Aufruf folgendermaßen:

```auto
get(objects.find(object), 'unc()');
```

**Beispiel**

```auto
/* global sessionController */

let objects = require('common/objects');
let beans = require('common/beans');

let file = objects.find('14181094370011');
beans.get(file, 'unc()');
```

**Ergebnis**

```auto
\\roihost\privat\tmp\14181094370011\Leitfaden-Ihr-Dokumentenmanagement-in-6-Schritten.pdf
```

Wenn das gelieferte Ergebnis mit *\\\\null\\* beginnt, ändern Sie den Aufruf wie folgt, da das Objekt hier mit einem internen Benutzer (etwa als Administrator) geholt wurde.

**Ergebnis**

```auto
\\null\privat\tmp\14181094370011\Leitfaden-Ihr-Dokumentenmanagement-in-6-Schritten.pdf
```

**Aufruf**

```auto
...
beans.get(objects.find(file), 'unc()');
```

#### set

Setzt Attribute und Metadaten auf ein Objekt.

* Für Metadaten gelten die API-Konventionen.
* Das System erwartet ein ~-Präfix für nicht vererbte und ein ~~-Präfix für vererbte Metadaten.

**Hinweis**: Diese Funktion ist veraltet. Verwenden Sie die JavaScript-Bibliothek [common-metadata](#). Sie unterstützt Entwickler mit Automatismen wie dem Konvertieren und Erkennen von Daten- und Vererbungstyp. Durch deren Verwenden vermeiden Sie später schwer zu korrigierende Inkonsistenzen.

**Beispiele**

* Internes Attribut: name
* Nicht vererbtes Metadatum: ~acmf\_lieferantenStatus
* Vererbtes Metadatum: ~~acmf\_lieferantenName

Zusätzlich können Sie das Datenformat angeben, in dem das System das Metadatum speichert. Folgende Formate existieren:

* string
* date
* double
* integer
* long
* float
* boolean

Verwenden Sie diese explizite Annotation insbesondere für nicht-String-Metadaten und dazu, um Datums-Metadaten korrekt zu setzen, da das Übertragungsformat (JSON) hierfür keinen Datentyp bietet.

**Metadaten entfernen**

Mit dieser Funktion können Sie auch Metadaten setzen, die nicht über den Metadatendesigner definiert wurden, allerdings wird das nur in Ausnahmefällen empfohlen, typischerweise bei der Entfernung von nicht mehr benötigten Metadaten.

Um Metadaten zu entfernen, setzen Sie den Wert des Metadatums auf *null* oder *undefined*:

```auto
beans.set(objects[0], {
  '~~acmf_lieferantenName:string': data.acmf_lieferantenName,
  '~~acmf_lieferantenNummer:string': data.acmf_lieferantenNummer,
  '~acmf_lieferantenStatus:string': data.acmf_lieferantenStatus,
  '~acmf_lieferantAktiv:boolean': true
  '~acmf_zuEntfernen': null,
  'description': 'Das ist eine Beschreibung'
});
```

**Eine ACL setzen**

```auto
let objects = require('common/objects');
let beans = require('common/beans');

let obj = objects.find('3015157'); // Objekt, auf das die ACL gesetzt wird.

let aclName = 'ACL_Musterfirma GmbH - Intern';

beans.set(obj, {
  acl: objects.find('acl:' + aclName)  // Das Objekt der ACL übergeben.
});
```

#### selected

Prüft, ob der gegebene Selektor auf das Objekt passt.

**Beispiel**

```auto
if (beans.selected(object, '[~~area=Test]')) {
  // ...
}
```

#### date

Konvertiert einen String mit einem API-kompatiblen Datum nach ISO-8601 in ein JavaScript-Datum.

**Beispiel**

```auto
let date = beans.date('2017-05-22T19:45:00+02:00');
```

### inline-Definition für Listen

* * *

Um mit „sicheren“ Datentypen innerhalb von Listen zu arbeiten, die verschiedene Werte enthalten, existieren verschiedene Möglichkeiten.

Wenn das Metadatum *~test\_netto* existiert und Sie diesem einmal die Zahl 10 und einmal die Zahl 10.5 zuordnen, würde das System den Typ durch die automatische Erkennung einmal als *int* und einmal als *double* interpretieren. Damit Sie den Datentyp mitgeben können, existiert die Ergänzung *inline*.

#### Metadaten mit Datentypen auslesen

Metadaten mit Datentypen können Sie folgendermaßen auslesen, unabhängig davon, ob es sich um ein Array, eine Map oder einen direkten Wert handelt:

```auto
let pos = beans.get(object, '~ERPosition:inline');
```

**Ergebnis bei einem Array**

```auto
{
  type: [
    {
      Konto: 'string',
      KostenStelle: 'string',
      GegenKonto: 'string',
      Positionsbetrag: 'double',
      ArtikelBezeichnung: 'string'
    },

    {
      Konto: 'string',
      KostenStelle: 'string',
      GegenKonto: 'string',
      Positionsbetrag: 'double',
      ArtikelBezeichnung: 'string'
    }
  ],
  value: [
    {
      Konto: '12605',
      KostenStelle: '1',
      GegenKonto: '2',
      Positionsbetrag: 0.0,
      ArtikelBezeichnung: 'Reparaturauftrag'
    },

    {
      Konto: '12605',
      KostenStelle: '1',
      GegenKonto: '2',
      Positionsbetrag: 0.0,
      ArtikelBezeichnung: 'Facharbeiterlohn - Kulanz'
    }
  ]
}
```

* Pro Wert existiert eine Definition des Werts unter *type*.
* Die Werte stehen in *value.*

* Dass die *types* mehrfach definiert sind, ist nicht unbedingt notwendig bei einem Array, das aus immer den gleichen Werten besteht.

#### Wert der Arrays ändern

Möchten Sie einen Wert des Arrays ändern, iterieren Sie die *values* und ändern den Wert.

**Beispiel**

```auto
pos.value.forEach(function(item) {
  item.Positionsbetrag = item.Positionsbetrag * 1.19;
});
```

**Array zurückschreiben**

Wenn Sie genau dieses Array wieder zurückschreiben möchten, verwenden Sie wieder die Angabe *inline*:

```auto
beans.set(object, '~ERPosition:inline', pos);
```

**Neuen Wert ergänzen**

Wenn Sie einen neuen Wert ergänzen möchten, löschen Sie bei *type* alle Definitionen bis auf eine und ergänzen Sie sie um die Definition des neuen Werts.***Beispiel***

```auto
pos.type = [
  pos.type[0]
];
pos.type[0].PositionsbetragBrutto = 'double';
```

Sie können den Betrag auch bei den Werten entsprechend setzen:

```auto
pos.value.forEach(function(item) {
  item.PositionsbetragBrutto = item.Positionsbetrag * 1.19;
});
```

Danach können Sie wieder mit [beans.set](#set) zurückschreiben.

## JavaScript-Bibliothek common-cache

**Ab welcher Version verfügbar?**

• *agorum core* 8.3.0

Diese Bibliothek bietet Funktionen zum Bearbeiten von Werten im Cache.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let cache = require('common/cache')('cache-name', max-items, max-life-time);
```

#### Konstruktoren

| Konstruktor | Beschreibung | Standard |
| --- | --- | --- |
| cache-name | Definiert den Namen des systemweiten Caches, in den das System Werte ablegt. | – |
| max-items | Definiert optional die Anzahl an maximalen Einträge im Cache. Sobald die Anzahl überschritten wird, entfernt das System die ältesten Werte automatisch. Ein lesender Zugriff auf einen Wert aktualisiert den Zeitstempel, sodass automatisch häufig verwendete Einträge im Cache bleiben. | 231-1 (der Maximalwert von Integer) |
| max-life-time | Definiert optional die Zeit in Millisekunden, wie lange ein Eintrag im Cache verbleibt, bevor das System ihn aus dem Cache entfernt. Ein lesender Zugriff auf einen Wert aktualisiert die Lebensdauer, sodass automatisch häufig verwendete Einträge im Cache bleiben. | 231-1 (der Maximalwert von Integer) |

### Funktionen

* * *

#### read

Liest einen Wert aus dem Cache, basierend auf einem Schlüssel (beliebiger String).

```auto
cache.read('key')
```

#### write

Schreibt einen Wert in den Cache, basierend auf einem Schlüssel (beliebiger String).

* Der Wert kann ein beliebiges Objekt sein.
* Das System ersetzt einen vorhandenen Eintrag mit demselben key.

```auto
cache.write('key', value)
```

#### delete

Löscht einen Eintrag aus dem Cache, basierend auf dem angegebenen Schlüssel.

```auto
cache.delete('key')
```

## JavaScript-Bibliothek common/csv

**Ab welcher Version verfügbar?**

• *agorum core* 8.0

Diese JavaScript-Bibliothek bietet Funktionen zum Parsen von CSV-Dateien.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let csv = require('common/csv');

let options = {
  delimiter: ';',
  quote: '"',
  encoding: 'ISO-8859-15',
  header: true
};

let csvList = csv.read(obj-csv-File, options);
```

### Return

* * *

Sie erhalten eine Map, die Sie in JavaScript lesen können.

#### Beispiel mit Header

```auto
value;text
Bericht;Bericht
Besuch;Besuch
Arzt;Arzt
```

**Ergebnis**

```auto
[
  {
    "text": "Bericht",
    "value": "Bericht"
  },
  {
    "text": "Besuch",
    "value": "Besuch"
  },
  {
    "text": "Arzt",
    "value": "Arzt"
  }
]
```

#### Beispiel ohne Header

```auto
Bericht;Bericht
Besuch;Besuch
Arzt;Arzt
```

**Ergebnis**

```auto
[
  [
    "Bericht",
    "Bericht"
  ],
  [
    "Besuch",
    "Besuch"
  ],
  [
    "Arzt",
    "Arzt"
  ]
]
```

### Eine CSV-Datei mit Header auslesen

* * *

#### Beispiel einer CSV-Datei

```auto
value;text
100;Baustelle
200;Fahrzeug
300;agorum
```

**Hinweis**: Sollten sich Leerzeichen zwischen dem Trenner *;* und dem Text befinden, liest das System sie mit aus, führt jedoch kein trim durch.

#### Skript zum Auslesen der Werte über alle Zeilen (mit einem Header)

```auto
/* global Packages, sessionController */

let objects = require('common/objects'),
    beans = require('common/beans'),
    csv = require('common/csv');

let options = {
  delimiter: ';',
  quote: '"',
  encoding: 'ISO-8859-15',
  header: true
};

// csv parsen
let csvList = csv.read(objects.find(id-to-csv), options);

// Die CSV-Datei über alle Zeilen auslesen und value und text verarbeiten
csvList.forEach(function(entry) {
  let text = entry.text;
  let value = entry.value;
  verarbeiten(value, text);
});

// Werte für jede Zeile verarbeiten
function verarbeiten(value, text) {
  ...
  ...
}
```

### Eine CSV-Datei ohne Header auslesen

* * *

#### Beispiel CSV-Datei ohne Header

```auto
100;Baustelle
200;Fahrzeug
300;agorum
```

#### Skript zum Auslesen der Werte über alle Zeilen (ohne Header)

```auto
/* global Packages, sessionController */

let objects = require('common/objects'),
    beans = require('common/beans'),
    csv = require('common/csv');

let options = {
  delimiter: ';',
  quote: '"',
  encoding: 'ISO-8859-15',
  header: false
};

// csv parsen
let csvList = csv.read(objects.find(id-to-csv), options);

// Die CSV-Datei über alle Zeilen auslesen und value und text verarbeiten
csvList.forEach(function(entry) {
  let value = entry[0]; // Spalte 1
  let text = entry[1]; // Spalte 2
  verarbeiten(value, text);
});

// Werte für jede Zeile verarbeiten
function verarbeiten(value, text) {
  ...
  ...
}
```

## JavaScript-Bibliothek common/data

Diese Bibliothek bietet Funktionen, um mit Datenquellen-Einträgen Folgendes zu machen:

**lesen (read)**Standard für alle DataHandler

**erstellen (create)**Wird derzeit vom JsDataHandler und JdbcDataHandler unterstützt

**aktualisieren (update)**Wird derzeit vom JsDataHandler und JdbcDataHandler unterstützt

**holen (get)**Wird derzeit nur vom UserDataHandler und UserGroupDataHandler unterstützt

**löschen (del)**Wird derzeit vom JsDataHandler und JdbcDataHandler unterstützt

Eine Datenquelle wird in der MetaDb definiert. Nicht alle Datenquellen können geändert werden.

### Verwendung

* * *

```auto
let data = require('common/data');
//Jetzt den gewünschten Händler setzen über die Übergabe des MetaDB-Schlüssels
let handler = data.handler('MAIN_MODULE_MANAGEMENT/customers/DocFormDemoVerify/Data/verify-lieferanten');
```

Der handler selbst besitzt folgende Funktionen:

### Funktionen

* * *

#### create

Mit dieser Funktion legen Sie einen neuen Datensatz an.

```auto
let ret = handler.create([ query, ] parameters);
```

**Parameter**

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| query | Hinweis: Verwenden Sie den query-Parameter bei create,  update und del nicht mehr, er ist nur noch aus Kompatibilitätsgründen aufgeführt. Definiert den String, der übergeben werden kann. Der String repräsentiert in der MetaDb-Definition für CreateQuery immer die Ersetzung ${query}. Beim CSV-Handler repräsentiert dieser Parameter immer das, was in der MetaDB-Definition QueryColumn steht, also in welcher Spalte nach query gesucht wird. Der Parameter ist optional. | handler.create('Hier steht ein Text', parameters); |
| parameters | Enthält eine Struktur mit den Parametern, die übergeben werden sollen. Diese Struktur muss immer mindestens die Daten enthalten, die Ihr DataHandler für den getätigten Aufruf benötigt. | let parameters = { LieferscheinNr: 'LI00001', BestellNr: '100000', Artikelnummer: 'ANR100001', LieferMenge: 100.5 }; handler.create(parameters); // ohne den ersten Parameter In der MetaDb können Sie jetzt auf die Keys der Struktur zugreifen: select \* from verify\_lieferschein where LieferscheinNr = '${LieferscheinNr}' and BestellNr = '${BestellNr}' and Artikelnummer = '${Artikelnummer}' Zugriff durch ein inneres JavaScript: select \* from verify\_lieferschein ${{js: let where = ''; let query = \[\]; if (global.LieferscheinNr || global.BestellNr || global.Artikelnummer) { ... ... } ... }} |

**Return**

Zurückgegeben wird die Anzahl an Datensätzen, die angelegt wurden.

Verwenden Sie diesen Aufruf nur mit der Übergabe des Wertes *parameters*:

```auto
handler.create(parameters);
```

#### read

Liest Datensätze aus.

Es werden die Datensätze gelesen, die in der Übergabe definiert werden.

```auto
let data = handler.read([ query, ] parameters);
```

**Parameter**

siehe [create](#create-parameter)

**Return**

Zurückgegeben werden die gelesenen Daten:

```auto
[

  {

    LieferscheinNr : 'LI00001',

    BestellNr      : '100000',

    Artikelnummer  : 'ANR100001',

    LieferMenge    : 100.5

  }

]
```

#### get

Ruft einen bestimmten Datensatz der Datenquelle ab.

Funktioniert nur bei den folgenden Handlern, die den Abruf unterstützen:

* UserDataHandler
* UserGroupDataHandler

```auto
let data = handler.get('id');
```

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| id | Definiert die id oder UUID aus agorum core. Auch Schreibweisen wie group:name-der-gruppe sind möglich. |

**Return**

Zurückgegeben wird ein Objekt mit *value* und *text*:

```auto
{
  value: "123456",
  text: "Name/Text des Elements"
}
```

#### update

Ändert Datensätze.

Es werden die Datensätze geändert, die in der Übergabe definiert werden.

```auto
let count = handler.update([ query, ] parameters);
```

**Parameter**

siehe [create](#create-parameter)

**Return**

Zurückgegeben wird die Anzahl der geänderten Datensätze als Zahl.

*parameters* muss dem Eintrag *DeleteQuery* in der MetaDb entsprechen.

#### del

Löscht Datensätze.

Es werden die Datensätze gelöscht, die in der Übergabe definiert werden.

```auto
let count = handler.del([ query, ] parameters);
```

**Parameter**

siehe [create](#create-parameter)

**Return**

Zurückgegeben wird die Anzahl gelöschter Datensätze als Zahl.

*parameters* muss dem Eintrag *DeleteQuery* in der MetaDb entsprechen.

### Allgemeine Information zu allen DataHandlern

* * *

Die in der MetaDB verwendete Schreibweise mit *${<Name Metadatum>}* wird über die JavaScript-Bibliothek [common-templates](#) ersetzt.

**Beispiel**

```auto
Query=[ 'acbasicarchive_aktesection_cs:${acbasicarchive_aktesection}', 'acbasicarchive_aktearea_cs:${acbasicarchive_aktearea}', 'inpath:9999', 'acbasicarchive_aktescope:${query}', 'acbasicarchive_aktescope:*' ]
```

Dies bedeutet, dass alles möglich ist, was diese Bibliothek kann.

### Verwendung

* * *

```auto
let data = require('common/data');
```

#### handler

Als Parameter geben Sie den MetaDb-Schlüssel zur gewünschten Datenquellen-Definition an:

```auto
let handler = data.handler('MAIN_MODULE_MANAGEMENT/customers/demo/data/NAME-DES-DATAHANDLERS');
```

#### Einträge lesen

```auto
let parameters = {};
let data = handler.read('beispiel-query', parameters);

data.forEach(entry => {
  let text = entry.text;
  let value = entry.value;
});
```

In diesem Beispiel kann *parameters* eine Map mit Name-Werte paaren, welche an den DataHandler weitergereicht wird und dort als Parameter verwendet werden kann.

**Beispiel**

```auto
let parameters = {
  testFeld: 'testWert'
};

// in der MetaDb, bei beispielsweise einem JDBC Handler kann nun testFeld verwendet werden als Kriterium in der Query, Beispiel: select name, value from testtable where test=${testFeld}
```

#### Einträge anlegen / ändern / löschen (nur JDBC oder JS-Handler)

```auto
let data = require('common/data');
let handler = data.handler('MAIN_MODULE_MANAGEMENT/customers/demo/data/test_jdbc');

// Allgemein im Beispiel dient "beispiel-name-123" als das Feld, das als ${query} ersetzt wird in dem JdbcHandler in der MetaDb

// create
handler.create('beispiel-name-123', { value: 'beispiel-value-123' );

// update
handler.update('beispiel-name-123', { oldValue: 'beispiel-value-123', newValue: 'beispiel-newvalue-123' });

// delete
handler().del('beispiel-name-123', { value: 'beispiel-value-123' });
```

#### Beispiel einer Tabelle mit mehr Spalten

Es wird eine Lieferscheintabelle benötigt, in die die Daten von Lieferscheinen hineingeschrieben werden. Diese Daten sind:

* LieferscheinNr
* BestellNr
* Artikelnummer
* LieferMenge

Die Tabelle für eine MySQL-DB sieht folgendermaßen aus:

```auto
CREATE TABLE `verify_lieferschein` (
    `LieferscheinNr` VARCHAR(200) NOT NULL,
    `BestellNr` VARCHAR(200) NOT NULL,
    `Artikelnummer` VARCHAR(200) NOT NULL,
    `LieferMenge` DOUBLE NOT NULL,
    PRIMARY KEY (`LieferscheinNr`, `BestellNr`, `Artikelnummer` )
)
ENGINE=InnoDB;
```

Es wird jetzt ein DataHandler definiert, der in dieser Tabelle Datensätze anlegen, ändern, lesen und löschen kann. Dazu wird der DataHandler in der MetaDb definiert.

**Schlüssel in der MetaDb**

```auto
MAIN_MODULE_MANAGEMENT/customers/DocFormDemoVerify/Data/ verify-lieferanten
```

Dort werden folgende Einträge angelegt:

```auto
Class=agorum.api.object.data.JdbcDataHandler

CreateQuery=insert into verify_lieferschein (LieferscheinNr, BestellNr, Artikelnummer, LieferMenge) values ('${LieferscheinNr}', '${BestellNr}', '${Artikelnummer}',  ${LieferMenge})

DeleteQuery=delete from verify_lieferschein where LieferscheinNr = '${LieferscheinNr}' and BestellNr = '${BestellNr}' and Artikelnummer = '${Artikelnummer}'

Driver=com.mysql.jdbc.Driver

LowerCaseKeys=false

LowerCaseValues=false

// Password wird verschlüsselt eingetragen
Password=******

// Hier wird ein mehrzeileger Eintrag gemacht, damit das JS besser lesbar ist
Query=select * from verify_lieferschein ${{js:
  let where = '';
  let query = [];
  if (global.LieferscheinNr || global.BestellNr || global.Artikelnummer) {
    if (global.LieferscheinNr) {
      query.push(' LieferscheinNr = \'' + global.LieferscheinNr + '\'');
    }
    if (global.BestellNr) {
      query.push(' BestellNr = \'' + global.BestellNr + '\'');
    }
    if (global.Artikelnummer) {
      query.push(' Artikelnummer = \'' + global.Artikelnummer + '\'');
    }
    where = ' where ';
  }
  where + query.join(' and ');
}}

UpdateQuery=update verify_lieferschein set LieferMenge = ${newLieferMenge} where  LieferscheinNr like '${LieferscheinNr}' and BestellNr like '${BestellNr}' and Artikelnummer like '${Artikelnummer}'

URL=jdbc:mysql://localhost:3306/roi?useUnicode=true&characterEncoding=UTF-8

Username=root
```

**Testprogramm zum DataHandler**

Mit dem folgenden Testprogramm testen Sie den DataHandler.

**Hinweis**: Bevor Sie das Testprogramm ausführen können, müssen Sie die Tabelle in der Datenbank anlegen, auf die die Einträge in der MetaDb verweisen.

```auto
let data = require('common/data');
let handler = data.handler('MAIN_MODULE_MANAGEMENT/customers/DocFormDemoVerify/Data/verify-lieferanten');

let value = {
  LieferscheinNr: 'LI00001',
  BestellNr: '100000',
  Artikelnummer: 'ANR100001',
  LieferMenge: 100.5
};

// Datensatz anlegen
try {
  handler.create(value);
} catch(e) {
  // Falls es einen Fehler gibt, etwa wenn es den Datensatz schon gibt
}

let keyPK = {
  LieferscheinNr: 'LI00001',
  BestellNr: '100000',
  Artikelnummer: 'ANR100001',
};

// Lesen
data = handler.read(keyPK);
data;
// Date hat folgenden Aufbau:
/**
[

  {
    "LieferscheinNr" : "LI00001",
    "BestellNr" : "100000",
    "Artikelnummer" : "ANR100001",
    "LieferMenge" : 100.5
  }

]
***/
// Hier in diesem Falle kann immer nur ein Datensatz gelesen werden.

/**
Jetzt noch die zu ändernden Werte mit reinnehmen
Hier in diesem falle wird der Wert Liefermenge durch den Namen "newLieferMenge" repräsentiert.
Diese setzten wir jetzt in die Struktur mit rein
**/
keyPK.newLieferMenge = 1234.998;

// Ändern
handler.update(keyPK);
data = handler.read(keyPK);
data;

//Jetzt wird noch gelöscht
handler.del(keyPK);

/**
Wenn hier nichts übergeben wird, werden alle Datensätze aus der Tabelle gelesen. Siehe dazu den Eintrag in der MetaDB mit dem Namen Query
**/
keyPK = {
//  LieferscheinNr: 'LI00001',
//  BestellNr: '100000',
//  Artikelnummer: 'ANR100001',
};

data = handler.read(keyPK);
data;
// Jetzt sollte die Tabelle wieder leer sein
```

#### Beispiel für die Verwendung in aguila

```auto
/* global sca */

let data = require('common/data');
let aguila = require('common/aguila');

let widget = aguila.create({
  // ...
});

function bind(field, dependencies) {
  let handler;

  field.on('query', query => {
    aguila
    .fork(() => {
      if (!handler) {
        // Handler erst bei Bedarf erzeugen
        handler = data.handler(Packages.agorum.api.metadata.Metadata.getField(sca, field.name).dataSource);
      }

      // Filter setzen, der Abhängigkeiten von anderen Eingabefeldern definiert
      let parameters = {};

      dependencies.forEach(field => parameters[field.name] = field.value);

      // Die ersten 100 Treffer darstellen
      return handler.read(query, parameters).slice(0, 100);
    })
    .then(rows => field.data = rows);
  });
}

// Das Feld acbasicarchive_akte ist abhängig von den Feldern
// acbasicarchive_aktesection und acbasicarchive_aktearea
bind(widget.down('acbasicarchive_akte ist abhängig von '), [
  widget.down('acbasicarchive_aktesection'),
  widget.down('acbasicarchive_aktearea')
]);
```

## Beispiel-Datenquellen für DataHandler

### Suche

* * *

Die Datenquelle *Suche* basiert auf einem Faceting (Gruppierung) der Solr-Suche und lädt etwa alle Werte eines Metadatums. Derartige Datenquellen werden etwa über metadata-YML angelegt, wenn *data=search* gewählt wird.

#### Ein Beispiel für eine Liste aller Tag-Felder

`MAIN_MODULE_MANAGEMENT/customers/demo/data/ag_tags`

```auto
// Schematische Darstellung der Einträge in der MetaDb
Class=agorum.api.object.data.SearchDataHandler

// das Feld, das gruppiert werden soll
Facet=ag_tags

// Sortierung
FacetSort=index

// maximale Anzahl von Element, die gleichzeitig geladen werden
Limit=100

// ${query} dient als Einschränkungskriterium, kann etwa der eingegebene Wert eine DropDown Box sein)
// Das Feld selbst ist ein Array
// Hinweis: Wenn ${query} nicht belegt ist (also keine Eingabe gemacht wurde), dann wird nach diesem Element (Array-Eintrag) nicht gesucht
Query=[ 'ag_tags:${query}', 'ag_tags:*' ]
```

#### Beispiel einer reinen Suche

```auto
// Schematische Darstellung der Einträge in der MetaDb
Class=agorum.api.object.data.SearchDataHandler

// das Feld, das als Text-Wert definiert wird (in einer Combobox)
Text=name

// das Feld, das als Wert-Feld definiert wird (in einer Combobox)
Value=name

// maximale Anzahl von Element, die gleichzeitig geladen werden

Limit=100

// ${query} dient als Einschränkungskriterium, kann etwa der eingegebene Wert eine DropDown Box sein)
// Das Feld selbst ist ein Array
// Hinweis: Wenn ${query} nicht belegt ist (also keine Eingabe gemacht wurde), dann wird nach diesem Element (Array-Eintrag) nicht gesucht

Query=[ 'name:${query}', 'identifier:ag_kundenakte' ]
```

#### Beispiel eines Facet mit Abhängigkeiten

```auto
// Schematische Darstellung der Einträge in der MetaDb
Class=agorum.api.object.data.SearchDataHandler

// das Feld, das gruppiert werden soll

Facet=acbasicarchive_aktescope

// Sortierung

FacetSort=index

// maximale Anzahl von Element, die gleichzeitig geladen werden

Limit=100

// ${query} dient als Einschränkungskriterium, kann etwa der eingegebene Wert eine DropDown Box sein)
// Das Feld selbst ist ein Array
// in diesem Beispiel gibt es noch die Abhängigkeit von bis zu zwei weiteren Metadaten: "acbasicarchive_aktesection" und "acbasicarchive_aktearea"
// Hinweis: Wenn ${query}, ${acbasicarchive_aktesection} oder ${acbasicarchive_aktearea} nicht belegt ist (also keine Eingabe gemacht wurde oder das Metadatum nicht belegt ist), dann wird nach diesem Element (Array-Eintrag) nicht gesucht

Query=[ 'acbasicarchive_aktesection_cs:${acbasicarchive_aktesection}', 'acbasicarchive_aktearea_cs:${acbasicarchive_aktearea}', 'inpath:9999', 'acbasicarchive_aktescope:${query}',  'acbasicarchive_aktescope:*' ]
```

### JDBC

* * *

Die Datenquelle *JDBC* enthält eine Verbindung zu einer Datenbank und einen Select, der die gewünschten Felder für die Datenquelle liefert.

*agorum core* liefert im Standard bereits Treiber für folgende Datenbanken mit:

* MySql/MariaDb (*agorum core open* + *agorum core pro*)
* ProstgreSQL (*agorum core open* + *agorum core pro*)
* Oracle (*agorum core pro*)
* MS SQL Server (*agorum core pro*)

Die Treiber befinden sich im Installationsverzeichnis unter *INSTALLDIR/agorumcore/jboss/server/default/lib*.

Neue JDBC-Treiber können Sie als JAR-Datei in dieses Verzeichnis kopieren. Die Treiber stehen nach einem Neustart von *agorum core* zur Verfügung.

**Achtung**: Beeinträchtigung des Systembetriebs durch 2 Treiber für ein und dieselbe Datenbank. Wenn Sie zwei Treiber für die gleiche Datenbank verwenden, verwendet das System willkürlich einen von beiden. Unvorhergesehene Probleme im Betrieb des Systems sind die Folge. Verwenden Sie daher immer nur 1 Treiber für eine Datenbank.

#### Beispiel für eine JDBC-Verbindung

`MetaDb: MAIN_MODULE_MANAGEMENT/customers/demo/data/test_jdbc`

```auto
Class=agorum.api.object.data.JdbcDataHandler

// JDBC-Treiber für die Datenbank
// Oracle
Driver=oracle.jdbc.OracleDriver

// MS SQL Server
// Driver=com.microsoft.sqlserver.jdbc.SQLServerDriver

// MariaDb/MySql
// Driver=org.mariadb.jdbc.Driver
// Driver=com.mysql.jdbc.Driver

// PostgreSQL
// Driver=org.postgresql.Driver

// Datenbank Benutzer
Username=DB User

// Datenbank Passwort
Password=DB Password

// JDBC-Connection URL
// Oracle
URL=jdbc:oracle:thin:@//db-server:1521:SCHEMA-NAME

// MS SQL Server
// URL=jdbc:sqlserver://db-server:1433;databaseName=SCHEMA-NAME

// MariaDb/MySql
// URL=jdbc:mariadb://db-server:3306/SCHEMA-NAME?useUnicode=true&characterEncoding=UTF-8&useSSL=false
// URL=jdbc:mysql://db-server:3306/SCHEMA-NAME?useUnicode=true&characterEncoding=UTF-8&useSSL=false
​​​​​​
// PostgreSQL
// URL=jdbc:postgresql://db-server:5432/SCHEMA-NAME

// Die zurückgegebenen Feldnamen werden kleingeschrieben (true)
LowerCaseKeys=true

// Die zurückgegebenen Werte werden nicht kleingeschrieben (false)
LowerCaseValues=false

// Die Datenbankabfrage, ${query} beinhaltet einen Filter, z. B. aus einer Combobox
Query=SELECT text, value FROM testtable WHERE name=${query} OR value=${query}

// Für neue Einträge
CreateQuery=insert into testtable (name, value) values ('${query}', '${value}')

// Zum Löschen von Einträgen
DeleteQuery=delete from testdata where name = '${query}' and value = '${value}'

// Zum Ändern von Einträgen
UpdateQuery=update testtable set value = '${newValue}' where name = '${query}' and value = '${oldValue}'
```

Um einen solchen Handler zu verwenden, verwenden Sie die [JavaScript-Bibliothek common/data](#).

#### Inline-JavaScript beim JDBC-Handler anhand einer Kostenstelle

Sie können in ein SQL-Statement im JDBC-Handler ein Inline-[JavaScript](#) definieren.

Beispiel für den Eintrag *Query=*, mit dem ein where-Statement erstellt werden soll, wenn der Parameter *query* belegt ist:

```auto
Query=select Kostenstelle value, Kostenstellenbezeichnung text, Kostenstelle v from Kostenstelle_demo_jdbc ${js: global.query ? ('where Kostenstellenbezeichnung like \'%' + query + '%\'') : '';}
```

**Selbiges als mehrzeiliges Inline-Skript**

```auto
Query=select Kostenstelle value, Kostenstellenbezeichnung text, Kostenstelle v from Kostenstelle_demo_jdbc ${{js:
  if (global.query) {
    'where Kostenstellenbezeichnung like \'%' + query + '%\'';
  }
  else {
    '';
  }
}}
```

**Handler aufrufen**

```auto
let data = require('common/data');

//Jetzt den gewünschten Händler setzen über die Übergabe des MetaDB-Schlüssels

let handler = data.handler('MAIN_MODULE_MANAGEMENT/customers/agorum.demo.jdbc.handler/data/sample-jdbc-mysql-handler-inline-js');

let parameters = {
  query: '0129'
};

let myData = handler.read(parameters);

myData;
```

**Weitere Beispiele von Inline-JavaScript**

```auto
Query=select * from verify_lieferschein ${{js:
  let where = '';
  let query = [];
  if (global.LieferscheinNr || global.BestellNr || global.Artikelnummer) {
    if (global.LieferscheinNr) {
      query.push(' LieferscheinNr = \'' + global.LieferscheinNr + '\'');
    }
    if (global.BestellNr) {
      query.push(' BestellNr = \'' + global.BestellNr + '\'');
    }
    if (global.Artikelnummer) {
      query.push(' Artikelnummer = \'' + global.Artikelnummer + '\'');
    }
    where = ' where ';
  }
  where + query.join(' and ');
}}
```

#### Statements durch Gruppierung steuern

**Hinweis**: Diese Methode ist veraltet. Verwenden Sie stattdessen das [Inline-JavaScript](#inline javascript).

Je nachdem, welche *parameters* übergeben werden, müssen Sie das Statement durch eine Steuerung der Gruppierung anpassen:

* $O\[...\]$
* $P( ...)$
* $B(...)$
* $M\[...\]$

**Beispiel**

```auto
Query=SELECT id as value,name as text, description as value1, UUID as value2 FROM globalobject $O[WHERE $P(name LIKE '%${query}%')$ $B(OR)$ $P(UUID like '%${query}%')$]$ LIMIT 1000
```

**Bedeutung der Gruppierungen**

| Gruppierung | Beschreibung |
| --- | --- |
| P/PREDICATE (Prädikat) | Gesamtes Prädikat wird nur eingefügt, wenn alle Platzhalter darin gefüllt wurden. |
| B/BETWEEN (Zwischentext) | Zwischentext wird nur eingefügt, wenn davor und danach ein Prädikat eingefügt wird. |
| O/OPTIONAL (optionaler Teil) | Gesamter optionaler Teil wird nur eingefügt, wenn darin mindestens ein Prädikat eingefügt wurde. |
| M/MANDATORY (Pflichtteil) | Pflichtteil wird immer eingefügt, unabhängig davon, ob darin Prädikate eingefügt wurden. |

**Hinweise**:

* Die Gruppen P und B dürfen ausschließlich innerhalb von entweder O oder M verwendet werden.
* Platzhalter dürfen nur innerhalb von P verwendet werden.
* Weitere Verschachtelungen sind nicht erlaubt.
* Werden keine Gruppierungen verwendet, werden Platzhalter über die Standard-Template-Logik gefüllt.

**Beispiel mit Kostenstelle und Gruppierung**

```auto
Query=select Kostenstelle value, Kostenstellenbezeichnung text, Kostenstelle v from Kostenstelle_demo_jdbc $O[ where Kostenstellenbezeichnung like $P('%${query}')$]$
```

#### value & text sind ungleich (lookup)

Wenn ein Metadatum auf einem JDBC-DataHandler aufbauen soll und dieses in einer form verwendet wird, werden Tabellenwerte ausgelesen und dem Benutzer angezeigt. Für diesen Prozess ist ein SELECT notwendig. Besitzen nun wie in folgendem Beispiel die ausgelesene Tabellen verschiedene Werte für value und text, benötigt *agorum core* Unterstützung:

```auto
v;text;value
"0050";"0050 - Ausstehende Einlagen auf das Komplementär-Kapital, nicht eingefordert";"0050"
"0060";"0060 - Ausstehende Einlagen auf das Komplementär-Kapital, eingefordert";"0060"
"0070";"0070 - Ausstehende Einlagen auf das Kommandit-Kapital, nicht eingefordert";"0070"
"0080";"0080 - Ausstehende Einlagen auf das Kommandit-Kapital, eingefordert";"0080"
```

Damit das System den Text und nicht den value-Wert anzeigt, wird ein lookup-Eintrag benötigt.

**Bedingungen, die für ein lookup notwendig sind**

* Sie verwenden einen JDBC-DataHandler.
* Der JDBC-DataHandler verweist auf eine Datenbank, deren value- & text-Werte unterschiedlich sind.
* Diese Datenquelle wird in einem Metadatum verwendet.
* Sie planen, die Datenquelle in einer aguila-form zu verwenden.

**Beispiel**

Die Datenquelle lautet folgendermaßen:

```auto
MAIN_MODULE_MANAGEMENT/customers/TESTPLUGIN/Data/test_datasource
```

Der dazugehörige Lookup-Eintrag muss wie folgt angelegt sein:

```auto
MAIN_MODULE_MANAGEMENT/customers/TESTPLUGIN/Data/test_datasource_lookup
```

Dahinter muss ein DataHandler definiert sein, der in der Lage ist, basierend auf dem gelieferten Wert (als *query*) den korrekten data-Teil zurückzugeben.

* Beispiel für einen solchen lookup-Handler siehe [Beispiel zu einem lookup handler](#).
* Ist kein lookup verfügbar, kommt es zu einer Fehlermeldung, außer text und value besitzen identische Werte.
* Bei Nutzung von aguila oder einem Metadatum (wenn *restricted = false* ist), wird ebenfalls kein lookup-Handler vorausgesetzt. In diesem Fall wird dieser zwar verwendet, sofern er vorhanden ist; ist er es jedoch nicht, wird der eingegebene Text als Wert verwendet.

### CSV

* * *

Die Datenquelle *CSV* basiert auf einer CSV-Datei. Eine solche CSV-Datei wird etwa angelegt, wenn Sie in der Datei *metadata.yml* im Bereich *data* eigene Paare für *value* und *text* anlegen.

#### Beispiel für eine CSV-Datei

`MetaDb: MAIN_MODULE_MANAGEMENT/customers/demo/data/test_csv`

```auto
// Schematische Darstellung der Einträge in der MetaDb
Class=agorum.api.object.data.CsvDataHandler

// Groß-/Kleinschreibung beim Suchen in den Feldern beachten (true/false)
CaseSensitive=false

// Trennzeichen in der CSV Datei
Delimitier=;

// Kodierung der CSV Datei
Encoding=UTF-8

// Teilwortsuche (false), oder gesamte Zeichenkette muss passen (true)
Exact=false

// Pfad oder ID zur CSV Datei selbst
PathOrId=/agorum/roi/customers/demo/data/test_csv.csv

// Spalte, in der über "query" (erster Parameter) gesucht werden soll
QueryColumn=text

// Zeichen für die Markierung zusammenhängender Spalten innerhalb der CSV Datei
Quote="

// Spalte, die auch Textschlüssel zur Übersetzung enthalten kann
Translate=text

// true, wenn die CSV Spaltenüberschriften enthält: value, text
WithHeader=true
```

#### Beispiel für Abhängigkeiten eines csv-Handler über require (common/data) und aguila

**CSV-Datei für das Metadatum „agorum\_demo\_csv\_handler\_type\_a“**

```auto
value;text
A1;Typ A1
A2;Typ A2
A3;Typ A3
```

**CSV für das Metadatum „agorum\_demo\_csv\_handler\_type\_b“ (mit einer Abhängigkeit vom Metadatum „agorum\_demo\_csv\_handler\_type\_a“)**

```auto
value;text;agorum_demo_csv_handler_type_a
B1;Typ B1 (A1);A1
B2;Typ B2 (A1);A1
B3;Typ B3 (A1);A1
B4;Typ B4 (A2);A2
B5;Typ B5 (A2);A2
B6;Typ B6 (A2);A2
B7;Typ B7 (A2);A2
B8;Typ B8 (A2);A2
B9;Typ B9 (A3);A3
B10;Typ B10 (A3);A3
```

**CSV für das „Metadatum agorum\_demo\_csv\_handler\_type\_c“ (mit einer Abhängigkeit vom Metadatum „agorum\_demo\_csv\_handler\_type\_b“)**

```auto
value;text;agorum_demo_csv_handler_type_b
C1;Typ C1(B1);B1
C2;Typ C2(B1);B1

C3;Typ C3(B2);B2
C4;Typ C4(B2);B2
C5;Typ C5(B2);B2

C6;Typ C6(B3);B3
C7;Typ C7(B3);B3
C8;Typ C8(B3);B3
C9;Typ C9(B3);B3
C10;Typ C10(B3);B3

C11;Typ C11(B4);B4
```

**Zugehöriges JavaScript**

```auto
let data = require('common/data');
let handler_a = data.handler('MAIN_MODULE_MANAGEMENT/customers/agorum.demo.csv.handler/Data/agorum_demo_csv_handler_type_a');
let handler_b = data.handler('MAIN_MODULE_MANAGEMENT/customers/agorum.demo.csv.handler/Data/agorum_demo_csv_handler_type_b');
let handler_c = data.handler('MAIN_MODULE_MANAGEMENT/customers/agorum.demo.csv.handler/Data/agorum_demo_csv_handler_type_c');

let parameters_a = {

};
let query_a = 'A1';
let value_a = handler_a.read(query_a, parameters_a);

value_a;

let parameters_b = {
  agorum_demo_csv_handler_type_a: value_a[0].value
};
let query_b = '';
handler_b.read(query_b, parameters_b);
```

**Ergebnis**

```auto
[

  {
    "agorum_demo_csv_handler_type_a" : "A1",
    "text" : "Typ B1 (A1)",
    "value" : "B1"
  },

  {
    "agorum_demo_csv_handler_type_a" : "A1",
    "text" : "Typ B2 (A1)",
    "value" : "B2"
  },

  {
    "agorum_demo_csv_handler_type_a" : "A1",
    "text" : "Typ B3 (A1)",
    "value" : "B3"
  }

]
```

**aguila-Oberfläche, bei der von oben nach unten die Auswahl abhängig von dem zuvor ausgewählten Wert ist**

```auto
let aguila = require('common/aguila');

let form = aguila.create({
  width: 300,
  height: 300,
  type: 'agorum.composite.form.basic',
  name: 'basicForm',

  elements: [
    {
      name: 'agorum_demo_csv_handler_type_a',
    },
    {
      name: 'agorum_demo_csv_handler_type_b',
    },
    {
      name: 'agorum_demo_csv_handler_type_c',
    }

  ]
});

form.on('input', data => {
  if (data.name === 'agorum_demo_csv_handler_type_a' ) {
    let parameters = {
      agorum_demo_csv_handler_type_a: data.value
    };
    form.set('agorum_demo_csv_handler_type_b.dataSourceParameter', parameters);
  }
  else if (data.name === 'agorum_demo_csv_handler_type_b' ) {
    let parameters = {
      agorum_demo_csv_handler_type_b: data.value
    };
    form.set('agorum_demo_csv_handler_type_c.dataSourceParameter', parameters);
  }
});

form;
```

Um die Auswahl einzuschränken, können in einer CSV-Datei beliebig viele abhängige Spalten vorkommen. Die Spalten können Sie über die *parameters* mitgeben.

### USER, USER-GROUP, GROUP, GROUP-USERS

* * *

Diese Datenquellen sind spezifisch eingebaut und liefern entweder:

* Benutzer
* Benutzer sowie Benutzergruppen
* nur Benutzergruppen

**Hinweis**: Die Datenquellen werden ebenfalls aktiviert, wenn Sie in der Datei *metadata.yml* folgende Werte wählen:

* data=user
* data=user-group
* data=group

#### Beispiel für eine User-/ Gruppen-Definition

`MetaDb: MAIN_MODULE_MANAGEMENT/customers/demo/data/test_user_group`

```auto
// Schematische Darstellung der Einträge in der MetaDb
Class=agorum.api.object.data.UserGroupDataHandler

// minimale Anzahl Zeichen, die als query vorhanden sein müssen, damit gesucht wird (z.B: in einer Combobox)
MinChars=2

// user=Benutzer, group=Benutzergruppen, user-group=Benutzer und Benutzergruppen, group-users=Benutzer einer Benutzergruppe
Type=user

// Name der Benutzergruppe, in der gesucht werden soll, gilt, wenn Type=group-users
Group=GRP_Demo
```

### JS

* * *

Der JS-DataHandler ruft ein Skript auf, das Daten zurückgeben oder manipulieren kann. Der JS-Handler kann ebenfalls verwendet werden, um etwa einen weiteren Handler aufzurufen, um diese Logik zu verleihen.

Folgende Parameter können Sie an den JS-DataHandler übergeben:

| Parameter | Beschreibung |
| --- | --- |
| Query | Eigener Such-String, der die Ergebnisse eingrenzt. Ausreichend ist ein Name oder ein Teil des Namens. Der Wert wird einerseits für den Lookup eines einzelnen Wertes gesucht (wichtig u. a. für ComboBoxen oder Drop-down-Listen), andererseits entspricht der Wert dem Parameter query der JavaScript-Bibliothek common/data. Ein DataHandler kann optional immer mit <query>, <parameters> aufgerufen werden. Den Lookup-Modus aktivieren Sie, indem Sie eine Query angeben und in den <parameters> die Einstellung {lookup: true } übergeben. |
| Parameters | Dient als Parameter-Objekt, das dem DataHandler über die JavaScript-Bibliothek common/data mitgegeben wird. Sie steuern hierüber das Verhalten des DataHandlers.  Wird der DataHandler innerhalb eines Suchfilters als Auswahlfeld (select) verwendet, so wird unter parameters die completeQuery mitgegeben. Sie enthält die komplette Query der umliegenden Suche. Ein JS-Handler kann darauf reagieren und etwa nur noch einen Teil der Daten anbieten, die zum Suchergebnis passen. |
| Command | Definiert, mit welchem Kommando der DataHandler aufgerufen wurde (Kommandos siehe JavaScript-Bibliothek common/data). JS-DataHandler unterstützen alle Kommandos, die implementiert sind. |
| Path | Enthält den Pfad, der für den DataHandler verwendet wird, sodass auf erweiterte MetaDB-Keys zugegriffen werden kann. Verwenden Sie etwa den DataHandler user-group, so würde Path Folgendes zurückgeben: MAIN\_MODULE\_MANAGEMENT/customers/Standard/Data/user-group |

```auto
// Schematische Darstellung der Einträge in der MetaDb
Class=agorum.api.object.data.JsDataHandler

// Pfad oder ID zu einer JS-Datei
Script=/agorum/roi/customers/demo/js/TestDataHandler.js

// oder Inline JavaScript Code
Script.js=Inline JavaScript Code
```

#### Beispiel: TestDataHandler.js

```auto
/* global sc, sca, query, parameters, command, path */

let items = [];
if (command === 'read') {
  items.push({
    text: 'dies ist Kommando: ' + command,
    value: 'dies ist die Query: ' + query
  });
}
items;
```

#### Beispiel: ParameterizedDataHandler.js

Für dieses Beispiel:

* muss der MetaDB-Key *Limit* angelegt werden
* muss der Parameter *elementName* angegeben werden

```auto
/* global sc, sca, query, parameters, command, path */
let metadb = require('common/metadb');

// Lese die MetaDB-Keys des DataHandlers aus
let limit = metadb.getParameter('limit', parameters, path, 100, 'number');

// Setze die Einstellungen des DataHandlers
let elementName = parameters.elementName;

let items = [];
if (command === 'read') {

  // Füge Elemente hinzu, bis die Anzahl <Limit> entspricht.
  while (items.length < limit) {
    let count = items.length + 1;
    items.push({
      text: 'Dies ist ' + parameters.elementName + ' Nummer: ' + count,
      value: count
    });
  }
}

// apply limit
items = items.splice(0, limit);

items;
```

#### Beispiel: Metadaten für Lieferantenname und Lieferantennummer

Beispiel für den Lieferantennamen und die Lieferantennummer siehe [Beispiel-Metadatum mit einem JS-Handler definieren](#).

#### Verwendung des JS DataHandlers innerhalb des agorum core information centers

**Ab welcher Version nutzbar?**

*agorum core* 9.5.0

Bei Verwendung des JS DataHandlers innerhalb der Suche liefert das System in *parameters.filterSelection* alles mit, was in der Suche gewählt wurde. So kann der DataHandler darauf reagieren und etwa in Abhängigkeit der Auswahl nur eine passende Untermenge liefern (Aufbau des Parameters *filterSelection* siehe [Einen Filter vorbelegen](#)).

**Beispiel**

```auto
/* global sc, sca, query, parameters, command, path */

let items = [];
if (command === 'read') {
  let filterValue = parameters.filterSelection.nameDesFilters.value;

  items.push({
    text: 'dies ist Kommando: ' + command,
    value: 'dies ist die Query: ' + query
  });
}
items;
```

## JavaScript-Bibliothek common/metadata

Diese Bibliothek bietet Funktionen zum Laden oder Speichern von Objekt-Metadaten.

* Für die Konvertierung und Zuordnung der Metadaten werden die Definitionen aus dem Metadaten-Designer verwendet.
* Es müssen dort alle verwendeten Metadaten definiert sein.
* Wenn Sie die empfohlene Datei *metadata.yml* zur [Erstellen von Metadaten](#) verwenden, sind die Metadaten automatisch im Metadaten-Designer vorhanden.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let metadata = require('common/metadata');
```

### Funktionen

* * *

#### load

Lädt entweder alle oder bestimmte Metadaten eines Objekts.

Das System lädt alle Metadaten, inklusiver interner, die direkt auf dem Objekt sitzen. Falls Sie dies nicht wünschen, verwenden Sie stattdessen folgenden Aufruf. Dadurch werden die internen Metadaten nicht ausgegeben:

```auto
metadata.load(object, '~')
```

**Hinweise**:

* Im Gegensatz zu *filingassistant/metadata.load()* werden von *load()* nur die Metadaten geladen, die direkt auf dem Objekt gesetzt sind.

* Die oben stehende Funktion kann nur auf ein einzelnes Objekt angewendet werden.

**Beispiel**

```auto
// alle Metadaten
let all = metadata().load(object [,filter1 [, filter2][,..]]]).data();
// filter siehe unten
// Zugriff auf diese Daten, etwa:
// all.name
// all.description

// ausgewählte Metadaten
let some = metadata().load(object, 'name', 'acmf_kundenName').data();
// Zugriff auf diese Daten, etwa:
// some.name
// some.acmf_kundenName

// gefilterte Metadaten
let acmf = metadata().load(object, /^acmf_/).data();
// Zugriff auf diese Daten, etwa:
// acmf.acmf_kundenName
// acmf.acmf_kundenNummer
```

Beachten Sie, dass alle Metadaten, die direkt auf dem Objekt sitzen, inklusive interner, geladen werden. Falls Sie dies nicht wünschen, verwenden Sie stattdessen folgenden Aufruf. Dadurch werden die internen nicht mit ausgegeben:

```auto
metadata.load(object, '~')
```

**Hinweise**: • Im Gegensatz zu `filingassistant/metadata.load()` werden von `load()` nur die Metadaten geladen, die direkt auf dem Objekt gesetzt sind.• Die oben stehende Funktion kann nur auf ein einzelnes Objekt angewendet werden.

#### all

Lädt alle benutzerdefinierten (keine eingebauten) Metadaten, die entweder auf dem Objekt selbst definiert sind oder darauf vererbt wurden, oder Metadaten vom Typ *list*.

Im Gegensatz zu [merge()](#merge) werden bei vererbten Metadaten alle Werte als Array zurückgegeben.

**Achtung**: Beeinträchtigung der Systemleistung durch Benutzung der Funktion. Wenn sehr viele Metadaten im System vorhanden sind, kann eine Abfrage durch diese Funktion das System verlangsamen. Filtern Sie stets nach Metadaten, wie im nachfolgenden Skript angegeben, um eine Verlangsamung des Systems zu vermeiden.

**Beispiel**

```auto
let data = metadata.all(object, /^acmf_/);

// Filtern nach Metadaten
// Sie können auch mehrere Filter angeben,
// deren Daten dann gesammelt zurückgegeben werden:
let dataMulti = metadata.all(object, /^acmf_/, 'identifier', '~', '~~', ...);
```

```auto
// Laden der direkten und vererbten Metadaten
metadata.load(object, '~', '~~')
```

#### merge

**Ab welcher Version verfügbar?**

• *agorum core* 9.0.0

Lädt die Metadaten des Objekts selbst als auch Werte, die nur darauf vererbt wurden.

* Existiert für einen Schlüssel mehr als ein Wert, so wird nur der erste Wert geladen.
* Die Funktion bildet das Verhalten der load-Methode der älteren filingassistant/metadata-Bibliothek ab.

**Beispiel**

```auto
// Kundeninfos der zu document gehörigen Akte abrufen
let kunde = metadata().merge(document, /^acmf_kunde/).data();
```

#### save

Schreibt Metadaten auf ein Objekt.

**Beispiel**

```auto
let data = {
  name: 'Name xy',
  acmf_kundenName: 'Name AG'
};

// einzelnes Objekt
metadata(data).save(object [,filter1 [, filter2][,..]]]);
// filter siehe unten

// mehrere Objekte
let m = metadata(data);

objects.forEach(object => m.save(object));
```

**Beispiel zum Entfernen von Metadaten**

```auto
let data = {
  name: null, // metadata "name" wird vom Objekt entfernt
  acmf_kundenName: '' // metadata "acmf_kundenName" bleibt erhalten und hat den Wert ''
};

metadata(data).save(object);
```

### Vorhandene filter bei load, save und merge

* * *

Die folgenden Filter können Sie bei *load*, *save* und *merge* übergeben.

* Mit den Filtern können Sie gezielt bestimmte Metadaten wählen.
* Die Filter beziehen sich immer auf den Namen des Metadatums, nicht auf den Inhalt.
* Allgemein können Sie beliebig viele Filter übergeben. Alle unten beschriebenen Möglichkeiten können Sie beliebig mischen.

#### Filtermöglichkeiten

**Möglichkeit 1**

Ein Filter kann der Name eines Metadatums sein:

```auto
// ausgewählte Metadaten

let some = metadata().load(object, 'name', 'acmf_kundenName').data();
```

In diesem Beispiel wird nur das Metadatum *name* und *acmf\_kundenName* geladen.

**Möglichkeit 2**

Ein Filter kann ein regulärer Ausdruck sein:

```auto
// ausgewählte Metadaten

let some = metadata().load(object, /^acmf_kunde/).data();
```

In diesem Beispiel werden alle Metadaten geladen, die mit *acmf\_kunde* beginnen.

**Möglichkeit 3**

**Ab welcher Version verfügbar?**

• *agorum core* 9.0.2

Ein Filter kann ein '~' sein. Diese Schreibweise definiert Metadaten, die nicht vererbt werden:

```auto
// ausgewählte Metadaten

let some = metadata().load(object, '~').data();
```

In diesem Beispiel werden alle Metadaten geladen, die nicht vererbt werden.

**Möglichkeit 4**

**Ab welcher Version verfügbar?**

• *agorum core* 9.0.2

Ein Filter kann ein '~~' sein. Diese Schreibweise definiert Metadaten, die vererbt werden:

```auto
// ausgewählte Metadaten

let some = metadata().load(object, '~~').data();
```

In diesem Beispiel werden alle Metadaten geladen, die vererbt werden.

#### Beispiele mit Filter

```auto
// ausgewählte Metadaten

let some = metadata().load(object, 'name', 'description', '~', '~~').data();
```

Hier werden alle (vererbte und nicht vererbte) Metadaten geladen.

Ferner werden die Attribute *name* und *description* des Objekts geladen.

#### Benutzer-Metadaten

Bestimmte Benutzer-Metadaten, etwa *user\_ag\_tags,* kann nur der jeweilige Benutzer setzen oder lesen.

Hierbei ist die Session des Benutzers entscheidend, für welchen Benutzer dieses Metadatum gesetzt wird:

```auto
/* global sc */
let objects = require('common/objects');
let metadata = require('common/metadata');

// holen eines agorum core Objektes
let obj = objectsUser.find('ID-des-Objektes');

metadata({
  user_ag_tags: ['Test'],
}).save(obj);
```

In dem obigen Beispiel wird *Test* als User-Tag auf das Objekt gesetzt. Dabei ist entscheidend, mit welchem Benutzer die Session (sc) verbunden ist.

Im folgenden Beispiel wird demonstriert, wie mit einer Admin-Session ein Benutzer-Metadatum für einen anderen Benutzer gesetzt werden kann:

```auto
/* global sc */
let objects = require('common/objects');
let metadata = require('common/metadata');

// session als user holen
let scUser = sc.asUser(objects.find('user:demo'));

// objects library als mit user-session initialisieren
let objectsUser = objects(scUser);

// Objekt mit der objects lib des Users holen
let obj = objectsUser.find('ID-des-Objektes');

// metadaten auf die mail setze, die zuvor über objectsUser geholt wurde.
metadata({
  user_ag_tags: ['Test'],
}).save(obj);
```

## JavaScript-Bibliothek common/metadata collection

**Ab welcher Version nutzbar?**

• *agorum core* 10.0.2

Diese Bibliothek bietet Funktionen zum Abrufen von [metadata collections](#) und zum Aufbauen von Masken oder Filtern

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let metadataCollection = require('common/metadata-collection');

let definition = metadataCollection.get('mu_ohne_migration_vertrag', 'docform');
```

### Funktionen

* * *

#### usages

Liefert alle im System verwendeten *usages* als Array.

**Beispiel**

```auto
let metadataCollection = require('common/metadata-collection');

let usages = metadataCollection.usages();
```

**Beispiel der Rückgabe**

```auto
[ 'acic', 'form', 'docform' ]
```

#### get

Liefert die Items der [metadata collection](#) zurück inklusive weiterer Angaben für den Verwendungszweck, sofern Sie einen *usage* angegeben haben.

**Beispiel mit der Angabe des usages „docform“**

```auto
let metadataCollection = require('common/metadata-collection');

// ohne definitionName (Name der Kollektion) oder usage (Verwendungszweck) erhalten Sie alle Kollektionen zurück
// Aufbau: metadataCollection.get([ definitionName ], [ usage ]);
let definition = metadataCollection.get('mu_ohne_migration_vertrag', 'docform');

definition;
```

**Beispiel der Rückgabe**

Sie erhalten die Items der [metadata collection](#) *mu\_ohne\_migration\_vertrag* für den usage *docform*.

Die Angabe *extractor* (fett markiert) gilt nur für *docform*.

```auto
{
  "displayName" : "Vertrag",
  "usage": [ 'acic', 'docform' ],
  "items" : [ {
    "displayName" : "Anlegedatum",
    "defaultValue" : null,
    "descriptionLong" : null,
    "format" : null,
    "inheritance" : "NOT_INHERITED",
    "description" : null,
    "extractor" : "date",
    "readOnly" : false,
    "optional" : false,
    "type" : "date",
    "mappedName" : "~mu_ohne_migration_createDate:date",
    "multi" : false,
    "displayType" : "default",
    "restricted" : false,
    "name" : "mu_ohne_migration_createDate",
    "verificationRegex" : null,
    "verificationType" : "none",
    "verificationFailText" : null,
    "dataSource" : null
  }, {
    "displayName" : "Vertragsnummer",
    "defaultValue" : null,
    "descriptionLong" : null,
    "format" : null,
    "inheritance" : "NOT_INHERITED",
    "description" : null,
    "extractor" : "string",
    "readOnly" : false,
    "optional" : false,
    "type" : "string",
    "mappedName" : "~mu_ohne_migration_vertragsnummer:string",
    "multi" : false,
    "displayType" : "default",
    "restricted" : false,
    "name" : "mu_ohne_migration_vertragsnummer",
    "verificationRegex" : null,
    "verificationType" : "none",
    "verificationFailText" : null,
    "dataSource" : null
  } ]
}
```

**Beispiel ohne usage**

```auto
let metadataCollection = require('common/metadata-collection');

// ohne definitionName (Name der Kollektion) oder usage (Verwendungszweck) werden alle Kollektionen zurückgeliefert
// Aufbau: metadataCollection.get([ definitionName ], [ usage ]);
let definition = metadataCollection.get('mu_ohne_migration_vertrag', '');

definition;
```

**Beispiel der Rückgabe**

Sie erhalten die Items der [metadata collection](#) *mu\_ohne\_migration\_vertrag*, im Vergleich zur [Angabe des usages „docform“](#usageDocform) dieses Mal ohne spezielle Angaben für den Verwendungszweck.

Die für *docform* gültige Angabe *extractor* fehlt jetzt:

```auto
{
  "displayName" : "Vertrag",
  "usage": [ 'acic', 'docform' ],
  "items" : [ {
    "displayName" : "Anlegedatum",
    "defaultValue" : null,
    "descriptionLong" : null,
    "format" : null,
    "inheritance" : "NOT_INHERITED",
    "description" : null,
    "readOnly" : false,
    "optional" : false,
    "type" : "date",
    "mappedName" : "~mu_ohne_migration_createDate:date",
    "multi" : false,
    "displayType" : "default",
    "restricted" : false,
    "name" : "mu_ohne_migration_createDate",
    "verificationRegex" : null,
    "verificationType" : "none",
    "verificationFailText" : null,
    "dataSource" : null
  }, {
    "displayName" : "Vertragsnummer",
    "defaultValue" : null,
    "descriptionLong" : null,
    "format" : null,
    "inheritance" : "NOT_INHERITED",
    "description" : null,
    "readOnly" : false,
    "optional" : false,
    "type" : "string",
    "mappedName" : "~mu_ohne_migration_vertragsnummer:string",
    "multi" : false,
    "displayType" : "default",
    "restricted" : false,
    "name" : "mu_ohne_migration_vertragsnummer",
    "verificationRegex" : null,
    "verificationType" : "none",
    "verificationFailText" : null,
    "dataSource" : null
  } ]
}
```

**Beispiel ohne Angabe einer metadata collection und ohne usage**

```auto
let metadataCollection = require('common/metadata-collection');

// ohne definitionName (Name der Kollektion) oder usage (Verwendungszweck) werden alle Kollektionen zurückgeliefert
// Aufbau: metadataCollection.get([ definitionName ], [ usage ]);
let definition = metadataCollection.get('', '');

definition;
```

**Beispiel der Rückgabe**

Sie erhalten alle vorhandenen [metadata collections](#) inklusive Items.

```auto
{
  "mu_ohne_migration_vertrag" : {
    "displayName" : "Vertrag",
    "usage": [ 'acic', 'docform' ],
    "items" : [ {
      "displayName" : "Anlegedatum",
      "defaultValue" : null,
      "descriptionLong" : null,
      "format" : null,
      "inheritance" : "NOT_INHERITED",
      "description" : null,
      "readOnly" : false,
      "optional" : false,
      "type" : "date",
      "mappedName" : "~mu_ohne_migration_createDate:date",
      "multi" : false,
      "displayType" : "default",
      "restricted" : false,
      "name" : "mu_ohne_migration_createDate",
      "verificationRegex" : null,
      "verificationType" : "none",
      "verificationFailText" : null,
      "dataSource" : null
    }, {
      "displayName" : "Vertragsnummer",
      "defaultValue" : null,
      "descriptionLong" : null,
      "format" : null,
      "inheritance" : "NOT_INHERITED",
      "description" : null,
      "readOnly" : false,
      "optional" : false,
      "type" : "string",
      "mappedName" : "~mu_ohne_migration_vertragsnummer:string",
      "multi" : false,
      "displayType" : "default",
      "restricted" : false,
      "name" : "mu_ohne_migration_vertragsnummer",
      "verificationRegex" : null,
      "verificationType" : "none",
      "verificationFailText" : null,
      "dataSource" : null
    } ]
  }
}
```

## JavaScript-Bibliothek common-MetaDb

**Ab welcher Version verfügbar?**

• *agorum core* 8.3.1

Diese Bibliothek bietet Funktionen zum Schreiben / Lesen von Werten aus / in die MetaDb.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let metadb = require('common/metadb');
```

### Funktionen

* * *

#### read

Liest einen Bereich (Gruppe, Bundle oder Entry) aus der MetaDb aus.

* Das System gibt die Bereiche rekursiv mit allen Bundles und Entrys aus.

* Ein Slash (/) am Ende des Pfads spielt keine Rolle.
* Das System kann den Pfad sowohl mit als auch ohne Gruppenname lesen.
* Sie erhalten als Ergebnis eine JSON-Struktur mit dem unveränderten Aufbau der Struktur.

| Pfad zeig auf … | Beschreibung |
| --- | --- |
| Entry | Rückgabe ist immer ein Array mit Werten. |
| Bundle | Rückgabe sind alle Bundles und Entrys, die darin enthalten sind, in Form einer Map. Ist der value ein Entry: key: \[ Array von values \] Ist der value ein Bundle: key: { bundle:{...} } |
| Gruppe | Rückgabe ist wie bei Bundle (Bundles und Entries gemischt). Wenn der Pfad nicht existiert oder der Entry leer ist, liefert das System ein leeres Objekt. Das System liefert die Daten „roh“, so wie sie in der MetaDb gespeichert sind. |

**Beispiel**

***Aufbau der MetaDb***

MAIN\_MODULE\_MANAGEMENT/aguila/\[ Gruppe1 \]/\[ Gruppe2 \]/test\_bundle:

* Bundle: test\_bundle2
    *   Entry: entry-B1
    *   Entry: entry-B2
* Entry: entry-A1

***Aufruf***

```auto
metadb.read( 'MAIN_MODULE_MANAGEMENT/aguila/[ Gruppe1 ]/[ Gruppe2 ]/ test_bundle/test_bundle2');
```

```auto
metadb.read('MAIN_MODULE_MANAGEMENT/aguila/[ Gruppe1 ]/test_bundle');
```

```auto
metadb.read('MAIN_MODULE_MANAGEMENT/aguila/test_bundle/');
```

***Ergebnis für alle Aufrufe***

```auto
{
  "test_bundle2" : {
    "entry-B1" : [ "content-B1" ],
    "entry-B2" : [ "content-B2" ]
  },
  "entry-A1" : [ "test_content_string3" ]
}
```

#### write

Übergibt einen Pfad in der MetaDb und einen zu erzeugenden Wert.

* Falls der Pfad bisher nicht vorhanden ist, erstellt das System ihn und legt den Entry an.
* Wenn der Entry bereits vorhanden ist, aktualisiert das System ihn mit dem neuen Wert.
* Rückgabewerte existieren nicht. Im Fehlerfall wirft das Systemeine Exception mit ausführlicher Beschreibung.

#### writeEncrypted()

**Ab welcher Version verfügbar?**

• *agorum core* 9.1.4

Speichert den Entry verschlüsselt ab.

* Encrypted wird nur schreibend unterstützt.
* Sinnvoll bei Passwörtern

**Beispiele**

***Normalen Entry mit Wert anlegen***

```auto
metadb.write('MAIN_MODULE_MANAGEMENT/aguila/control/widgets/[ Group ]/bundle/entry', 'Wert in der MetaDb'); // STRING
```

***Entrys mit mehreren Werten (Array) anlegen***

```auto
metadb.write('MAIN_MODULE_MANAGEMENT/aguila/control/widgets/[ group ]/bundle' + '/entryAsArray', [ '123', 'ABC', 'next']); // STRING_ARRAY
```

***JSON-Struktur übergeben***

Wenn Sie eine JSON-Struktur übergeben, legt das System nicht nur einen einzelnen Entry an, sondern die komplette Struktur (mit Bundles und Gruppen):

```auto
let json = {
  "[ TestGroup ]": {
    "bundleName": {
      Entry1: 'content1',
      Entry2: 'content2',
    }
  }
};
// Aufruf
metadb.write('MAIN_MODULE_MANAGEMENT/aguila/control/widgets', json);
```

***Entry oder Bundle löschen***

Wenn Sie ein Entry oder komplettes Bundle löschen möchten, übergeben Sie der Funktion *write* als *entryValue* den Wert *null*.

Im folgenden Beispiel existiert das Bundle *ac.testWidget*. Das System löscht das darin enthaltene Entry *script*:

```auto
metadb.write('MAIN_MODULE_MANAGEMENT/aguila/control/widgets/[ acGroup ]/ac.testWidget/script', null);
```

***Datentypen***

Die Funktion erkennt den Datentyp automatisch. Unterschieden wird zwischen:

* String
* Arrays, die nur Strings enthalten
* Content
* JSON

Typen wie boolean oder Zahlen (int, double) sind nicht erlaubt. Sie müssen sie vor dem Schreiben in einen String formatieren, damit der Benutzer beim Lesen und Schreiben den gewünschten Typ erhält.

* Schreiben Sie Arrays mit einem Element als normalen String, da dies eine Speicheroptimierung bedeutet.
* Die Bibliothek entscheidet selbstständig anhand der Länge eines Inhalts, ob der String als Content oder normaler String abgespeichert wird.

**Gruppen**

**Ab welcher Version verfügbar?**

• *agorum core* 9.0.1

Das Anlegen von Entrys direkt in Gruppen ist möglich.

***Ältere Versionen***

Bevor Sie ein Entry schreiben können, muss auf eine Gruppe immer erst ein Bundle folgen.

Aufbau des Pfads:

```auto
MAIN_MODULE_MANAGEMENT / + opt. GruppeName / + BundleNamen / + EntryName
```

**Hinweis**: Die Werte erlauben ausschließlich Strings als Datentyp, da die MetaDb ausschließlich Strings speichern kann. Werte, die etwa boolean oder integer sind, müssen Sie in das gewünschte Format umwandeln.

Anstelle eines Strings können Sie ein Array übergeben, vorausgesetzt, die darunterliegenden Elemente sind ebenfalls ausschließlich Strings.

#### inc

Liest einen übergebenen MetaDB-Entry aus, erhöht dessen Zahl um 1 und speichert sie wieder zurück.

* Das System führt diese Aktion in einer einzigen Transaktion durch.
* Die Aktion ist per lock vor gleichzeitigen Zugriffen geschützt.
* Wenn ein gleichzeitiger Zugriff stattfindet, wartet einer der Zugriffe, bis der erste Zugriff seine Zahl gesichert und wieder freigegeben hat.
* Wenn der Entry nicht vorhanden ist, legt das System ihn an und initialisiert ihn mit 1.

**Beispiel**

```auto
metadb.inc('MAIN_MODULE_MANAGEMENT/aguila/control/widgets/myCounterEntry');

// Rückgabe initial 1
```

**Parameter „defaultValue“**

**Ab welcher Version verfügbar?**

• *agorum core* 9.0

Definiert den Startwert.

* Das System beginnt anstatt mit einer 0 mit der definierten Zahl.
* Sie können so etwa Nummernkreise definieren.

***Beispiel***

```auto
metadb.inc('MAIN_MODULE_MANAGEMENT/aguila/control/widgets/myCounterEntry', 10000);

// Rückgabe initial 10001
```

### Rohdaten auslesen

* * *

**Ab welcher Version verfügbar?**• *agorum core* 9.0

#### listGroupsRaw**,** listBundlesRaw und listEntriesRaw

Liefert ein Array mit allen Gruppen (als Objekt) in diesem Pfad.

* Das System liest ausschließlich die angefragte Ebene aus.
* Übergebener Parameter ist der Pfad in der MetaDb.

**Beispiel**

Der Bundle *widgets* enthält die Gruppen:

* \[ Standard \]
* \[ Group1 \]

```auto
let data = MetaDb.listGroupsRaw('MAIN_MODULE_MANAGEMENT/aguila/control/widgets/');

data.map(b => b.name);      // Rückgabe [ "[ Standard ]", "[ Group1 ]" ]
data.length;                // Rückgabe: 2
```

#### listAllGroupsRaw

Liest alle Gruppen ab dem übergebenen Pfad rekursiv aus.

* Das System liefert JavaScript-Map.
* Jeder Key repräsentiert den Namen der Gruppe.
* Wenn eine Gruppe weitere Untergruppen besitzt, steht dies im *value* der Map, ansonsten *null*.

**Beispiel**

```auto
metadb.listAllGroupsRaw('MAIN_MODULE_MANAGEMENT/aguila/control/widgets);

/* Rückgabe ist:
{
  "[ Standard ]": null,
  "[ Group1 ]": {
    "[ Group c ]": null,
    "[ Group b ]": null,
    "[ Group a ]": null
  }
}
*/
```

### Verschlüsselte Werte verwenden

* * *

**Ab welcher Version verfügbar?**• *agorum core* 10.0.2

#### decrypt

Entschlüsselt den übergebenen String mit dem MetaDB-Schlüssel des Systems, um etwa Werte zu entschlüsseln, die Sie etwa per [read()](#read) gelesen haben.

**Beispiel**

```auto
let metadb = require('common/metadb');

let secret = metadb.decrypt(metadb.read('MAIN_MODULE_MANAGEMENT/customers/test/secret')[0]);
```

### Werte beim Auslesen konvertieren

* * *

**Ab welcher Version verfügbar?**• *agorum core* 10.0.5

#### readArray

Liest den angegebenen MetaDb-Schlüssel aus und liefert ihn als Array.

Wenn der Schlüssel nicht existiert, liefert das System stattdessen ein leeres Array.

**Beispiel**

```auto
let metadb = require('common/metadb');

metadb.readArray('MAIN_MODULE_MANAGEMENT/my/test/key').join('\n');
```

#### readString

Liest den angegebenen MetaDb-Schlüssel aus und liefert ihn als String.

Wenn der Schlüssel nicht existiert, liefert das System stattdessen *undefined*.

**Beispiel**

```auto
let metadb = require('common/metadb');

metadb.readString('MAIN_MODULE_MANAGEMENT/my/test/key');
```

#### readNumber

Liest den angegebenen MetaDb-Schlüssel aus und liefert ihn als Number.

Wenn der Schlüssel nicht existiert, liefert das System stattdessen *null*.

**Beispiel**

```auto
let metadb = require('common/metadb');

metadb.readNumber('MAIN_MODULE_MANAGEMENT/my/test/key');
```

#### readBoolean

**Ab welcher Version verfügbar?**• *agorum core* 10.0.6

Liest den angegebenen MetaDb-Schlüssel aus und liefert ihn als Boolean.

Das System interpretiert einen String-Wert von *true* als *true*, alles andere (auch ein fehlender Schlüssel) als *false*.

**Beispiel**

```auto
let metadb = require('common/metadb');

metadb.readBoolean('MAIN_MODULE_MANAGEMENT/my/test/key');
```

#### getParameter

**Ab welcher Version verfügbar?**• *agorum core* 10.0.8

Liefert Parameter, die einerseits übergeben (Standardwerte) und andererseits aus der MetaDb geholt werden, wenn diese dort vorhanden sind.

**Beispiel**

```auto
let metadb = require('common/metadb');

// metadb.getParameter(name, parameters, path, fallback, dataType);
metadb.getParameter('parameterName1', {
  parameterName1: 'Wert 1'
}, 'MAIN_MODULE_MANAGEMENT/my/test', 'Wert Fallback', 'string');
```

* Das System prüft im Beispiel zuerst, ob der Wert für *parameterName1* in den übergebenen Parametern vorhanden ist.
* Wenn nicht, prüft das System, ob der Parameter *parameterName1* in der MetaDb unterhalb des Bundles *MAIN\_MODULE\_MANAGEMENT/my/test* existiert.
* Findet das System auch hier keinen Wert, liefert es den Fallback-Wert.
* Das System erwartet als Wert einen String als Datentyp.

Die Datentypen-Angabe wandelt den gelesenen Wert in den gewünschten Datentyp um.

Mögliche Datentypen:

* string
* boolean
* array
* number
* json

Die Funktion können Sie etwa in JavaScript-DataHandlern verwenden, um Parameter entweder in den *dataSourceParameters* mitzugeben oder diese Parameter in einem MetaDb-Schlüssel (dort, wo der DataHandler registriert ist) zu überladen. So können Sie die Standardwerte eines DataHandlers in seiner MetaDb-Konfiguration definieren und das Verhalten eines DataHandlers konfigurieren.

**Beispiel für einen DataHandler, der „getParameters“ verwendet**

```auto
/* global sc, sca, query, parameters, command, path */
let mc = require('/agorum/roi/customers/agorum.metadata.collection/js/metadata-collection');
let i18n = require('common/i18n');
let metaDb = require('common/metadb');

if (command !== 'read') {
  throw new Error('this datahandler only supports read');
}

let result = [];

if (parameters.lookup) {
  if (query) {
    let collection = mc.get(query, metaDb.getParameter('usage', parameters, path));
    if (collection) {
      result.push({
        text: i18n.translate(collection.displayName || query)  + ' (' + query + ')',
        value: query
      });
    }
  }
}
else {
  let collections = mc.get(null, metaDb.getParameter('usage', parameters, path));
  for (let name in collections) {
    let collection = collections[name];
    result.push({
      text: i18n.translate(collection.displayName || name) + ' (' + name + ')',
      value: name
    });
  }

  result = result.filter(entry => {
    return !query || entry.text.toLowerCase().indexOf(query.toLowerCase()) !== -1 || entry.value.toLowerCase().indexOf(query.toLowerCase()) !== -1;
  });

  result = result.sort((a, b) => {
    return a.text.localeCompare(b.text);
  });
}

result;
```

## JavaScript-Bibliothek common/objects

Mit dieser Bibliothek und den enthaltenen Funktionen können Sie Objekte:

* erzeugen
* finden
* analysieren
* modifizieren

### Verwendung

* * *

```auto
let objects = require('common/objects');
```

Der Rückgabewert "Objekt" meint immer den Typ "GlobalObject". Die Dokumentation dazu finden Sie unter [GlobalObject](#).

Im Standard verwendet das System die Sitzung des eingeloggten Benutzers. Eine hiervon abweichende Sitzung können Sie wie in der Dokumentation zu [SessionController(sc)](#) beschrieben verwenden.

### Funktionen

* * *

#### find, tryFind

Diese Funktionen finden Objekte.

**Aufruf**

```auto
objects.find('<id>')
objects.tryFind('<id>')
```

Es werden alle Arten von IDs unterstützt, die auch die agorum API akzeptiert, unter anderem:

* Numerische IDs: `9999`
* UUIDs: `550e8400-e29b-11d4-a716-446655440000`
* Pfade: `/agorum/roi/Files`, `home:MyFiles/Test`, `relative:12345/Sub`
* Namensbasiert: `user:roi`, `group:GRP_Demo, acl:ACL_Demo, pai:AclList`

Der Unterschied zwischen `find()` und `tryFind()` besteht darin, dass Erstere einen Fehler wirft, wenn das Objekt nicht gefunden wird, während Letztere `null` zurück gibt.

**Beispiel**

```auto
// Homeordner des Users und darunter den Ordner MyFiles
let home = objects.find('home:MyFiles');

// Homeordner des Users und darunter den Ordner MyFiles/Test
let homeTest = objects.find('home:MyFiles/Test');

// Object mit der id 9999
let root = objects.find('9999');

// Benutzer roi
let user = objects.find('user:roi');

// PAI holen
let pai = objects.find('pai:AclList');
```

**Ergebnis**

Sie erhalten bei beiden Funktionen ein Objekt vom Typ "GlobalObject" zurück.

#### find mit create

**Ab welcher Version verfügbar?**•  *agorum core 9.2.0*

Sie können beim Holen eines Pfades den Pfad gleich anlegen lassen. Ist der Pfad noch nicht vorhanden, wird dieser angelegt, ansonsten wird er zurückgegeben, wie beim normalen `find` auch.

Zu beachten ist, dass auf diese Weise nur Ordner angelegt werden können, es dürfen beim `find` also auch nur Ordner angegeben sein. Die Berechtigung wird vom übergeordneten Ordner vererbt. Der User ist der User, mit dessen Session der `find`\-Befehl aufgerufen wird.

Bevor Sie diese Funktion nutzen, überlegen Sie sich, in welchem Bereich Sie diesen Ordner anlegen wollen. Ihnen stehen die Benutzerbereiche und der [Root Ordner](#) zur Verfügung.

**Benutzerbereich**

Jeder User in *agorum core* besitzt einen Benutzerbereich. In diesem liegen seine "Eigenen Dateien" oder auch benutzerspezifische Einstellungen, wie Einstellungen des *information centers* oder gesetzte Filter. Sie als Entwickler werden diesen Benutzerbereich vermutlich nie oder kaum nutzen.

So finden Sie den Benutzerbereich:

1. Öffnen Sie auf der Startseite von *agorum core* **Administration** und dann **Root Ordner**.
2. Öffnen Sie den Ordner **Home**.**Ergebnis**: Alle Ordner, die Sie hier sehen, stehen für je einen Benutzer. Die Ordner unterhalb eines Benutzernamens gehören zum Benutzerbereich.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/f4daf640-4739-11ea-aad2-005056aa0ecc)

```auto
OCR: Administration, Alles, Root, Ordner, Benutzer, Gruppen, Rechte, ACLS, MetaDb, Root, Ordner, Serverpapierkorb, Suche, QSuche, von, Root, Root, eingeben, Name, Beschreibung, Betreff, Administration, anorum, Home, acba.admin, acba.user, home, agorum.roi.objects.mailfilter.MyMailFilter, agorum.roi.objects.myrecycling, MyRecycling, Eigene, Dateien, Mail, MyAdmin, tmp, agorumdocproxy, d4wdemo_en, Administration, Admin, Folder, agorum, Home, Root, Folder, ..., Home, Folder, Der, Benutzerbereich, einese, Users, Eigene, Dateien, myFiles, Mails, sollte, agorum, core, als, Mailserver, verwendet, werden, Konfiguraionsspezifische, Ordner
```

Haben Sie etwa eine eigene Oberfläche erstellt, in der Sie Ihren Anwendern ermöglichen, Einstellungen zur Darstellbarkeit vorzunehmen, dann speichern Sie diese in den Benutzerbereich des angemeldeten Users ab. Hierzu können Sie Ordner mit dem folgenden Befehl erstellen:

```auto
let o1 = objects.find('home:Testordner/Unterordner:create');
```

Das Synonym home: steht für den Bereich:

```auto
home/<angemeldeter user> //Im Beispiel des Screenshots: Home/demo
```

Möchten Sie direkt in den "Eigenen Dateien" des angemeldeten Users einen Ordner anlegen, nutzen Sie folgenden Befehl:

```auto
let o2 = objects.find('home:myFiles/Testordner unter Eigene Dateien:create');
```

Der Vorteil bei der Nutzung von home: liegt auf der Hand: Sie müssen nicht den kompletten Pfad zusammenbasteln, sondern können anhand von diesem Kürzel direkt auf den Benutzerbereich des angemeldeten Users zugreifen.

**Root-Ordner**

In einem Root-Ordner liegen alle Dateien / Objekte, einschließlich des Benutzerbereiches, die sich nicht im Serverpapierkorb befinden.

Sie haben hier Zugriff auf den Benutzerbereich sowie den Dateien des Systems, müssen allerdings den kompletten Pfad kennen, in dem Sie Ordner erstellen möchten:

```auto
let o1 = objects.find('relative:9999/Testordner/Unterordner:create');
```

Dieser Befehl erstellt folgende Ordnerstruktur:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/f59fec90-473c-11ea-aad2-005056aa0ecc)

```auto
OCR: Administration, Root, Ordner, Benutzer, Gruppen, Root, Testordner, Root, Administration, Rechte, ACLS, MetaDb, Root, Ordner, Serverpapierkorb, Suche, Suche von agorum, Home, Testordner, Unterordner, Alles
```

Die Option "create" in der Funktion "find" bietet sich immer dann an, wenn Sie mehrere Ordner, also eine Ordnerstruktur, anlegen möchten. Möchten Sie nur einen einzigen Ordner erstellen, können Sie dies auch so umsetzen:

```auto
<parentpath>.createPath("<New Folder>")
```

#### search

**Achtung**: Beeinträchtigung der Systemleistung durch Aufruf. Dieser Aufruf ist nicht für große Ergebnismengen oder Objekte mit Unterobjekten geeignet. Führen Sie ihn nur für einfache Suchanfragen aus. Nutzen Sie für große Ergebnismengen die Funktion [query](#query).

Diese Funktion führt eine einfache Suchanfrage aus, die sowohl Lucene als auch Solr als Back-end unterstützt.

**Aufruf**

```auto
let objArr = objects.search('<query>')
```

**Ergebnis**

Sie erhalten ein Array mit Objekten zurück.

#### query

**Hinweis**: Funktioniert nur mit Solr als Back-end. Achten Sie auf die korrekte [Solr-Syntax](#).

Diese Funktion führt eine erweiterte Suchanfrage aus. Damit verarbeiten Sie durch zusätzliche Möglichkeiten bei Sortierung, Limitierung und Paging auch beliebig große Ergebnismengen. Durch die Verwendung von Objektattributen aus dem Index erzielen Sie zudem eine höhere Performance, da keine Datenbankzugriffe stattfinden müssen. Außerdem sind durch Faceting auch tiefere Analyse- und Statistikmöglichkeiten gegeben.

**Aufruf**

```auto
objects.query('<query>')
```

#### query.find

Diese Funktion fordert ein Lookup der gefundenen Objekte an. Der Aufruf ist fast äquivalent zur Verwendung von [search](#search), mit dem Unterschied, dass Sie mit `query.find()` auch Unterobjekte finden können.

**Aufruf**

```auto
let results = objects.query('name:demo').find();
```

**Ergebnis**

Sie erhalten ein Array mit Objekten zurück und können direkt mit den Objekten arbeiten. Die Funktion arbeitet im Gegensatz zu [search](#search) langsamer, es dauert also länger, bis sie die Objekte zurückerhalten.

```auto
[
  123456,
  123457,
  123458
]
```

#### Mit limit() die Anzahl der zurückgegebenen Ergebnisse beschränken

Erwarten Sie eine größere Menge an Treffern, sollten Sie die Anzahl der zurückgegebenen Ergebnisse mit `limit()` beschränken.

**Aufruf**

```auto
let results = objects.query('*').limit(10).find();
```

**Ergebnis**

Sie erhalten die ersten zehn Treffer zurück.

**Hinweis**: Die Suche mit `search/find` ist auf maximal 10.000 Elemente (limit) beschränkt. Wenn Sie mit einer Suchanfrage mehr Elemente in einem Durchlauf durchsuchen möchten, nutzen Sie `cursor` und / oder `iterate`.

#### Nächste 10 Treffer des Ergebnisses mit start() zurückgeben lassen

Diese Funktion ruft die nächsten zehn Treffer ab.**Aufruf**

```auto
let results = objects.query('*').start(10).limit(10).find();
```

**Ergebnis**

Sie erhalten die Treffer 11–20 zurück.

#### Ergebnismenge mit sort() sortieren

Sie können die Ergebnismenge sortieren. Wenn Sie keine explizite Sortierung durch `sort` angegeben haben, sortiert das System automatisch absteigend nach dem letzten Änderungsdatum der Objekte.

**Aufruf**

```auto
let results = objects.query('*').sort('createdate').limit(10).find();
```

**Ergebnis**

Sie erhalten die zehn ältesten Objekte (nach Erstelldatum aufsteigend) zurück.

#### Suchanfragen mit sort() kombinieren

Sie können mehrere Sortieranfragen kombinieren.

**Aufruf**

```auto
let results = objects.query('*').sort('nameextension', 'contentsize desc').limit(10).find();
```

**Ergebnis**

Sie erhalten die Objekte primär nach der Namenserweiterung aufsteigend und sekundär nach der Dateigröße absteigend zurück.

#### Filter verwenden

Verwenden Sie Teil-Suchanfragen häufiger, ist es möglich, diese in getrennte Filter auszulagern. Dadurch signalisieren Sie der Suchmaschine, dass diese gefilterte Mengen bevorzugt im Cache halten kann.

**Aufruf**

```auto
let results = objects
.query('name:test')
.filter('inpath:9999', 'nameextension:pdf')
.sort('contentsize desc')
.limit(5)
.find();
```

**Ergebnis**

Sie erhalten die fünf größten, noch nicht gelöschten (inpath:9999) PDF-Dokumente zurück, bei denen das Wort "test" im Namen vorkommt. Die Suche nach `name:test` bildet hier die Ausnahme. Benutzen Sie stattdessen `inpath:9999` und `nameextension:pdf`.

#### query.search

Diese Funktion fragt ohne Datenbankabfrage direkt aus dem Index Attribute ab und zeigt Ihnen an, wie viele Treffer die Suche insgesamt hatte.

* Bei *query.search* können Sie im Gegensatz zu [query.find](#query.find) direkt angeben, welche Propertys aus dem Suchindex zurückkommen.
* Wenn keine Propertys angegeben sind, liefert das System alle Propertys zurück. Das System sucht dadurch schneller.

**Aufruf**

```auto
let result = objects.query('isfolder:true').limit(10).search('id', 'name');

'Total: ' + result.total + '\n\n' + result.rows.map(function(row) {
  return row.id + ': ' + row.name;
})
.join('\n');
```

**Ergebnis**

Sei erhalten eine Übersicht über die Gesamtanzahl an Ordnern inklusive IDs und Namen der zehn zuletzt geänderten Ordner zurück.

```auto
{
  "nextCursor": null,
  "total": 3,
  "highlights": null,
  "rows": [
    {
      "name": "demo",
      "id": "6909861"
    },
    {
      "name": "demo-Info Profile",
      "id": "6909862"
    },
    {
      "name": "Demo",
      "id": "6909863"
    }
  ],
  "facetFields": null,
  "facets": null
}
```

#### Ergebnismenge mit limit() unterdrücken

Ist lediglich die Anzahl der Treffer interessant, kann die Ergebnismenge selbst sogar völlig unterdrückt werden:

```auto
let fileCount = objects.query('isfolder:false').limit(0).search().total;
```

Für große Datenmengen sollten Sie nicht mehr `start()` für Paging verwenden, sondern `cursor()`. Hierbei liefert das System bei jedem Suchergebnis ein Cursor für die nächste Anfrage mit. Das hat außerdem den Vorteil, dass auch bei zwischenzeitlichen Veränderungen in der Ergebnismenge, insbesondere bei neuen / entfernten Elementen vor der aktuellen Position, ein konsistentes Paging erreicht wird:

```auto
let result = objects.query('isfolder:true').cursor().limit(500).search('id');

// .. do something with result.rows ..

result = objects.query('isfolder:true').cursor(result.nextCursor).limit(500).search('id');

// .. do something with result.rows ..

// ...
```

#### query.iterate

**Ab welcher Version verfügbar?**

*• agorum core 8.1.3*

Diese Funktion geht alle gefundenen Objekte im System durch und führe für jedes Objekt eine gewünschte Aktion durch.

* Das System verwendet intern einen `cursor` und eine Begrenzung pro Suche.
* iterate verhält sich wie [search](#query.search). Sie können angeben, welche Propertys Sie erhalten.

**Aufruf**

```auto
// iterate over specific fields without retrieving the associated objects
objects.query('isfolder:true').iterate('uuid', 'name', function(row) {
  // .. do something with row.uuid and row.name ..
});
```

#### query.iterate mit limit() verwenden

**Ab welcher Version verfügbar?**

*• agorum core* 10.0.10

Sie können der Funktion "query.iterate" ein limit mitgeben. Dadurch iteriert das System nicht über alle, sondern nur über x Objekte.

**Aufruf**

```auto
//

objects.query('isfolder:true').limit(10).iterate('uuid', 'name', function(row) {
  // .. do something with row.uuid and row.name ..
});
```

**Ergebnis**

Sie erhalten 10 Ordner inklusive der UUID und des Ordnernamens zurück.

#### query.foreach

Diese Funktion durchläuft wie [query.iterate](#query.iterate) alle Objekte, liefert aber ein anderes Ergebnis pro Objekt.

* forEach verhält sich wie [find](#query.find). Es liefert das Objekt zurück.

**Aufruf**

```auto
// visit all matching objects
objects.query('ancestors:mailobject').forEach(function(object) {
  // .. do something with the object ..
});
```

**Ergebnis**

Sie erhalten alle E-Mail-Objekte zurück.

#### Nach verborgenen Objekten mit includeHidden() suchen

Sie können auch nach verborgenen Objekten suchen, die sonst üblicherweise ausgeblendet werden (History-Objekte, Unterobjekte).

**Aufruf**

```auto
objects.query('*').includeHidden(true).limit(0).search().total;
```

**Ergebnis**

Sie erhalten die gesamte Anzahl an indizierten Objekten im System zurück.

#### Ergebnismenge analysieren

Um die Ergebnismenge weiter zu analysieren, werden zwei Verfahren unterstützt:

* [Feldbasiertes Faceting](#feldbasiertesFaceting)
* [Erweitertes Faceting/Analyse](#erweitertesFaceting)

Bei Letzterem bezieht sich die Analyse in jedem Fall auf die im Suchergebnis enthaltenen Objekte. Möchten Sie alle Objekte analysieren, suchen Sie nach `*` .

**Feldbasiertes Faceting**

Feldbasiertes Faceting ermöglicht auf einfache Weise, Wertemengen für bestimmte Felder zu erzeugen.

```auto
objects
.query('area:Kundenakte ac_customernumber:12345')
.facetFields('nameextension', 'ac_ticketstate')
.facetLimit(3)
.facetSort('count')
.limit(0)
.search()
.facetFields;
```

Hier wird innerhalb einer bestimmten Kundenakte nach vorhandenen Dateitypen und verwendeten Ticketstatus gesucht (die eigentlichen Suchtreffer sind nicht relevant, daher auf 0 limitiert). Das Ergebnis hat folgende Form:

```auto
{
  nameextension: {
    pdf: 12345,
    eml: 5432,
    html: 123
  },
  ac_ticketstate: {
    closed: 123,
    waiting: 12,
    open: 1
  }
}
```

Die Wertemengen wurden nach Vorkommen (count) sortiert und auf drei Werte beschränkt.

Wenn die Suchergebnisse selbst nicht unterdrückt werden, lässt sich damit etwa einfach eine Verfeinerung von Suchergebnissen ermöglichen, indem Sie einen oder mehrere der zurückgegebenen Werte vom Benutzer als Filter auswählen und auf dieser Basis eine neue Suche starten.

**Vorhandene Methoden und ihre Parameter**

| Methode | Parameter | Beschreibung |
| --- | --- | --- |
| facetFields | <field>, ... | Felder, die berücksichtigt werden sollen. default keine |
| facetMinCount | <count> | Mindestanzahl an Stellen, an denen ein Wert vorkommen muss, um berücksichtigt zu werden. Achtung: Unbeabsichtigte Einsicht durch Angabe 0.Es werden Feldwerte ausgegeben, die laut ACL für den aktuellen Benutzer nicht sichtbar wären. Tragen Sie einen positiven Wert ein. default 1 |
| facetLimit | <limit> | Maximale Anzahl an Werten pro Feld, die zurückgegeben werden sollen. default 100 |
| facetMissing | true/false | Zusätzlicher Pseudo-Wert (leerer String), der die Stellen zählt, an denen das Feld keinen Wert hatte. default false |
| facetSort | <order> | Sortierung der Werte, entweder count oder index. • default count: Vorkommen index: Alphabetisch |

**Erweitertes Faceting/Analyse**

**Hinweis**: Diese Beschreibung ist gekürzt und umfasst nicht alles.

Über erweitertes Faceting wird sowohl die Funktionalität des einfachen Faceting (Wertemengen) abgedeckt als auch zusätzliche Analyse- und Aggregierungsfunktionalität:

```auto
objects
.query('*')
.limit(0)
.facets({
  mails: {
    type: 'query',
    q: 'ancestors:mailobject'
  },
  mail_content: {
    type: 'query',
    q: 'ancestors:(mailobject OR maildocumentobject)',
    facet: {
      sum_size: 'sum(contentsize)'
    }
  },
  extensions: {
    type: 'terms',
    field: 'nameextension',
    minCount: 10
  },
  content: {
    type: 'terms',
    field: 'classname',
    facet: {
      sum_size: 'sum(contentsize)'
    },
    sort: {
      sum_size: 'desc'
    },
    limit: 99999
  }
})
.search()
.facets;
```

Dieses Beispiel ermittelt folgende Informationen über alle für den aktuellen Benutzer sichtbaren Objekte (`*`):

* Anzahl der Objekte, die auf die Suche `ancestors:mailobject` passen (Anzahl Mails)
* Anzahl der Objekte, die auf die Suche `ancestors:(mailobject OR maildocumentobject)` passen (Anzahl Mails und Mail-Teile)
    *   Aufsummierte Größe dieser Objekte in Bytes
* Unterschiedliche Werte des Felds `classname` (Alle vorkommenden Objektklassen)
    *   je Objektklasse aufsummierte Größe der zugehörigen Objekte in Bytes
    *   je Objektklasse Anzahl der zugehörigen Objekte (vgl. einfaches Faceting)
    *   Sortierung absteigend nach Anzahl
    *   Maximal 99999 Objektklassen

#### Suchtreffer hervorheben ("Highlighting")

**Ab welcher Version verfügbar?**• *agorum core 9.1.2*

Sie können die Suchmaschine ebenfalls dazu verwenden, um im Dokumentinhalt oder in Metadaten hervorzuheben, an welcher Stelle der Suchtreffer aufgetreten ist.

```auto
objects
.query('test')
.highlights({
  limit: 5
})
.limit(10)
.search('uuid', 'name');
```

Das Suchergebnis enthält nun neben UUID und Name der passenden Objekte auch die Treffer innerhalb des Inhalts der jeweiligen Objekte im Abschnitt "highlights", unterhalb der UUID des jeweiligen Objekts.

**Parameter**

| Parameter | Beschreibung | Default |
| --- | --- | --- |
| field | Wählt das Index-Feld aus, in dem nach Treffern gesucht werden soll. | 'contentonly' |
| limit | Legt fest, wie viele Treffer pro Objekt maximal zurückgegeben werden sollen. | 100 |
| pre | Definiert die Zeichenfolge, die vor jedem Treffer eingefügt wird. | '\[' |
| post | Definiert die Zeichenfolge, die nach jedem Treffer eingefügt wird | '\]' |
| query | Ab welcher Version verfügbar? • agorum core 9.2.0 Gibt eine von der Suche unabhängige query für das Highlighting mit. | keine |
| allFields | Ab welcher Version verfügbar? • agorum core 9.2.1 true Nimmt das Highlighting in allen Feldern vor. false Nimmt das Highlighting nur in den Feldern vor, in denen das jeweilige Wort gefunden wurde. | false |
| context | Ab welcher Version verfügbar? • agorum core 9.2.1 Definiert, wie viele Zeichen um einen Treffer herum zurückgeliefert werden sollen. (Ungefähre Angabe, auch die Worte an sich werden als Ganzes in Betracht gezogen.) | 100 |

#### create, tryCreate

Mit diesen Funktionen erzeugen Sie neue Objekte einer definierten Klasse mit initialen Attributen. Die Funktion "tryCreate()" prüft zudem, ob das zu erzeugende Objekt bereits vorhanden ist und liefert es in diesem Fall zurück. Die Attribute eines bereits existierenden Objekts werden dabei nicht verändert.

```auto
objects.create('<class>', data)
objects.tryCreate('<class>', data)
```

Es folgt ein Überblick über die unterstützten Werte für `class` und `data`.

**Alle Klassen**

Für alle Klassen wird das Attribut `target` unterstützt, das im Fall von Notizen das zugehörige Hauptobjekt und im Fall der anderen Klassen den Zielordner bestimmt. Für alle Klassen außer Notizen existiert zusätzlich ein optionales Attribut `path`, das einen Pfad unterhalb von target definiert, in den das Objekt abgelegt werden soll. Dieser Pfad wird bei Bedarf angelegt.

**Hinweis**: Sie können Ordner durch den Befehl nicht erstellen, siehe Abschnitt [find mit create](#find mit create).

**Tipp**: Für Benutzer, Gruppen und ACLs verwenden Sie üblicherweise kein `target`, sondern nur einen relativer `path` unter dem jeweiligen Wurzelordner für die Objektklasse.

#### file

Mit `file` erzeugen Sie eine Datei. Die Angabe von `target` oder `path` ist notwendig. Der Offset-Wert von path, wenn dieser ohne '/' beginnt, ist `/agorum/roi/Files`:

```auto
let file = objects.create('file', {
  name: 'test.txt',
  description: 'Eine Textdatei',
  target: target,
  path: 'Ordner 1/Ordner 2'
});
```

Dieser Aufruf legt eine leere Textdatei im Ordner `/agorum/roi/Files/Ordner 1/Ordner 2` an. Wenn dieser Dateiname im Zielordner schon belegt ist, hängt das System automatisch ein numerisches Suffix an.

Weitere Parameter:

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| target | <Object> | •  target let target = objects.find('/agorum/roi/Files'); •  target darf kein String sein. |
| content | <stream> | • content: object.contentStream • Hier wird aus einer vorhandenen Datei der Content gestreamt. |
| path | Relative Angabe: • Wird an target angehängt. • Falls die Ordnerstruktur nicht existiert, wird diese erstellt. Absolute Angabe: • Wird nicht an target angehängt. • target wird ignoriert, es wird nur path benutzt. • Falls die Ordnerstruktur nicht existiert, wird diese erstellt. | Relative Angabe: • <target>/<path>: 'Ordner 1/Ordner 2' Absolute Angabe: •  <path>: '/agorum/roi/Files/Demo/x/y' |

**Hinweise**:• In `path` können Sie keine Platzhalter wie z. B. ${date:yy/MM/dd} nutzen.• `path` kann nicht mit einem agorum Object umgehen. Es wird zudem ein String erwartet.

Sie können Content auch setzen, wenn das Objekt angelegt ist. Hier können Sie auch einen String setzen:

`file.contentString = 'hhhh';`

#### folder (createPath)

Das ist ein Sonderfall, der hier dokumentiert wird, aber momentan noch keine Methode von "objects" ist.

Um einen "Ordner" anzulegen, benötigen Sie ein Ordner-Objekt. Auf diesem Ordner-Objekt können Sie jetzt direkt die Methode "createPath(path)" aufrufen.

**Beispiel**Sie wollen direkt unter "/agorum/roi/Files" einen neuen Ordner oder eine Ordnerstruktur anlegen. Dann können Sie das so umsetzen:

```auto
let files = objects.find('/agorum/roi/Files');

// Jetzt wollen Sie darunter einen Ordner "Beispiele" anlegen
let beispiele = files.createPath('Beispiele');

// Es wird der Ordner "Beispiele" zurückgegeben

// Jetzt wollen Sie noch einen Pfad anlegen
let pdf = files.createPath('Archive01/Dokumente/Ablage/PDF');

// Es wird der letzte Ordner zurückgegeben
```

**Hinweis**: Wenn der Pfad bereits existiert, wird der vorhandene Pfad zurückgegeben.**Beispiel**Wenn es den Pfad "agorum/roi/Files/Archive01/Dokumente/Ablage/PDF" schon gibt, wird der Ordner "PDF" zurückgegeben.

**Beispiel templates.fill mit createPath zum Erstellen einer Ordnerstruktur nach einem Datum**

Hier noch ein [Beispiel](#) in Kombination mit `templates.fill` und einem Datum.

#### pai (ParameterAccessIdentifier)

**Ab welcher Version verfügbar?**• *agorum core 9.0*

Mit `pai` erzeugen Sie einen ParameterAccessIdentifier (PAI). Diesen können Sie zur Steuerung von Oberflächenfunktionen nutzen.

```auto
let pai = objects.tryCreate('pai', {
  name: 'Test_1',
  acl: 'Published'
});
```

Dieser Aufruf legt einen neuen PAI mit dem Namen *Test\_1* an. Ist dieser bereits vorhanden, so wird dieser lediglich zurückgegeben (wegen dem Aufruf mit tryCreate).

Weitere Parameter:

| Parameter | Beschreibung |
| --- | --- |
| name | Name des PAI Legt standardmäßig immer ein ACL mit dem Namen "ACL\_PAI\_\[Name-des-PAI\]\_" an, etwa "ACL\_PAI\_Test\_1\_". |
| acl (optional) | Übergibt ein existierendes ACL. Gruppen / Benutzer des ACLs werden mit denselben Rechten in das PAI übertragen. Geben Sie kein ACL an, erhält das zu erstellende PAI keinen Eintrag. |

**Hinweis**: Möchten Sie, dass die Sichtbarkeit der Module auf der Startseite auch für den Administrator gilt, müssen Sie hierzu den PAI im desk4web bearbeiten und den Parameter "ACL gilt auch für Administratoren**"** setzen.

#### user

Mit `user` legen Sie einen Benutzer an, optional mit Bild:

```auto
// Legt Benutzer an
let user = objects.create('user', {
  name: 'testuser',
  password: 'testpass',
  path: 'Testbenutzer',
  admin: false,
  givenName: 'Test',
  familyName: 'User',
  language: 'de',
  emailAddresses: [ 'testuser@agorum.com' ]
});

//Legt ein Bild zum Benutzer an (optional)
let image = user.getProfilePicture();

// Wenn noch kein Bild vorhanden, dann anlegen
if (!image) {
  let home = user.primaryUserProfile.homeFolder;

  image = objects.create('file', {
    name: 'picture.png',
    target: home
  });

  user.setProfilePicture(image, true);
  image = user.getProfilePicture();

  // Das Bild in den Benutzer laden
  objects.find('/agorum/roi/Files/irgeneinbild.png').streamContent(image);
}

```

#### group

Mit `group` legen Sie eine Gruppe an:

```auto
let group = objects.create('group', {
  name: 'GRP_Buchhaltung',
  path: 'Testfirma',
  members: [ 'user:user1', user ]
});
```

Die neu angelegte Gruppe enthält zwei Benutzer:

* den per ID referenzierten user1,
* den neu angelegten Benutzer (user) aus dem vorherigen Beispiel, der als Objektreferenz übergeben wurde.

Wenn Sie einen *path* angeben:

* überprüft die Funktion, ob der Pfad bereits existiert und legt ihn an, wenn er nicht existiert
* verwenden Sie nicht die Funktion *get require(...)* im *agorum core template manager,* da das System die Benutzergruppe sonst im falschen Ordner anlegt. Verweisen Sie stattdessen direkt auf die Ordnerstruktur unter dem Benutzergruppen-Ordner. Aus der folgenden Abbildung wäre das etwa:

```auto
path: 'academy.workflow/Beispiele/Neuer Ordner'
```

**Weitere Member zur Gruppe hinzufügen**

Mit folgendem Code fügen Sie nachträglich weitere Members zur Gruppe hinzu:

```auto
let members = [
  'group:Gruppenname1',
  'user:Username1'
];

// es werden lediglich Gruppen oder User hinzugefügt, die auch vorhanden sind
function addMembersToGroup(group, members) {
  group.addMembers(members.map(member => objects.tryFind(member)).filter(m => m));​​​​​
}
```

**Member aus einer Gruppe erweitern**

Wenn Sie die Members einer Gruppe erweitern möchten, müssen Sie sicherstellen, dass das System weiß, dass es sich um eine Gruppe handelt:

```auto
let singlegroup = "GRP_Musterfirma Group GmbH";
let members = [

  'group:GRP_INFOS UND WISSEN',
  'group:GRP_KUNDEN',
  'group:GRP_MARKETING',
  'group:GRP_PERSONAL',
];

addMembersToGroup(objects.tryFind('group:' + singlegroup), members);

// es werden lediglich Gruppen oder User hinzugefügt, die auch vorhanden sind
function addMembersToGroup(group, members) {
   group.addMembers(members.map(member => objects.tryFind(member)).filter(m => m));
}
```

**Member aus einer Gruppe entfernen**

Mit folgenden Code entfernen Sie die Members aus einer Gruppe:

```auto
let members = [
  'group:Gruppenname1',
  'user:Username1'
];

// es werden lediglich Gruppen oder User entfernt, die auch vorhanden sind
group.removeMembers(members.map(member => objects.tryFind(member)).filter(m => m));
```

**Member aus einer Gruppe auslesen**

Mit folgenden Befehlen lesen Sie die Mitglieder aus einer Benutzergruppe aus:

| Befehl | Beschreibung |
| --- | --- |
| directUserMembers | Liest alle Benutzer aus einer Gruppe aus, die direkt in dieser enthalten sind. |
| allUserMembers | Liest alle Benutzer aus einer Gruppe und deren enthaltenen Untergruppen aus. |
| directMembers | Gibt alle Benutzer und Benutzergruppen einer Gruppe zurück, die direkt in dieser enthalten sind. |
| allMembers | Gibt alle Benutzer und Benutzergruppen einer Gruppe und deren enthaltenen Untergruppen zurück. |

**Beispiel**

```auto
objects.find('group:<Name der Gruppe, z.B. GRP_wf_allgemein_beobachter>').directUserMembers.map(user => user.UUID);
```

#### acl

Mit `acl` legen Sie ein ACL an:

```auto
let acl = objects.create('acl', {
  name: 'ACL_Kundenakten',
  path: 'Testfirma',
  entries: [
    {
      entity: 'group:GRP_Verwaltung',
      access: 'write'
    },
    {
      entity: group,
      access: 'read'
    },
    {
      entity: 'user:user1',
      access: 'read'
      revoke: true
    }
  ]
});
```

Das ACL gewährt der Gruppe "GRP\_Verwaltung" Schreibrechte, der Gruppe aus dem vorherigen Beispiel Leserechte, mit Ausnahme des Benutzers "user1". Für `access` sind folgende Werte möglich. Die Werte in Klammer mit xml: ist die Kennung für das XML-Script über agoscript:

| Wert | Zugriff |
| --- | --- |
| xml:AG\_PB\_READ | r = read = Leserechte |
| xml:AG\_PB\_CHECK\_OUT | c = check\_out = Leserechte + Check-out/Check-in-Rechte |
| xml:AG\_PB\_WRITE | w = write = Leserechte + Schreibrechte |
| xml:AG\_PB\_PROTECTED | p = protected = Leserechte + das Recht, ein neues Objekt anzulegen |
| xml:AG\_PB\_ALL | a = all = Vollrechte |

Momentan können Sie ACLs, die auch für Admins gelten, nicht direkt auf diese Weise anlegen. Sie können das Flag aber nachträglich setzen:

```auto
acl.adminsAffected = true;
```

#### note

Mit note erzeugen Sie eine neue Notiz. Hierbei unterscheidet das System zwischen dem Text-Format und dem HTML-Format

**Text-Format**

```auto
objects.create('note', {
  content: 'Hallo Welt',
  target: file,
  recipients: [ 'group:GRP_Mitarbeiter' ]
});
```

**HTML-Format**

```auto
objects.create('note', {
  content: '<p>Hallo Welt<br>Neue Zeile</p>',
  target: file,
  noteFormat: 'text/html',
  recipients: [ 'group:GRP_Mitarbeiter' ]
});
```

Die Notiz wird an die oben erzeugte Datei gehängt und an alle Mitglieder der Gruppe "GRP\_Mitarbeiter" adressiert.

Möchten Sie, dass als Absender der Notiz nicht der Systemadministrator "roi" genannt wird, können Sie auch den Absender setzen.

**Text-Format**

```auto
/* global sc */

//Gibt den Absender an
let objectsUser = objects(sc.asUser(objects.find('user:demo')));

objectsUser.create('note', {
content: 'Hallo Welt',
  target: file,
  recipients: [ 'group:GRP_Mitarbeiter' ]
});
```

**HTML-Format**

```auto
/* global sc */

//Gibt den Absender an
let objectsUser = objects(sc.asUser(objects.find('user:demo')));

objectsUser.create('note', {
content: '<p>Hallo Welt<br>Neue Zeile</p>',
  target: 'text/html',
  recipients: [ 'group:GRP_Mitarbeiter' ]
});
```

#### update

**Ab welcher Version verfügbar?**• *agorum core 8.2.2*

Mit dieser Funktion aktualisieren Sie spezielle Klassen, etwa User. Es folgt ein Überblick über die unterstützten Werte für `class` und `data`.

```auto
objects.update('<class>', object, data)
```

**user**

Mit `user` aktualisieren Sie einen Benutzer:

```auto
let user = objects.update('user', objects.find('user:USERNAME'), {
  name: 'testuser',
  password: 'testpass',
  admin: false,
  givenName: 'Test',
  familyName: 'User',
  language: 'de',
  emailAddresses: [ 'testuser@agorum.com' ]
});
```

Die jeweiligen Felder sind optional. Geben Sie beispielsweise nur `password` an, aktualisiert sich auch nur das Passwort.

#### addTo

**Ab welcher Version verfügbar?**• *agorum core 9.0.0*

Mit dieser Funktion fügen Sie Objekte zu bestehenden Objekten hinzu, die weitere Objekte beinhalten können (Beispiel: ein weiterer Grantee zu einer bestehenden ACL).

```auto
objects.addTo('<class>', object, data)
```

Folgend eine Übersicht der bisher unterstützten Werte für `class` und den daraus resultierendem `data.`

**acl**

```auto
objects.addTo('acl', objects.find('group:World'), {
  aclObject: objects.find('acl:Testacl'),
  access: 'read',
  revoke: false
});
```

Es wird die Gruppe `World` dem bestehenden ACL `Testcl` mit lesendem Recht (`read`) zugewiesen.

Weitere Werte für `access`:

| Wert | Zugriff |
| --- | --- |
| read | Lesender Zugriff |
| write | Schreibender Zugriff |
| all | Vollzugriff |
| check\_out | Dokument auschecken |
| protected | Dokument schreibgeschützt setzen |

Weitere mögliche Werte für `revoke`:

| Wert | Beschreibung |
| --- | --- |
| true | Entzieht dem Benutzer das angegebene Recht. |
| false | Gibt dem Benutzer das angegebene Recht. |

#### removeFrom

**Ab welcher Version verfügbar?**• *agorum core 9.0.0*

Mit dieser Funktion entfernen Sie Objekte aus bestehenden Objekten, die weitere Objekte beinhalten können (Beispiel: das Löschen eines Grantees aus einer bestehenden ACL). Folgend eine Übersicht der bisher unterstützten Werte für `class` und den daraus resultierendem `data.`

```auto
objects.removeFrom('<class>', object, data);
```

**acl**

```auto
objects.removeFrom('acl', objects.find('acl:Testacl'), objects.find('group:World'));
```

Es wird die Gruppe `World` aus der bestehenden ACL `Testacl` entfernt.

In dieser Ausprägung von `removeFrom` ist `object` die bestehende ACL und data der `Grantee`, der aus der ACL entfernt werden soll.

#### mayDiscover

**Ab welcher Version verfügbar?**• *agorum core 8.2.2*

Diese Funktion liefert Ihnen `true` zurück, wenn der angemeldete Benutzer auf das angegebene ACL zumindest lesendes Recht (read) besitzt.

```auto
objects.mayDiscover('name-des-acls');
```

#### link/unlink, add/remove

Mit diesen Funktionen erzeugen oder entfernen Sie Verlinkungen des übergebenen Objekts in einem oder mehreren angegebenen Ordnern. Der Unterschied zwischen `link()`/`unlink()` und `add()`/`remove()` bezieht sich auf Scope-ACLs.

```auto
objects.link(object, targets, name)
objects.unlink(object, parents)
objects.add(object, targets, name)
objects.remove(object, parents)
```

In *agorum core* müssen grundsätzlich Objekte mit einem Haupt-ACL versehen werden. Mit diesem ACL ist es möglich, alle Anforderungen an die Berechtigungen umzusetzen.

Um die Umsetzung komplexer Anforderungen wesentlich zu vereinfachen, wurde die Technik der Scope-ACL's (zu Deutsch: Geltungsbereich/Anwendungsbereich) eingeführt. Scope-ACL's sind ACL's, die sich auf einen bestimmten Bereich (Scope) beziehen. Diese Technik bedeutet, dass Sie beliebig viele ACL's als Scope-ACL's auf ein Objekt setzen können.`add()`verwaltet somit zusätzlich noch die Scope-ACLs auf dem Objekt:

* `add()` ergänzt fehlende Scope-ACLs.
* `remove()` entfernt nicht mehr benötigte Scope-ACLs.

Für `targets` oder `parents` können einzelne Objekte oder Arrays von Objekten übergeben werden, `parents` ist außerdem optional – bei Fehlen werden alle aktuellen Elternordner verwendet. Wird `name` gesetzt, kann das Objekt außerdem noch umbenannt werden – bei Namenskollisionen wird hier automatisch ein numerisches Suffix angehängt.

**Tipps**: • Nutzen Sie das Funktionspaar (`link()`/`unlink()`, `add()`/`remove())` zusammen, um Objekte zu verschieben.• Nutzen Sie eine der Funktionen `link()/``add(),` um Dokumente zu verlinken.• Nutzen Sie `unlink()`/`remove(),` um Verlinkungen zu entfernen.

#### copy

Mit dieser Funktion erstellen Sie eine Kopie des übergebenen Objekts in einem oder mehreren angegebenen Ordnern. Das ACL des ersten Ordners wird als ACL der Kopie verwendet, eventuelle weitere ACLs als Scope-ACL. Optional können Sie das Objekt umbenennen. Namenskollisionen werden vermieden.

Die Funktion gibt als Ergebnis die Kopie des Objekts zurück.

```auto
let newObject = objects.copy(object, targets, name)
```

#### trash

Mit dieser Funktion entfernen Sie Verlinkungen des übergebenen Objekts in einem oder mehreren übergebenen Ordnern und markieren sie dort als gelöscht. Lassen Sie `parents` weg oder geben explizit alle Elternordner an, legt das System das Objekt außerdem in den Papierkorb.

```auto
objects.trash(object, parents)
```

#### rename

**Ab welcher Version verfügbar?**• *agorum core 9.5.1*

Mit `rename` benennen Sie ein Objekt um. Bei Namenskollisionen hängt das System automatisch ein numerisches Suffix an, ähnlich wie bei `add`, `link` und copy.

```auto
objects.rename(object, name)
```

#### convert, tryConvert

**Ab welcher Version verfügbar?**• *agorum core 8.3.1*• Bei älteren Versionen können Sie die Bibliothek mit folgendem ZIP-Template installieren: [objects-convert.zip](#)• Die Installation dieses ZIP-Templates funktioniert erst ab *agorum core 8.1.9.*​​​​​​

```auto
objects.convert(object, {
   name: 'test.txt', // optional, wenn nicht angegeben, wird der übergebene Name genommen.

   description: 'Eine Textdatei', // optional, wenn nicht angegeben, wird die übergebene Beschreibung genommen.

   path: 'Ordner 1/Ordner 2', // entweder muss "path" oder "target" angegeben sein.
   format: 'pdf', // Pflicht, gibt das Zielformat an.
   target: folder // entweder muss "path" oder "target" angegeben sein.
});

//Es gelten die gleichen Regeln wie oben bei "convert"
objects.tryConvert(object, {
  name: 'test.txt',
  description: 'Eine Textdatei',
  path: 'Ordner 1/Ordner 2',
  format: 'pdf', // Pflicht
  target: folder // Pflicht
});
```

Die Parameter `format` und `target` (oder `path`) sind Pflicht, als Name wird im Standard `<baseName>.<format>` verwendet, ansonsten wird der Rest 1:1 an `objects.create('file')` durchgereicht.

Der Unterschied zwischen `convert()` und `tryConvert()` besteht darin, dass Erstere einen Fehler wirft, wenn das Objekt nicht gefunden wird, während Letztere `null` zurückgibt.

**Hinweis**: Grundlegende Informationen zur Dokumentkonvertierung erhalten Sie in der Dokumentation [DocumentService](#).

Beispiel (inklusive. Prüfung, ob eine Konvertierung überhaupt funktioniert):

```auto
let beans = require('common/beans');..
let pdf = null;
if (beans.selected(object, '[convertible(pdf)]')) {
   pdf = objects.tryConvert(object, {

           format: 'pdf',

           path: '/agorum/roi/Files/Samples'
   });
}
```

Das übergebene "object" wird in ein PDF konvertiert. Wenn die Konvertierung nicht funktioniert, wird `null` zurückgegeben.

**Hinweis**: Sie können für `format` alle [Dokumentformate](#) angeben, für die ein Konverter vom vorhandenen Quellformat aus existiert. Die möglichen Konverter finden Sie in der MetaDb unter folgendem Pfad und dort in den jeweiligen Unterordnern:

```auto
MAIN_MODULE_MANAGEMENT/documentservice/control/services
```

#### writer

**Ab welcher Version verfügbar?**• *agorum core 9.5.0*

Mit `writer` schreiben Sie Text in eine Datei, wodurch diese Datei zu einer Logdatei wird. Bei dieser Datei kann es sich etwa um eine TXT- oder um eine HTML-Datei handeln, also alle Dateien, in die Text geschrieben werden kann.

**Beispiel**

```auto
let object = objects.find('1591610'); // ID '1591610' dient als Beispiel und verweist auf die genutzte LOG-Datei

objects.writer(object, w => {
    w.println('Bla');
    w.print('Irgendwas', '+ etwas weiteres'); // Ausgabe: Irgendwas + etwas weiteres

    w.print('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt
    w.println('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt

  // best practice
    w.print([ 1, 2, 3 ].join(' '));
    [ 1, 2, 3 ].forEach(w.print);

    [ 1, 2, 3 ].forEach(w.println);
});
```

**Ausgabe**

```auto
Bla
Irgendwas + etwas weiteresWert von x: x Test 123Wert von x: x Test 123
1 2 31 0 1,2,32 1 1,2,33 2 1,2,31 0 1,2,3
2 1 1,2,3
3 2 1,2,3
```

Führen Sie das obige Skript erneut aus, aber mit anderem Textinhalt, wird der neue Inhalt der Datei angefügt.

Wenn Sie mehrere Texte über `println` ausgeben, wird der zweite Eintrag an den ersten usw. angehängt, er taucht also dann unterhalb des ersten Eintrags in der Logdatei auf:

```auto
let object = objects.find('1591610'); // ID '1591610' dient als Beispiel und verweist auf die genutzte LOG-Datei

objects.writer(object, w => {

    //erstes 'Bla'
    w.println('Bla');
    w.print('Irgendwas', '+ etwas weiteres'); // Ausgabe: Irgendwas + etwas weiteres

    w.print('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt
    w.println('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt

  // best practice
    w.print([ 1, 2, 3 ].join(' '));
    [ 1, 2, 3 ].forEach(w.print);

    [ 1, 2, 3 ].forEach(w.println);

  //Zweites 'Bla'
  w.println('Bla');
    w.print('Irgendwas', '+ etwas weiteres'); // Ausgabe: Irgendwas + etwas weiteres

    w.print('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt
    w.println('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt

  // best practice
    w.print([ 1, 2, 3 ].join(' '));
    [ 1, 2, 3 ].forEach(w.print);

    [ 1, 2, 3 ].forEach(w.println);
});
```

**Ausgabe**

```auto
Bla Erste Logausgabe
Irgendwas + etwas weiteresWert von x: x Test 123Wert von x: x Test 123
1 2 31 0 1,2,32 1 1,2,33 2 1,2,31 0 1,2,3
2 1 1,2,3
3 2 1,2,3
Bla Zweite Logausgabe
Irgendwas + etwas weiteresWert von x: x Test 123Wert von x: x Test 123
1 2 31 0 1,2,32 1 1,2,33 2 1,2,31 0 1,2,3
2 1 1,2,3
3 2 1,2,3
```

| Parameter | Beschreibung |
| --- | --- |
| object | Hängt den Text an das angegebene Objekt an. Das Objekt muss zuvor über objects.find gefunden werden. Als Objekt empfiehlt sich eine TXT- oder eine HTML-Datei. |
| encoding (optional) | Gibt ein spezielles Encoding (im Format: 'ISO-8859-15') mit. Im Standard wird UTF-8 verwendet, egal, wie das System eingestellt ist. |
| callback | Über diese Funktion kann direkt geschrieben werden. Zur Verfügung stehen diese Methoden: print() Gibt die übergebenen Parameter direkt aus. Mehrere Parameter werden durch Leerzeichen getrennt. println() Gibt alle Parameter aus und erzeugt danach einen Absatz. Mehrere Parameter werden durch Leerzeichen getrennt. flush() Ab welcher Version verfügbar? • agorum core 10.2.2 Ermöglicht das Speichern der Datei, um den Inhalt sichtbar zu machen. Dies kann etwa nach allen paar Einträgen stattfinden. |

Beispiel eines mitgegebenen encodings:

```auto
objects.writer(object, 'ISO-8859-15', w => {
  w.println('abc;defä');
});
```

Beispiele, um ein Array auszugeben:

```auto
let values = [ 1, 2, 3 ];
objects.writer(object, 'ISO-8859-15', w => {
   // Einträge per Semikolon trennen

   w.print(values.join(';'));

   // Pro Eintrag eine neue Zeile schreiben:
   values.forEach(w.println);
});
```

Über die Angabe eines `sessionControllers` zu require('common/objects') steuern Sie, ob eine Historie für das Objekt erzeugt werden soll oder nicht, wenn in die Datei geschrieben wird:

```auto
// Es wird keine Historie für das geladene Objekt über objects erstellt.
let objects = require('common/objects')(sc.asService());

// Es wird eine Historie für das geladene Objekt über objects erstellt.
let objects = require('common/objects');
```

**Komplettes Beispiel**

```auto
/* global sc */
let objects = require('common/objects');

let object = objects.find('1591610'); ID '1591610' dient als Beispiel

objects.writer(object, w => {
    w.println('Bla');
    w.print('Irgendwas', '+ etwas weiteres2'); // Ausgabe: Irgendwas + etwas weiteres

    w.print('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt
    w.println('Wert von x:', 'x', 'Test 123'); // intern mit Leerzeichen getrennt

  // best practice
    w.print([ 1, 2, 3 ].join(' '));
    [ 1, 2, 3 ].forEach(w.print);

    [ 1, 2, 3 ].forEach(w.println);

  sc.asService();
});
```

#### getContentString

Mit dieser Funktion lesen Sie den Content eines Objekts in UTF-8.

```auto
let contentString = objects.getContentString(object);
```

| Parameter | Beschreibung |
| --- | --- |
| object | Liest vom Objekt den Content in UTF-8. |

| Return | Beschreibung |
| --- | --- |
| contentString | Enthält den Content des Objekts 'object'. |

#### setContentString

Mit dieser Funktion schreiben Sie den Content eines Objekts in UTF-8.

```auto
objects.setContentString(object, contentString);
```

| Parameter | Beschreibung |
| --- | --- |
| object | Schreibt den Content in UTF-8 in das Objekt. |
| contentString | Definiert den Content, der in UTF-8 in das Objekt 'object' geschrieben wird. |

#### SystemFlags

**Ab welcher Version verfügbar?**• *agorum core 10.0.4*​​

Siehe [Systemflags per JavaScript setzen](#)[.](#)

#### reIndex

**Ab welcher Version verfügbar?**• *agorum core 8.3.1*

Mit dieser Funktion indizieren Sie ein Objekt neu.

```auto
objects.reIndex(object);
```

#### forceOcr

**Ab welcher Version verfügbar?**• *agorum core 10.2.0*

Mit dieser Funktion erzwingen Sie die Neuerstellung des Dokumententextes des übergebenen Objekts per OCR, sofern ein entsprechender Konverter verfügbar ist.

```auto
objects.forceOcr(object);
```

**Hinweis**: Erstellen Sie ein neues Objekt oder extrahieren etwa einen Anhang aus einer E-Mail innerhalb eines Workflows, dann können Sie `forceOcr` nicht sofort verwenden. Ein Workflow läuft normalerweise innerhalb einer Transaktion ab, wodurch die neuen Objekte nicht sofort zur Verfügung stehen. Bauen Sie den Knoten [delay](#) ein, um dem Problem entgegenzuwirken und die aktuelle Transaktion abzuschließen.

## JavaScript-Bibliothek common/pdf

**Ab welcher Version verfügbar?**

• *agorum core* 9.3.0

Dieses Modul bietet Funktionen zum Bearbeiten von PDF-Dokumenten.

### Anwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let pdf = require('common/pdf');
```

### Funktionen

* * *

#### readMetadata()

Liest Metadaten aus einem PDF.

Übergeben wird eine ObjektId oder ein vollqualifizierter Pfad aus *agorum core* die / der ein PDF-Dokument darstellt, von dem die Metadaten gelesen werden sollen.

**Hinweis**: Wenn ein PDF-Dokument verschlüsselt ist, können keine Metadaten ausgelesen werden und die Funktion wirft einen Fehler.

**Beispiel**

```auto
let pdf = require('common/pdf');
let metadataDefinition = pdf.readMetadata(ObjektId/Pfad des PDF-Dokuments);
```

**Ergebnis des Aufrufs**

Das Ergebnis besteht aus dem XML-JavaScript-Format, da es sich bei Metadaten in einem PDF-Dokument um eine XMP-XML-Struktur handelt.

Informationen zum XML-JavaScript-Format siehe [JavaScript-Bibliothek common/xml](#).

```auto
{
  type: 'DocumentFragmentNode',
  children: [
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'begin=\"\uFEFF\" id=\"W5M0MpCehiHzreSzNTczkc9d\"',
      attributes: [ ],
      children: [ ]
    },
    {
      name: 'x:xmpmeta',
      type: 'ElementNode',
      children: [
        {
          name: 'rdf:RDF',
          type: 'ElementNode',
          children: [
            {
              name: 'rdf:Description',
              type: 'ElementNode',
              children: [
                {
                  name: 'agorum:testProperty',
                  type: 'ElementNode',
                  value: 'testValue',
                  children: [ ],
                  attributes: [ ],
                }
              ],
              attributes: [
                {
                  name: 'xmlns:agorum',
                  value: 'http://agorum.com/agorum/1.0'
                }

              ],
            }

          ],
          attributes: [
            {
              name: 'xmlns:rdf',
              value: 'http://www.w3.org/1999/02/22-rdf-syntax-ns#'
            }
          ]
        }

      ],
      attributes: [
        {
          name: 'xmlns:x',
          value: 'adobe:ns:meta/'
        }
      ]
    },

    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'end=\"w\"',
      children: [ ],
      attributes: [ ],
    }
  ]
}
```

#### writeMetadata()

Schreibt Metadaten auf ein PDF-Dokument.

Übergeben werden:

* eine ObjektId oder ein vollqualifizierter Pfad zu einem PDF-Dokument innerhalb von *agorum core*
* eine Metadaten-Definition, die auf das PDF-Dokument geschrieben werden soll

Eine Metadaten-Definition kann entweder durch das Lesen von Metadaten eines PDF-Dokuments erstellt werden oder durch die Hilfsfunktion dieser Bibliothek.

Wenn die übergebene Metadaten-Definition fehlerhaft ist, wirft die Funktion einen Fehler.

**Hinweis**: Wenn ein PDF-Dokument verschlüsselt ist, können keine Metadaten geschrieben werden und die Funktion wirft einen Fehler.

**Beispiel**

```auto
let pdf = require('common/pdf');
let xml = require('common/xml');
pdf.writeMetadata(ObjektId/Pfad des PDF-Dokuments, {
  type: 'DocumentFragmentNode',
  children: [
    {
      name : 'xpacket',
      type : xml.PROCESSING_INSTRUCTION_NODE,
      value : 'begin=\"\uFEFF\" id=\"W5M0MpCehiHzreSzNTczkc9d\"'
    },

    {
      name: 'x:xmpmeta',
      type: xml.ELEMENT_NODE,
      children: [
        {
          name : 'rdf:RDF',
          type : xml.ELEMENT_NODE,
          children: [
            {
              name : 'rdf:Description',
              type : xml.ELEMENT_NODE,
              children: [
                {
                  name : 'agorum:testProperty',
                  type : xml.ELEMENT_NODE,
                  value : 'testValue'
                }

              ],
              attributes: [
                {
                  name : 'xmlns:agorum',
                  value : 'http://agorum.com/agorum/1.0'
                }
              ]
            }
          ],
          attributes: [
            {
              name : 'xmlns:rdf',
              value : 'http://www.w3.org/1999/02/22-rdf-syntax-ns#'
            }
          ],
        }
      ],
      attributes: [
        {
          name : 'x:xmptk',
          value : 'XMP Core 5.5.0'
        },

        {
          name : 'xmlns:x',
          value : 'adobe:ns:meta/'
        }
      ]
    },
    {
      name : 'xpacket',
      type : xml.PROCESSING_INSTRUCTION_NODE,
      value : 'end=\"w\"'
    }

  ]
});
```

#### createMetadataDefinition()

Erstellt eine für XMP gültige Metadaten-Definition.

* Verwenden Sie diese Funktion, wenn Sie eine komplett neue Metadaten-Definition anlegen oder verwenden möchten.
* Die Metadaten-Definition ist die Grundlage, um Metadaten in einem PDF-Dokument ablegen zu können. Ohne diese Definition werden die Metadaten nicht als solche erkannt, und das PDF-Dokument kann die Metadaten nicht weitergeben.

Rückgabewert der Funktion ist eine komplett angelegte Metadaten-Definition, die mit eigenen Schemas und Propertys gefüllt werden kann.

**Beispiel**

```auto
let pdf = require('common/pdf');
let metadataDefinition = pdf.createMetadataDefinition()
```

**Ergebnis des Aufrufs**

```auto
{
  type: 'DocumentFragmentNode',
  children: [
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'begin=\"\uFEFF\" id=\"W5M0MpCehiHzreSzNTczkc9d\"'
    },
    {
      name: 'x:xmpmeta',
      type: 'ElementNode',
      children: [
        {
          type: 'ElementNode',
          name: 'rdf:RDF',
          attributes: [
            {
              name: 'xmlns:rdf',
              value: 'http://www.w3.org/1999/02/22-rdf-syntax-ns#'
            }
          ],
        }
      ],
      attributes: [
        {
          name: 'xmlns:x',
          value: 'adobe:ns:meta/'
        }
      ]
    },
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'end=\"r\"'
    }

  ]
}
```

#### createCustomSchema()

Erstellt ein Custom-Schema für eine Metadaten-Definition.

* Ein Custom-Schema ist ein Container für Metadaten-Informationen, die keinem speziellen Format der XMP-Definition entsprechen. Metadaten können somit nur in entsprechenden Schemas abgelegt werden und sind daher zwingend notwendig.
* Mit einem Custom-Schema können Metadaten aus *agorum core* als Metadatum für ein PDF-Dokument abgelegt und gespeichert werden.

**Hinweis**: Andere XMP-Schemas werden von der Bibliothek nicht unterstützt

Sie können der Funktion übergeben:

* den Namespace (NAMESPACE)
* die Beschreibungs-URL (URI)
* ein Beschreibungstext des Schemas (ABOUT)

**Namespace**

Den Namespace benötigen Sie, um die einzelnen Schemas und somit Metadaten-Definitionen innerhalb eines PDF-Dokuments zu unterscheiden.

**Beschreibungs-URL**

Die Beschreibungs-URL für das Schema gibt für Parser der XML-Struktur Auskunft über die Schema-Definition und ist essenziell für das korrekte Interpretieren der gespeicherten Informationen.

**Beschreibungstext des Schemas**

Als zusätzliche Informationsquelle können Sie einen Beschreibungstext übergeben, der grob beschreibt, um welche Daten es sich in diesem Schema handelt. Für die Übergabe zwingend notwendig sind folgende Parameter:

* Namespace
* Beschreibungs-URL

Als Rückgabewert sieht die Funktion eine fertige XML-JavaScript-Struktur vor, in der Propertys oder die Struktur einer Metadaten-Definition eingefügt werden können.

**Beispiel**

```auto
let pdf = require('common/pdf');
let customSchema = pdf.createCustomSchema('NAMESPACE', 'URI', 'ABOUT');
```

**Ergebnis des Aufrufs**

Das Ergebnis ist vom Format der Struktur her immer gleich. Lediglich die Werte können sich zu den eingetragenen Informationen ändern:

```auto
{
  type: 'ElementNode'
  children: [ ],
  name: 'rdf:Description',
  attributes: [

    {
      name: 'xmlns:NAMESPACE',
      value: 'URI'
    },
    {
      name: 'rdf:about',
      value: 'ABOUT'
    }
  ],
}
```

#### createProperty()

Erstellt ein Property für ein XMP-Schema.

* Ein Property in einem XMP-Schema enthält die eigentlichen Informationen der Metadaten.
* Das mit dieser Funktion erstellte Property kann einen Text enhalten, der CDATA-Encoded in der XML-Struktur angelegt wird.
* Wenn Sie ein Struktur-Property benötigen, verwenden Sie die Funktion [createContainerProperty()](#createContainerProperty\(\)).

Sie können der Funktion folgende Werte übergeben:

| Wert | Beschreibung | Datentyp |
| --- | --- | --- |
| name | Definiert den Namen der Property. | String |
| value | Definiert den Wert der Property. | String |
| namespace | Definiert den Namen des Namespaces, unter dem das Property angelegt wird. | String |

Alle Werte des Aufrufs sind Pflichtfelder. Sollte eines der Felder nicht gefüllt sein, meldet die Funktion einen Fehler.

Als Rückgabewert sieht die Funktion eine fertige XML-JavaScript-Struktur vor, die einem Schema oder einem Struktur-Property zugeordnet werden kann.

**Beispiel**

```auto
let pdf = require('common/pdf');
let property = pdf.createProperty('NAME', 'VALUE', 'NAMESPACE');
```

**Ergebnis des Aufrufs**

Das Ergebnis ist vom Format der Struktur her immer gleich. Lediglich die Werte können sich zu den eingetragenen Informationen ändern:

```auto
{
  type: 'ElementNode',
  name: 'NAMESPACE:NAME',
  value: 'VAlUE'
}
```

#### createContainerProperty()

Erstellt ein Struktur-Property für ein XMP-Schema.

* Ein Struktur-Property kann zur weiteren Strukturierungen für Propertys dienen.
* Als Kindelemente eines Struktur-Propertys können Sie weitere Property-Definitionen hinzufügen.
* Über die Funktion [createProperty()](#createProperty\(\)) erzeugen Sie Propertys.

Sie können der Funktion folgende Werte übergeben:

| Wert | Beschreibung | Datentyp |
| --- | --- | --- |
| name | Definiert den Namen der Property. | String |
| namespace | Definiert den Namen des Namespaces, unter dem das Property angelegt wird. | String |

Alle Werte des Aufrufs sind Pflichtfelder. Sollte eines der Felder nicht gefüllt sein, meldet die Funktion einen Fehler.

Als Rückgabewert sieht die Funktion eine fertige XML-JavaScript-Struktur vor, die einem Schema zugeordnet werden kann.

**Beispiel**

```auto
let pdf = require('common/pdf');
let structureProperty = pdf.createStructureProperty('NAME', 'NAMESPACE');
```

**Ergebnis des Aufrufs**

Das Ergebnis ist vom Format der Struktur her immer gleich. Lediglich die Werte können sich zu den eingetragenen Informationen ändern:

```auto
{
  type: 'ElementNode',
  name: 'NAMESPACE:NAME',
  children: [ ]
}
```

#### addPropertyToSchema()

Fügt zu einem Schema ein Property hinzu.

Sie können der Funktion folgende Werte übergeben:

| Wert | Beschreibung | Erwartet wird |
| --- | --- | --- |
| property | Definiert die Struktur der hinzuzufügenden Property. | Struktur einer Property oder einer Structure-Property |
| schema | Definiert die Struktur des Schemas, das der Property hinzugefügt wird. | Struktur eines Schemas |

**Beispiel**

```auto
let pdf = require('common/pdf');
let property = pdf.createProperty('NAME', 'VALUE', 'NAMESPACE');
let schema = pdf.createCustomSchema('NAMESPACE', 'URI', 'ABOUT');
let modifiedSchema = pdf.addPropertyToSchema(property, schema);
```

**Ergebnis des Aufrufs**

```auto
{
  type: 'ElementNode'
  name: 'rdf:Description',
  children: [
    {
      type: 'ElementNode',
      name: 'NAMESPACE:NAME',
      value: 'VALUE'
    }
  ],
  attributes: [

    {
      name: 'xmlns:NAMESPACE',
      value: 'URI'
    },
    {
      name: 'rdf:about',
      value: 'ABOUT'
    }
  ],
}
```

#### addSchemaToMetadataDefinition()

Fügt einer Metadaten-Definition ein Schema hinzu.

* Ein Schema legen Sie über die Funktion [createCustomSchema()](#createCustomSchema\(\)) an.
* Die Metadaten-Definition kann entweder bereits zur Verfügung stehen, wenn ein entsprechend präpariertes PDF-Dokument geladen wurde ([readMetadata()](#readMetadata\(\))), oder Sie können Siedurch die Funktion [createMetadataDefinition()](#createMetadataDefinition\(\)) anlegen.

Sie können der Funktion folgende Werte übergeben:

| Wert | Beschreibung | Erwartet wird |
| --- | --- | --- |
| schema | Definiert die Schema-Definition des Schemas, das hinzugefügt wird. | Struktur eines Schemas |
| metadataDefinition | Definiert die Metadaten-Definition, in die das Schema aufgenommen wird. | Struktur einer Metadatendefinition |

Alle Werte des Aufrufs sind Pflichtfelder. Sollte eines der Felder nicht gefüllt sein, meldet die Funktion einen Fehler.

Als Rückgabewert sieht die Funktion die geänderte Metadaten-Definition vor, die über den Aufruf zur Verfügung gestellt wurde.

**Beispiel**

```auto
let pdf = require('common/pdf');
let metadataDefinition = pdf.createMetadataDefinition();
let schema = pdf.createCustomSchema('NAMESPACE', 'URI', 'ABOUT');
let modifiedMetadataDefinition = pdf.addSchemaToMetadataDefinition(schema, metadataDefinition);
```

**Ergebnis des Aufrufs**

```auto
{
  type: 'DocumentFragmentNode',
  children: [
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'begin=\"\uFEFF\" id=\"W5M0MpCehiHzreSzNTczkc9d\"'
    },
    {
      name: 'x:xmpmeta',
      type: 'ElementNode',
      children: [
        {
          type: 'ElementNode',
          name: 'rdf:RDF',
          attributes: [
            {
              name: 'xmlns:rdf',
              value: 'http://www.w3.org/1999/02/22-rdf-syntax-ns#'
            }
          ],
          children: [
            {
              type: 'ElementNode'
              children: [ ],
              name: 'rdf:Description',
              attributes: [

                {
                  name: 'xmlns:NAMESPACE',
                  value: 'URI'
                },
                {
                  name: 'rdf:about',
                  value: 'ABOUT'
                }
              ],
            }
          ]
        }
      ],
      attributes: [
        {
          name: 'xmlns:x',
          value: 'adobe:ns:meta/'
        }
      ]
    },
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'end=\"r\"'
    }

  ]
}
```

**Praxisbeispiel**

Das folgende Praxisbeispiel zeigt, wie Sie eine Metadaten-Definition, ein Schema sowie ein Property anlegen und einem PDF-Dokument zur Verfügung stellen:

```auto
let pdf = require('common/pdf');
let metadataDefinition = pdf.createMetadataDefinition(); // Metadaten-Definition erzeugen
let customSchema = pdf.createCustomSchema('agorum', 'http://agorum.com/agorum/1.0'); // Schema erstellen
let customProperty = pdf.createProperty('testProperty', 'testValue', 'agorum'); // Property erstellen
let modifiedCustomSchema = pdf.addPropertyToSchema(customProperty, customSchema); // Property zu Schema hinzufügen
let modifiedMetadatDefinition = pdf.addSchemaToMetadataDefinition(modifiedCustomSchema, metadataDefinition); // Schema zu Metadatadefinition hinzufügen
pdf.writeMetadata(ObjektId/Pfad PDF-Dokument, modifiedMetadatDefinition); // Metadaten schreiben
```

Die Struktur, die in diesem Beispiel geschrieben wurde, sieht folgendermaßen aus:

```auto
{
  type: 'DocumentFragmentNode',
  children: [
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'begin=\"\uFEFF\" id=\"W5M0MpCehiHzreSzNTczkc9d\"'
    },
    {
      name: 'x:xmpmeta',
      type: 'ElementNode',
      children: [
        {
          type: 'ElementNode',
          name: 'rdf:RDF',
          attributes: [
            {
              name: 'xmlns:rdf',
              value: 'http://www.w3.org/1999/02/22-rdf-syntax-ns#'
            }
          ],
          children: [
            {
              type: 'ElementNode'
              children: [

                {
                  type: 'ElementNode',
                  name: 'NAMESPACE:NAME',
                  value: 'VALUE'
                }

              ],
              name: 'rdf:Description',
              attributes: [

                {
                  name: 'xmlns:NAMESPACE',
                  value: 'URI'
                },
                {
                  name: 'rdf:about',
                  value: 'ABOUT'
                }
              ],
            }
          ]
        }
      ],
      attributes: [
        {
          name: 'xmlns:x',
          value: 'adobe:ns:meta/'
        }
      ]
    },
    {
      name: 'xpacket',
      type: 'ProcessingInstructionNode',
      value: 'end=\"r\"'
    }

  ]
}
```

#### create()

**Ab welcher Version verfügbar?**• *agorum core* 9.4.0

Erstellt eine PDF basierend auf Previews beliebiger Dateiformate (PDF, E-Mail, Word, ...) und schreibt folgende Elemente in diese PDF:

* Rechtecke
* Text
* Linien
* Bilder

Wenn das Quelldokument OCR-Informationen mit Koordinaten enthält, wird die Textinformation aus dem PDF-Dokument des Ergebnisses rekonstruiert.

Sind nur Textinformationen vorhanden, werden diese unsichtbar in das Dokument geschrieben, sodass dieses immer noch durchsuchbar wäre.

**Aufruf**

```auto
let pdf = require('common/pdf');

pdf.create(
  {
    document: objects.find('path-to-input-document.ext'),
    coordinates: 'px',
    outputStream: objects.find('path-to-output-document.ext').contentOutputStream,
    format: 'A4',
    orientation: 'portrait',

    // Optional. Wenn die Seite noch nicht vorhanden ist, wird sie angelegt.
    pages: [
      {
        page: 1,
        items: [
          {
            type: 'line',
            xStart: 200,
            yStart: 200,
            xEnd: 300,
            yEnd: 300,
            lineWidth: 10,
            color: '#FF0000'
          },
          // ... more items
        ]
      },
      // ... more pages
    ],
​​​​​
    // Alternative oder zusätzliche Angabe von items.
    // "page" muss angegeben werden, zudem muss es die Seite als Vorschau bereits geben.
    items: [
      {
         type: 'line',
         page: 2,
         xStart: 200,
         yStart: 200,
         xEnd: 300,
         yEnd: 300,
         lineWidth: 10,
         color: '#FF0000'
       },
       // ... more items
    ]
  }
);
```

**Ablauf**

Die Preview-Bilder der Objektes *document* werden als Basis genommen und es wird eine neue PDF-Datei erstellt. Auf die jeweiligen Seiten werden die *items*, wie in *pages* definiert, erzeugt. Das PDF des Ergebnisses wird auf den in *outputStream* definierten Stream geschrieben.

Folgende Werte existieren:

| Wert | Beschreibung/Werte |
| --- | --- |
| document | Definiert ein agorum core-Objekt, etwa ein Word-Dokument oder PDF-Dokument oder ein Dokument, aus dem ein Preview erzeugt werden kann. |
| coordinates | px (Standard) Definiert die Koordinaten für x, y, width, height usw. in Pixeln. Die Angaben beziehen sich auf die Dimensionen des Preview-Bilds. % Definiert die Koordinaten für x, y, width, height usw. in % (0 - 1, 50 % wären 0,5). Die Angaben beziehen sich auf die Dimensionen des Preview-Bilds. |
| outputStream | Definiert den Stream zum agorum core-Objekt, auf den das PDF des Ergebnisses geschrieben wird. Das Objekt muss zuvor erstellt worden sein. |
| format | Definiert das Ausgabeformat des Dokumentes, etwa DIN-A4. Das jeweilige Preview-Bild wird auf dieses Format automatisch eingepasst. Folgende Angaben sind möglich: A0 A1 A2 A3 A4 (Standard) A5 A6 LETTER |
| orientation | portrait (Standard) Richtet das Dokument im Hochformat aus. landscape Richtet das Dokument im Querformat aus. |
| pages | Definiert die Definition der einzelnen Elemente wie Text, Line usw. auf den jeweiligen Seiten (siehe pages). |
| items | Definiert die Definition der einzelnen Elemente wie Text, Line usw. inklusive Angabe, auf welcher Seite diese erscheinen. |

**pages**

Definiert die Definition der einzelnen Elemente wie Text, Line usw. auf den jeweiligen Seiten.

* *pages* ist optional.
* Alternativ können Sie direkt mit *items* arbeiten
* Verwenden Sie *pages*, wenn neue Seiten mit einem definierten Format angelegt werden sollen.

**Beispiel**

```auto
// ...
pages: [
  {
    page: 1,
    format: 'A4',
    orientation: 'portrait',
    items: [
      {
        type: 'line',
        xStart: 200,
        yStart: 200,
        xEnd: 300,
        yEnd: 300,
        lineWidth: 10,
        color: '#FF0000'
      }
    ]
  }
]
// ...
```

* Für jede Seite können Sie Elemente hinzufügen.
* Als Basis dient immer zuerst das Preview-Bild für die jeweilige Seite. Auf dieses werden dann die einzelnen in items definierten Elemente gezeichnet.

Folgende Werte existieren:

| Wert | Beschreibung |
| --- | --- |
| page | Definiert die Nummer der Seite beginnend mit 1. Diese Seite muss auch als Preview vorhanden sein, sonst wird sie nicht gezeichnet. |
| format | Definiert das Format pro Seite. Wenn Sie diesen Wert nicht definieren, verwendet das System die globale format-Einstellung. |
| orientation | Definiert die Orientierung pro Seite. Wenn Sie diesen Wert nicht definieren, verwendet das System die globale orientation-Einstellung. |
| items | Definiert die einzelnen Elemente (items), die auf diese Seite gezeichnet werden. |

​​​​​​ items

Definiert die Definition der einzelnen Elemente, wie Text, Line usw., unabhängig von der Seite.

* *items* können Sie auch direkt angeben, dann ist es jedoch wichtig, dass Sie beim jeweiligen *item* auch die *page* angeben.
* Wenn Sie *page* nicht angeben, wird das *item* nicht gezeichnet.
* *items* können Sie mit *pages* kombinieren.

**Beispiel**

```auto
// ...
items: [
  {
    type: 'line',
    page: 1,
    xStart: 200,
    yStart: 200,
    xEnd: 300,
    yEnd: 300,
    lineWidth: 10,
    color: '#FF0000'
  }
]
// ...
```

Für jede Seite können Sie Elemente hinzufügen. Als Basis dient dann immer zuerst das Preview-Bild für die jeweilige Seite. Darauf werden dann die einzelnen in items definierten Elemente gezeichnet.​​​​​

**items (unterhalb von pages)**

Zeichnet verschiedene Elemente auf eine PDF-Seite.

**line**

Zeichnet eine Linie.

**Beispiel**

```auto
// ...
{
  type: 'line',
  xStart: 200,
  yStart: 200,
  xEnd: 300,
  yEnd: 300,
  lineWidth: 10,
  alpha: 0.5,
  color: '#FF0000'
}
// ...
```

Folgende Werte existieren:

| Wert | Beschreibung |
| --- | --- |
| type | line |
| xStart | Definiert den Start der x-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| yStart | Definiert den Start der y-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| xEnd | Definiert das Ende der x-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| yEnd | Definiert das Ende der y-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| lineWidth (optional) | Definiert die Liniendicke in Pixeln. |
| alpha (optional) | Definiert die Deckkraft in %. 0 Unsichtbar 1 Vollständig sichtbar |
| color (optional) | Definiert die Farbe der Linie als RGB-Hex-Code. |

**rect**

Zeichnet ein Rechteck.

**Beispiel**

```auto
// ...
{
  type: 'rect',
  x: 300,
  y: 300,
  width: 100,
  height: 100,
  lineWidth: 1,
  alpha: 0.2,
  fill: '#FF0000',
  stroke: '#0000FF'
}
// ...
```

Folgende Werte existieren:

| Wert | Beschreibung |
| --- | --- |
| type | rect |
| x | Definiert den Start der x-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| y | Definiert den Start der y-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| width | Definiert die Breite in Pixeln oder %. |
| height | Definiert die Höhe in Pixeln oder %. |
| lineWidth (optional) | Definiert die Liniendicke in Pixeln für den Rand. |
| alpha (optional) | Definiert die Deckkraft in %. 0 Unsichtbar 1 Vollständig sichtbar |
| fill (optional) | Definiert die Farbfläche des Rechtecks als RGB-Hex-Code. |
| stroke (optional) | Definiert den Farbrahmen des Rechtecks als RGB-Hex-Code. |

**text**

Zeichnet einen Text.

**Beispiel**

```auto
// ...
{
  type: 'text',
  x: 100,
  y: 100,
  text: 'Hallo, dies ist ein Test',
  color: '#FF0000',
  width: 100,
  font: 'Helvetica',
  lineHeight: 20,
  fontSize: 20,
  bold: true,
  italic: false
}
// ...
```

Folgende Werte existieren:

| Wert | Beschreibung |
| --- | --- |
| type | text |
| x | Definiert den Start der x-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| y | Definiert den Start der y-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| width (optional) | Definiert die Breite in Pixeln oder % (wenn angegeben, wird der Text von der Breite her beschränkt und bricht automatisch um). |
| lineHeight (optional) | Definiert die Linienhöhe zwischen den Zeilen. |
| alpha (optional) | Definiert die Deckkraft in %. 0 Unsichtbar 1 Vollständig sichtbar |
| color (optional) | Definiert die Farbe des Textes als RGB-Hex-Code. |
| text | Definiert den zu erscheinenden Text. |
| fontSize | Definiert die Schriftgröße in Pixeln. |
| bold | true Fettdruck false Kein Fettdruck |
| italic | true Kursivschrift false Keine Kursivschrift |
| font (optional) | Definiert die Schriftart. Mögliche Werte sind: Helvetica (Standard) Courier |
| origin | Definiert den Bezugspunkt des Textes. Mögliche Werte sind: top left (Standard) Der Text beginnt oben (y) links (x). Die Ausrichtung ist linksbündig. OCR: x/y, Lorem ipsum dolor sit amet, Lorem ipsum dolor sit amet top right Der Text beginnt oben (y) rechts (x). Die Ausrichtung ist rechtsbündig. OCR: x/y, Lorem ipsum dolor sit amet, Lorem ipsum dolor sit amet bottom-right Der Text beginnt unten (y) rechts (x). Die Ausrichtung ist rechtsbündig. OCR: Lorem ipsum dolor sit amet x/y Lorem ipsum dolor sit amet, bottom-left Der Text beginnt unten (y) links (x). Die Ausrichtung ist linksbündig. OCR: Lorem ipsum dolor sit lamet x/y Lorem ipsum dolor sit lamet |
| rect | Versieht den Text mit einem Rechteck. Das Rechteck orientiert sich exakt an den Ausmaßen des Textes. Mögliche Werte sind: lineWidth (optional) Definiert die Liniendicke in Pixeln für den Rand. alpha (optional) Definiert die Deckkraft in %. 0 Unsichtbar 1 Vollständig sichtbar fill (optional) Definiert die Farbfläche des Rechtecks als RGB-Hex-Code. stroke (optional) Definiert den Farbrahmen des Rechtecks als RGB-Hex-Code. padding (optional) Definiert den Abstand zum Text in Pixeln oder in % (Angabe muss bei % zwischen 0 und 1 liegen). |

**Beispiel mit origin und rect**

```auto
// ...
{
  type: 'text',
  x: 100,
  y: 100,
  text: 'Hallo, dies ist ein Test',
  color: '#FF0000',
  width: 100,
  font: 'Helvetica',
  lineHeight: 20,
  fontSize: 20,
  bold: true,
  italic: false,
  origin: 'top-left',
  rect: {
    fill: '#FFFF00',
    padding: 10,
    alpha: 0.5
  }
}
// ...
```

**image**

Zeichnet ein Bild.

**Beispiel**

```auto
// ...
{
  type: 'image',
  x: 400,
  y: 400,
  width: 200,
  alpha: 1.0,
  image: objects.find('path-to-image.png')
}
// ...
```

Folgende Werte existieren:

| Wert | Beschreibung |
| --- | --- |
| type | image |
| x | Definiert den Start der x-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| y | Definiert den Start der y-Koordinate in Pixeln oder % vom linken oberen Rand aus. |
| width | Definiert die Breite in Pixeln oder % (wenn nicht angegeben, wird die Breite entweder aus der Höhe berechnet oder die Originalbreite des Bildes verwendet). |
| height | Definiert die Höhe in Pixeln oder % (wenn nicht angegeben, wird die Höhe entweder aus der Höhe berechnet oder die Originalbreite des Bildes verwendet). |
| image | Definiert ein Bild-Dokument (png oder jpg) aus agorum core. |
| alpha | Definiert die Deckkraft in %. 0 Unsichtbar 1 Vollständig sichtbar |

#### getTextHeight

Berechnet die Höhe des Textes bei einem automatisch umbrechenden Text.

**Beispiel**

```auto
let text = 'Hallo, dies ist ein Test, dieser Text wird in eine Box eingefügt.';
let height = pdf.getTextHeight(text, {
  font: 'Courier',
  bold: true,
  italic: false,
  lineHeight: 20,
  size: 20
}, 280);
```

**Komplettes Beispiel**

Das folgende Skript zeigt ein komplettes Beispiel, basierend auf den Demo-Dokumenten, die bei einer Installation von *agorum core* enthalten sind.

```auto
let pdf = require('common/pdf');
let objects = require('common/objects');

let start = new Date();

// the input document
let document = objects.find('/agorum/roi/Files/Demo/Checkliste-DMS.docx');

// the output document, create it if not present, otherwise overwrite it
let outPdf = objects.tryFind('/agorum/roi/Files/Demo/create-pdf-sample.pdf');
if (!outPdf) {
  outPdf = objects.create('file', {
    name: 'create-pdf-sample.pdf',
    target: objects.find('/agorum/roi/Files/Demo')
  });
}

// sample image
let image = objects.find('/agorum/roi/Preview/SampleApprovalSet/Stamps/StampApproved.png');

// get the calculated height for the text, to build the box around it
let text = 'Hallo, dies ist ein Test, dieser Text wird in eine Box eingefügt.';
let height = pdf.getTextHeight(text, {
  font: 'Courier',
  size: 20
}, 280);

// create the sample pdf
pdf.create(
  {
    document: document,
    coordinates: 'px',

    outputStream: outPdf.contentOutputStream,
    format: 'A4',
    orientation: 'portrait',

    pages: [
      {
        page: 1,
        items: [
          {
            type: 'line',
            xStart: 200,
            yStart: 200,
            xEnd: 300,
            yEnd: 300,
            lineWidth: 10,
            color: '#FF0000'
          },
          {
            type: 'rect',
            x: 100,
            y: 100,
            width: 300,
            height: height + 10,
            lineWidth: 1,
            alpha: 0.2,
            stroke: '#0000FF'
          },
          {
            type: 'text',
            x: 110,
            y: 100,
            text: text,
            width: 280,
            color: '#FF0000',
            font: 'Courier',
            fontSize: 20
          },
          {
            type: 'rect',
            x: 300,
            y: 300,
            width: 100,
            height: 100,
            lineWidth: 1,
            alpha: 0.2,
            fill: '#FF0000',
            stroke: '#0000FF'
          },
          {
            type: 'image',
            x: 400,
            y: 400,
            width: 200,
            image: image
          }
        ]

      },
      {
        page: 2,
        // may be defined per page, if needed
        format: 'A4',
        orientation: 'portrait',
        items: [
          {
            type: 'line',
            xStart: 200,
            yStart: 200,
            xEnd: 300,
            yEnd: 300,
            lineWidth: 10,
            color: '#FF0000'
          },
          {
            type: 'text',
            x: 100,
            y: 100,
            text: 'Hallo, dies ist ein Test auf Seite 2',
            color: '#FF0000',
            fontSize: 20
          },
          {
            type: 'rect',
            x: 300,
            y: 300,
            width: 100,
            height: 100,
            lineWidth: 1,
            alpha: 0.2,
            fill: '#FF0000',
            stroke: '#0000FF'
          }
        ]

      }
    ]
  }
);

'finished: ' + ((new Date().getTime() - start.getTime())/1000) + ' s';
```

## JavaScript-Bibliothek common/property

Diese Bibliothek bietet Funktionen zum Wandeln von Strings in JavaScript-Strukturen und umgekehrt.

**Hinweis**: Property ist ein agorum-internes Format zur Kommunikation mit der API.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let property = require('common/property');
```

### Funktionen

* * *

#### parse

Wandelt einen JSON-String in eine Property-Struktur.

```auto
property.parse('string ....')
```

```auto
let property = require('common/property');
let value = property.parse('{ "Hallo": "Welt" }');

// Rückgabe JS Objekt:
{
  "Hallo": "Welt"
}
```

#### from

Wandelt eine Java/JavaScript-interne Struktur, basierend auf Maps und ArrayLists in ein Property-basiertes-Objekt.

```auto
let prop = property.from(object);
```

Wandlung einer Java-Objektstruktur in eine JSON-String Struktur, als Alternative zu *JSON.stringify*:

```auto
let jsonStr = property.from(javaObject).toString();
```

#### unwrap

Wandelt eine Property-Struktur in Java-native Maps und Lists um.

```auto
let javaObject = property.unwrap(propertyObject);
```

## JavaScript-Bibliothek common/svg

**Ab welcher Version verfügbar?**• *agorum core* 9.4.1

Diese Bibliothek bietet Funktionen zum Wandeln von SVG-Dateien in JPG und PNG.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let svg = require('common/svg');

let svgS = '...PUT-IN-SOME-SVG-XML...';
svg.svgToJpg(svgS, output-agorum-core-object, {
  width: 800,
  quality: 0.9
});
```

### Funktionen

* * *

#### svgToJpg

Konvertiert eine SVG-Datei in eine JPG-Datei.

**Aufruf**

```auto
svg.svgToJpg(input, output, options);
```

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| input | Definiert die SVG-Datei. Folgende Typen sind möglich: agorum core-Objekt String inputStream |
| output | Definiert die JPG-Datei. Folgende Typen sind möglich: agorum core-Objekt outputStream |
| options | Definiert eine Struktur, die folgende Werte enthalten kann: width (optional) Definiert einen Hinweis auf die zu erzeugende Breite. Standard wird automatisch bestmöglich ermittelt. height (optional) Definiert einen Hinweis auf die zu erzeugende Höhe. Standard wird automatisch bestmöglich ermittelt. quality (optional) Definiert einen Wert zwischen 0 (niedrig) und 1 (hoch) für die Qualität der JPG-Datei (Standard = 0.8 (80 %). |

Das Ergebnis wird in das in *output* angegeben Objekt geschrieben.

#### svgToPng

Konvertiert eine SVG-Datei in eine PNG-Datei.

**Aufruf**

```auto
svg.svgToPng(input, output, options);
```

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| input | Definiert die SVG-Datei. Folgende Typen sind möglich: agorum core-Objekt String inputStream |
| output | Definiert die JPG-Datei. Folgende Typen sind möglich: agorum core-Objekt outputStream |
| options | Definiert eine Struktur, die folgende Werte enthalten kann: width (optional) Definiert einen Hinweis auf die zu erzeugende Breite. Standard wird automatisch bestmöglich ermittelt. height (optional) Definiert einen Hinweis auf die zu erzeugende Höhe. Standard wird automatisch bestmöglich ermittelt. |

Das Ergebnis wird in das in *output* angegeben Objekt geschrieben.

### Komplettes Beispiel

* * *

```auto
let svg = require('common/svg');
let objects = require('common/objects');

let target = objects.find('home:myFiles');

// create a sample output file in myFiles of the current user
let jpg = objects.create('file', {
  name: 'test-svg-jpg-' + new Date().getTime() + '.jpg',
  target: target
});

// the agorum core logo as svg
let svgS = '<?xml version="1.0" encoding="utf-8"?><svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 501.4 500" style="enable-background:new 0 0 501.4 500;" xml:space="preserve"><style type="text/css">.st0{fill:#0069B5;} .st1{fill:#003F85;} .st2{fill:#5696E8;}</style><rect x="200.7" y="200.9" transform="matrix(0.7071 -0.7071 0.7071 0.7071 -103.9823 250.782)" class="st0" width="100" height="100"/><polygon class="st1" points="237.6,50 179.5,108.1 215.3,143.9 309.3,50 "/><polygon class="st2" points="262.8,450 320.9,391.9 286.1,357 193.1,450 "/><polygon class="st1" points="108.8,250.5 180,179.3 144.2,143.5 73,214.6 50.7,236.9 50.7,263.1 179.5,391.9 214.9,356.5 "/><polygon class="st2" points="321.4,108.6 286.1,143.9 392.6,250.5 321.9,321.2 357.2,356.5 427.9,285.8 450.7,263.1 450.7,237.9 "/></svg>';

// create jpg with 800 pixel width
svg.svgToJpg(svgS, jpg, {
  width: 800,
  quality: 0.9
});
```

## JavaScript-Bibliothek common/templates

Diese Bibliothek bietet Funktionen, um Platzhalter in einen String mit Objekt-Metadaten oder Variablen zu füllen. Im Fall von Zahlen und Datumswerten legen Sie die Formatierung fest.

### Verwendung

* * *

```auto
let templates = require('common/templates');
```

### Funktionen

* * *

#### fill

```auto
templates.fill(template, variables, object, clearEmpty)
```

| Parameter | Beschreibung | Pflichtfeld |
| --- | --- | --- |
| template | Erwartet einen String, der die zu füllenden Platzhalter enthält. | ja |
| variables | Definiert explizit belegte Variablen. Aufbau { <variable>: <Variablenwert>} | nein |
| object | Definiert ein Objekt, dessen Metadaten verwendet werden sollen. | nein |
| clearEmpty | Definiert, ob Platzhalter, deren Werte nicht definiert sind, entfernt werden. Der Standard ist false (Platzhalter werden nicht entfernt). | nein |

**Beispiel 1**

```auto
let objects = require('common/objects');
let user = objects.find('user:roi');
templates.fill('${num:de|0} ${name} ${name:1,2} (${owner.fullName})', { num: 12345678.9 }, user);
```

Das Ergebnis dieses Aufrufs könnte folgendermaßen aussehen:

```auto
12345678 Testobject Te (Max Mustermann)
```

* Wert der Variable *num* im deutschen Format, ohne Tausendertrennzeichen oder Nachkommastellen
* Name von *object*
* die ersten beiden Zeichen des Namens von *object*
* Vor- und Nachname des Besitzers von *object*

**Beispiel 2**

Bei Variablen muss immer folgendes Format angegeben werden:

```auto
{<variable>: <variablenwert>}
```

```auto
let vorname = 'Marta'
let nachname = 'Müller'

let username = templates.fill('${vorname}.${nachname}',{vorname: vorname, nachname: nachname});
let usermail = templates.fill('${vorname}.${nachname}@agorumcore.com', {vorname: vorname, nachname: nachname});
```

### Strings formatieren

* * *

Handelt es sich bei dem Attribut um eine Zeichenkette, können auch nur Teile davon verwendet werden.

Durch die Verwendung der Syntax *${<Attribut>:x,y}* wird der Teil vom x-ten bis zum y-ten Zeichen ausgeschnitten, etwa extrahiert *${<Attribut>:2,5}* die Zeichen 2 bis 5 (jeweils einschließlich).

* Sind die verwendeten Zahlen negativ, beginnt die Zählung vom Ende des Attributs, eine Mischung ist ebenfalls möglich, etwa *${<Attribut>:2,-2}*, um das erste und letzte Zeichen zu entfernen.
* Fehlt die zweite Positionsangabe, werden die ersten x Zeichen (bei positivem x) oder die letzten x Zeichen (bei negativem x) selektiert.

Dieses kann in einer JavaScript-Konsole mit folgendem Skript getestet werden:

```auto
/* global Packages, sc */

let templates = require('common/templates');

// Ausgabe ohne Tausendertrennung, Dezimaltrennung in Deutsch
//              Formatierung    Belegen des Strings, der formatiert ausgegeben wird
templates.fill('${str:2}',     { str: 'Hier steht ein Text' });

// Ergebnis: Hi
```

#### Beispiele

**Ausgabe der ersten beiden Zeichen**

```auto
templates.fill('${str:2}', { str: 'Hier steht ein Text' });
```

***Ergebnis***

```auto
'Hi'
```

**Ausgabe von Zeichen 2 bis Zeichen 4 jeweils einschließlich (gezählt wird ab 1)**

```auto
//                                   1234567890123456789
templates.fill('${str:2,4}', { str: 'Hier steht ein Text' });
```

***Ergebnis***

```auto
'ier'
```

**Ausgabe von Zeichen 2 bis Zeichen -2 (also von hinten gezählt) jeweils einschließlich (gezählt wird ab 1)**

```auto
//  von hinten gezählt:              9876543210987654321
//                                    1234567890123456789
templates.fill('${str:2,-2}', { str: 'Hier steht ein Text' });
```

***Ergebnis***

```auto
'ier steht ein Tex'
```

**Ausgabe von Zeichen -6 (also von hinten gezählt)  (gezählt wird ab 1)**

```auto
//  von hinten gezählt:            9876543210987654321
templates.fill('${str:-6}', { str: 'Hier steht ein Text' });
```

***Ergebnis***

```auto
'n Text'
```

### Strings mit :f formatieren

* * *

Wenn ein String formatiert wird, der als Name eines Objekts gesetzt wird, können Sie mit der Formatierung :f dafür sorgen, dass alle Sonderzeichen, die im Windows-Filesystem nicht erlaubt sind, als \_ im String ersetzt werden.

Das f muss immer nach dem Doppelpunkt (:) stehen und vor der Zahl.

**Beispiel**

```auto
/* global Packages, sc */

let templates = require('common/templates');

templates.fill('${name:f2}',     { name: 'a/' });

// Ergebnis: a_

templates.fill('${name:f}',     { name: 'a/b/c' });

// Ergebnis: a_b_c
```

### Zahlen formatieren

* * *

#### Allgemeine Schreibweise

```auto
${<Name Metadatum>[:Locale[|Formatangabe]]}
```

#### Schreibweisen

| Schreibweise | Beschreibung |
| --- | --- |
| ${ | Beginn eines Metadatums |
| ${js | Beginn eines einzeiligen JavaScripts |
| ${{js | Beginn eines mehrzeiligen JavaScripts |
| : | Nach dem Doppelpunkt können Sie ein Format angeben. |
| Locale | (optional) Definiert eine Locale. Die Locale besteht aus dem Sprachcode und dem Ländercode (etwa de-DE für deutsch und Deutschland), siehe Unterstütze Sprachcodes und Ländercodes. |
| | | Optional, wenn eine Locale und eine Formatangabe angegeben wird. |
| Formatangabe | Optional sind folgende Formatangaben möglich. Wenn Sie die Formatangabe angeben, müssen Sie zwingend auch die Locale angeben. 0 Number Represent digit # Number Digit, zero shows as absent . Number Decimal separator or monetary decimal separator (Nachkommastellen) - Number Minus sign , Number Grouping separator (Tausendertrennung) E Number Separates mantissa and exponent in scientific notation. ; Subpattern boundary Separates positive and negative subpatterns % Prefix or suffix Multiply by 100 and show as percentage } Ende der Metadatum-Beschreibung oder eines einzeiligen JavaScriptes }} Ende eines mehrzeiligen JavaScriptes |

#### Beispiel

Sie können die Schreibweise in einer JavaScript-Konsole mit folgendem Beispiel testen:

```auto
/* global Packages, sc */

let templates = require('common/templates');

// Ausgabe ohne Tausendertrennung, Dezimaltrennung in Deutsch
// Test für die Formatierung einer Zahl

//              Metadatum ausgeben    Zahl definieren für die Testausgabe
templates.fill('${num:de|####.##}', { num: 12345678.987654 });

// Ergebnis: 12345678.99
```

#### Beispiel in der fill-Methode

**Ausgabe**Deutsche Nachkommatrennung, ohne Tausendertrennung, 2 Nachkommastellen:

```auto
templates.fill('${num:de|####.##}', { num: 12345678.987654 });
```

***Ergebnis***

```auto
12345678.99
```

**Ausgabe mit Tausendertrennung, Dezimaltrennung in Deutsch**

```auto
templates.fill('${num:de|#,###.##}', { num: 12345678.987654 });
```

***Ergebnis***

```auto
12.345.678,99
```

**Beispiel in der fill-Methode mit Ländercode (Deutsch) und locale (Schweiz)**

```auto
templates.fill('${num:de-CH|#,###.##}', { num: 12345678.987654 });
```

***Ergebnis***

```auto
12'345'678.99
```

**Beispiel Ausgabe in % (Zahl wird mit 100 multipliziert)**

```auto
templates.fill('${num:de|#%}', { num: 0.11 });
```

***Ergebnis***

```auto
11%
```

**Beispiel mit 2 Formatangaben, einmal für positive Zahl, und für negative Zahl (num ist negativ))**

```auto
templates.fill('${num:de|#,###.##;#,###.##-}', { num: -12345678.987654 });
```

***Ergebnis***

```auto
12.345.678,99-
```

**Beispiel mit 2 Formatangaben, einmal für positive Zahl, und für negative Zahl (num ist positiv)**

```auto
templates.fill('${num:de|#,###.##;#,###.##-}', { num: 12345678.987654 });
```

***Ergebnis***

```auto
12.345.678,99
```

**Beispiel Ausgabe als Ganzzahl (Nachkomma wird gerundet)**

```auto
templates.fill('${num:de|####}', { num: 12345678.987654 });
```

***Ergebnis***

```auto
12345679
```

**Beispiel Ausgabe als Ganzzahl mit führenden Nullen**

```auto
templates.fill('${z:de|000}', {z:3});
```

***Ergebnis***

```auto
003
```

### Datumswerte formatieren

* * *

Um ein Metadatum mit dem Datentyp *Datum* zu formatieren, wird folgender Syntax aufgerufen:

```auto
${Rechnungsdatum:[Länderkennung|]formatstring[|Geschäftsjahr]}
```

**Hinweis**: \[Länderkennung|\] und \[|Geschäftsjahr\] sind optional. Wenn Geschäftsjahr, dann auch Länderkennung.

Für den Formatstring können Sie Folgendes verwenden:

| Symbol | Bedeutung | Präsentation |
| --- | --- | --- |
|

G

 | Ära | Text Beispiel: AD |
|

yy

 | Jahr zweistellig | Nummer Beispiel: 07 |
|

yyyy

 | Jahr vierstellig | Nummer Beispiel: 2007 |
|

M

 | Monat im Jahr | Nummer Beispiel: 7 |
|

MM

 | Monat im Jahr mit 0 | Nummer Beispiel: 07 |
|

MMM

 | Monat im Jahr kurz | Text Beispiel: Sep |
|

MMMM

 | Monat im Jahr lang | Text Beispiel: September |
|

d

 | Tag im Monat | Nummer Beispiel: 26 |
|

h

 | Stunde (1–12) | Nummer Beispiel: 9 |
|

H

 | Stunde am Tag (0–23) | Nummer Beispiel: 0 |
|

m

 | Minute der Stunde | Nummer Beispiel: 13 |
|

s

 | Sekunde der Minute | Nummer Beispiel: 22 |
|

S

 | Millisekunde | Nummer Beispiel: 257 |
|

E

 | Tag der Woche kurz | Text Beispiel: Mi |
|

EEEE

 | Tag der Woche lang | Text Beispiel: Mittwoch |
|

D

 | Tag im Jahr | Nummer Beispiel: 304 |
|

F

 | Tag der Woche im Monat | Nummer Beispiel: 3 |
|

w

 | Woche im Jahr | Nummer Beispiel: 12 |
|

W

 | Woche im Monat | Nummer Beispiel: 3 |
|

a

 | am- und pm-Text | Text Beispiel: AM |
|

k

 | Stunde am Tag (1–24) | Nummer Beispiel: 24 |
|

K

 | Stunde (0–11) | Nummer Beispiel: 0 |
|

z

 | Allgemeine Zeitzone | Text Beispiel: GMT+02:00 |
|

Z

 | Zeitzone nach RFC 822 | Text Beispiel: +0200 |
|

'

 | Zeichen für unbehandelten Text | Trennzeichen Beispiel: templates.fill('${date:yyyy\\'/\\'MM\\'/\\'dd}'); Ergebnis (wenn heute der 18.02.2021 ist): 2021/02/18 |
|

''

 | Einzelnes Hochkomma | Literal (muss im String als \\'\\' angegeben werden) Beispiel:' |
| <leer> | Vollständiger Zeitstempel nach ISO-8601 in der UTC-Zeitzone | Text Beispiel: 2016-11-27T16:54:36.164Z |

Für das Geschäftsjahr können Sie Folgendes verwenden:

| Zeitraum | Nachlaufendes Geschäftsjahr | Vorauseilendes Geschäftsjahr |
| --- | --- | --- |
| Januar bis Dezember | M-0 | M+0 |
| Februar bis Januar | M-1 | M+11 |
| März bis Februar | M-2 | M+10 |
| April bis März | M-3 | M+9 |
| Mai bis April | M-4 | M+8 |
| Juni bis Mai | M-5 | M+7 |
| Juli bis Juni | M-6 | M+6 |
| August bis Juli | M-7 | M+5 |
| September bis August | M-8 | M+4 |
| Oktober bis September | M-9 | M+3 |
| November bis Oktober | M-10 | M+2 |
| Dezember bis November | M-11 | M+1 |

Testen können Sie dies in der JavaScript-Konsole mit folgendem Skript:

```auto
/* global Packages, sc */

let templates = require('common/templates');

// Formatierung des Datums: Datum für den Test belegen
templates.fill('${datum:yyyy-MM-dd HH:mm:ss}', { datum: new Date(2017, 1, 28, 12, 14, 39) });
// Ergebnis: 2017-02-28 12:14:39
​​​​​
```

**Hinweise:**

* Der Platzhalter *date* ist reserviert und kann nicht als Wert übergeben werden.

* *date* entspricht immer dem aktuellen Datum.

* Die folgende Formatierung des Datums ist nicht funktionsfähig:

```auto
templates.fill('${date:yyyy-MM-dd HH:mm:ss}', { date: new Date(2017, 1, 28, 12, 14, 39) });
```

* Geben Sie dem Platzhalter einen anderen Namen.

#### Aufbau von new Date()

*new Date()* hat folgenden Aufbau:

```auto
new Date(year, monthIndex [, day [, hour [, minutes [, seconds [, milliseconds]]]]]);
```

Als *monthIndex* geben Sie einen Wert zwischen 0 und 11 an, wobei 0 = Januar und 11 = Dezember ist.

Folgendes Beispiel verdeutlicht die Funktionsweise:

```auto
/* global sc */

let templates = require('common/templates');

let datum = new Date(2021, 1, 1);
//Ausgabe: 2021-01-31T23:00:00.000Z

// Formatierung des Datums: Datum für den Test belegen
templates.fill('${datum:EEEE}', { datum: datum });
```

* *let datum = new Date(2021, 1, 1);* ergibt den 2021-01-31T23:00:00.000Z.
* Das JavaScript-Datum wird immer in GMT+0 ausgegeben.
* In Deutschland gilt GMT+1, daher tritt der Februar in Deutschland exakt eine Stunde früher ein als in Greenwich, London (wo der 0-Meridian verläuft). *agorum core* kann jedoch mit Zeitzonen umgehen und berechnet daher das Datum automatisch um. Als Tag wird daher *Monday* ausgegeben.

#### Die aktuelle Kalenderwoche ausgeben

Möchten Sie die aktuelle Kalenderwoche ausgeben, arbeiten Sie mit local-Angaben:

```auto
/* global Packages, sc */

let templates = require('common/templates');

// Formatierung des Datums: Datum für den Test belegen
templates.fill('${datum:de|w}', { datum: new Date(2021, 1, 1) });
```

Als Ausgabe wird die Kalenderwoche 5 zurückgegeben.

**Hinweis**: Die local-Angaben benötigen Sie bei folgenden Datumswerten:• w• W• EEEE

#### Das Datumsformat nach ISO-8601 angeben

**Ab welcher Version verfügbar?**

• *agorum core* 10.0.8

Beispiel für das Datumsformat nach ISO-8601, etwa für die Verwendung als Übergabeparameter im FileWorkflow oder in Suchanfragen:

```auto
let templates = require('common/templates');

let d = new Date('2016-11-27T16:54:36.164Z');

// Formatierung des Datums

let ds = templates.fill('${datum}', {
  datum: d
});

d + ' - ' + ds;
```

**Ergebnis (Beispiel Zeitzone Deutschland Winterzeit)**

```auto
Sun Nov 27 2016 17:54:36 GMT+0100 (CET) - 2016-11-27T16:54:36.164Z
```

#### Beispiel einer Formatierung für ein Geschäftsjahr

```auto
templates.fill('${datum:de|yyyy|M+11}', { datum: new Date(2017, 1, 28, 12, 14, 39) });
```

Gleiches funktioniert auch, wenn Sie statt *M* (für *month*) ein *H* (für *hour*) verwenden:

```auto
templates.fill('${datum:de|yyyy|H+11}', { datum: new Date(2017, 1, 28, 12, 14, 39) });
```

In diesem Fall werden 11 Stunden zum Datum hinzugezählt.

**Ergebnis**

```auto
2018
```

#### Beispiel für die Länderkennung de und ausgeschriebenem Monat und Tag

**Hinweis**: Die Länderkennung wird hier für die Landesschreibweise des Monats und des Tages verwendet.

```auto
templates.fill('${datum:de|EEEE dd MMMM yyyy}', { datum: new Date(2017, 1, 28, 12, 14, 39) });
```

**Ergebnis**

```auto
Dienstag 28 Februar 2017
```

#### Besonderheit bei Sekunden

Möchten Sie lediglich die Sekunden eines Zeitstempels verwenden, müssen Sie zwingend zusätzlich eine Länderkennung angeben, etwa:

```auto
${datum:de|ss}
```

Der Grund hierfür ist, dass *ss* selbst eine Länderkennung ist und als solche interpretiert wird, wenn sie allein steht.

#### Beispiel templates.fill mit createPath zum Erstellen einer Ordnerstruktur nach einem Datum

Wenn Sie eine Ordnerstruktur nach einem Datum anlegen wollen, kombinieren Sie die Funktion [createPath(..)](#) mit *templates.fill*.

```auto
..
.
// Sie benötigen einen Ordner, an den sie die neue Struktur anlegen wollen
let folder = objects.find('FolderID');

// Unter diesen Ordner wollen Sie jetzt eine Struktur anlegen im Format yyyy/MM/dd
// Wenn heute der 23.08.2021 ist, dann sieht die Struktur wie folgt aus:
// <Folder>/2021/08/23
let dd = folder.createPath(templates.fill('${myDate:yyyy}/${myDate:MM}/${myDate:dd}', {myDate: new Date()});
// als Rückgabewert wird der letzte Ordner der neu angelegten Struktur zurück gegeben in diesem falle der Ordner mit dem Namen "23"
..
.
```

### Inline-JavaScript

* * *

In der fill-Methode können Sie auch ein JavaScript ausführen lassen. Mit dem JavaScript führen Sie Berechnungen aus und das Ergebnis kann zurückgegeben werden.

Berechnet wird von links nach rechts. Dies bedeutet, eine JS-Variable aus einem JS-Skript kann in einem nächsten JS-Skript, das rechts davon steht, weiter verwendet werden.

Testen kann man dieses mit folgendem Skript in der JavaScript-Konsole:

```auto
/* global Packages, sc */

let templates = require('common/templates');

//           num formatiert ausgeben     num im JS verwenden           ab hier die Metadaten für den Test definieren
templates.fill('${num:de|000000.0000} - ${js: i = global.num + 123.88;i;}', { num: 234.998 });
// Ergebnis: '000234,9980 - 358.878'
```

#### Besonderheiten des JavaScripts

* Der Aufruf **${js:** .... **}** läuft in einer eigenen Sandbox. Dort ist nicht alles zugelassen.
* Der Aufruf **${{js:** .... **}}** läuft in einer eigenen Sandbox. Dort ist nicht alles zugelassen.

Der Unterschied zwischen **${js:..** und **${{js:..** ist folgender:

* **${js:** ...**}**  bedeutet, dass der JavaScript-Code in einer Zeile stehen muss. Es darf kein \\n darin vorkommen.
* **${{js:** ...**}}** bedeutet, dass der JavaScript-Code über mehrere Zeilen verteilt werden kann. Dieses bedingt eine bessere Lesbarkeit von größeren Programmteilen, hat aber den Nachteil, dass es etwas langsamer ausgeführt wird.

Verwenden Sie bei kleinen Programmstücken, die nur einzeilig sind, Folgendes:

```auto
${js: ... }
```

Bei größeren Programmstücken, die über mehrere Zeilen besser lesbar sind:

```auto
${{js:....}}
```

**Tipp**: Verwenden Sie einen JavaScript-Editor für das Erstellen des JavaScripts, das zwischen ${{js: ... und .... }} steht. Damit lassen sich Fehler vermeiden, da diese in dem Editor sofort angezeigt werden.

#### Beispiel

Berechnet wird von links nach rechts. Dies bedeutet, eine JS-Variable aus einem JS-Skript kann in einem nächsten JS-Skript, das rechts davon steht, weiter verwendet werden.

```auto
templates.fill('${num:de|000000.0000} - ${{js: i = global.num + 123.88; i;}}  - ${js: i - 10;}',

{ num: 234.998 });
```

**Ergebnis**

```auto
'000234,9980 - 358.878 - 348.878'
```

#### Aufruf von extern definierten JavaScript-Skripten

Im Standard werden die Skripte unter */agorum/roi/Scripting/Libraries/default* automatisch geladen. Darin sind die beiden DocForm-Scripte *transform* und *validate* enthalten. Aus historischen Gründen ist auch noch das Skript *AC* enthalten, um die Abwärtskompatibilität zu erhalten. Für diese Skripte muss kein *require* durchgeführt werden.

**Achtung**: Verlangsamung des Prozesses durch weitere Skripte. Legen Sie keine weiteren Skripte in den oben aufgeführten Ordner, da diese immer gezogen werden und den Prozess dadurch verlangsamen. Überlegen Sie, ob ein solches Skript nicht innerhalb der fill-Methode aufgerufen wird, sondern einen Schritt zuvor.

**Beispiel**

```auto
templates.fill('${js: transform(test).remove(/[^0-9]+/g).value() }', {
  test: 'XY-00-12345'
});
```

**Ergebnis**

```auto
'0012345'
```

#### Find

In der *fill*\-Funktion kann auch ein *find* ausgeführt. Mit dem *find* und einer *ID/UUID* kann ein Objekt in *agorum core* gesucht werden, das als Grundlage zur Ersetzung der Variablen dient.

* Die *ID/UUID* kann entweder fest im Template hinterlegt oder ebenfalls durch das Template ersetzt werden lassen.
* Mit der Angabe des Metadatums wird der Wert des Metadatums zur Laufzeit zum Austauschen des Metadatums verwendet.

**Minimales Beispiel**

```auto
templates.fill('${find(uuid).~metadatum}', {
  uuid: '1234-1234-1234-1234' //Ersetzen Sie die UUID mit der UUID eines realen Objekts Ihrer agorum core-Installation
});
```

**Erweitertes Beispiel 1: Neuen Dateinamen durch gesetztes Metadatum erzeugen**

Das folgende Beispiel lädt die Metadaten eines gewünschten Dokuments und verwendet anschließend ein gesetztes Metadatum, um einen neuen Dateinamen zu erzeugen. Zum Erzeugen des neuen Namen wird die oben beschriebene *fill*\-Funktion (templates.fill) verwendet:

```auto
/* global sc, data */

let objects = require('common/objects');
let metadata = require('common/metadata');
let templates = require('common/templates');

let file = objects.find('/agorum/roi/customers/TestDaten/test.pdf');

// lade die Metadaten des Objektes die mit dem (custom) Präfix acmf_ beginnen

let md = metadata().load(file, /^acmf_/).data();

// wenn es ein Metadatum acmf_displayName gibt, dann benenne die Datei um, hierzu wird templates.fill() genutzt

if (md.acmf_displayName) {

  let newname = templates.fill('${acmf_displayName:f}', md) + '.' + file.nameExtension;
  file.name = newname;
}
```

Erweitertes Beispiel 2: Umwandeln von Metadaten über common/beans (veraltete Funktion)

Das folgende Beispiel liest von einem Objekt Metadaten, wandelt diese in Strings um und schreibt diese wieder zurück. Die Wandlung ist so aufgebaut, dass beim Zurückschreiben wieder der richtige Datentyp erstellt wird:

```auto
let objects = require('common/objects');
let beans   = require('common/beans');
let templates = require('common/templates');

let test = objects.find('1307827');

let data = beans.get(test, '~');
let ret = [];

ret.push( templates.fill('acmf_testLong        : ${acmf_testLong}', {} , test));
ret.push( templates.fill('acmf_testDouble      : ${acmf_testDouble:en|########.##########}', {} , test));
ret.push( templates.fill('acmf_testZeichenkette: ${acmf_testZeichenkette}', {} , test));
ret.push( templates.fill('acmf_testInteger     : ${acmf_testInteger}', {} , test));
ret.push( templates.fill('acmf_testDate        : ${acmf_testDate:yyyy-MM-dd\'T\'HH:mm:ss.SSSXXX}', {} , test));
ret.push( templates.fill('acmf_testFloat       : ${acmf_testFloat:en|########.############}', {} , test));
ret.push( templates.fill('acmf_testBoolean     : ${acmf_testBoolean:}', {} , test));
ret.push(new Date(templates.fill('${acmf_testDate:yyyy-MM-dd\'T\'HH:mm:ss.SSSXXX}', {} , test)));

beans.set(test, {
  '~acmf_testLong:long'          : templates.fill('${acmf_testLong}', {} , test),
  '~acmf_testDouble:double'      : templates.fill('${acmf_testDouble:en|########.##########}', {} , test),
  '~acmf_testZeichenkette:string': templates.fill('${acmf_testZeichenkette}', {} , test),
  '~acmf_testInteger:long'       : templates.fill('${acmf_testInteger}', {} , test),
  '~acmf_testDate:date'          : templates.fill('${acmf_testDate:yyyy-MM-dd\'T\'HH:mm:ss.SSSXXX}', {} , test),
  '~acmf_testFloat:double'       : templates.fill('${acmf_testFloat:en|########.############}', {} , test),
  '~acmf_testBoolean:boolean'    : templates.fill('${acmf_testBoolean:}', {} , test)
});

JSON.stringify(data, null, 4)  + '\n' + ret.join('\n');
```

## JavaScript-Bibliothek common-text

Diese JavaScript-Bibliothek bietet Funktionen zum Erzeugen von Text aus Dokumenten, etwa die Extraktion durch OCR.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let text = require('common/text');
```

### Funktionen

* * *

#### extract

Extrahiert Text aus einem gegebenen Dokument.

* Nach der Erstellung eines neuen Dokumenttextes führt das System automatisch eine Neuindizierung durch.
* Das Property-Entry *MaxDocumentSize* (zu finden unter: *MAIN\_MODULE\_MANAGEMENT/textindexservice/control/syncdata/indexer/MaxDocumentSize*) beeinflusst, ob das System einen Dokumenttext erzeugt.

**Syntax**

```auto
text.extract(object, settings);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard |
| --- | --- | --- | --- |
| object | Definiert ein agorum core-Objekt, von dem das System den Text extrahiert. | ja | – |
| settings | Ermöglicht diverse Einstellungen zur Extraktion (siehe settings). | nein | – |

**settings**

| Parameter | Beschreibung | Pflicht | Standard |
| --- | --- | --- | --- |
| extractionType | Definiert die Art der Extraktion (siehe EXTRACTION\_TYPES). | nein | – |
| parameters | Definiert ein Array von Parametern, die dem dahinterliegenden Konverter mitgegeben werden können, etwa zum Steuern von OCR-Parametern. Beispiel \['--bitonal-auto:True', '--bitonal-brightness:100'\] | nein | – |
| forceOcr | true Das System führt die OCR immer durch, auch dann, wenn etwa PDF-Dateien bereits Text enthalten. false Das System führt die OCR nur durch, wenn es notwendig ist. | nein | false |

**EXTRACTION\_TYPES**

| EXTRACTION\_TYPE | Beschreibung |
| --- | --- |
| CREATE | Erzeugt Text nur, wenn er nicht existiert. Existiert der Text bereits, führt das System nichts durch. |
| UPDATE | Aktualisiert veralteten Text. |
| FORCE | Erzeugt Text immer neu, unabhängig davon, ob er existiert oder veraltet ist. |

**Beispiel**

```auto
let text = require('common/text');
let objects = require('common/objects');

let obj = objects.find('ID of an agorum core document');
let dto = text.extract(obj, {
  extractionType: text.EXTRACTION_TYPES.FORCE,
  parameters: [
    '--bitonal-auto:True',
    '--bitonal-brightness:100'
  ],
  forceOcr: true
}).object;

console.log('text: ', dto.contentString);
```

**Rückgabewerte**

Sie erhalten folgende Struktur, die das *DocumentTextObject* enthält, d. h. das Objekt, das den generierten Text enthält:

```auto
let result = text.extract(obj);

// Den Textinhalt des Textes herauslesen
result.object.contentString;
```

**Beispiel: Text direkt holen**

```auto
let txt = textLib.extract(obj, {
  extractionType: textLib.EXTRACTION_TYPES.CREATE,
}).text;
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie Text kontrolliert von einem Objekt erzeugen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### canForceOcr

Prüft, ob es bei dem übergebenen Objekt möglich ist, OCR zu erzwingen.

**Syntax**

```auto
text.canForceOcr(object);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Standard |
| --- | --- | --- | --- |
| object | Definiert ein agorum core-Objekt, das das System prüft. | ja | – |

**Beispiel**

```auto
let text = require('common/text');
let objects = require('common/objects');

let obj = objects.find('ID of an agorum core document');
let forceOcrPossible = text.canForceOcr(obj);
```

**Rückgabewerte**

| Rückgabewert | Beschreibung |
| --- | --- |
| true | OCR kann für das Objekt erzwungen werden. |
| false | OCR kann für das Objekt nicht erzwungen werden. |

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie prüfen möchten, ob für ein Objekt die Generierung per OCR erzwungen werden kann.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

## JavaScript-Bibliothek common/time

Mithilfe dieser JavaScript-Bibliothek ändern Sie Datumsobjekte. Diese Bibliothek folgt dem Fluent-API-Konzept, bei dem das System immer den aktuellen Zustand als Objekt zurückgibt, um mehrere Aufrufe zu kombinieren.

### Verwendung

* * *

Sie benötigen die folgende Bibliothek, um diese JavaScript-Bibliothek verwenden zu können. Die Bibliothek geben Sie am Anfang des Skripts an.

```auto
let time = require('common/time');
```

### Konstruktoren (Factory Pattern)

* * *

Die Konstruktoren verwenden Sie, um ein Time-Object zu erhalten, das Sie mit den hier aufgeführten [Funktionen](#Funktionen) auslesen und verarbeiten können. Initial ist als Zeitzone die Standard-Zeitzone des *agorum core*\-Servers hinterlegt.

#### time.now

Liefert die aktuelle Uhrzeit zurück.

**Syntax**

```auto
let fieldValue = time.now();
```

**Parameter**Zu diesem Konstruktor existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung des Konstruktors.

```auto
let time = require('common/time');

let t1 = time.now();
t1;
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diesen Konstruktor verwenden Sie, wenn Sie die aktuelle Uhrzeit benötigen.

**Exceptions**

Zu diesem Konstruktor existieren keine Exceptions.

#### time.fromEpoch

Liefert eine angegebene Epoche zurück.

**Syntax**

```auto
let fieldValue = time.fromEpoch(milliseconds);
```

**Parameter**

Diese Parameter existieren im Konstruktor:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| milliseconds | Definiert die Epoche-Millisekunden. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung des Konstruktors.

```auto
let time = require('common/time');

let t2 = time.fromEpoch(0); // Liefert 01.01.1970 00:00:00.000 zurück
t2;
```

**Rückgabewerte**

Sie erhalten die angegebene Epoche und die dazugehörige Time-Instanz zurück:

```auto
01.01.1970 00:00:00.000
```

**Verwendung**

Diesen Konstruktor verwenden Sie, wenn Sie die angegebene Epoche benötigen.

**Exceptions**

Zu diesem Konstruktor existieren keine Exceptions.

#### time.fromDateObject

Liefert ein angegebenes Time-Object zurück.

**Syntax**

```auto
let fieldValue = time.fromDateObject(fieldValue);
```

**Parameter**

Diese Parameter existieren im Konstruktor:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Variable, deren Datum das System ausliest. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung des Konstruktors.

```auto
let time = require('common/time');

let date = new Date(2022, 02, 11);
let t1 = time.fromDateObject(date); // 11.03.2022 00:00:00.000 Server-Zeit
```

**Rückgabewerte**

Sie erhalten das Time-Object zurück.

**Verwendung**

Diesen Konstruktor verwenden Sie, wenn Sie ein angegebenes Time-Object benötigen.

**Exceptions**

Zu diesem Konstruktor existieren keine Exceptions.

### Funktionen

* * *

Mit den folgenden Funktionen können Sie die oben aufgeführten [Konstruktoren](#Konstruktoren) weiter verarbeiten und bearbeiten.

**Beispiel**

```auto
let time = require('common/time');
time.fromEpoch(40271111).addYears(52).getDateObject();
```

**Hinweis**: Die hier aufgeführten Funktionen sind kaskadierend und können hintereinander angereiht werden.

**Rückgabewert**

```auto
2022-01-01T11:11:11.111Z
```

#### addYears

Addiert Jahre zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addYears(years);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| years | Definiert die Anzahl an Jahren, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addYears(52); //Addiert 52 Jahre zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
{
  "_utcTime": "2022-01-01T11:11:11.111Z[UTC]",
  "_firstDayOfWeek": "MONDAY",
  "_pattern": "yyyy-MM-dd['T'HH[:mm[:ss[.SSS]]]][X]['['z']']",
  "_targetZone": "Europe/Berlin"
}
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Jahre hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addMonths

Addiert Monate zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addMonths(months);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| months | Definiert die Anzahl an Monaten, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addMonths(42); //Addiert 42 Monate zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1973-07-01T11:11:11.111Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Monate hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addWeeks

Addiert Wochen zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addWeeks(weeks);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| weeks | Definiert die Anzahl an Wochen, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addWeeks(4); //Addiert 4 Wochen zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1970-01-29T11:11:11.111Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Wochen hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addDays

Addiert Tage zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addDays(days);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| days | Definiert die Anzahl an Tagen, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addDays(42); //Addiert 42 Tage zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1970-02-12T11:11:11.111Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Tage hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addHours

Addiert Stunden zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addHours(hours);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| hours | Definiert die Anzahl an Stunden, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addHours(4); //Addiert 4 Stunden zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1970-01-01T15:11:11.111Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Stunden hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addMinutes

Addiert Minuten zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addMinutes(minutes);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| minutes | Definiert die Anzahl an Minuten, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addMinutes(120); //Addiert 120 Minuten zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1970-01-01T13:11:11.111Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Minuten hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addSeconds

Addiert Sekunden zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addSeconds(seconds);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| seconds | Definiert die Anzahl an Sekunden, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addSeconds(120); //Addiert 120 Sekunden zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1970-01-01T11:13:11.111Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Sekunden hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### addMillis

Addiert Millisekunden zu einem Datum hinzu.

**Syntax**

```auto
time.fromEpoch(milliseconds).addMillis(milliseconds);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| milliseconds | Definiert die Anzahl an Sekunden, die das System hinzuaddiert. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).addMillis(3293); //Addiert 3293 Millisekunden zum Datum 01.01.1970 11:11:11.111 [UTC]
```

**Rückgabewerte**

Sie erhalten das addierte Datum zurück.

```auto
1970-01-01T11:11:14.404Z[UTC]
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie zu einem Datum Millisekunden hinzuaddieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getPattern

Liefert ein Pattern zurück. Das Pattern müssen Sie zuvor mit der Funktion [setPattern](#setPattern) gesetzt haben.

**Syntax**

```auto
fieldValue.getPattern();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Pattern auf das deutsche Format und liest das Pattern aus
let t1 = time.now().setPattern('dd.MM.yyyy HH:mm:ss');
t1.getPattern();
```

**Rückgabewerte**

Sie erhalten das gesetzte Pattern zurück.

```auto
dd.MM.yyyy HH:mm:ss
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Pattern benötigen, das Sie zuvor mit der Funktion [setPattern](#setPattern) gesetzt haben.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getZoneId

Liefert eine Zeitzone zurück. Die Zeitzone müssen Sie zuvor mit der Funktion [setZoneById](#setZoneById) gesetzt haben.

Ermöglicht eine automatische Umwandlung von MEZ <-> MESZ.

**Syntax**

```auto
fieldValue.getZoneId();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Zeitzone setzen und lesen
let t1 = time.now().setZoneById('Europe/Berlin');
t1.getZoneId();
```

**Rückgabewerte**

Sie erhalten die gesetzte ZoneId zurück.

```auto
Europe/Berlin
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine Zeitzone benötigen, die Sie zuvor mit der Funktion [setZoneById](#setZoneById) gesetzt haben.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getZoneOffsetId

Liefert eine Zeitzone anhand der Offset-ID zurück. Die Zeitzone müssen Sie zuvor mit der Funktion [setZoneByOffsetId](#setZoneByOffsetId) gesetzt haben.

**Syntax**

```auto
fieldValue.getZoneOffsetId();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Zeitzone anhand einer Offset-ID setzen und lesen
let t1 = time.now().setZoneByOffsetId('+0100');
t1.getZoneOffsetId();
```

**Rückgabewerte**

Sie erhalten die gesetzte ZoneOffsetId zurück.

```auto
+01:00
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die ZoneOffsetId benötigen, die Sie zuvor mit der Funktion [setZoneByOffsetId](#setZoneByOffsetId) gesetzt haben.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getZoneOffsetSeconds

Liefert die Offset-Sekunden der Zeitzone zurück. Die Offset-Sekunden müssen Sie zuvor mit der Funktion [setZoneByOffsetSeconds](#setZoneByOffsetSeconds) gesetzt haben.

Es erfolgt keine automatische Umwandlung von MEZ <-> MESZ.

**Syntax**

```auto
fieldValue.getZoneOffsetSeconds();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Zeitzone anhand von Offset-Sekunden und liest die Offset-Sekunden aus.
let t1 = time.now().setZoneByOffsetSeconds(3600);
t1.getZoneOffsetSeconds();
```

**Rückgabewerte**

Sie erhalten die gesetzten Offset-Sekunden zurück.

```auto
3600
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Zeitzone anhand von Offset-Sekunden erhalten möchten, die Sie zuvor mit der Funktion [setZoneByOffsetSeconds](#setZoneByOffsetSeconds) gesetzt haben.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getFirstDayOfWeek

Liefert den ersten Tag der Woche zurück. Den ersten Tag der Woche müssen Sie zuvor mit der Funktion [setFirstDayOfWeek](#setFirstDayOfWeek) gesetzt haben.

**Syntax**

```auto
fieldValue.getFirstDayOfWeek();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.now().setFirstDayOfWeek(time.SUNDAY); // Setzt den ersten Tag der Woche auf Sonntag
t1.getFirstDayOfWeek();
```

**Rückgabewerte**

Sie erhalten den gesetzten Wert zurück, der dem Wert von time.SUNDAY entspricht.

```auto
7
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den ersten Tag der Woche benötigen, den Sie zuvor mit der Funktion [setFirstDayOfWeek](#setFirstDayOfWeek) gesetzt haben.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getEpoch

Liefert die Millisekunden einer Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getEpoch();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getEpoch();
```

**Rückgabewerte**

Sie erhalten die Epochen-Millisekunden zurück:

```auto
40271111
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Epochen-Millisekunden benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getDateObject

Liefert ein JavaScript Date-Objekt zurück. Das JavaScript Date-Objekt müssen Sie zuvor mit der Funktion [setFromDateObject](#setFromDateObject) setzen.

**Syntax**

```auto
time.fromEpoch(milliseconds).getDateObject();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getDateObject();
```

**Rückgabewerte**

Sie erhalten ein JavaScript Date-Objekt zurück.

```auto
1970-01-01T11:11:11.111Z
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein JavaScript Date-Objekt benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getYear

Liefert das Jahr für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getYear();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getYear();
```

**Rückgabewerte**

Sie erhalten das Jahr für die Epoche zurück.

```auto
1970
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Jahr für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getMonth

Liefert den Monat für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getMonth();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getMonth();
```

**Rückgabewerte**

Sie erhalten den Monat für die Epoche zurück.

```auto
1
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Monat für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getDay

Liefert den Tag für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getDay();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getDay();
```

**Rückgabewerte**

Sie erhalten den Tag für die Epoche zurück.

```auto
1
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Tag für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getDayOfWeek

Liefert den Tag der Woche für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getDayOfWeek();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getDayOfWeek();
```

**Rückgabewerte**

Sie erhalten den Tag der Woche für die Epoche zurück, hier den Wert 4, der [time.THURSDAY](#Konstanten) entspricht.

```auto
4
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Tag der Woche für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getDayOfYear

Liefert den Tag des Jahres für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getDayOfYear();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getDayOfYear();
```

**Rückgabewerte**

Sie erhalten den Tag des Jahres für die Epoche zurück.

```auto
1
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Tag des Jahres für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getHour

Liefert die Stunde für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getHour();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getHour();
```

**Rückgabewerte**

Sie erhalten die Stunde für die Epoche zurück.

```auto
1
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Stunde für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getMinute

Liefert die Minute für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getMinute();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getMinute();
```

**Rückgabewerte**

Sie erhalten die Minute für die Epoche zurück.

```auto
11
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Minute für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getSecond

Liefert die Sekunde für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getSecond();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getSecond();
```

**Rückgabewerte**

Sie erhalten die Sekunde für die Epoche zurück.

```auto
11
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Sekunde für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getMilli

Liefert die Millisekunde für eine Epoche zurück.

**Syntax**

```auto
time.fromEpoch(milliseconds).getMilli();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).getMilli();
```

**Rückgabewerte**

Sie erhalten die Millisekunde für die Epoche zurück.

```auto
111
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Millisekunde für eine Epoche benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getYearsTo

Liefert den Unterschied zwischen Epochen in Jahren zurück.

**Syntax**

```auto
fieldValue.getYearsTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getYearsTo(t2); // Liefert den Unterschied in Jahren zurück: 2
t2.getYearsTo(t1); // Liefert den Unterschied in negativen Jahren zurück: -2
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Jahren zurück:

```auto
2
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Jahren benötigen.

#### getMonthsTo

Liefert den Unterschied zwischen Epochen in Monaten zurück.

**Syntax**

```auto
fieldValue.getMonthsTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getMonthsTo(t2); // Liefert den Unterschied in Monaten zurück: 26
t2.getMonthsTo(t1); // Liefert den Unterschied in negativen Monaten zurück: -26
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Monaten zurück:

```auto
26
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Monaten benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getWeeksTo

Liefert den Unterschied zwischen Epochen in Wochen zurück.

**Syntax**

```auto
fieldValue.getWeeksTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getYearsTo(t2); // Liefert den Unterschied in Wochen zurück: 113
t2.getYearsTo(t1); // Liefert den Unterschied in negativen Wochen zurück: -113
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Wochen zurück:

```auto
113
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Wochen benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getDaysTo

Liefert den Unterschied zwischen Epochen in Tagen zurück.

**Syntax**

```auto
fieldValue.getDaysTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getDaysTo(t2); // Liefert den Unterschied in Tagen zurück: 792
t2.getDaysTo(t1); // Liefert den Unterschied in negativen Tagen zurück: -792
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Tagen zurück:

```auto
792
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Tagen benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getHoursTo

Liefert den Unterschied zwischen Epochen in Stunden zurück.

**Syntax**

```auto
fieldValue.getHoursTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getHoursTo(t2); // Liefert den Unterschied in Stunden zurück: 1908
t2.getHoursTo(t1); // Liefert den Unterschied in negativen Stunden zurück: -1908
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Stunden zurück:

```auto
1908
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Stunden benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getMinutesTo

Liefert den Unterschied zwischen Epochen in Minuten zurück.

**Syntax**

```auto
fieldValue.getMinutesTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getMinutesTo(t2); // Liefert den Unterschied in Minuten zurück: 1140480
t2.getMinutesTo(t1); // Liefert den Unterschied in negativen Minuten zurück: -1140480
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Minuten zurück:

```auto
1140480
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Minuten benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getSecondsTo

Liefert den Unterschied zwischen Epochen in Sekunden zurück.

**Syntax**

```auto
fieldValue.getSecondsTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getSecondsTo(t2); // Liefert den Unterschied in Sekunden zurück: 68428800
t2.getSecondsTo(t1); // Liefert den Unterschied in negativen Sekunden zurück: -68428800
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Sekunden zurück:

```auto
68428800
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Sekunden benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getMillisTo

Liefert den Unterschied zwischen Epochen in Millisekunden zurück.

**Syntax**

```auto
fieldValue.getMillisTo(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Epoche, die das System vergleicht. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111); // 1970-01-01T11:11:11.111Z
let t2 = t1.clone().addYears(2).addMonths(2).addDays(2);

t1.getMillisTo(t2); // Liefert den Unterschied in Millisekunden zurück: 68428800000
t2.getMillisTo(t1); // Liefert den Unterschied in negativen Millisekunden zurück: -68428800000
```

**Rückgabewerte**

Sie erhalten den Unterschied zwischen Epochen in Millisekunden zurück:

```auto
68428800000
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Unterschied zwischen Epochen in Millisekunden benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### getIsoWeekNumber

Liefert die ISO-Kalenderwoche des Jahres zurück.

**Syntax**

```auto
time.now().setTime(year, month, day).getIsoWeekNumber()
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| year | Definiert das Jahr. | ja | – | Beispiel |
| month | Definiert den Monat. | ja | – |
| day | Definiert den Tag. | ja | – |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.now().setTime(1970, 2, 14).getIsoWeekNumber();
```

**Rückgabewerte**

Sie erhalten die ISO-Kalenderwoche des Jahres zurück.

```auto
7
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die ISO-Kalenderwoche eines Jahres benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setPattern

Setzt ein Pattern. Das gesetzte Pattern können Sie anschließend mit der Funktion [getPattern](#getPattern) auslesen.

**Syntax**

```auto
let fieldValue = time.now().setPattern('dateFormat');
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| dateFormat | Definiert das Datumsformat. | ja | – | Beispiele |

**Beispiele**

Diese Beispiele zeigen die Anwendung der Funktion.

Pattern auf deutsches Format setzen:

```auto
let time = require('common/time');

// Setzt das Pattern auf das deutsche Format
let t1 = time.now().setPattern('dd.MM.yyyy HH:mm:ss');
```

Pattern auf Standard zurücksetzen (ISO-Zeitzonen-Datums-Format)

```auto
let time = require('common/time');

// Setzt das Pattern auf Standard zurück  (ISO-Zeitzonen-Datums-Format)
let t1 = time.now().setPattern(time.DEFAULT_PATTERN);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Pattern setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setFirstDayOfWeek

Setzt den ersten Tag der Woche auf einen bestimmten Tag. Den gesetzten Tag können Sie anschließend mit der Funktion [getFirstDayOfWeek](#getFirstDayOfWeek) auslesen.

**Syntax**

```auto
let fieldValue = time.now().setFirstDayOfWeek(time.DAY);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| time.DAY | Definiert den Tag, den das System als ersten Tag der Woche setzt. Verwenden Sie als Tage die Konstanten. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt den ersten Tag der Woche auf Sonntag
let t1 = time.now().setFirstDayOfWeek(time.SUNDAY);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den ersten Tag der Woche setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setZoneByOffsetId

Setzt eine Zeitzone anhand einer Offset-ID. Die gesetzte Offset-ID der Zeitzone können Sie anschließend mit der Funktion [getZoneOffsetId](#getZoneOffsetId) auslesen.

Es erfolgt keine automatische Umwandlung von MEZ <-> MESZ.

**Syntax**

```auto
let fieldValue = time.now().setZoneByOffsetId('offset');
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| offset | Definiert den Offset für die Zeitzone. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.now().setZoneByOffsetId('+0100');
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Zeitzone anhand einer Offset-ID setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setZoneById

Setzt eine Zeitzone anhand einer ID. Alle möglichen Zeitzonen können Sie mit der Konstanten *time.ZONE\_IDS;* abfragen.

Ermöglicht eine automatische Umwandlung von MEZ <-> MESZ.

**Syntax**

```auto
time.now().setZoneById('ID');
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| ID | Definiert die Zeitzone als ID. Zeitzonen fragen Sie mit der Konstanten time.ZONE\_IDS; ab. | ja | . | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.now().setZoneById('Europe/Berlin');
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie die Zeitzone anhand einer ID setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setZoneByOffsetSeconds

Setzt eine Zeitzone anhand von Offset-Sekunden. Es erfolgt keine automatische Umwandlung von MEZ <-> MESZ.

**Syntax**

```auto
let fieldValue = time.now().setZoneByOffsetSeconds(seconds);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| seconds | Definiert die Sekunden für den Offset der Zeitzone. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time ');

time.now().setZoneByOffsetSeconds(3600);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine Zeitzone anhand von Offset-Sekunden setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setFromDateObject

Setzt das Datum anhand eines JavaScript-Date-Objekts. Das JavaScript-Date-Objekt können Sie anschließend mit der Funktion [getDateObject](#getDateObject) auslesen.

**Syntax**

```auto
time.now().setFromDateObject(new Date(year, month, day));
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| year | Definiert das Jahr. | ja | – | Beispiel |
| month | Definiert den Monat. | ja | – |
| day | Definiert den Tag. | ja | – |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.now().setFromDateObject(new Date(2022, 03, 11));
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Datum anhand eines JavaScript-Date-Objekts setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setEpoch

Setzt das Datum auf die Epoche-Millisekunde.

**Syntax**

```auto
time.now().setEpoch(milliseconds);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| milliseconds | Definiert die Epoche-Millisekunden. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf die entsprechende Epoche-Millisekunde: 01.01.1970 00:00:00.000
time.now().setEpoch(0);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf die Epoche-Millisekunde setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setTime

Setzt ein Datum anhand der eingegebenen Parameter.

**Syntax**

```auto
time.now().setTime(year, month, day, hour, minute, second, millisecond);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| year | Definiert das Jahr. | ja | – | Beispiel |
| month | Definiert den Monat. | ja | – |
| day | Definiert den Tag. | ja | – |
| hour | Definiert die Stunde. | ja | – |
| minute | Definiert die Minute. | ja | – |
| second | Definiert die Sekunde. | ja | – |
| millisecond | Definiert die Millisekunde. | ja | – |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum anhand der eingegebenen Parameter, hier: 11.03.2022 20:15:30.404
time.now().setTime(2022, 03, 11, 20, 15, 30, 404);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum anhand der eingegebenen Parameter setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setYear

Setzt ein bestimmtes Jahr.

**Syntax**

```auto
time.fromEpoch(milliseconds).setYear(year);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| year | Definiert das Jahr, das das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Jahr auf 1984 => 01.01.1984 11:11:11.111
time.fromEpoch(40271111).setYear(1984);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein bestimmtes Jahr setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setMonth

Setzt einen bestimmten Monat.

**Syntax**

```auto
time.fromEpoch(milliseconds).setMonth(month);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| month | Definiert den Monat, den das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt den Monat auf 12 => 01.12.1970 11:11:11.111
time.fromEpoch(40271111).setMonth(12);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen bestimmten Monat setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setDay

Setzt einen bestimmten Tag.

**Syntax**

```auto
time.fromEpoch(milliseconds).setDay(day);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| day | Definiert den Tag, den das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt den Tag auf 24 => 24.01.1970 11:11:11.111
time.fromEpoch(40271111).setDay(24);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen bestimmten Tag setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setDayOfYear

Setzt das Datum auf einen bestimmten Tag eines Jahres.

**Syntax**

```auto
time.fromEpoch(milliseconds).setDayOfYear(day);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| day | Definiert den Tag des Jahres, den das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den 48. Tag des Jahres => 17.02.1970 11:11:11.111
time.fromEpoch(40271111).setDayOfYear(48);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Datum auf einen bestimmten Tag eines Jahres setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setWeekOfMonth

Setzt das Datum auf eine bestimmte Woche eines Monats.

**Syntax**

```auto
time.fromEpoch(40271111).setWeekOfMonth(week);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| week | Definiert die Woche eines Monats, die das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den Wochenstart (hier Montag) der dritten Woche des aktuellen Monats (hier Januar) => 19.01.1970 11:11:11.111
time.fromEpoch(40271111).setWeekOfMonth(3);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Datum auf eine bestimmte Woche eines Monats setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setHour

Setzt eine bestimmte Stunde.

**Syntax**

```auto
time.fromEpoch(milliseconds).setHour(hour);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| hour | Definiert die Stunde, die das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Stunde auf 20 => 01.01.1970 20:11:11.111
time.fromEpoch(40271111).setHour(20);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine bestimmte Stunde setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setMinute

Setzt eine bestimmte Minute.

**Syntax**

```auto
time.fromEpoch(milliseconds).setMinute(minute);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| minute | Definiert die Minute, die das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Minute auf 15 => 01.01.1970 11:15:11.111
time.fromEpoch(40271111).setMinute(15);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine bestimmte Minute setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setSecond

Setzt eine bestimmte Sekunde.

**Syntax**

```auto
time.fromEpoch(milliseconds).setSecond(second);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| second | Definiert die Sekunde, die das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Sekunde auf 30 => 01.01.1970 11:11:30.111
time.fromEpoch(40271111).setSecond(30);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine bestimmte Sekunde setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setMilli

Setzt eine bestimmte Millisekunde.

**Syntax**

```auto
time.fromEpoch(milliseconds).setMilli(milliseconds);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| milliseconds | Definiert die Millisekunde, die das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Millisekunde auf 404 => 01.01.1970 11:11:11.404
time.fromEpoch(40271111).setMilli(404);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine bestimmte Millisekunde setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setNano

Setzt eine bestimmte Nanosekunde.

**Syntax**

```auto
time.fromEpoch(milliseconds).setNano(nanosecond);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| nanosecond | Definiert die Nanosekunde, die das System setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Nanosekunde auf 404 => 01.01.1970 11:11:11:.000000404
time.fromEpoch(40271111).setNano(404);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine bestimmte Nanosekunde setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToMidnight

Setzt die Zeit auf Mitternacht.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToMidnight();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt die Zeit auf Mitternacht => 01.01.1970 00:00:00.000
time.fromEpoch(40271111).setToMidnight();
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie eine Zeit auf Mitternacht setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToPrevious

Setzt das Datum auf einen vorhergehenden bestimmten Tag.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToPrevious(time.DAY);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| time.DAY | Definiert den vorhergehenden Tag, auf den das System das Datum setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den vorhergehenden Donnerstag => 25.12.1969 11:11:11.111
time.fromEpoch(40271111).setToPrevious(time.THURSDAY);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf einen vorgehenden bestimmten Tag setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToPreviousOrSame

Setzt das Datum auf einen vorhergehenden bestimmten Tag und liefert den aktuellen Tag zurück, wenn dieser Tag der aktuelle Tag ist.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToPreviousOrSame(time.DAY);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| time.DAY | Definiert den vorhergehenden Tag, auf den das System das Datum setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den jüngsten Donnerstag; gibt den aktuellen Tag zurück, wenn es ein Donnerstag ist. => 01.01.1970 11:11:11.111
time.fromEpoch(40271111).setToPreviousOrSame(time.THURSDAY);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Datum auf einen vorhergehenden bestimmten Tag setzen und den aktuellen Tag erhalten möchten, wenn dieser Tag der aktuelle Tag ist.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToNext

Setzt das Datum auf einen nächsten bestimmten Tag.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToNext(time.DAY);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| time.DAY | Definiert den nächsten Tag, auf den das System das Datum setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den nächsten Donnerstag; gibt den aktuellen Tag zurück, wenn es ein Donnerstag ist. => 08.01.1970 11:11:11.111
time.fromEpoch(40271111).setToNext(time.THURSDAY);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Datum auf einen nächsten bestimmten Tag setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToNextOrSame

Setzt das Datum auf einen nächsten bestimmten Tag und liefert den aktuellen Tag zurück, wenn dieser Tag der aktuelle Tag ist.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToNextOrSame(time.DAY);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| time.DAY | Definiert den nächsten Tag, auf den das System das Datum setzt. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den nächsten Donnerstag; gibt den aktuellen Tag zurück, wenn es ein Donnerstag ist. => 01.01.1970 11:11:11.111
time.fromEpoch(40271111).setToNextOrSame(time.THURSDAY);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf einen nächsten bestimmten Tag setzen oder den aktuellen Tag erhalten möchten, wenn dieser Tag der aktuelle Tag ist.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToFirstDayOfWeek

Setzt das Datum auf den ersten Tag einer Woche.

* Den ersten Tag einer Woche können Sie mit der Funktion [setFirstDayOfWeek](#setFirstDayOfWeek) setzen.
* Wenn Sie den ersten Tag der Woche nicht setzen, gilt automatisch Montag als erster Tag der Woche.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToFirstDayOfWeek();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111)
.setFirstDayOfWeek(time.FRIDAY) // Setzt den ersten Tag der Woche auf Freitag
.setToFirstDayOfWeek(); // Setzt das Datum auf den ersten Tag der aktuellen Woche. 01.01.1970 = Donnerstag -> Letzter Tag der Woche. Das System setzt das Datum entsprechend auf den vorhergehenden Freitag: 26.12.1969 11:11:11.111
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf den ersten Tag einer Woche setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToLastDayOfWeek

Setzt das Datum auf den letzten Tag einer Woche.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToLastDayOfWeek();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111)
.setFirstDayOfWeek(time.THURSDAY) // Setzt den ersten Tag der Woche auf Donnerstag
.setToLastDayOfWeek(); // Setzt das Datum auf den letzten Tag der aktuellen Woche. 01.01.1970 = Donnerstag -> Erster Tag der Woche. => Letzter Tag der Woche = Mittwoch. Das System setzt das Datum entsprechend auf den nachfolgenden Mittwoch: 07.01.1970 11:11:11.111
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf den letzten Tag einer Woche setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToFirstDayOfMonth

Setzt das Datum auf den ersten Tag eines Monats.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToFirstDayOfMonth();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111)
.setMonth(2).setDay(14) // Setzt das Datum auf den 14.02.1970
.setToFirstDayOfMonth(); // Setzt das Datum auf den Monatsersten: 01.02.1970 11:11:11.111
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf den ersten Tag eines Monats setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToLastDayOfMonth

Setzt das Datum auf den letzten Tag eines Monats.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToLastDayOfMonth();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111)
.setMonth(2).setDay(14) // Setzt das Datum auf den 14.02.1970
.setToLastDayOfMonth(); // Setzt das Datum auf den Monatsletzten: 28.02.1970 11:11:11.111
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf den letzten Tag eines Monats setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToFirstDayOfYear

Setzt das Datum auf den ersten Tag eines Jahres.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToFirstDayOfYear();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111)
.setMonth(2).setDay(14) // Setzt das Datum auf den 14.02.1970
.setToFirstDayOfYear(); // Setzt das Datum auf den ersten Tag des entsprechenden Jahres: 01.01.1970 11:11:11.111
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf den ersten Tag eines Jahres setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToLastDayOfYear

Setzt das Datum auf den letzten Tag eines Jahres.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToLastDayOfYear();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111)
.setMonth(2).setDay(14) // Setzt das Datum auf den 14.02.1970
.setToLastDayOfYear(); // Setzt das Datum auf den letzten Tag des entsprechenden Jahres: 31.12.1970 11:11:11.111
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum auf den letzten Tag eines Jahres setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### setToIsoWeek

Setzt das Datum auf einen gleichen Wochentag einer Kalenderwoche eines Jahres.

**Syntax**

```auto
time.fromEpoch(milliseconds).setToIsoWeek(year, week);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| year | Definiert das Jahr. | ja | – | Beispiel |
| week | Definiert die Woche. | ja | – |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

// Setzt das Datum auf den gleichen Wochentag in KW 7 des Jahres 1970. Da der 01.01.1970 ein Donnerstag ist, setzt das System das Datum auf den Donnerstag von KW 7: 12.02.1970 00:00:00.000 [UTC]
time.fromEpoch((40271111)).setToIsoWeek(1970, 7);
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie das Datum auf einen gleichen Wochentag einer Kalenderwoche eines Jahres setzen möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### clone

Kopiert den Zustand / das Datum eines Objekts.

**Syntax**

```auto
let fieldValue = fieldValue.clone();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.now(); // Holt die aktuelle Uhrzeit und das Datum
let t2 = t1.clone(); // Kopiert den Zustand / das Datum von t1
t1.setToMidnight(); // Setzt t1 auf Mitternacht, t2 bleibt unberührt
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie den Zustand / das Datum eines Objekts kopieren möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parse

Liest einen String ein und versucht, diesen in ein Datumsobjekt mit Uhrzeit umzuwandeln.

**Syntax**

```auto
let fieldValue = time.now().parse(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Variable, die das System parst. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let date1 = '2022-12-24T18:30:00.000+0100[Europe/Berlin]';
let t1 = time.now().parse(date1); // Setzt nur die Uhrzeit
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String in ein Datumsobjekt mit Uhrzeit umwandeln möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### parseZoned

Liest einen String ein und versucht, dieses in ein Datumsobjekt mit Uhrzeit und Zeitzone umzuwandeln.

**Syntax**

```auto
let fieldValue = time.now().parseZoned(fieldValue);
```

**Parameter**

Diese Parameter existieren in der Funktion:

| Parameter | Beschreibung | Pflicht | Standard | Weitere Informationen |
| --- | --- | --- | --- | --- |
| fieldValue | Definiert die Variable, die das System parst. | ja | – | Beispiel |

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let date2 = '2022-12-24T18:30:00[Japan]';
let t2 = time.now().parseZoned(date2); // Setzt Uhrzeit und Zeitzone
```

**Rückgabewerte**

Sie erhalten die aktuelle Time-Instanz zurück.

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie einen String in ein Datumsobjekt mit Uhrzeit und Zeitzone umwandeln möchten.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### toString:

Liefert ein Datum als String zurück.

**Syntax**

```auto
fieldValue.toString();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

let t1 = time.fromEpoch(40271111);
t1.setPattern('dd.MM.yyyy').toString();
```

**Rückgabewerte**

Sie erhalten das Datum im Format des angegebenen Patterns in der konfigurierten Zeitzone:

```auto
'01.01.1970'
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum als String benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### toISOString:

Liefert ein Datum als JavaScript verständlichen String in UTC zurück.

**Syntax**

```auto
fieldValue.toISOString();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Beispiel**

Dieses Beispiel zeigt die Anwendung der Funktion.

```auto
let time = require('common/time');

time.fromEpoch(40271111).toISOString();
```

**Rückgabewerte**

Sie erhalten das Datum als ISO-String in der Zeitzone UTC:

```auto
'1970-01-01T11:11:11.111Z'
```

**Verwendung**

Diese Funktion verwenden Sie, wenn Sie ein Datum als ISO-String benötigen.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

### Konstanten

* * *

| Konstante | Beschreibung | Link |
| --- | --- | --- |
| time.DEFAULT\_PATTERN; | Setzt das Standard-Pattern für das ISO-Zeitzonen-Datums-Format zurück. | Pattern auf Standard zurücksetzen (ISO-Zeitzonen-Datums-Format |
| time.ZONE\_IDS; | Listet alle möglichen Zeitzonen auf. Die Bezeichnungen benötigen Sie für die Funktion setZoneById. | – |
| time.MONDAY; | Repräsentiert den Wochentag Montag mit Wert =1. | Die Wochentage benötigen Sie für die Funktionen: setFirstDayOfWeek setToPrevious setToPreviousOrSame setToNext setToNextOrSame |
| time.TUESDAY; | Repräsentiert den Wochentag Dienstag mit Wert =2. |
| time.WEDNESDAY; | Repräsentiert den Wochentag Mittwoch mit Wert =3. |
| time.THURSDAY; | Repräsentiert den Wochentag Donnerstag mit Wert =4. |
| time.FRIDAY; | Repräsentiert den Wochentag Freitag mit Wert =5. |
| time.SATURDAY; | Repräsentiert den Wochentag Samstag mit Wert =6. |
| time.SUNDAY; | Repräsentiert den Wochentag Sonntag mit Wert =7. |

### Anwendungsbeispiele

* * *

#### Wert eines Datum-Metadatums verarbeiten

```auto
let time = require('common/time');

let today = new Date();
time.fromEpoch(today).addYears(52).getDateObject();
```

## JavaScript-Bibliothek common/transaction

Diese Bibliothek bietet Funktionen zum Ablaufen von Modifikationen in Transaktionen.

### Regeln für Transaktionen

* * *

* Eine Transaktion ist fest an einen Thread gebunden, außerhalb davon ist sie nicht sichtbar.
* Tritt während einer laufenden Transaktion ein Fehler auf, [rollen Sie die Transaktion zurück](#Beispiel3). Ansonsten können Inkonsistenzen entstehen (kein try-catch-ignore).
* Der Index wird frühestens nach Ende einer Transaktion aktualisiert, vorher sind Änderungen nicht sichtbar.
* Transaktionen dürfen nicht zu lange laufen und nicht zu viele Objekte innerhalb einer Transaktion verarbeiten. Ansonsten können Deadlocks auftreten.
* Wenn viele Objekte verarbeitet werden sollen, teilen Sie die Menge in Teilblöcke unter.
* In der Regel wird innerhalb der Iteration über alles mit einem Modulo einer gewissen Menge gearbeitet, etwa 100, und ein *transaction.restart()* ausgeführt. Dadurch wird die Transaktion bis dahin commited und neu gestartet.
* Zu große Transaktionen können bei einem Neustart dazu führen, dass das System für den Neustart lange benötigt, da die Transaktion abgebrochen wird und komplett [zurückgerollt](#Beispiel3) werden muss.
* In Bezug auf andere Systeme wirken Transaktionen nicht oder müssen gesondert beachtet werden (siehe Beispiel).

**Beispiel**: *agorum core* schickt Daten per API an DATEV oder an eine andere Schnittstelle. Tauchen währenddessen im Workflow oder im ausführenden Skript Fehler auf, rollt *agorum core* die Transaktion zwar zurück, das Fremdsystem jedoch nicht. Das kann dazu führen, dass doppelt oder falsch gebucht wird. Planen Sie den Prozess so, dass diese Fehler nicht in der gleichen Transaktion stattfinden, oder entwickeln Sie ein Konzept, um der API mitzuteilen, dass die Daten ungültig sind.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let transaction = require('common/transaction');
```

### Aufruf

* * *

```auto
transaction(timeout, (t) => callback(t));
```

#### Parameter

| Parameter | Beschreibung | Standard |
| --- | --- | --- |
| timeout | Definiert in Sekunden, wie lange die Transaktion maximal dauern darf. Wenn diese Zeit abgelaufen ist, wird die Transaktion abgebrochen und es wird ein Rollback ausgeführt. | \-1  (Time-out wird nicht berücksichtigt, die Transaktion kann beliebig lange laufen.) |
| callback | Definiert die zu übergebene Funktion, die innerhalb der Transaktion ausgeführt wird. Läuft diese Funktion ohne Fehler durch, wird am Ende automatisch ein Commit durchgeführt. Wird ein Fehler geworfen, so wird stattdessen ein Rollback durchgeführt.​​​​​​ Der Funktion wird als Parameter eine Referenz auf das Transaktions-Objekt übergeben. Für kleinere Transaktionen ist dieses typischerweise nicht nötig, aber bei der Verarbeitung von größeren Datenmengen muss die Transaktion regelmäßig über t.restart() neu gestartet werden. Hinweis: Rollen Sie die Transaktion nicht manuell zurück, sondern verwenden Sie den automatischen Rollback, indem ein geeigneter Fehler per throw geworfen wird. Nur so ist sichergestellt, dass der Transaktionsblock nach dem Rollback korrekt verlassen wird. Folgende Funktionen bietet der Parameter t an: restart Führt einen Commit aus und startet sofort eine neue Transaktion. Es existieren keine weiteren Parameter für restart. | – |

**Allgemein mit Time-out in Millisekunden (ms)**

```auto
let obj = require('common/objects'),
    transaction = require('common/transaction');

let timeout = 300; // Maximal 5 Minuten

transaction(timeout, t => {
  // Alles was hier drin abläuft wird in einer Transaktion gemacht
});
```

**Allgemein ohne Time-out**

Der Time-out wird auf den Standard *\-1* gesetzt.

```auto
let transaction = require('common/transaction');

transaction(t => {
  // Alles, was hier drin abläuft, wird in einer Transaktion gemacht
});
```

### Beispiele

* * *

#### Beispiel 1

Nachfolgendes Beispiel zeigt eine Iteration über alle Objekte, bei der der Name eines jeden gefundenen Objekts umgesetzt wird. Es werden immer 50 Objekte in einer Transaktion umgesetzt.

```auto
let obj = require('common/objects');
let transaction = require('common/transaction');

function forEach(query, threshold, callback) {
  transaction(t => {
    let c = 0;

    obj.query(query).forEach(object => {
      if (++c > threshold) {
        t.restart();
        c = 0;
      }

      callback(object);
    });
  });
}

let ret = [];

forEach('name:("Dokumente" NOT "Sonstige_Dokumente") area:(Vorgangsdokumente NOT "Vorgangsdokumente - Ablage")', 50, object => {
  object.name = "Sonstige_Dokumente";
  ret.push(object.ID);
});

ret;
```

#### Beispiel 2

Nachfolgendes Beispiel zeigt, wie jede Änderung innerhalb einer Schleife als einzelne Transaktion durchgeführt wird.

```auto
// Delete DocumentTextObjects
// Unten in den Aufruf: clear(..) das entsprechende Suchmuster einstellen.
// Mit diesem Script kann das selbe gemacht werden wie unter desk4web Tooles 'Delete Document Text of objects'

let IndexHelper = Packages.agorum.roi.searchengine.IndexHelper;
let MessageUtils = Packages.agorum.roi.ejb.messaging.common.MessageUtils;
let MessageBean = Packages.agorum.roi.ejb.messaging.common.MessageBean;

let objects = require('common/objects');
let transaction = require('common/transaction');

function clear(query) {
  let count = 0;
  let mu = new MessageUtils();

  objects.query(query).forEach(object => {
    transaction(() => {
      IndexHelper.disableRealtimeIndex();

      object.deleteDocumentText();

      let mb = new MessageBean();

      mb.setObjectProperty('value', new java.lang.Long(object.getId()));
      mb.setObjectProperty('eventType', 'updateObjectListener');
      mb.setObjectProperty('className', object.className);
      mb.setObjectProperty('NoEventAssistanceObject', '');

      mu.publishToTopic('updateObjectListener', mb, true);

      ++count;
    });
  });

  return count;
}

clear('nameextension:(html OR htm OR txt OR json OR xml)');
```

#### Beispiel 3

Nachfolgendes Beispiel zeigt, wie Sie eine Transaktion nach einer gewissen Zeit und nicht nach x Durchgängen neu starten.

```auto
let transaction = require('common/transaction');

// Definiere die Abbruchfunktion
// nach x Sekunden wird der übergebene callback ausgeführt
let periodic = (period, fn) => {
  let next = Date.now() + period;

  return () => {
    if (Date.now() > next) {
      fn();
      next = Date.now() + period;
    }
  };
};

transaction(t => {
  // ...

  // Definiere genaue Funktion, in dem Fall wird bei jedem Transaktionsneustart auch ein flush auf ein Logfile ausgeführt
  // Die Periode wird auf 30 Sekunden gesetzt
  let auto = periodic(30 * 1000, () => {
    ow.flush();
    t.restart();
  });

  // z. B. Schleife oder forEach
  // In dieser Schleife wird regelmäßig geprüft, ob die Zeit um ist und erneut ausgeführt werden muss
  while (...) {

    // ...
    auto();
    // ...
  }
});
```

#### Beispiel 3

Nachfolgendes Beispiel zeigt, wie Sie eine Transaktion zurückrollen.

```auto
transaction(t => {
  // Alles, was hier drin abläuft, wird in einer Transaktion gemacht

  throw new Error('Transaktion beenden und rollback machen');
});
```

## JavaScript-Bibliothek common/xml

**Ab welcher Version nutzbar?**• *agorum core* 8.1.10

Diese Bibliothek bietet Funktionen zum Parsen oder Ausführen von XML-Dateien (agoscript) oder zum Parsen oder Erstellen allgemeingültiger XML-Dateien.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let xml = require('common/xml');
```

### Funktionen

* * *

#### read()

Liest XML-Dateien aus.

**A​ufruf**

```auto
let xml = require('common/xml');
let objects = require('common/objects');

let obj = objects.find('id oder Pfad eines XML-Files');
let result = xml.read(obj);
```

**Rückgabewert**

Sie erhalten eine Objektstruktur, die Sie direkt in JavaScript lesen können.

**Hinweis**: Neben Objekten akzeptiert die Funktion auch Streams und Strings. Bei letzteren ist der Aufrufer selbst dafür verantwortlich, eventuelle Eingangsdaten im korrekten Encoding zu lesen.

**Beispiel**

```auto
<test>
  <knoten1>Inhalt 1</knoten1>
  <knoten2 attr1="Inhalt Attr 1">Inhalt 2</knoten2>
  <knoten3 attr2="Inhalt Attr 2">
    <knoten3sub>Inhalt 3.1</knoten3sub>
    <knoten3sub>Inhalt 3.2</knoten3sub>
    <knoten3sub>Inhalt 3.3</knoten3sub>
  </knoten3>
  <knoten4 attr3="Inhalt Attr 3">
    <knoten4sub1>Inhalt 4.1</knoten4sub1>
    <knoten4sub2>Inhalt 4.1</knoten4sub2>
  </knoten4>
</test>
```

**Ergebnis**

```auto
{
  "test": {
    "knoten1": "Inhalt 1",
    "knoten2": {
      "~attr1": "Inhalt Attr 1",
      "#text": "Inhalt 2"
    },
    "knoten3": {
      "~attr2": "Inhalt Attr 2",
      "knoten3sub": [
        "Inhalt 3.1",
        "Inhalt 3.2",
        "Inhalt 3.3"
      ]
    },
    "knoten4": {
      "~attr3": "Inhalt Attr 3",
      "knoten4sub1": "Inhalt 4.1",
      "knoten4sub2": "Inhalt 4.1"
    }
  }
}
```

* Attribute werden als Element mit einer *~* eingefügt.
* Wenn das einzige Subelement ein Text ist, wird der Wert direkt zugeordnet.
* Wenn sich auf gleicher Ebene noch mehr Elemente befinden, wird der Text mit *#text* eingefügt.

#### run()

Führt agoscript-Skripte aus.

* Die Übergabe erfolgt als Objekt innerhalb von *agorum core*, als InputStream oder als String
* Beim manuellen Auslesen einer Datei als String (etwa, um vor der Übergabe an *run()* noch Platzhalter zu ersetzen) muss auf die korrekte Codierung geachtet werden.
* Wird das Skript als Objekt oder Stream übergeben, kümmert sich der Parser selbst um die Decodierung laut XML-Header.

**Rückgabewerte**

Sie erhalten die in dem jeweiligen Skript definierten XmlReturn-Werte.

**Beispiel**

```auto
let xml = require('common/xml');
let objects = require('common/objects');

let script = objects.find('/agorum/roi/customers/test/xml/test.xml');
let folder = objects.find('/agorum/roi/Files/test');

// führt das script test.xml im Kontext des Ordners /agorum/roi/Files/test aus
xml.run(script, folder);
```

Der zweite Parameter für den Ordner ist optional. Wird er nicht angegeben, wird stattdessen der Root-Ordner als Kontext verwendet.

#### parse()

**Ab welcher Version nutzbar?**• *agorum core* 9.3.0

Wandelt allgemeingültige XML-Dateien und Strukturen in ein für JavaScript angenehmes Format.

* Die Übergabe erfolgt als Objekt innerhalb von *agorum core*, als InputStream oder als String.
* Beim manuellen Auslesen einer Datei als String (etwa, um vor der Übergabe an *run()* noch Platzhalter zu ersetzen) muss auf die korrekte Codierung geachtet werden.
* Wird das Skript als Objekt oder Stream übergeben, kümmert sich der Parser selbst um die Decodierung laut XML-Header.

**Rückgabewerte**

Sie erhalten eine JavaScript-Objektstruktur mit den Inhalten der geparsten XML-Struktur.

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| source | Definiert einen String, ein agorum core-Objekt oder ein Stream, der die XML-Daten enthält. |
| parameters (Optional) | Definiert zusätzliche Parameter als Parameter-Objekt. |

```auto
// Liste der verfügbaren Parameter
let parameters = {
  ignoreNamespaces: true  // deaktiviert die Validierung der XML-Namespaces
}
```

**Beispiel**

```auto
let xml = require('common/xml');
xml.parse('<CdataTest><xyz><![CDATA[vor innerem cdata <![CDATA[test]]]]><![CDATA[> nach innerem cdata]]></xyz></CdataTest>');
```

**Ergebnis**

```auto
{
  children: [
    {
      children: [],
      name: 'xyz',
      attributes: [],
      type: 'ElementNode',
      value: 'vor innerem cdata <![CDATA[test]]> nach innerem cdata'
    }
  ],
  name: 'CdataTest',
  attributes: [],
  type: 'ElementNode'
}
```

#### streamify()

**Ab welcher Version nutzbar?**• *agorum core* 9.3.0

Überführt eine XML-JavaScript-Struktur in eine gültige XML-Struktur.

Die Übergabe erfolgt als JavaScript-Struktur.

**Rückgabewerte**

Sie erhalten einen InputStream, der dazu verwendet werden kann, um direkt in Dateien schreiben zu können oder APIs anzusprechen.

**Beispiel**

```auto
let xml = require('common/xml');
xml.stringify({
  children: [
    {
      children: [],
      name: 'xyz',
      attributes: [],
      type: 'ElementNode',
      value: 'vor innerem cdata <![CDATA[test]]> nach innerem cdata'
    }
  ],
  name: 'CdataTest',
  attributes: [],
  type: 'ElementNode'
}, {forceCDATA: true}); // optionaler Parameter, siehe folgende Tabelle
```

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| forceCDATA | Ab welcher Version verfügbar? • agorum core 10.0.4 true Legt für jeden Wert, der in das XML geschrieben wird, einen CDATA-Bereich an (etwa bei value). false Legt keine CDATA-Bereiche in den XML-Werten an. |

#### stringify()

**Ab welcher Version nutzbar?**• *agorum core* 9.3.0

Überführt eine XML-JavaScript-Struktur in eine gültige XML-Struktur.

Die Übergabe erfolgt als JavaScript-Struktur.

**Hinweis**: Sie müssen zuvor die Funktion [parse()](#parse) angewandt haben, um das XML in eine gültige XML-Struktur zu überführen. Die Funktion [read()](#read) gibt lediglich eine simple Struktur des XML zurück, die zwar ausreicht, um die Daten zu extrahieren, jedoch nicht, um diese zuverlässig zurück zu überführen.

**Rückgabewerte**

Sie erhalten einen String mit einer gültigen XML-Struktur.

**Beispiel**

```auto
let xml = require('common/xml');
xml.stringify({
  children: [
    {
      children: [],
      name: 'xyz',
      attributes: [],
      type: 'ElementNode',
      value: 'vor innerem cdata <![CDATA[test]]> nach innerem cdata'
    }
  ],
  name: 'CdataTest',
  attributes: [],
  type: 'ElementNode'
}, {forceCDATA: true}); // optionaler Parameter, siehe folgende Tabelle
```

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| forceCDATA | Ab welcher Version verfügbar? • agorum core 10.0.4 true Legt für jeden Wert, der in das XML geschrieben wird, einen CDATA-Bereich an (etwa bei value). false Legt keine CDATA-Bereiche in den XML-Werten an. |

**Ergebnis**

Mit Parameter *forceCDATA* auf *true*:

```auto
<?xml version="1.0" encoding="UTF-8"?><CdataTest><xyz><![CDATA[vor innerem cdata <![CDATA[test]]]]><![CDATA[> nach innerem cdata]]></xyz></CdataTest>
```

Ohne Parameter *forceCDATA* oder auf *false*:

```auto
<?xml version="1.0" encoding="UTF-8"?><CdataTest><xyz>vor innerem cdata &lt;![CDATA[test]]&gt; nach innerem cdata</xyz></CdataTest>
```

### XML-JavaScript-Struktur

* * *

**Ab welcher Version nutzbar?**• *agorum core* 9.3.0

Die Methoden [parse()](#parse), [streamify()](#streamify) und [stringify()](#stringify) arbeiten mit der XML-JavaScript-Struktur. Die Struktur abstrahiert eine XML-Struktur auf eine in JavaScript verwendbare Objektnotation. Auf dieser Objektnotation kann ein JavaScript durch die Informationen des XML traversieren und gegebenenfalls manipulieren.

Die Struktur besitzt ein bestimmtes Format, das an dieser Stelle näher erläutert wird.

### Allgemeines Format der verschiedenen Bausteine

* * *

Das Format für die verschiedenen Bausteine innerhalb der Struktur ist grundsätzlich gleich. Die Bausteine unterscheiden sich lediglich in der Interpretation des Formats bei der Erzeugung der XML-Struktur oder wenn das Format aus der XML-Struktur erzeugt wurde:

| Format | Beschreibung |
| --- | --- |
| name | Definiert den Namen der Struktur oder des Tags innerhalb der XML-Struktur. Der Name muss den allgemeinen Richtlinien für Tags innerhalb von XML-Strukturen entsprechen. |
| type | Definiert den Typ der Struktur oder des Bausteins. Wenn Sie den Typ des Bausteins nicht angeben, geht die Bibliothek davon aus, dass es sich um eine Element-Node handelt. |
| value | Definiert den geltenden Wert für den Baustein. Nähere Einschränkungen und Beschreibung zur Verwendung des values finden Sie in den Beschreibungen der Bausteine. |
| attributes | Definiert Attribute für den Baustein, die in der XML-Struktur ebenfalls als Attribute auf Tag-Ebene zu finden sind. Die Definition der Attribute ist ein Array bestehend aus einer Objektnotation, die name und value enthält. { name: 'Name des Attributes', value: 'Value des Attributes' } |
| children | Definiert ein Array aus weiteren Bausteinen oder Knotendefinitionen, um die weitere Struktur der XML-Struktur zu repräsentieren. |

### Bausteine verwenden und kombinieren

* * *

Die folgenden Bausteine können Sie in der Struktur verwenden und kombinieren.

#### Element-Node

Ein Element-Node ist ein allgemeiner Knoten, der verwendet werden kann, um:

* weitere Knoten aufzunehmen (eine neue Verschachtelungstiefe einzuführen)
* Textinhalte in einer Struktur einzufügen.
* Text- und CDATA-Nodes zu repräsentieren.

Ein Element-Node ist der Standard, wenn kein Typ in der Struktur angegeben wird.

* Ist in einer XML-Struktur einer der beiden Knoten vorhanden, wird eine Element-Node mit einem *value* erzeugt.
* *value* entspricht dabei dem Wert aus dem Text- und CDATA-Node.
* Es werden auch mehrere aufeinanderfolgende Text- und CDATA-Nodes zusammengefasst und gemeinsam im Parameter *value* zur Verfügung gestellt.
* Soll ein Text- bzw. CDATA-Node in einer XML-Struktur erzeugt werden, muss ein Element-Node mit dem Parameter *value* erzeugt werden. Bei der Generierung der XML-Struktur wird geprüft, ob der Parameter *value* in der Element-Node angegeben ist und wenn ja, wird automatisch und immer ein oder mehrere CDATA-Nodes erstellt.

Der Element-Node kann weitere Nodes zugewiesen werden. Diese müssen im Schlüssel *children* hinterlegt werden.

Wenn die Node Attribute besitzen soll, können diese über den Schlüssel *attributes* der Node zugewiesen werden.

Der Typ der Element-Node ist als Konstante in der Bibliothek verfügbar und kann über den Wert ELEMENT\_NODE verwendet werden.

```auto
{
  name: 'ElementNode',
  type: xml.ELEMENT_NODE,
  value: 'Wert 123',
  attributes: [],
  children: []
}
```

#### Processing-Instruction-Node

Ein Proccesing-Instruction-Node ist ein Knoten, der einer XML-Struktur weitere Parsing und Verarbeitungsinformationen hinterlegt. Dieser Knoten hat bei der Erstellung der XML-Struktur keine direkte Auswirkung auf die Erstellung, jedoch Auswirkung in dem Bereich, in dem die XML-Struktur geparst und interpretiert wird. Das Format des *values* einer Processing-Instruction-Node ist frei wählbar und abhängig vom gewählten Anwendungsfall.

* Der Processing-Instruction-Node können keine weiteren Knoten zugewiesen werden.
* Der Parameter *children* wird bei der Erstellung der XML-Struktur ignoriert.
* Wenn die Node Attribute besitzen soll, können diese über den Schlüssel *attributes* der Node zugewiesen werden.

Der Typ der Element-Node ist als Konstante in der Bibliothek verfügbar und kann über den Wert PROCESSING\_INSTRUCTION\_NODE verwendet werden.

```auto
{
  name: 'ProcessingInstructionNode',
  type: xml.PROCESSING_INSTRUCTION_NODE,
  value: 'id="abc"',
  attributes: []
}
```

#### Comment-Node

Ein Comment-Node ist ein Knoten, der einer XML-Struktur ein Kommentar hinzufügt.

* Der Wert einer Comment-Node wird über den Parameter *value* definiert.
* Der Comment-Node können keine weiteren Knoten zugewiesen werden.
* Der Parameter *children* wird bei der Erstellung der XML-Struktur ignoriert.
* Der Comment-Node können keine Attribute zugewiesen werden.

Der Typ der Element-Node ist als Konstante in der Bibliothek verfügbar und kann über den Wert COMMENT\_NODE verwendet werden.

```auto
{
  name: 'CommentNode',
  type: xml.COMMENT_NODE,
  value: 'Kommentar'
}
```

#### Document-Fragment-Node

Ein Document-Fragment-Node stellt einen Root-Knoten für XML-Strukturen dar, die nicht der allgemeingültigen XML-Struktur entsprechen. Hauptsächlich handelt es sich hier um XML-Strukturen, die in andere XML-Strukturen integriert werden sollen oder allgemein um XML-Strukturen, die nicht als eigenständige Struktur verwendet werden möchten. Die Document-Fragment-Node wird bei der Generierung nicht in die XML-Struktur übernommen, sondern vielmehr durch die sich unterhalb des Parameter *children* befindlichen Struktur ersetzt. Wird die Document-Fragment-Node als Root-Knoten verwendet, wird auch keine Präambel mit *<xml>...:* erzeugt.

* Ein Document-Fragment-Node kann weitere Knoten zugewiesen werden.
* Die weiteren Knoten müssen dem Parameter *children* zugewiesen werden.
* Ein Document-Fragment-Node kann keinen weiteren *value* besitzen. Daher wird bei der Erstellung der XML-Struktur der Parameter *value* ignoriert.
* Ein Document-Fragment-Node kann keine weiteren Attribute besitzen. Daher wird bei der Erstellung der XML-Struktur der Parameter *attributes* ignoriert.

Der Typ der Document-Fragment-Node ist als Konstante in der Bibliothek verfügbar und kann über den Wert DOCUMENT\_FRAGMENT\_NODE verwendet werden.

```auto
{
  name: 'DocumentFragmentNode',
  type: xml.DOCUMENT_FRAGMENT_NODE,
  children: []
}
```

### Anwendungsbeispiele

* * *

#### Attributen zu einer Node hinzufügen

```auto
{
  name: 'ElementNode',
  type: xml.ELEMENT_NODE,
  attributes: [
    {
      name: 'AttributeName1',
      value: 'AttributeValue1'
    },
    {
      name: 'AttributeName2',
      value: 'AttributeValue2'
    }
  ]
}
```

#### Text- oder CDATA-Node erstellen

```auto
{
  name: 'MyTextValue',
  type: xml.ELEMENT_NODE,
  value: 'MyValue'
}
```

#### Einfache Struktur mit einer oder mehreren Text- oder CDATA-Nodes erstellen

```auto
{
  name: 'MyElementNode',
  type: xml.ELEMENT_NODE,
  children: [
    {
      name: 'MyTextValue1',
      type: xml.ELEMENT_NODE,
      value: 'MyValue1'
    },
    {
      name: 'MyTextValue2',
      type: xml.ELEMENT_NODE,
      value: 'MyValue2'
    }
  ]
}
```

#### Struktur mit einer Document-Fragment-Node erstellen

```auto
{
  type: xml.DOCUMENT_FRAGMENT_NODE,
  children: [
    {
      name: 'ElementNode',
      type: xml.ELEMENT_NODE,
      children: [
        {
          name: 'MyTextValue1',
          type: xml.ELEMENT_NODE,
          value: 'MyValue1'
        }
      ]
    },
    {
      name: 'MyTextValue2',
      type: xml.ELEMENT_NODE,
      value: 'MyValue2'
    }
  ]
}
```

#### XML aus der REDDOXX-Schnittstelle

```auto
<?xml version="1.0" encoding="UTF-8"?>
<Reddoxx>
  <TRdxExportMetadata>
    <Id>1A540A0DC2AD4127BC551A44614FB1A71DCE5D5F</Id>
    <IndexAlias>{851235E9-F1F9-49D7-9BA0-D0E560F4248F}</IndexAlias>
    <Subject>Re:AW: [CISS] Re:Unser Gespräch am 23.07.2010</Subject>
    <MessageId>&lt;32734840.15902.1280213625807.JavaMail.root@agamd01&gt;</MessageId>
    <InReplyToId>&lt;20100726215326718DNB@reddoxx.com&gt;</InReplyToId>
    <Sender>Oliver Schulze &lt;oliver.schulze@agorum.com&gt;</Sender>
    <Score>0</Score>
    <AttachmentNameList Count="0"></AttachmentNameList>
    <AttachmentSizeList Count="0"></AttachmentSizeList>
    <ToRecipients Count="1">
      <L0>Andreas Dannenberg &lt;andreas.dannenberg@reddoxx.com&gt;</L0>
    </ToRecipients>
    <CcRecipients Count="0">
    </CcRecipients>
    <BccRecipients Count="0"></BccRecipients>
    <Size>1129860</Size>
    <Date>2010-07-27 08:53:45</Date>
    <ArchiveStamp>2010-07-27 08:54:00</ArchiveStamp>
    <StoreStamp>2010-07-27 08:54:50</StoreStamp>
    <MessageType>1</MessageType>
    <Encryption>0</Encryption>
    <Direction>2</Direction>
    <State>0</State>
    <EnvRecipients Count="1">
      <L0>andreas.dannenberg@reddoxx.com</L0>
    </EnvRecipients>
    <EnvSender>oliver.schulze@agorum.com</EnvSender>
    <Spam>0</Spam>
  </TRdxExportMetadata>
</Reddoxx>
```

####  Ergebnis von var result = xml.read(obj);

```auto
{
  "Reddoxx": {
    "TRdxExportMetadata": {
      "ArchiveStamp": "2010-07-27 08:54:00",
      "InReplyToId": "<20100726215326718DNB@reddoxx.com>",
      "Size": "1129860",
      "ToRecipients": {
        "L0": "Andreas Dannenberg <andreas.dannenberg@reddoxx.com>",
        "~Count": "1"
      },
      "EnvRecipients": {
        "L0": "andreas.dannenberg@reddoxx.com",
        "~Count": "1"
      },
      "Encryption": "0",
      "Direction": "2",
      "IndexAlias": "{851235E9-F1F9-49D7-9BA0-D0E560F4248F}",
      "Subject": "Re:AW: [CISS] Re:Unser Gespräch am 23.07.2010",
      "Date": "2010-07-27 08:53:45",
      "Spam": "0",
      "Sender": "Oliver Schulze <oliver.schulze@agorum.com>",
      "Score": "0",
      "CcRecipients": {
        "~Count": "0"
      },
      "AttachmentNameList": {
        "~Count": "0"
      },
      "EnvSender": "oliver.schulze@agorum.com",
      "BccRecipients": {
        "~Count": "0"
      },
      "State": "0",
      "Id": "1A540A0DC2AD4127BC551A44614FB1A71DCE5D5F",
      "AttachmentSizeList": {
        "~Count": "0"
      },
      "StoreStamp": "2010-07-27 08:54:50",
      "MessageType": "1",
      "MessageId": "<32734840.15902.1280213625807.JavaMail.root@agamd01>"
    }
  }
}
```

#### Programm, um die Daten aus der XML-Datei als Metadaten zu belegen

In diesem Beispiel werden die Metadaten auf das XML-Objekt selbst gesetzt:

```auto
/* global sc */

let objects = require('common/objects');
let beans = require('common/beans');
let metadata = require('filingassistant/metadata');

// ID auf die xml-Datei
let obj = objects.find('13645631');

let xml = require('common/xml');

let result = xml.read(obj);

setMetaData(obj, result);

function setMetaData(obj, xml) {
  let data = {};
  // Bereich "Reddoxx" auslesen
  let reddoxx = xml.Reddoxx;
  // Aus dem Bereich "Reddoxx" jetzt den Bereich "TRdxExportMetadata" auslesen
  let TRdxExportMetadata = reddoxx.TRdxExportMetadata;

  // Jetzt alle Metadaten aus dem Bereich "TRdxExportMetadata" auslesen
  data.reddoxx_archiveStamp             = toDate(TRdxExportMetadata.ArchiveStamp);
  data.reddoxx_inReplyToId              = isEmpty(TRdxExportMetadata.InReplyToId);

  data.reddoxx_size                     = isEmpty(TRdxExportMetadata.Size);
  data.reddoxx_toRecipients             = toArray(TRdxExportMetadata.ToRecipients, TRdxExportMetadata.ToRecipients['~Count']);
  data.reddoxx_toRecipientsCount        = TRdxExportMetadata.ToRecipients['~Count'];
  data.reddoxx_envRecipients            = toArray(TRdxExportMetadata.EnvRecipients, TRdxExportMetadata.EnvRecipients['~Count']);
  data.reddoxx_envRecipientsCount       = TRdxExportMetadata.EnvRecipients['~Count'];
  data.reddoxx_encryption               = isEmpty(TRdxExportMetadata.Encryption);
  data.reddoxx_direction                = isEmpty(TRdxExportMetadata.Direction);
  data.reddoxx_indexAlias               = isEmpty(TRdxExportMetadata.IndexAlias);
  data.reddoxx_subject                  = isEmpty(TRdxExportMetadata.Subject);
  data.reddoxx_date                     = toDate(TRdxExportMetadata.Date);
  data.reddoxx_spam                     = isEmpty(TRdxExportMetadata.Spam);
  data.reddoxx_sender                   = isEmpty(TRdxExportMetadata.Sender);
  data.reddoxx_score                    = isEmpty(TRdxExportMetadata.Score);
  data.reddoxx_ccRecipients             = toArray(TRdxExportMetadata.CcRecipients, TRdxExportMetadata.CcRecipients['~Count']);
  data.reddoxx_ccRecipientsCount        = TRdxExportMetadata.CcRecipients['~Count'];
  data.reddoxx_attachmentNameList       = toArray(TRdxExportMetadata.AttachmentNameList, TRdxExportMetadata.AttachmentNameList['~Count']);
  data.reddoxx_attachmentNameListCount  = TRdxExportMetadata.AttachmentNameList['~Count'];
  data.reddoxx_envSender                = isEmpty(TRdxExportMetadata.EnvSender);
  data.reddoxx_state                    = isEmpty(TRdxExportMetadata.State);
  data.reddoxx_id                       = isEmpty(TRdxExportMetadata.Id);
  data.reddoxx_attachmentSizeList       = toArray(TRdxExportMetadata.AttachmentSizeList, TRdxExportMetadata.AttachmentSizeList['~Count']);
  data.reddoxx_attachmentSizeListCount  = TRdxExportMetadata.AttachmentSizeList['~Count'];
  data.reddoxx_storeStamp               = toDate(TRdxExportMetadata.StoreStamp);
  data.reddoxx_messageType              = isEmpty(TRdxExportMetadata.MessageType);
  data.reddoxx_messageId                = isEmpty(TRdxExportMetadata.MessageId);

 // metadata(data).save(obj);
  return data;

}

function toDate(datestr) {
  // 2010-07-24 10:35:40
  let da = datestr.split('-').join(' ').split(':').join(' ').split(' ');
  return new Date(da[0], da[1]-1, da[2], da[3], da[4], da[5]);
}

function toArray(obj, count) {
  let array = [];
  for (var i = 0; i < count; i++) {
    array[i] = obj['L' + i];
  }
  return array;
}

function isEmpty(obj) {

    // null and undefined are "empty"
    if (obj === null) return null;

    // Assume if it has a length property with a non-zero value
    // that that property is correct.
    if (obj.length > 0)    return obj;
    if (obj.length === 0)  return null;

    // If it isn't an object at this point
    // it is empty, but it can't be anything *but* empty
    // Is it empty?  Depends on your application.
    if (typeof obj !== "object") return null;

    // Otherwise, does it have any properties of its own?
    // Note that this doesn't handle
    // toString and valueOf enumeration bugs in IE < 9
    for (var key in obj) {
        if (hasOwnProperty.call(obj, key)) return obj;
    }

    return null;
}
```

## JavaScript-Bibliothek transform

Diese Bibliothek bietet Funktionen für das Transformieren eines Strings in eine JavaScript-Variable.

### Verwendung

* * *

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```auto
let transform = require('docform/transform');
```

### Funktionen

* * *

#### replace

Ersetzt das erste gefundene Zeichenmuster.

**Beispiel**

```auto
transform('abca').replace('a', 'xxx');
```

**Ergebnis**

```auto
{
  "val" : "xxxbca"
}
```

#### replaceAll

Ersetzt alle gefundenen Zeichenmuster.

**Beispiel**

```auto
transform('abca').replaceAll('a', 'xxx');
```

**Ergebnis**

```auto
{
  "val" : "xxxbcxxx"
}
```

#### extract

Extrahiert aus einem String ein Muster, das in RegEx angegeben wird.

**Beispiel**

```auto
transform('acbca').extract('a.*c');
```

**Ergebnis**

```auto
{
  "val" : "acbc"
}
```

#### int

Transformiert eine String-Zahl in einen Integer.

**Beispiel**

```auto
transform('1223').int();
```

**Ergebnis**

```auto
1223
```

#### float

Transformiert einen String-Float in einen Float.

Als Parameter wird die Sprache angegeben:

```auto
float(language)
```

**Beispiel**

```auto
transform('1234,21').float('de');
```

**Ergebnis**

```auto
1234.21
```

#### bool

Transformiert einen Boolean-String in einen Bolean.

Der true-Wert wird in *bool(trueVal)* übergeben.

**Beispiel**

```auto
transform('xxx').bool('xxx');
```

**Ergebnis**

```auto
true
```

#### date

Transformiert einen Datums-String in ein Date.

**Beispiel**

```auto
transform('2018-05-21').date('yyyy-MM-dd', 'de');
```

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| yyyy-MM-dd | Definiert das Format, in dem der zu transformierende String vorliegt. |
| de | Definiert den Ländercode. Dieses Kürzel spiegelt die Sprache des Strings wider. Für das System macht es einen Unterschied, ob es Folgendes in ein Datum umwandeln soll: 22 Dec 2019 oder 22 Dez 2019 Ergebnis 22 Dec 2019 --> .date('yyyy MMM dd', 'en'); 22 Dez 2019 --> .date('yyyy MMM dd', 'de'); |

**Ergebnis**

```auto
"2018-05-21T00:00:00.000Z"  (ist ein Date)
```

## JavaScript-Bibliothek preview/objects

**Ab welcher Version verfügbar?**

• *agorum core* 9.4.1

Diese Bibliothek bietet Funktionen, um:

* per Overlay-Objekt einen Stempel oder eine Notiz auf ein Preview-Image zu setzen
* Preview-Images zu holen und zu erstellen

Ein Overlay ist ein Objekt, mit dem Sie eine Notiz oder einen Stempel (eine Grafik) als Bemerkung (Annotation) an einer bestimmten Position (Seite und x- sowie y-Koordinaten auf der Seite) auf ein Dokument setzen können. Die Position wird in Pixeln, bezogen auf das Preview, angegeben.

Ein Preview-Image ist die grafische Darstellung einer Seite eines Dokuments. Ein Preview-Image wird unterschieden in:

* Master-Image
* Thumbnail-Images

Das Master-Image hat die Größe der Dokumentseite, die es repräsentiert.

Das Thumbnail-Image ist kleiner, damit es etwa innerhalb einer Liste schnell angezeigt werden kann.

### Verwendung

* * *

Diese Bibliothek binden Sie stets am Anfang eines Skripts ein:

```auto
let previewobjects = require('preview/objects');
```

### Funktionen

* * *

#### create

**overlay**

Legt ein neues Overlay-Objekt an und verknüpfen dieses mit dem richtigen Preview des Objekts.

Das Objekt kann eine Notiz oder eine Grafik (Stempel) sein, die auf ein Dokument gesetzt wird.

```auto
let overlay = previewobjects.create('overlay', data);
```

**data**

```auto
  data = {
    // mandatory parameters
    x: 0,                                 // x coordinate in "value parameter coordinates",

                                          // beginning from top left
    y: 0,                                 // y coordinate in "value parameter coordinates",

                                          // beginning from top left
    page: 1,                              // page, starting with 1
    target: 'id-or-path-to-document',     // the document, to that the overlay should be added

    text: 'Text of note',                 // text of the overlay (optional, when image is set)
    image: 'id-or-path-to-image',         // image of the  (optional, when text is set), could be png or jpg

    // optional parameters
    coordinates: 'px',                    // coordinates x and y
                                          // 'px' in pixel
                                          // '%'  in percent  (0 - 1) e.g: 0.22343
                                          // Default: 'px'
    width: 100,                           // optional width in pixels or percent

                                          // (if not set, it is done automatically, depending on the text)
                                          // 0 <= width <= 1  ==> in percent
                                          // width > 1        ==> in pixel
    height: 100,                          // optional height in pixels or percent
                                          // (if not set, it is done automatically, depending on the text)
                                          // 0 <= height <= 1  ==> in percent
                                          // height > 1        ==> in pixel
    depth: 0,                             // depth, default is 0. If there are several notes overlapping.
                                          // the higher the depth, the more top is the note
    background: '#FFFF00',                // background color with HEX RGB
  }
```

**Beispiel**

Das folgende Beispiel zeigt eine Notiz, die als Annotation auf ein Dokument aufgebracht wird:

```auto
let previewobjects = require('preview/objects');

overlay = previewobjects.create('overlay', {
  target: doc,  // agorum core Dokument-Object
  x: 200 ,
  y: 200 ,
  text: 'Hier steht meine erste Notiz\n, die per JavaScript als Annotation\ngesetzt wird',
  page: 1,

});
```

Nachfolgend die RGB-Werte für die im Standard angebotene Notiz, die in 24 unterschiedlichen Hintergründen als Annotation gesetzt werden kann. Mit dem kleinen Programm im Folgenden können Sie diese auf ein Dokument setzen, sodass Sie sehen, wie diese aussehen:

```auto
let std = [

  {
    background : '#ff0000',
    text : 'rot (1)'
  }, {
    background : '#ff9900',
    text : 'Orange (2)'
  }, {
    background : '#99cc00',
    text : 'gr\u00FCn (3)'
  }, {
    background : '#339966',
    text : 'gr\u00FCn (4)'
  }, {
    background : '#33cccc',
    text : 'Blau (5)'
  }, {
    background : '#3366ff',
    text : 'Blau (6)'
  }, {
    background : '#800080',
    text : 'rot (7)'
  }, {
    background : '#969696',
    text : 'grau (8)'
  }, {
    background : '#ff00ff',
    text : 'Lila (9)'
  }, {
    background : '#ffcc00',
    text : 'Orange (10)'
  }, {
    background : '#ffff00',
    text : 'Gelb (11)'
  }, {
    background : '#00ff00',
    text : 'Gr\u00FCn (12)'
  }, {
    background : '#00ffff',
    text : 'Balu (13)'
  }, {
    background : '#00ccff',
    text : 'Blau (14)'
  }, {
    background : '#993366',
    text : 'Rot (15)'
  }, {
    background : '#c0c0c0',
    text : 'Grau (16)'
  }, {
    background : '#ff99cc',
    text : 'Lila (17)'
  }, {
    background : '#ffcc00',
    text : 'Orange (18)'
  }, {
    background : '#ffff99',
    text : 'Gelb (19)'
  }, {
    background : '#ccffcc',
    text : 'Blau (20)'
  }, {
    background : '#99ccff',
    text : 'Blau (21)'
  }, {
    background : '#cc99ff',
    text : 'Blau (23)'
  }, {
    background : '#ffffff',
    text : 'Weis (24)'
  }

];

let start = 100;
let counter = 0;
std.forEach(std => {
  previewobjects.create('overlay', {
    target: doc,
    x: 20,
    y: start,
    width: 300,
    background: std.background,
    text: std.text,
    page: 1,
  });
  start += 120;
});
```

**Ergebnis**

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/d466bb10-a058-11ea-88f4-005056aa0ecc)

```auto
OCR: Demo, Rolf, Demo, Rolf, Orange, 121, Demo, Rolf, Demo, Rolf, Demo, Rolf, Blau, OCR, Testdokument, Demo, Roll, Blau, Demo, Rolf, rot, Demo, Roll, grau, Demo, Rolf, Lia, Demo, Rolf, Orange, Dies, ist, ein, Dokument, ohne, Textinformationen, Perfekt, somit, den, OCR, Ih res, Systems, testen, Ziehen, Sie, dazu, diese, Datei, per, Drag, Drop, einen, beliebigen, Ordner, von, agorum, core, Sobald, der, Upload, abgeschlossen, ist, wird, die, Datei, den, OCR, versendet, Dies, kann, einen, Moment, dauern, von, ..., Auslastung, Ih res, Systems, Hardwareaustattung, des, Servers, Anzahl, Dokumenten, die, durch, den, OCR, laufen, Demo, Rolf, Gelb, Demo, Rolf, Demo, Rolf, Dalu, Demo, Rolf, Blau, Demo, Rolf, Ret, Demo, Rolf, Grau, Demo, Rolf, Suchen, Sie, nach, einer, gewissen, Wartezeit, nach, Begriffen, dieses, Textes, innerhalb, des, information, centers, Anbei, haben, wir, Ihnen, ein, paar, herausgesucht, die, vermutlich, recht, wenigen, Dokumenten, Ih res, Systems, vorkommen, machen, Kinder, froh, agorum, core, ist, eine, flexible, Software, Digitalisierung, ist, gar, nicht, schwer, Demo, Rolf, Orange, Demo, Rolf, Gelb, Demo, Rolf, Demo, Roll, Blau, Demo, Roll, B123, Demo, Roll, Weis
```

OCR-Testdokument

**Beispiel für einen Stempel**

Ein Stempel ist eine Grafik als png- oder als jpg-Datei:

```auto
overlay = previewobjects.create('overlay', {
  target: doc,
  x: 100,
  y: 100,
  width: 1200,
  image: objects.find('/agorum/roi/customers/agorum.test.preview.objects/test-daten/agorum_logo_dark_mode_komplett_claim.png'),
  page: 1,
});
```

**Ergebnis**

Auf dem Dokument ist jetzt oben links das agorum-Logo zu sehen:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/95934960-a05a-11ea-88f4-005056aa0ecc)

```auto
OCR: make progress not work OCR Testdokument Dies ist ein Dokument ohne Textinformationen Perfekt somit den OCR Ihres Systems testen Ziehen Sie dazu diese Datei per Drag Drop einen beliebigen Ordner von agorum core Sobald der Upload abgeschlossen ist wird die Datei den OCR versendet Dies kann einen Moment dauern von ... der Auslastung Ihres Systems Hardware austattung des Servers Anzahl Dokumenten die durch den OCR laufen Suchen Sie nach einer gewissen Wartezeit nach Begriffen dieses Textes innerhalb des information centers Anbei haben wir Ihnen ein paar herausgesucht die vermutlich recht wenigen Dokumenten Ihres Systems vorkommen machen Kinder froh agorum core ist eine flexible Software Digitalisierung ist gar nicht schwerl,
```

OCR-Testdokument mit agorum-Logo

#### update

**overlay**

Ändert ein Overlay-Object.

```auto
previewobjects.update('overlay', object, data);
```

**data**

```auto
data = {
    // optional parameters
    x: 0,                                 // x coordinate in "value parameter coordinates",

                                          // beginning from top left
    y: 0,                                 // y coordinate in "value parameter coordinates",

                                          // beginning from top left
    coordinates: 'px'                     // coordinates x and y
                                          // 'px' in pixel
                                          // '%'  in percent (0 - 1) e.g: 0.22343
                                          // Default: 'px'
    page: 1,                              // page, starting with 1
    width: 100,                           // optional width in pixels or %

                                          // (if not set, it is done automatically, depending on the text)
                                          // 0 <= width <= 1  ==> in percent
                                          // width > 1        ==> in pixel
    height: 100,                          // optional height in pixels or %
                                          // (if not set, it is done automatically, depending on the text)
                                          // 0 <= height <= 1  ==> in percent
                                          // height > 1        ==> in pixel
    depth: 0,                             // depth, default is 0. If there are several notes overlapping.
                                          // the higher the depth, the more top is the note
    background: '#FFFF00',                // background color with HEX RGB
    text: 'Text of note',                 // text of the note,
    image: 'id-or-path-to-image',         // image of the  (optional, when text is set), could be png or jpg

  }
```

**Beispiel**

```auto
previewobjects.update('overlay', object, {
  text: 'Das ist der neue Text vom Overlay'
});
```

#### load

**overlay**

Holt alle Overlays, die auf einem Dokument sitzen.

```auto
let overlays = previewobjects.load('overlay', object [, filter ]);
```

**object**

```auto
object = <agorum core object> von dem Sie die Overlays holen
```

**filter (optional)**

Schränkt auf bestimmte Overlays ein.

```auto
filter = {
    type:      // Optional 'txt' or 'jpg' or 'png'
    page:      // Optional 1 od 2 ... or n
  }
```

**Ergebnis**

Sie erhalten ein Array von Overlay-Objekten mit folgendem Aufbau:

```auto
let overlays = [
    {
      overlay: overlay                      // agorum core Overlay-Object
      name:                                 // name from tghe Overlay
      x: 0,                                 // x coordinate in pixels, beginning from top left
      y: 0,                                 // y coordinate in pixels, beginning from top left
      page: 1,                              // page, starting with 1
      width: 100,                           // width in pixels

      height: 100,                          // optional height

      depth: 0,                             // depth. If there are several notes overlapping.
                                            // the higher the depth, the more top is the note
      background: '#FFFF00',                // background color with HEX RGB
      text: 'Text of note',                 // text of the note
    },
    ..
    ..
  ]
```

**Beispiele**

***Alle Overlays holen***

```auto
let overlays = previewobjects.load('overlay', object);
```

***Nur die Overlays von Seite 1 holen***

```auto
let overlays = previewobjects.load('overlay', object, {page: 1});
```

***Nur txt-Overlays holen***

```auto
let overlays = previewobjects.load('overlay', object, {type: 'txt'});
```

***Nur image-png-Overlays von Seite 1 holen***

```auto
let overlays = previewobjects.load('overlay', object, {page: 1, type: 'png'});
```

**image**

Holt ein Preview-Image.

Wenn das Image nicht vorhanden ist, wird es den übergebenen Parametern entsprechend erstellt.

**Aufruf**

```auto
let imageData = previewobjects.load('image', object, data);
```

**object**

Object ist das Dokument, von dem das Image geholt wird.

**data**

Mit *data* übergeben Sie Parameter, die definieren, welches Image Sie holen wollen.

```auto
data = {
     width: -1,        // Width in pixels
                       //  x > 0 width in pixels, if height is set to -1, height is calculated
                       //                         If height is also set, the image can be distorted
                       // Default: -1 = is not considered
     height: -1,       // Height in pixels
                       //  x > 0 height in pixels, if width is set to -1, width is calculated
                       //                       If width is also set, the image can be distorted
                       // Default: -1 = is not considered

     size: -1,         // Specified in pixels. Refers to the longer edge,

                       //                  the shorter edge is then calculated automatically
                       // Default: -1 = is not considered

                       // Rule for width, height, size:
                       //           If width or height are set, no size may be set
                       //           If size is set, no width or height may be set
                       //
                       // MasterImage: A MasterImage is an image with the original height and width of the
                       //              document page
                       //             if width, height and size are not assigned or

                       //             are each assigned with -1, a MasterImage is created
     page: 1           // page of the document, always start at 1
                       // Default: 1
                       // If the page does not exist an exception is thrown

     cached: true,     // Specifies whether the image is cached.
                       // true = is stored as object
                       // false = is not stored as object
                       // Default: true

     readOnly:true,    // Specifies whether the set expiration date is increased for each viewing
                       // This means that the image is only deleted when it is no longer viewed
                       // This only has an effect if it is entered in the MetaDb that a expiration date is set.
                       // The default value is recommended here
                       // true = ExpirationDate is NOT increased when the image is viewed.
                       // false = Expiration date is increased with each viewing.
                       // Default: true

     onlyCreated: true // Here you can control that the image is only fetched if it is already is created.
                       // true = The image is only fetched if it is already created. If the image is not

                       //        created, an exception is thrown
                       // false = The image is always fetched, if it is not available, it is created
                       // Default: false
  }
```

**Ergebnis**

```auto
imageData = {
      count: 8,             // Count, how many images are there in total
      stream: { },          // contentStream of the image
      contentSize: 127861,  // contentSize of the image in bytes
      masterWidth: 1240,    // Width of the MasterImage in pixels
      masterHeight: 1754,   // Height of the MasterImage in pixel
      width: 1240,          // Width of this image
      height: 1754          // Height of this image
    };
```

**Beispiele**

***MasterImage von Seite 1 holen***

```auto
let imageData = previewobjects.load('image', object, { page: 1 });
```

Wenn das Image nicht vorhanden ist, wird es erzeugt und zurückgegeben.

***Thumbnail von Seite 1 holen***

```auto
let imageData = previewobjects.load('image', object, { page: 1, size: 32, cached: false });
```

Die lange Seite hat 32 Pixel, das image wird nicht gespeichert.

Wenn das Image nicht vorhanden ist, wird es erzeugt und zurückgegeben.

#### delete

Löscht das angegebene Overlay-Objekt.

Ab *agorum core* 10.2.7 prüft das System beim Löschen zusätzlich, ob es sich bei dem Dokument um ein Overlay-Objekt handelt.

**Aufruf**

```auto
previewobjects.delete(object);
```

**Beispiel**

Das folgende Skript holt alle Overlay-Objekte und löscht diese nacheinander.

```auto
let overlays = previewobjects.load('overlay', doc);

overlays.forEach(overlay => {
  previewobjects.delete(overlay.overlay);
});
```

## GlobalObject

Diese Dokumentation beschreibt die Methoden *getter* und *setter* eines GlobalObjects.

Bei den Beispielen wird davon ausgegangen, dass Sie ein Objekt haben. Dieses können Sie etwa folgendermaßen holen:

```auto
let objects = require('common/objects');
let object = objects.find('<Object.id>');
```

### Methoden für Ordner

* * *

Die hier beschriebenen Methoden gelten nur für Objekte vom Typ *Ordner* (FOLDEROBJECT).

Ob ein Objekt ein Ordner ist oder nicht, prüfen Sie über die Methode [isFolder](#IsFolder).

#### items()

Liefert ein Array aller Objekte in diesem Ordner zurück.

* Sie erhalten *null* zurück, wenn das Objekt kein Ordner ist.
* Sie erhalten ein leeres Array zurück, wenn das Objekt ein leerer Ordner ist.

**Syntax**

```auto
object.items().map(item => item.name);
```

base.items().map(item => item.name);

#### itemsCount

Enthält die Anzahl der Unterelemente dieses Ordners.

**Syntax**

```auto
object.itemsCount;
```

#### itemsNoFolder

Liefert alle Elemente außer Ordner zurück.

**Syntax**

```auto
object.itemsNoFolder;
```

#### itemsOnlyFolder

Liefert alle Unterordner zurück.

**Syntax**

```auto
object.itemsOnlyFolder;
```

#### .createPath()

Erstellt einen neuen Ordner.

* Rufen Sie diese Methode direkt auf dem Objekt auf, nicht global.
* Sie benötigen keinen Basisordner als Objekt und müssen ihn oder nicht per Methode *find()* holen.

* Übergeben Sie den Pfad des neuen Ordnernamens. Sie können hierbei auch mehrere Ordner untereinander anlegen.

**Beispiel**

```auto
let base = objects.find('/Home/roi/MyFiles');

// Prüfen, ob das Objekt auch ein Ordner ist
if (base.isFolder) {
   base.createPath('Mein neuer Ordner/Mein neuer Unterordner');
}
```

**Rückgabewert**

Sie erhalten den untersten Ordner der neu erstellten Struktur zurück.

### acl

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des ACL des Objekts. | AccessControlList |

#### acl setzen

Hier wird die ACL *public* gesetzt.

```auto
object.acl = objects.find('acl:public');
```

#### acl lesen

```auto
let acl = object.acl;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### aclByName

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des ACL des Objekts. |  |

#### aclByName(string)

```auto
object.aclByName('public');
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### addAttachment

* * *

| Aufgabe | Datentype |
| --- | --- |
| Hinzufügen eines Anhangs an das Objekt. | – |

#### addAttachament(GlobalObject)

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');
let obj3 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test2.js');

object.addAttachment(obj3);
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### addToPathDateQueue()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Function addToPathDateQueue() des Objektes |  |

#### addToPathDateQueue()

```auto
let xxx = object.addToPathDateQueue()
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### allAclIDs

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller allAclIDs und Scope-ACLs des Objektes. | long\[\] |

#### allAclIDs holen

```auto
let allAclIDs = object.allAclIDs;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### allAttachments

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller Anhänge des Objektes. | GlobalObject \[\] |

#### allAttachments lesen

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');
let obj1 = objects.find('/agorum/roi/customers/test-auto-plugin/js/read-meta.json.js');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');
let obj3 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test2.js');

let attachments = [obj1, obj2];
object.setAttachments(attachments);
object.addAttachment(obj3);

let allAttachments = object.allAttachments;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### allFolderPath

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller Pfade des Objekts. | string\[\] allFolderPath |

#### allFolderPath lesen

```auto
let objects = require('common/objects');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');

obj2.allFolderPath;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Sie erhalten nur die Pfade, die der ausführende Benutzer sehen kann.
* Siehe auch [getAllFolderPath( \[ folder-Id \] )](#)

### anyFolderPath

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des anyFolderPath des Objekts. | string |

#### anyFolderPath lesen

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

let anyFolderPath = object.anyFolderPath;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Wenn das Objekt mit mehreren Pfaden verknüpft ist, wird nur einer zurückgegeben.

### areaName (alt von desk4web)

* * *

Der *areaName* wird noch im Modul *desk4web* verwendet. Im neuen *agorum core* hat er keine Bedeutung mehr und sollte auch nicht verwendet werden.

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des areaName des Objekts. | string |

#### areaName setzen

```auto
object.areaName = 'Das ist der AreaName';
```

#### areaName holen

```auto
let areaName = object.areaName;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### associatedUser

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des associatedUser des Objekts (zugehöriger Benutzer eines Objekts). | DirectoryUserObject |

#### associatedUser holen

```auto
let associatedUser = object.associatedUser;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### attachedTo()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller Objekte, an denen das Objekt angehängt ist. | GlobalObject \[\] |

#### attachedTo() lesen

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');
let obj1 = objects.find('/agorum/roi/customers/test-auto-plugin/js/read-meta.json.js');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');
let obj3 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test2.js');

let ret = [];
let attachments = [obj1, obj2];

object.setAttachments(attachments);

object.addAttachment(obj3);

obj3.attachedTo();
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### attachments()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller Anhänge des Objekts. | GlobalObject \[\] |

#### attachments() lesen

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');
let obj1 = objects.find('/agorum/roi/customers/test-auto-plugin/js/read-meta.json.js');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');
let obj3 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test2.js');

let attachments = [obj1, obj2];
object.setAttachments(attachments);
object.addAttachment(obj3);

attachments = object.attachments();
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### baseName

* * *

| Aufgabe | Datentype |
| --- | --- |
| Nur Lesend. Gibt den Namen des Objektes ohne Extension zurück. | string |

#### Syntax

```auto
let baseName = object.baseName;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### behaviorName

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des behaviorName des Objekts. | string |

#### behaviorName schreiben

```auto
object.behaviorName = 'bh01';
```

#### behaviorName lesen

```auto
let behaviorName = object.behaviorName;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Dieses Attribut ist ein Text-Feld, in das 60 Byte Text geschrieben werden kann.

### belongingObject

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des belongingObject des Objekts. | GlobalObject |

#### belongingObject holen

```auto
let belongingObject = object.belongingObject;
```

#### Bedingungen/Ausnahmen

Lesrechte notwendig

### cancelCheckOut()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Bricht das Auschecken eines Objekts ab. | – |

#### cancelCheckOut()

```auto
object.cancelCheckOut()
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Alle bis dahin gemachten Änderungen an der Arbeitskopie werden verworfen.

### checkinComment

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des checkinComment des Objekts. | string |

Der checkinComment ist der Kommentar, der beim Einchecken eines Objekts eingegeben wird. Hier schreibt der Änderer einen kurzen Kommentar, was er an dem Dokument geändert hat.

#### checkinComment holen

```auto
let checkinComment = object.checkinComment;
```

#### Bedingungen/Ausnahmen

Lesrechte notwendig

### checkedOut

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt ausgecheckt ist. true Objekt ist ausgecheckt. false Objekt ist nicht ausgecheckt. | boolean |

#### checkedOut holen

```auto
let checkedOut = object.checkedOut
```

```auto
if (object.checkedOut) {
  // ist ausgechecked
  ..
}
else {
  // ist nicht ausgechecked
  ..
}
```

#### Bedingungen/Ausnahmen

* Lesesrechte notwendig
* Die zugehörige Funktion lautet *isCheckedOut()*.

### checkedOutByMe

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt von Ihnen ausgecheckt ist. true Objekt ist von Ihnen ausgecheckt. false Objekt ist nicht von Ihnen ausgecheckt. | boolean |

#### checkedOutByMe holen

```auto
let checkedOutByMe = object.checkedOutByMe
```

```auto
if (object.checkedOutByMe) {
  // ist von Ihnen ausgechecked
  ..
}
else {
  // ist nicht von Ihnen ausgechecked
  ..
}
```

#### Bedingungen/Ausnahmen

* Lesrechte notwendig
* Die zugehörige Funktion lautet *isCheckedOutByMe()*.

### checkIn(comment, versionNumber, isMayjorVersion)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Checkt die Arbeitskopie eines ausgecheckten Dokuments ein (checkOut). | GlobalObject |

 Der Aufruf wird auf dem Original-Objekt ausgeführt. Der Rückgabewert entspricht dem Originalobject, das zuvor ausgecheckt wurde.

#### Parameter

| Parameter | Datentype | Beschreibung |
| --- | --- | --- |
| comment | string | Der Kommentar, den der Bearbeiter beim CheckIn eingibt (checkinComment) |
| versionNumber | null | Übergeben Sie bei der Versionsnummer null, wird diese über die Standardberechnung berechnet. Wenn nicht vorhanden, fängt die Nummer bei 1.0 an. Wenn isMayjorVersion === true, wird die Zahl vor dem Komma hochgezählt. Beispiel 1.0 - 2.0 - 3.0 Wenn isMayjorVersion === false, wird die Zahl nach dem Komma hochgezählt. Beispiel 1.0 - 1.1 - 1.2 |
| versionNumber | string | Wenn Sie die Versionsnummer als String übergeben, wird genau der Inhalt des Strings in die Versionsnummer gesetzt. Jetzt sind Sie für die Berechnung der Versionsnummer selbst verantwortlich. |
| isMayiorVersion | boolean | true Hauptversion false keine Hauptversion |

**Beispiel**Version automatisch berechnet mit dem Standardverhalten:

```auto
let objects = require('common/objects');
let text = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.txt');

// checkOut
let co = text.checkOut(null);
// Jetzt wird was geändert
co.contentString += '\nNoch eine Zeile';
let obj = text.checkIn('Kommentar ' + new Date(), null, false);
```

**Beispiel**Version mit eigener Versionsnummer:

```auto
let objects = require('common/objects');
let text = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.txt');

// checkOut
let co = text.checkOut(null);
// Jetzt wird was geändert
co.contentString += '\nNoch eine Zeile - xx';

let obj = text.checkIn('Kommentar ' + new Date(), 'V17.89.55-987', false);
```

**Beispiel***checkIn()* auf dem ausgecheckten Objekt aufrufen:

```auto
let objects = require('common/objects');
let text = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.txt');

// checkOut
let co = text.checkOut(null);
// Jetzt wird was geändert
co.contentString += '\nNoch eine Zeile - yy';
// Jetzt wird checkIn auf der Arbeitskopie aufgerufen.
let obj = co.checkIn('Kommentar ' + new Date(), 'V17.89.55-987', false);
```

#### Bedingungen/Ausnahmen

Schreibrechte oder CheckIn-Rechte notwendig.

### checkOut(GlobalObject versionToCheckout)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Checkt eine Datei aus. | GlobalObject |

Beim Auschecken erstellt das System im Verzeichnis *Home/{user\_id}/myFiles/In Bearbeitung* eine Arbeitskopie Ihrer Datei und sperrt das Original, damit das Original von anderen Benutzern nicht verändert werden kann. Der Rückgabewert ist Ihre Arbeitskopie, in der Sie anschließend Ihre Änderungen vornehmen können.​

**Beispiel**Eine Datei hat drei Versionen:

* Version 2.0 (aktuell): 1185750
* Version 1.0 (alt): 1414507

Sie können verschiedene Szenarien abbilden, je nachdem, welche Dateiversion Sie auschecken möchten:

```auto
/* global sc */

let objects = require('common/objects');
let metadata = require('common/metadata');

// Datei (ID) holen, die ausgecheckt werden soll
let versions = {
  current: objects.find(1185750), // aktuelle Version 2.0 der Datei
  version1: objects.find(1414507) // alte Version 1.0 der Datei
};

// Checkout durchführen
if (versions.current.historyObject) {

  // Checkt die aktuelle Version 2.0 aus
  return versions.version1.belongingObject.checkOut(null);
}

  // Checkt die alte Version 1.0 aus
  return versions.version1.belongingObject.checkOut(versions.version1);
}

// Checkt die aktuelle Version 2.0 aus
return versions.current.checkOut(null);

//  Checkt die alte Version 1.0 aus
return versions.current.checkOut(versions.version1);
```

#### Bedingungen/Ausnahmen

Schreibrechte oder Checkout-Rechte notwendig, um den Checkout durchführen zu können.

### convertablePDF

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des convertablePDF des Objekts. | boolean |

#### convertablePDF holen

```auto
let convertablePDF = object.convertablePDF;
```

#### Bedingungen/Ausnahmen

Lesrechte notwendig

### createDate

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des createDate des Objekts. | date |

Dieses Datum gibt an, wann das Objekt angelegt wurde. Im Normalfall wird dieses Datum intern gesetzt, wenn das Objekt angelegt wird.

#### createDate setzen

```auto
object.createDate = new Date();
```

#### createDate holen

```auto
let createDate = object.createDate;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### creator

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des creator des Objekts. | DirectoryUserObject |

Der *creator* gibt an, welcher Benutzer das Objekt angelegt hat. Im Normalfall wird der creator intern gesetzt, wenn das Objekt angelegt wird.

#### creator setzen

```auto
object.creator = objects.find('user:rolf.lang');
```

#### creator holen

```auto
let creator = object.creator;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### creatorByName

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des creator des Objekts anhand des Benutzernamens. | – |

#### creatorByName(string)

```auto
object.creatorByName('rolf.lang');
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### delete()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Löscht das Objekt endgültig. | – |

**Achtung**: Datenverlust durch Aufruf der Funktion. Das Objekt kann nicht mehr aus dem Serverpapierkorb wiederhergestellt werden. Löschen Sie das Objekt mit diesem Aufruf nur, wenn Sie es wirklich nicht mehr benötigen.

Möchten Sie, dass das Objekt nach dem Löschen im Serverpapierkorb verbleibt, verwenden Sie den Aufruf [trash](#).

#### delete()

```auto
object.delete()
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### deleteAllScopeAcls()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Löscht alle Scope-ACL eines Objektes. | – |

#### deleteAllScopeAcls()

```auto
object.deleteAllScopeAcls()
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### deleteScopeAcl(acl)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Löscht einen Scope-ACL eines Objekts. | – |

#### deleteScopeAcl(acl)

```auto
object.deleteScopeAcl(acl)
```

#### Bedingungen/Ausnahmen

Administrative Rechte notwendig.

### deleted

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des Flags deleted des Objekts. | boolean |

#### deleted holen

```auto
let deleted = object.deleted;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### deleteDeferred

* * *

| Aufgabe | Datentype |
| --- | --- |
| Function deleteDeferred des Objekts. | – |

#### deleteDeferred

```auto
let xxx = object.deleteDeferred
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### deleteDocumentText()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Löscht den DokumentText eines Objekts. | – |

#### deleteDocumentText()

```auto
let xxx = object.deleteDocumentText()
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Das System erstellt den [DokumentText](#) beim nächsten Indizieren neu.

### deletor

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des deletor des Objekts. | DirectoryUserObject |

#### deletor(DirectoryUserObject?) setzen

```auto
object.deletor(DirectoryUserObject?) =
```

#### deletor(DirectoryUserObject?) holen

```auto
let deletor(DirectoryUserObject?) = object.deletor(DirectoryUserObject?);
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### description

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen der Objekt-Beschreibung. | string |

#### description schreiben

```auto
object.description = 'Das ist die Beschreibung des Objekts';
```

#### description lesen

```auto
let description = object.description;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Dieses Attribut ist ein Text-Feld, in das 32 KB Text geschrieben werden kann.

### displayableObject

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der displayableObject eines Objekts. | GlobalObject |

#### displayableObject lesen

```auto
let displayableObject = object.displayableObject;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### displayName

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des Displayname des Objekts. | string |

#### displayName lesen

```auto
let displayName = object.displayName
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### documentText

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des DokumentText-Objektes des Objekts. | DocumentTextObject |

#### documentText holen

```auto
let pdf = objects.find('/agorum/roi/customers/test-auto-plugin/test/Willkommen.pdf');
let dto = pdf.documentText;

throw 'Das ist der Text, der in den Volltext-Index kommt:\n\n' + dto.contentString;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Es muss sich um ein Objekt handeln, das einen Content besitzt, etwa ein File-Object.

### ensureHistory

* * *

**Ab welcher Version nutzbar?**• *agorum core* 9.5.1

| Aufgabe | Datentype |
| --- | --- |
| Erzwingt das Erzeugen einer Historie bei der nächsten Aktion mit diesem Objekt. | – |

Wird bei einer Änderung kein *ensureHistory* verwendet, kann es sein, dass die letzte Änderung innerhalb der letzten Minute war und somit nicht erneut eine Historie erzeugt wird.

#### Name ändern und vorher eine Historie erzeugen

```auto
obj.ensureHistory().name = 'neuer-name.pdf';
```

#### Inhalt einer Datei mit dem Inhalt einer anderen Datei überschreiben

Der Inhalt eines Quellobjekts (srcObj) kann hierdurch auf ein Zielobjekt (dstObject) geschrieben werden. Verwenden Sie diese Art von content stream bevorzugt, da das System im Hintergrund direkt Optimierungen vornimmt, Stichwort dedup. Vor Setzen des Contents wird eine Historie erzeugt.

```auto
srcObj.streamContent(dstObj.ensureHistory());
```

#### Metadaten setzen

```auto
metadata({
  xx: 'yy'
}).save(obj.ensureHistory());
```

### expirationDate

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des expirationDate des Objekts. Löscht das Objekt automatisch an diesem Datum endgültig. Tipp: Setzen Sie zuerst das expirationDate und anschließend Systemflags. | date |

#### expirationDate setzen

```auto
let date = new Date();
date.setFullYear(date.getFullYear() + 11);
object.expirationDate = date;
```

Zurücksetzen, wenn es gesetzt ist und wieder weggenommen werden soll:

```auto
object.expirationDate = new Date(0);
```

#### expirationDate holen

```auto
let expirationDate = object.expirationDate;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Solange das Objekt nicht gelöscht ist, können Sie das Datum immer wieder neu setzen.

### firstParent

* * *

| Aufgabe | Datentype |
| --- | --- |
| (nur lesend) Gibt das erste übergeordnete Objekt des Objektes zurück. | GlobalObject |

#### firstParent lesen

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

let nameFirstParent = object.firstParent.name;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### flags

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen der Flags des Objekts. | long |

#### flags setzen

```auto
object.flags = 2;
```

#### flags holen

```auto
let flags = object.flags = 2 ;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### getAllFolderPath( \[ folder-Id \] )

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller Pfade, unter denen das Objekt verknüpft ist. | string\[\] |

Optional können Sie der Funktion eine Folder-ID übergeben, damit das System die Pfade relativ zu diesem Ordner ausgibt.

#### getAllFolderPath()

```auto
let objects = require('common/objects');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');

obj2.getAllFolderPath();
```

#### getAllFolderPath(folder.ID)

```auto
let objects = require('common/objects');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');

// relativ zu dem übergebenen Ordner holen
obj2.getAllFolderPath(objects.find('/agorum/roi/customers').getId());
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Sie erhalten nur die Pfade, die der ausführende Benutzer sehen kann.
* Siehe auch [allFolderPath](#)

### getId()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der eindeutigen Objekt-ID des Objekts. | long |

#### getId() holen

```auto
let id = object.getId();
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Die Objekt-ID ist für diesen Server eindeutig.

### getParent(name)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des Parent des Objekts mit einem bestimmten Namen. | GlobalObject |

Der *Parent* ist ein Ordner, an dem das Objekt mit einem *FolderPathRelation* verknüpft ist.

#### getParent(name)

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

let parentJs = object.getParent('js');
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### hasAttachments

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt Anhänge besitzt. true Objekt hat Anhänge. false Objekt hat keine Anhänge. | boolean |

#### hasAttachments

```auto
if(object.hasAttachments()) { ??
   ...
}
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### hasOwnAttachments

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt eigene Anhänge besitzt. true Objekt hat eigene Anhänge. false Objekt hat keine eigenen Anhänge. | boolean |

#### hasOwnAttachments lesen

```auto
object.hasOwnAttachments()
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### hasParents()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt Parents hat. true Objekt hat Parents. false Objekt hat keine Parents. | boolean |

#### hasParents()

```auto
let hasParents = object.hasParents();
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### historyCount

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des HistoryCounters des Objekts. | int |

Der *HistoryCount* gibt an, wie viele Historien das Objekt besetzt.

#### historyCount holen

```auto
let historyCount = object.historyCount;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### historyObject

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob es sich bei diesem Objekt um ein History-Objekt handelt. true Es handlet sich um ein History-Objekt. false Es handlet sich nicht um ein History-Objekt. | boolean |

#### historyObject

```auto
let historyObject = object.historyObject;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### ID

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der ID des Objekts. | string |

#### ID holen

```auto
let ID = object.ID;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### immutable

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des immutable des Objekts. | boolean |

#### immutable holen

```auto
let immutable = object.immutable;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### indexAble

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des indexAble des Objekts. | boolean |

#### indexAble holen

```auto
let indexAble = object.indexAble;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### inTrash

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt im Serverpapierkorb liegt. true Objekt liegt im Serverpapierkorb. false Objekt liegt nicht im Serverpapierkorb. | boolean |

#### inTrash holen

```auto
let inTrash = object.inTrash;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### isAttached()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt an einem anderen Objekt angehängt ist. true Objekt ist an einem anderen Objekt angehängt.  false Objekt ist nicht an einem anderen Objekt angehängt. | boolean |

#### isAttached()

```auto
if(object.isAttached()) {

   ...
}
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### isFolder

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt ein Ordner ist. true Objekt ist ein Ordner. false Objekt ist kein Ordner. | boolean |

#### isFolder lesen

```auto
if(object.isFolder) {
   ...
}
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### isLocked()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt gesperrt ist. true Objekt ist gesperrt. false Objekt ist nicht gesperrt. | boolean |

#### isLocked()

```auto
let isLocked = object.isLocked();
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### isOrdinaryFolder()

* * *

| Aufgabe | Datentype |
| --- | --- |
| true false | boolean |

#### isOrdinaryFolder()

```auto
if(object.isOrdinaryFolder()) {
   ...
}
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### isTemporary()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt nur ein temporäres Objekt ist. true Objekt ist ein temporäres Objekt. false Objekt ist kein temporäres Objekt. | boolean |

#### isTemporary()

```auto
let isTemporary = object.isTemporary();
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### lastModifier

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des lastModifier des Objekts. | DirectoryUserObject |

Der *lastModifier* gibt an, welcher Benutzer das Objekt zuletzt geändert hat. Im Normalfall wird der *lastModifier* intern gesetzt, wenn das Objekt geändert wird.

#### lastModifier setzen

```auto
object.lastModifier = objects.find('user:rolf.lang');
```

#### lastModifier holen

```auto
let lastModifier = object.lastModifier;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### lastModifierByName

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des lastModifier des Objektes anhand des Benutzernamens. | – |

#### lastModifierByName(string)

```auto
object.lastModifierByName('rolf.lang');
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### lastModifyDate

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des lastModifyDate des Objekts. | date |

Das *lastModifyDate* gibt an, wann das Objekt zuletzt geändert wurde. Im Normalfall wird dieses Datum intern gesetzt, wenn sich das Objekt geändert hat.

#### lastModifyDate setzen

```auto
object.lastModifyDate = new Date();
```

#### lastModifyDate holen

```auto
let lastModifyDate = object.lastModifyDate;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Manchmal wird dieses Datum nicht gesetzt.

### leftwardRelations

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der leftwardRelations des Objekts. Gibt alle RelationObjects, die linksseitig am Objekt hängen, zurück. | RelationObject \[\] |

#### leftwardRelations holen

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

object.leftwardRelations;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Es werden nur die Relations zurückgegeben, die der Benutzer von der Berechtigung her sehen kann.

### leftwardRelationObjects

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der leftwardRelationObjects des Objekts. Gibt die GlobalObjects, die linksseitig am Object hängen, zurück. | GlobalObject \[\] |

#### leftwardRelationObjects holen

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

object.leftwardRelationObjects;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Es werden nur die GlobalObjects zurückgegeben, die der Benutzer von der Berechtigung her sehen kann.

### linked

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob ein Objekt verlinkt ist. Dies bedeutet, dass ein Objekt mehr wie einen Parent hat. true Objekt ist verlinkt. false Objekt ist nicht verlinkt. | boolean |

#### linked holen

```auto
let linked = object.linked;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### linkedNotVisible

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob ein Objekt unsichtbare Links hat. Prüft die für den Benutzer unsichtbaren Links. true Objekt besitzt unsichtbare Links. false Objekt besitzt keine unsichtbaren Links. | boolean |

#### linkedNotVisible holen

```auto
let linkedNotVisible = object.linkedNotVisible;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### lock()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Sperrt ein Objekt für den aktuellen Benutzer. | – |

#### lock()

```auto
object.lock();
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### lockedBy

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der Benutzer, für die dieses Objekt gesperrt ist. |  |

#### lockedBy holen

```auto
let lockedBy = obj2.lockedBy;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### lockedFor

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der SessionId, für die dieses Objekt gesperrt ist. > 0 Definiert die SessionId, für die dieses Objekt gesperrt ist. -1 Wurde für keine Session gesperrt. Dies bedeutet, die Sperre bleibt auch über ein Log-out und über einen neuen Systemstart bestehen. | long |

#### lockedFor holen

```auto
let lockedFor = object.lockedFor;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### lockedForSession

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob auf dem Objekt ein Sessionlock ist. true Objekt besitzt einen Sessionlock. false Objekt besitzt keinen Sessionlock. | boolean |

#### lockedForSession holen

```auto
let lockedForSession = object.lockedForSession;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### lockState

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des Lockstate. 0 Nicht gelockt 1 Hardlock 4 SessionLock 8 lockShared ACHTUNG: Das ist eine spezielle Implementierung für ein Programm, das ein Dokument von mehreren Benutzern gleichzeitig bearbeiten kann. Beispiel: ONLYOFFICE ACHTUNG: Der lockState darf nicht einfach gesetzt werden, sondern muss immer über eine Funktion gesetzt werden. Dieser Funktion muss eine Kennung mitgegeben werden, siehe lockState auf 8 setzen. | int |

#### lockState setzen

```auto
object.lockState = 0
```

#### lockState(int?) holen

```auto
let lockState = object.lockState;
```

#### lockState auf 8 setzen (LOCKSTATE\_SHAREDLOCK)

```auto
Das kann nur über eine Funktion im Objekt selbst geschehen. Beispiel:
let obj = objects.find('<ID des agorum-Objektes>');
..
..
obj.lockShared('onlyoffice');  // Beispiel für die ONLYOFFICE - Implementierung
..
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### mainObj

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des MainObjects des Objekts. | GlobalObject |

Das MainObject verweist auf das Hauptobjekt. Dies bedeutet, das Objekt, das auf ein anderes Objekt verweist, ist nur ein Teil des gesamten Objekts. Wenn ein Objekt keinen Verweis auf ein Hauptobjekt hat, ist im MainObject immer das Objekt selbst eingetragen.

#### mainObj lesen

```auto
let mainObj = object.mainObj;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayBeDeleted()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayBeDeleted des Objekts. | boolean |

#### mayBeDeleted

```auto
let mayBeDeleted = object.mayBeDeleted();
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayCheckOut

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayCheckOut des Objektes. Prüft, ob Sie das Objekt auschecken dürfen. true Objekt darf ausgecheckt werden. false Objekt darf nicht ausgecheckt werden. | boolean |

#### mayCheckOut holen

```auto
let mayCheckOut = object.mayCheckOut;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayDelete

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayDelete des Objekts. Prüft, ob Sie das Objekt löschen dürfen. true Objekt darf gelöscht werden. false Objekt darf nicht gelöscht werden. | boolean |

#### mayDelete holen

```auto
let mayDelete = object.mayDelete;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayInsert

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayInsert des Objekts. Prüft, ob Sie das Objekt in einen Ordner ablegen dürfen. true Objekt darf in den Ordner abgelegt werden. false Objekt darf nicht in den Ordner abgelegt werden. | boolean |

#### mayInsert holen

```auto
let mayInsert = object.mayInsert;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayModify

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayModify des Objekts. Prüft, ob Sie die Attribute des Objekts ändern dürfen. true Attribute des Objekts dürfen geändert werden. false Attribute des Objekts dürfen nicht geändert werden. | boolean |

#### mayModify holen

```auto
let mayModify = object.mayModify;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayObjectBeMoved

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayObjectBeMoved des Objekts. Prüft, ob Sie das Objekt verschieben dürfen. true Objekt darf verschoben werden. false Objekt darf nicht verschoben werden. | boolean |

#### mayObjectBeMoved holen

```auto
let mayObjectBeMoved = object.mayObjectBeMoved;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mayRemove

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayRemove des Objekts. Prüft, ob Sie das Objekt abhängen dürfen. true Objekt darf abgehängt werden. false Objekt darf nicht abgehängt werden. | boolean |

#### mayRemove holen

```auto
let mayRemove = object.mayRemove;
```

### mayRemove(parent)

* * *

Prüft zusätzlich, ob das Objekt noch über den Ordner geschützt ist. Diese Methode ist der Methode *mayRemove* vorzuziehen.

| Aufgabe | Datentype |
| --- | --- |
| Holen des mayRemove des Objekts. Prüft, ob Sie das Objekt abhängen dürfen. true Objekt darf abgehängt werden. false Objekt darf nicht abgehängt werden. | boolean |

#### mayRemove holen

```auto
let mayRemove = object.mayRemove(parent);
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mailAttachment

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt ein Mailattachment ist. true Objekt ist ein Mailattachment. false Objekt ist kein Mailattachment. | boolean |

#### mailAttachment prüfen

```auto
let objects = require('common/objects');
let attachment = objects.find('1880852');

attachment.mailAttachment;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mailAttachments

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der IDs der E-Mail-Anhänge. | GlobalObject \[\] |

#### mailAttachments abfragen

```auto
let objects = require('common/objects');

let mail = objects.find('891fdea0-b31f-11ef-812f-02420a0a000e');

mail.mailAttachments;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mailBody

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt ein Mailbody ist. true Objekt ist ein Mailbody​​​​​​. false Objekt ist kein Mailbody. | boolean |

#### mailBody prüfen

```auto
let objects = require('common/objects');
let body = objects.find('891fdea0-b31f-11ef-812f-02420a0a000e');

body.mailBody;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mailMsg

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt eine Mailmsg ist. true Objekt ist eine Mailmsg. false Objekt ist keine Mailmsg. | boolean |

#### mailMsg prüfen

```auto
let objects = require('common/objects');
let msg = objects.find('891fdea0-b31f-11ef-812f-02420a0a000e');

msg.mailMSG;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### mutable

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des mutable des Objekts. Prüft, ob Sie die Attribute des Objekts ändern dürfen. true Attribute des Objekts dürfen geändert werden. false Attribute des Objekts dürfen nicht geändert werden. | boolean |

#### mutable holen

```auto
let mutable = object.mutable;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### name

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen oder holen des Namens des Objekts. | string |

#### name setzen

```auto
object.name = 'Neuer name.txt';
```

#### name lesen

```auto
let name = object.name;
```

#### Bedingungen/Ausnahmen

* Es werden Schreibrechte benötigt.
* max. 253 Byte
* Wenn bereits ein Objekt mit demselben Namen in einem der Ordner vorhanden ist, in dem das Objekt vorkommt, wird ein Fehler erzeugt.

### nameExtension

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des nameExtension des Objekts. | string |

#### nameExtension holen

```auto
let nameExtension = object.nameExtension;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Der Name besteht aus baseName + '.' + nameExtension.

### notes

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen aller Notizen des Objekts. | NoteObject\[\] |

#### notes holen

```auto
let notes = object.notes;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### notesRelation

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des notesRelation des Objekts. | RelationObject\[\] |

#### notesRelation holen

```auto
let notesRelation = object.notesRelation;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### objectTextKey

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen oder holen des objectTextKey des Objekts. Übersetzt einen Ordnernamen. | string |

#### objectTextKey setzen

```auto
object.objectTextKey = 'agorum.textkey.file.private';
```

#### objectTextKey lesen

```auto
let objectTextKey = object.objectTextKey;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* max. 253 Byte

### owner

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des Owners des Objekts. | DirectoryUserObject |

#### owner setzen

```auto
object.owner = objects.find('user:rolf.lang');
```

#### owner holen

```auto
let owner = object.owner;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Der Owner gibt an, welchem Benutzer das Objekt gehört.
* Das System setzt den Owner automatisch, wenn der Benutzer das Objekt anlegt.
* In automatisierten Prozessen kann der Owner auch manuell gesetzt werden, um ihm das Objekt zuzuordnen.

### ownerByName()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des Owners des Objekts anhand des Namens. | – |

#### ownerByName(string)

```auto
object.ownerByName('rolf.lang');
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### parents()

* * *

| Aufgabe | Datentype |
| --- | --- |
| • Holen der parents des Objekts. • Gibt alle Ordner zurück, in denen das Objekt verknüpft ist. | GlobalObject \[\] |

#### parents holen

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

let parents = object.parents();
let ret = [];
parents.forEach(function(parent){
  ret.push(parent.name);
});
ret;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Es werden nur die *parents* zurückgegeben, die der Benutzer von der Berechtigung her sehen kann.

### previewable

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des previewable des Objekts. | boolean |

#### previewable holen

```auto
let previewable = object.previewable;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### privateWorkingCopy

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob das Objekt eine PWC (privat working copy) ist. true Objekt ist eine PWC. false Objekt ist keine PWC. | boolean |

#### privateWorkingCopy holen

```auto
let privateWorkingCopy = object.privateWorkingCopy;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### pWCFolder

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des pWCFolder des Objekts. | FolderObject |

#### pWCFolder holen

```auto
let pWCFolder = object.pWCFolder;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### read

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des read des Objekts. | boolean |

#### read holen

```auto
let read = object.read;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### reIndex()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Reindiziert das Objekt / legt das Objekt nochmals in den Index. | – |

#### reIndex()

```auto
object.reIndex()
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### related

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des related des Objekts. | boolean |

#### related holen

```auto
let related = object.related;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### removeAttachments

* * *

| Aufgabe | Datentype |
| --- | --- |
| Löscht Anhänge eines Objekts. | – |

#### removeAttachments(GlobalObject \[\])

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');
let obj1 = objects.find('/agorum/roi/customers/test-auto-plugin/js/read-meta.json.js');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');
let obj3 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test2.js');

let removeAttachments = [obj1, obj2, obj3];
object.removeAttachments(removeAttachments);
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### restoreObject(FolderObject target)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Function restoreObject(FolderObject target) des Objekts. |  |

#### restoreObject(FolderObject target)

```auto
let xxx = object.restoreObject(FolderObject target)
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### rightwardRelations

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der rightwardRelations des Objekts. Gibt alle RelationObjects zurück, die rechtsseitig am Objekt hängen. | RelationObject \[\] |

#### rightwardRelations holen

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

object.rightwardRelations;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Es werden nur die Relations zurückgegeben, die der Benutzer von der Berechtigung her sehen kann.

### rightwardRelationObjects

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der rightwardRelationObjects des Objekts. Gibt alle GlobalObjects zurück, die rechtsseitig am Objekt hängen. | GlobalObject \[\] |

#### rightwardRelationObjects holen

```auto
let objects = require('common/objects');
let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');

object.rightwardRelationObjects;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Es werden nur die *GlobalObjects* zurückgegeben, die der Benutzer von der Berechtigung her sehen kann.

### rawText

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des rawText des Objekts. | string |

#### rawText holen

```auto
let rawText = object.rawText;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### scopeAcl

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des scopeAcl des Objekts (ACL oder ACL\[\]) | ACL\[\] |

#### scopeAcl setzen

```auto
object.scopeAcl = acl;
```

**Beispiel 1**

```auto
let acl = objects.find('acl:NameDesAcls');
irgendEinObject.scopeAcl = acl;
```

**Beispiel 2**

```auto
let acls = [ objects.find('acl:NameDesAcls1'), objects.find('acl:NameDesAcls2') ];
irgendEinObject.scopeAcl = acls;
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Bedeutung siehe [scope acl](#)

### scopeAclNames

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des scopeAclNames des Objekts. | string\[\] |

#### scopeAclNames holen

```auto
let scopeAclNames = object.scopeAclNames;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### scopeAcls

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des scopeAcls des Objekts. | ACL\[\] |

#### scopeAcls holen

```auto
let scopeAcls = object.scopeAcls;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### sessionController

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des sessionController des Objekts. | sessionController |

#### sessionController holen

```auto
let sessionController = object.sessionController;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Siehe [sessionController(sc)](#)

### sessionLockWithTimer(long)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des sessionLockWithTimer(long) des Objekts. | – |

#### sessionLockWithTimer(long) setzen

```auto
object.sessionLockWithTimer(long) =
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### setAttachments

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen von Anhängen an das Objekt. | – |

#### setAttachments(GlobalObject \[\])

```auto
let objects = require('common/objects');

let object = objects.find('/agorum/roi/customers/test-auto-plugin/js/test-go-api.js');
let obj1 = objects.find('/agorum/roi/customers/test-auto-plugin/js/read-meta.json.js');
let obj2 = objects.find('/agorum/roi/customers/test-auto-plugin/js/test.js');

let attachments = [obj1, obj2];

object.setAttachments(attachments);
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### setExpirationDateSilent

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des expirationDate des Objekts, ohne dass die Updatedates gesetzt werden. | – |

#### setEexpirationDateSilent(date)

```auto
let dae = new Date();
date.setFullYear(date.getFullYear() + 11);
object.setExpirationDateSilent(date);
```

#### Bedingungen/Ausnahmen

* Schreibrechte notwendig
* Solange das Objekt nicht gelöscht ist, kann das Datum immer wieder neu gesetzt werden.

### setNote(NoteObject)

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen des setNote(NoteObject) des Objekts. | – |

#### setNote(NoteObject) setzen

```auto
object.setNote(NoteObject) =
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### specificParents

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des specificParents des Objekts. | GlobalObject\[\] |

#### specificParents(className)

```auto
let subObjects = object.specificParents('');
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### subObjects

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des subObjects des Objekts. | GlobalObject\[\] |

#### subObjects holen

```auto
let subObjects = object.subObjects;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### supportsPreview

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des supportsPreview des Objekts. | boolean |

#### supportsPreview holen

```auto
let supportsPreview = object.supportsPreview;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### systemFlag

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des systemFlags des Objekts. | long |

#### systemFlag holen

```auto
object.systemFlags = 28;
let systemFlag = object.systemFlag;
```

**Ergebnis**

```auto
[4, 8, 16]
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Siehe [Übersicht Systemflags und deren Zahl (Systemflag)](#)

### systemFlags

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen der systemFlags des Objekts. | long |

#### systemFlags(long) setzen

```auto
object.systemFlags = 28
```

#### systemFlags holen

```auto
let systemFlags = object.systemFlags;
```

#### Bedingungen/Ausnahmen

* Leserechte notwendig
* Siehe [Systemflags verwenden](#)

### text

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des text des Objekts. | string |

#### text holen

```auto
let text = object.text;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### textAvailable

* * *

| Aufgabe | Datentype |
| --- | --- |
| Prüft, ob Text am Objekt verfügbar ist. true Text ist verfügbar. false Text ist nicht verfügbar. | boolean |

#### textAvailable holen

```auto
let textAvailable = object.textAvailable;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### timePhasedAction

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen der timePhasedAction des Objekts. | string |

#### timePhasedAction setzen

```auto
object.timePhasedAction = 'StartDocFormRobot';
```

#### timePhasedAction holen

```auto
let timePhasedAction = object.timePhasedAction;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### timePhasedActionDate

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und Holen des timePhasedActionDate des Objekts. | date |

#### timePhasedActionDate setzen

```auto
object.timePhasedActionDate = new Date();
```

#### timePhasedActionDate holen

```auto
let timePhasedActionDate = object.timePhasedActionDate;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### unlock()

* * *

| Aufgabe | Datentype |
| --- | --- |
| Funktion unlock() des Objekts | – |

#### unlock()

```auto
let xxx = object.unlock()
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### UUID

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen der UUID des Objekts. | string |

Die UUID wird normalerweise automatisch vergeben. Sie können sie auch gezielt auf eine vorgegebene UUID setzen.

#### UUID setzen

```auto
object.UUID = '0e3a3c00-d104-11e5-a821-080027cddacf';
```

#### UUID holen

```auto
let UUID = object.UUID;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### updateDate

* * *

| Aufgabe | Datentype |
| --- | --- |
| Setzen und holen des updateDate des Objekts. Dieses Datum gibt an, wann das Objekt zuletzt geändert wurde. | date |

#### updateDate setzen

```auto
object.updateDate = new Date();
```

#### updateDate holen

```auto
let updateDate = object.updateDate;
```

#### Bedingungen/Ausnahmen

Schreibrechte notwendig

### versionNumber

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der versionNumber des Objekts. | string |

#### versionNumber holen

```auto
let versionNumber = object.versionNumber;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### workingCopy

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen der workingCopy des Objekts. | GlobalObject |

#### workingCopy holen

```auto
let workingCopy = object.workingCopy;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### writable

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des writable des Objekts. Prüft, ob Sie auf das Objekt Schreibrechte besitzen. true Sie besitzen Schreibrechte. false Sie besitzen keine Schreibrechte. | boolean |

#### writable holen

```auto
let writable = object.writable;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

### xml

* * *

| Aufgabe | Datentype |
| --- | --- |
| Holen des xml des Objekts. | string |

#### xml holen

```auto
let xml = object.xml;
```

#### Bedingungen/Ausnahmen

Leserechte notwendig

## ContentTask

Ein ContentTask reagiert auf definierte Dokumentarten. Sobald diese Dokumentarten neu in *agorum core* angelegt werden oder sich deren Textinhalt ändert, führt das System einen Automatismus aus.

Ein Beispiel stellt der ContentTask *MSG* dar, der eine abgelegte msg-Datei automatisch in eine eml-Datei wandelt, die dann von allen E-Mail-Clients darstellbar ist. Das Original (der Inhalt der msg-Datei) bleibt dabei in der E-Mail erhalten.

**Hinweis**: Der ContentTask ist ein mächtiges Werkzeug und eignet sich für Prozesse, die bei Anlage und jeder Änderung von bestimmten Dateiformaten sofort ausgeführt werden müssen. Laden Sie etwa ein Bild in *agorum core* hoch, setzt das System automatisch Metadaten auf dieses Bild. Im Gegensatz zu [Workern](#) und [Aktiven Ordnern](#) starten ContentTasks synchron mit dem Schreibvorgang. Ein Fehler kann dazu führen, dass der Schreibvorgang fehlschlägt und etwa keinerlei Dateien mehr angelegt oder geändert werden können. Sollen Prozesse also nicht synchron ausgeführt werden, weil das Risiko, nicht mehr mit dem System zu arbeiten, zu hoch ist, setzen Sie [Worker](#) und [Aktive Ordner](#) ein.Welche Methode Sie einsetzen, hängt vom Anwendungsszenario ab.**ContentTask**Wenn die Verarbeitung bei der Anlage / Änderung sofort stattfinden soll und generell auch auf geänderten Inhalt reagieren muss, nicht nur auf neue Objekte.**Worker**Wenn besonders große Datenmengen verarbeitet werden sollen.**Aktiver Ordner/CronJob**Alle anderen Szenarien

### Mitgelieferte ContentTasks

* * *

* .arw
* .bmp
* .cr2
* .gif
* .jpg
* .nef
* .png
* .tif
* .tiff

Die genannten ContentTasks werden als [ImageMetaData](#imagemetadata) bezeichnet.

Außerdem existieren folgende ContentTasks:

* .doc
* .docm
* .docx
* .pdf
* .xls
* .xlsm
* .xlsx
* **ac.js**
* **ac.xml**
* **eml**
* **msg**

Die letzten vier ContentTasks (fett hervorgehoben) sind die relevantesten.

#### AC.JS

**ACL**

| ACL | Beschreibung |
| --- | --- |
| ACL\_ParseACJs | Definiert, welche Benutzergruppen / Benutzer diesen ContentTask verwenden dürfen. |

So finden Sie die ACL:

1. Öffnen Sie links in der Seitenleiste **Administration** und dann **ACLs/Rechte**.
2. Öffnen Sie den Pfad:

    ```auto
    System/contenttask/ACL_ParseACJs
    ```

**Hinweise**:

* Die dem Property-Eintrag *ACL* zugeordnete ACL muss sich selbst als Recht besitzen. Dies ist notwendig, da hier nur abgefragt wird, ob der Benutzer, der die ContentTask ausführen möchte, die ACL lesen kann. Für Benutzer / Benutzergruppen reicht daher ein Leserecht. Ist dies nicht vorhanden, wird die ContentTask nicht ausgeführt.

* Wenn Sie keine ACL eintragen, kann jeder Benutzer den ContentTask verwenden.

* Wenn Sie eine nicht vorhandene ACL eintragen, ist dieser ContentTask für alle Benutzer (auch Administratoren) gesperrt.

**AutomaticTaskUser**

Wenn der ContentTask bei der Synchronisation eines Adapters ausgeführt werden soll, definieren Sie einen Benutzer mit den erforderlichen Rechten und tragen Sie ihn hier ein.

Standardmäßig ist kein Benutzer eingetragen, die ContentTask würde also bei Synchronisation eines Adapters nicht funktionieren.

**Beispiel: Einen Ordner anlegen**

Aufbau der Datei *akte.ac.js*:

```auto
/* global Packages, sc, folder */
//
// folder = Ordner, in dem das Skript ausgeführt wird
// sc = sessionController
//

let objects = require('common/objects');
let templates = require('common/templates');

folder.createPath(templates.fill( 'F ${xx:f}', { xx: '' + new Date()}));
```

#### AC.XML

Dieser ContentTask führt den *agorum core*\-XML-Parser bei Neuanlage oder Änderung einer .ac.xml-Datei auf diese aus.

* Ein Umbenennen einer solchen Datei hat keine Auswirkung auf die Ausführung.
* Sie können hiermit komplexe Ordnerstrukturen anlegen.

**ACL**

| ACL | Beschreibung |
| --- | --- |
| ACL\_ParseACXml | Definiert, welche Benutzergruppen / Benutzer diesen ContentTask verwenden dürfen. |

So finden Sie die ACL:

1. Öffnen Sie links in der Seitenleiste **Administration** und dann **ACLs/Rechte**.
2. Öffnen Sie den Pfad:

    ```auto
    System/contenttask/ACL_ParseACXml
    ```

**Hinweise**:

* Die dem Property-Eintrag *ACL* zugeordnete ACL muss sich selbst als Recht besitzen. Dies ist notwendig, da hier nur abgefragt wird, ob der Benutzer, der die ContentTask ausführen möchte, die ACL lesen kann. Für Benutzer / Benutzergruppen reicht daher ein Leserecht. Ist dies nicht vorhanden, wird die ContentTask nicht ausgeführt.

* Wenn Sie keine ACL eintragen, kann jeder Benutzer den ContentTask verwenden.

* Wenn Sie eine nicht vorhandene ACL eintragen, ist dieser ContentTask für alle Benutzer (auch Administratoren) gesperrt.

**AutomaticTaskUser**

Wenn der ContentTask bei der Synchronisation eines Adapters ausgeführt werden soll, definieren Sie einen Benutzer mit den erforderlichen Rechten und tragen Sie ihn hier ein.

Standardmäßig ist kein Benutzer eingetragen, die ContentTask würde also bei Synchronisation eines Adapters nicht funktionieren.

**Beispiel: Zusatzattribute für eine Datei setzen**

Das folgende Beispiel und Vorgehen verdeutlicht, wie Sie Zusatzattribute für eine Datei setzen. Dazu benötigen Sie die Datei *MeineDatei.pdf*, für die Sie weitere Attribute vergeben möchten.

1. Laden Sie die Datei **MeineDatei.pdf** in *agorum core* hoch.
2. Laden Sie eine zweite Datei namens **MeineDatei.pdf.ac.xml** in denselben Ordner.
3. Wählen Sie dabei **xml-Dateien nach dem Hochladen parsen**.**Ergebnis**: Das System setzt die Attribute auf die Original-PDF-Datei.

    **Tipp**: Wenn die zweite Datei *MeineDatei.pdf.ac.xml* nicht gelöscht wird, können Sie die Attribute immer wieder ändern, indem Sie diese Datei ändern.

Aufbau der Datei *MeineDatei.pdf.ac.xml*:

```auto
<?xml version = "1.0" encoding =" ISO-8859-1"?>
<ObjectList>
  <FileObject>
    <Update>./MeineDatei.pdf</Update>
    <ExtendedAttributesXML>
      <![CDATA[<Dateistatus DataType="STRING">offen</Dateistatus>
<Dateitype DataType="STRING">testdatei</Dateitype>]]>
    </ExtendedAttributesXML>
  </FileObject>
</ObjectList>
```

#### MSG/EML

Dieser ContentTask erzeugt aus einer msg-/ eml*\-*Datei ein *agorum core-*E-Mail-Objekt. Die Original-Datei wird mit in das E-Mail-Objekt abgelegt. Durch diesen Wandel können Sie alle Funktionen von *agorum core* verwenden, etwa Notizen hinzufügen, Verlinken, Metadaten anhängen, Volltextsuche usw.

**Hinweis**: Dateien, die über einen File-Adapter eingebunden sind, werden nicht gewandelt.

**NewName**

Template, mit dem vorgeben werden kann, wie der neue Dateiname erzeugt wird.

Folgende Platzhalter existieren:

| Platzhalter | Beschreibung |
| --- | --- |
| CreateDate | Anlegedatum |
| SentDate | Sendedatum |
| Subject | Betreff |
| OriginalName | Ursprünglicher Dateiname der E-Mail |
| Extension | Dateiendung |
| ID | ID des Mailobjekts |

#### .doc, .dcm, .xls, .pdf (Beschreibungsinformationen von Dokumenten)

**DocumentProperties**

Eigenschaften, die aus dem Dokument ausgelesen werden:

* title
* subject
* category
* keywords

**ExtendedAttributeMapping**

Definition der Namen der Metadaten-Tags. Nach Installation sind folgende Standards definiert und können um beliebig viele Attribute erweitert werden:

* title
* subject
* category
* keywords

**OverrideOldMetaData (nur für PDF)**

Definiert, ob die mit *ExtendedAttributeMapping* automatisch ausgelesenen Metadaten überschrieben werden dürfen oder nicht.

| Wert | Beschreibung |
| --- | --- |
| true | Metadaten werden überschrieben. |
| false | Metadaten werden nicht überschrieben. |

### Einen ContentTask definieren

* * *

1. Öffnen Sie links in der Seitenleiste **Administration** und dann **MetaDB**.
2. Öffnen Sie den Pfad:

    ```auto
    /MetaDb/MAIN_MODULE_MANAGEMENT/roi/control/contenttask
    ```

    **Ergebnis**: Alle ContentTasks erscheinen.
3. Legen Sie ein Property-Bundle an, um einen neuen ContentTask zu definieren:**Beispiel**

    ```auto
    CT
    ```

    **Hinweis**: Eigene Konfigurationen wirken sich nur auf neue Dokumente und neue Änderungen aus.

#### Allgemeine Property-Entrys

Folgende Property-Entrys sind in jedem ContentTask vorhanden:

| Property-Entry | Beschreibung |
| --- | --- |
| class | Definiert die hinterlegte Java-Klasse, die für diesen ContentTask verwendet wird. |
| DeleteFileAfterTask | Definiert, ob die Original-Datei nach Ablauf des ContentTasks erhalten bleibt oder gelöscht werden soll. true Die Original-Datei wird gelöscht. false Die Original-Datei bleibt erhalten. |
| Extension | Definiert die Dateiendung, auf welche der ContentTask reagieren soll. |

### Einen ContentTask deaktivieren

* * *

Um eine Contenttask zu deaktivieren, stellen Sie dem Namen des Property-Bundles ein # voran:

```auto
##CT
```

### TimephasedAction starten

* * *

**Tipp**: Sie können auch die Aktiven Ordner verwenden, um eine TimephasedAction zu definieren.

Mit einer ContentTask können Sie auch das Starten einer TimephasedAction definieren, etwa wenn bei PDFs grundsätzlich ein Posteingangsworkflow starten soll.

Folgende Property-Entrys müssen Sie im Property-Bundle der gewünschten ContentTask definieren.

| Property-Entry | Wert/Beschreibung |
| --- | --- |
| class | agorum.roi.ejb.common.ContentTaskSetTimePhasedAction |
| DeleteFileAfterTask | Definiert, ob die Original-Datei nach Ablauf der ContentTask erhalten bleibt oder gelöscht werden soll. true Die Original-Datei wird gelöscht. false Die Original-Datei bleibt erhalten. |
| Extension | Definiert die Dateiendung, auf welche der ContentTask reagieren soll. |
| InFolders | Definiert den Pfad zu den Ordnern, in denen der ContentTask verwendet werden soll. Mehrere Einträge werden mit || getrennt eingegeben. |
| TimePhasedActionName | Definiert den Namen der aufzurufenden TimephasedAction. |

### ImageMetaData

* * *

Als ImageMetaData werden bestimmte Metadaten bezeichnet, die von *agorum core* automatisch auf Bilder gesetzt werden. Laden Sie etwa ein Bild in *agorum core* hoch, besitzt dieses Bild automatisch bestimmte Metadaten, die nur bei Bildern vorkommen.

**Beispiele als Metadatum**

* Auflösung
* Breite
* Höhe

So finden Sie die ImageMetaData:

1. Öffnen Sie links in der Seitenleiste **Administration** und dann **MetaDB**.
2. Öffnen Sie den Pfad:

    ```auto
    MAIN_MODULE_MANAGEMENT/roi/control/contenttask/[ ImageMetaData ]
    ```

Alle Grafikformate, die hier angezeigt werden, werden auch von *agorum core* unterstützt.

#### Property-Entrys

Neben den [allgemeinen Property-Entrys](#allgemeine property entries) existieren für die ImageMetaData folgende Property-Entrys:

| Property-Entry | Beschreibung |
| --- | --- |
| ExtendedAttributeMapping | Definiert die Metadaten, die in agorum core bei einem Bild angezeigt werden. Enthalten ist ein Array mit Metadatennamen, in welche die ausgelesenen Metadaten der Exif-Dateien gemappt werden (aus dem Property-Entry ImageMetaProperties). Beispiel Ist im Bild das Metadatum Exif IFD0:X Resolution vorhanden, wird es in agorum core auf das Metadatum image\_x\_resolution gemappt. |
| ImageMetaProperties | Definiert die Metadaten, die in den Exif-Dateien des Bilds vorkommen. Enthalten ist ein Array der auszulesenden Metadaten. |
| Manual | Beschreibt, welche Metadaten generell in dem gewählten Grafikformat enthalten sein können. Klicken Sie auf ein nachfolgendes Format, um diese Metadaten aufgelistet zu sehen: .arw .bmp .cr2 .gif .jpg .nef .png .tif .tiff |

#### Gesetzte Metadaten prüfen

Welche Metadaten tatsächlich auf einem Bild gesetzt sind, können Sie auf zwei verschiedene Arten herausfinden:

* in den *desk4web Tools*
* per JavaScript

**desk4web Tools**

1. Kopieren Sie die Objekt-ID des Bilds (zu finden in der Registerkarte **Objektinfo** des Bilds) in die Zwischenablage.
2. Öffnen Sie links in der Seitenleiste **Weitere Apps** und dann **desk4web Tools**.
3. Öffnen Sie unter **Tools/helpers** den Eintrag **List Image Metadata of an object**.
4. Fügen Sie die **kopierte Objekt-ID** aus der Zwischenablage ein und geben Sie die Zugangsdaten des Benutzers **roi** ein.
5. Klicken Sie auf **Submit**.**Ergebnis**: Das System gibt alle auf dem Bild gesetzten Metadaten samt Werte aus.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/cc94a2a0-b15d-11eb-b06b-005056aa0ecc)

```auto
OCR: Num Directorys: 4, Image MetaProperties: PNG-IHDR:Image Width, PNG-IHDR:Image Height, PNG-IHDR:Bits Per Sample, PNG-IHDR:Color Type, PNG-IHDR:Compression Type, PNG-IHDR:Filter Method, PNG-IHDR Interlace Method, PNG-sRGB:sRGB Rendering Intent, PNG-gAMA:Image Gamma, PNG-PHYs:Pixels Per Unit X, PNG-PHYs:Pixels Per Unit Y, PNG-PHYs:Unit Specifier, Value: 1795, 2613, 8, True Color, Deflate, Adaptive, No Interlace, Perceptual, 0.455, 7716, 7716, Metres
```

Ausgelesene Metadaten mit den *desk4web Tools*

**Per JavaScript**

Mit folgendem JavaScript können Sie ebenfalls die gesetzten Metadaten auf einem Bild prüfen. Das JavaScript können Sie etwa in Ihren eigenen Dateien in *agorum core* erstellen.

```auto
/* Global Packages */

// Kleines Skript, mit dem Sie prüfen können, welche Metadaten auf einem Bild gesetzt sind.

// ACHTUNG: Es handelt sich um Low-Level-Java-Methoden, die sich ändern können.
//          Kapseln Sie diese, wenn Sie sie in eigenen Projekten verwenden wollen.
//          Die Methoden können von uns jederzeit ersetzt werden.
let BufferedInputStream = Packages.java.io.BufferedInputStream;
let ImageMetadataReader = Packages.com.drew.imaging.ImageMetadataReader;

let objects = require('common/objects');

let object = objects.find('1432508'); // Geben Sie hier ID eines Objekts an, das Sie prüfen wollen.

/**/

let bis = new BufferedInputStream(object.contentStream);
let metadata = ImageMetadataReader.readMetadata(bis);

let ret = [];

metadata.directories.forEach(dir => {
  let name = dir.name;
  let iter = dir.tags.iterator();

  while (iter.hasNext()) {
    let tag = iter.next();

    ret.push({
      tag: name + ':' + tag.tagName,
      description: tag.description
    });
  }
});

ret;
```

Speichern Sie das Skript, nachdem Sie die Objekt-ID aus Ihrer Zwischenablage in das Skript eingefügt haben, und klicken Sie auf *Run*.

Die Ausgabe könnte etwa folgendermaßen aussehen:

```auto
[ {
  "description" : "1795",
  "tag" : "PNG-IHDR:Image Width"
}, {
  "description" : "2613",
  "tag" : "PNG-IHDR:Image Height"
}, {
  "description" : "8",
  "tag" : "PNG-IHDR:Bits Per Sample"
}, {
  "description" : "True Color",
  "tag" : "PNG-IHDR:Color Type"
}, {
  "description" : "Deflate",
  "tag" : "PNG-IHDR:Compression Type"
}, {
  "description" : "Adaptive",
  "tag" : "PNG-IHDR:Filter Method"
}, {
  "description" : "No Interlace",
  "tag" : "PNG-IHDR:Interlace Method"
}, {
  "description" : "Perceptual",
  "tag" : "PNG-sRGB:sRGB Rendering Intent"
}, {
  "description" : "0.455",
  "tag" : "PNG-gAMA:Image Gamma"
}, {
  "description" : "7716",
  "tag" : "PNG-pHYs:Pixels Per Unit X"
}, {
  "description" : "7716",
  "tag" : "PNG-pHYs:Pixels Per Unit Y"
}, {
  "description" : "Metres",
  "tag" : "PNG-pHYs:Unit Specifier"
} ]
```

### ContentTaskScript

* * *

Der ContentTask *ContentTaskScript* hat folgende Property-Entrys als Einträge:

#### ACL

Sperrt die Contenttask für Benutzer oder gibt sie frei.

Damit das System die Contenttask ausführt, benötigen Benutzer mindestens ein Leserecht auf diese ACL.

#### Class

Tragen Sie Folgendes ein:

```auto
agorum.roi.ejb.common.ContentTaskScript
```

#### Selector

Ermöglicht es, einen [Selektor](#) einzutragen. Wenn dieser greift, führt das System die Contenttask für das geänderte Objekt aus.

Damit die Contenttask sich ausschließlich auf dieses Objekt bezieht, tragen Sie einen eindeutigen Selektor ein.

```auto
[name=/.*(\.h|\.nc|\.r|\.acc)|(O[0-9]{4})/i][!isFolder]
```

#### Script

Erwartet ein auszuführendes (externes) Skript.

Als Übergabe wird dem Skript *object* mitgegeben. Darin steht das Objekt, mit dem das System das Skript ausführt.

```auto
/* global sc, object */
//
// Skript wird inline, nicht als Objektverweis erwartet
//

// Damit kann ich trotzdem ein externes Script aufrufen.
require('/agorum/roi/customers/sample/js/sampleScript');
```

**Externes Skript**

```auto
/* global Packages, sessionController, object */

let ChangeHistoryUtils = Packages.agorum.roi.ejb.common.ChangeHistoryUtils(sessionController),
    utils = require('/agorum/roi/customers/CNC/JS/utils'),
    grp     = require('common/objects').find('group://GRP_CNCRestore'),
    grpNote = require('common/objects').find('group://GRP_CNCNote'),
    text = '';

// Darf nicht gemacht werden, wenn ein Benutzer aus der Gruppe GRP_CNCRestore eine Änderung macht
if (!utils.isUserInGroup(grp,object.lastModifier)) {

  let objectHistory = ChangeHistoryUtils.getLastHistoryObject(object);

  if (objectHistory) {
    if (!utils.compare(object, objectHistory)) {
      // Jetzt muss eine Notiz angehängt werden
      //

      text = '<p>Ge&auml;ndert links:</p>' +
      '<ul>' +
      '  <li><a href="agorum:cnc_compare:' + object + '">Vergleich</a></li>' +

      '  <li><a href="agorum:cnc_historyRestore:' + object + ':' + objectHistory + '">Historie wiederherstellen</a></li>' +
      '</ul>' +
      '<p>&nbsp;</p>';

      utils.writeNote(object,text,grpNote.allUserMembers); //object.acl.allGrantedUsers

    } else {
      //text = 'Das CNC-Programm hat sich nicht geändert';
    }
  } else {
    //text = 'Das CNC-Programm wurde neu abgelegt';

  }
}
```

## Objektnamen per Skript überschreiben

Wenn Sie die Namen einzelner Objekte in *agorum core* ändern möchten, können Sie sie mit `objectTextKey` überschreiben. Sie sehen den neuen, mit `objectTextKey` angegebenen Namen anschließend überall in den Bedienoberflächen angezeigt, wenn nicht der technische Name des Objekts direkt für die Anzeige verwendet wird.

Objekte in *agorum core* haben verschiedene Namen:

* der Name oder technische Name
* der Textschlüssel
* der Anzeigename

Wenn Sie den angezeigten Namen verändern möchten, ist es oft möglich, den Textschlüssel zu setzen und dadurch in den Bedienoberflächen einen anderen Namen anzuzeigen.

Angenommen, Sie möchten den Anzeigenamen eines Ordners im Verzeichnis *Eigene Dateien* ändern. Sie können etwa den Namen des Ordners 'doctest' durch den besseren Namen 'Testverzeichnis für die Dokumentation' ersetzen:

```auto
let objects = require('common/objects');

objects.find('home:myfiles/doctest').objectTextKey = 'Testverzeichnis für die Dokumentation';
```

**Hinweis:** Der `objectTextKey` muss nach JavaScript-Konventionen angegeben werden. Verwenden Sie Escape-Zeichen für die Angabe von reservierten Zeichen, etwa \\' zur Angabe eines Apostrophs:

```auto
objects.find('home:myfiles/doctest').objectTextKey = 'Markus\' Dateien';
```

Durch das Setzen des `objectTextKey` wird der Name in der Anzeige geändert.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/cd7c0930-21b5-11ef-8dc6-005056aa0ecc)

```auto
OCR: Bitte gib mir den OCR-Text, den ich zusammenfassen soll. Ich werde dann:
```

Geänderter Objektname in der Suche

Wenn Sie `objectTextKey` oder `displayName` abfragen, wird der angegebene `objectTextKey` zurückgegeben.

```auto
let objects = require('common/objects');

[
  objects.find('home:myfiles/doctest').name,
  objects.find('home:myfiles/doctest').objectTextKey,
  objects.find('home:myfiles/doctest').displayName,
];
```

### Namen einer Benutzergruppe per Skript überschreiben

* * *

Sie können neben den Namen von Ordnern auch die Namen von anderen Objekten mit `objectTextKey` überschreiben, etwa den Namen einer Benutzergruppe.

```auto
let objects = require('common/objects');

objects.find('group:GRP_Demo').objectTextKey = 'Demo-Gruppe DOCTEST';
```

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/1fe75fc0-21bc-11ef-8dc6-005056aa0ecc)

```auto
OCR: Gruppen, MetaDB, Benutzer, Gruppen, Demo, acds, acw, agorum, agorum.admin.tools, agorum.ai.llm, agorum.mail.filter, d4wdemo, d4wdr, Demo, Demo, Gruppe, DOCTEST, DocForm, Kalender, SAP, Test, Ansicht, Vorschau, Objektinfo, Notizen, Rechte, Name, Beschreibung, Allgemein, Demo, Gruppe, DOCTEST, GRP_Demo, Beschreibung, Ersteller, roi, Erstelldatum, Dienstag, 04. 2008, 14:53:32, Besitzer, roi, Zuletzt durch, roi, Zuletzt, Dienstag, 04. 2008, 14:53:32, Inhalt, Intern, aktualisiert, Montag, 03. Juni 2024, 13:49:08
```

Anzeige einer Benutzergruppe mit geändertem Namen

## DocumentTextObjects löschen und neu indizieren (Skript)

Das folgende Skript löscht **DocumentTextObject** und sendet dieses neu durch den Index. Je nach Datenmenge verändert sich die Laufzeit des Skripts.

**Hinweis**: Sie benötigen die [Solr](#)\-Suchmaschine in *agorum core*, um das Skript benutzen zu können.

```auto
// DocumentTextObjects löschen
// Unten in den Aufruf: clear(..) das entsprechende Suchmuster einstellen.
// Mit diesem Skript können Sie dasselbe durchführen wie mit dem desk4web-Tool "Delete Document Text of objects".

let IndexHelper = Packages.agorum.roi.searchengine.IndexHelper;

let objects = require('common/objects');
let transaction = require('common/transaction');

function clear(query) {
  let count = 0;

  objects.query(query).iterate('uuid', row => {
    let object = objects.tryFind(row.uuid);
    if (!object) return;

    // Prüft, ob "documentText" bereits vorhanden ist.
    if ((object.text || '').trim().length > 0) return;

    transaction(() => {
      // disable realTime indexing in current transaction
      IndexHelper.disableRealtimeIndex();

      // Entfernt den existierenden "documentText".
      object.deleteDocumentText();

      objects.reIndex(object);

      ++count;
    });
  });

  return count;
}

// Suche definieren, für welche Objekte der Dokumenttext weggeworfen werden soll.
clear('nameextension:(html OR htm OR txt OR json OR xml)');
```

