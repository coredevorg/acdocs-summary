# JavaScript per CronJob ausführen summary

## JavaScript per CronJob ausführen

Mithilfe eines CronJobs führen Sie ein JavaScript in definierten Abständen aus.

* Zeitpunkt und Intervall sind individuell einstellbar.
* Bei Aktiven Ordnern und Workern ist das Zeitintervall vorgegeben und kann nicht geändert werden, etwa werden Aktive Ordner jede Minute ausgeführt.
* Durch einen CronJob ist es möglich, jede Nacht um 3 Uhr ein Skript auszuführen. Hierdurch vermeiden Sie eine permanente Belastung des Systems.

### Unterschied zwischen CronJob, Task und Worker

* * *

**CronJob**

Ein [CronJob](#CronJob) ist eine Konfiguration für die regelmäßige Ausführung eines JavaScripts in der MetaDB. Die Log-Informationen für die Überwachung eines CronJobs finden Sie im *Support Tool* im Bereich *Active Folder*.

**Task**

Ein [Task](#) wird mithilfe der JavaScript-Bibliothek *agorum.task* entwickelt. Die Bibliothek erlaubt es, Aufgaben zu automatisieren, und einmalig, zu einem geplanten Zeitpunkt oder regelmäßig auszuführen. Zudem können Tasks parallel ausgeführt werden. Im Workspace bekommen Sie einen Überblick über alle vorhandenen Tasks und können den nächsten Ausführungszeitpunkt einsehen. Die Überwachung erfolgt über das *Support Tool* im Bereich *Base System*.

**Worker**

Ein [Worker](#) ist eine Einstellung im Support Tool, die häufig auf einer Suchanfrage basiert. Die Suchtreffer werden mit einem JavaScript weiterverarbeitet. Die Überwachung erfolgt über das *Support Tool* im Bereich Worker. Im Gegensatz zu CronJobs und Tasks werden Worker sofort ausgeführt, sobald die Situation zutrifft, die den Worker auslöst, etwa wenn ein Suchtreffer gefunden wird. Durch die Suchanfragen kann das System belastet werden. Sie sollten Worker also vor allem dann verwenden, wenn die Änderungen wirklich sofort nach Eintreten einer bestimmten Bedingung durchgeführt werden müssen und nicht auf den nächsten Zeitpunkt einer regelmäßigen Ausführung durch einen CronJob oder Task warten können.

| Kriterium | Task/CronJob | Worker |
| --- | --- | --- |
| Einrichtung | Script-Erstellung durch Entwickler | Oberflächengestützte Einrichtung im Support Tool |
| Verwendungszweck | Einmalige oder wiederkehrende Aufgaben. | Unmittelbare Ausführung bei Eintreten der Ausgangssituation. |
| Parallelität | Tasks mit verschiedenen IDs können parallel ausgeführt werden. Wiederkehrende, identische Aufgaben werden nach einander gestartet. CronJobs können nur sequenziell ausgeführt werden. | Parallele Ausführung mehrer Worker konfigurierbar. |
| Zeitliche Steuerung | Konfigurierbare zeitliche Taktung, bei Nichtverfügbarkeit des Systems wird der Task zum nächstmöglichen Zeitpunkt ausgeführt. | Unmittelbare Ausführung. |
| Überwachung | Fehler im agorum core support tool im Log sichtbar. | Fehler im agorum core support tool im Log sichtbar. |

#### Wann benutze ich CronJob, Task oder Worker?

**Wann sollten Sie einen CronJob oder einen Task benutzen?**CronJobs sind optimal für regelmäßige, sequenzielle Aufgaben, die in festen Intervallen ausgeführt werden. Tasks eignen sich ebenfalls für wiederkehrende oder einmalige Aufgaben und können zusätzlich parallel ausgeführt werden. Sie bieten Flexibilität und eine gute Fehlerbehandlung.

**Wann sollten Sie einen Worker** **benutzen?**Worker eignen sich für zeitnahe und parallele Aufgaben, insbesondere wenn kontinuierliche Überwachung und sofortige Reaktion erforderlich sind. Sie belasten das System jedoch durch laufende Suchanfragen.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/802d1350-69cb-11ef-99b9-005056aa0ecc)

```auto
OCR: nein, CronJob, nein, Parallele erforderlich, Automatisierung wiederkehrender Aufgaben, Sofortige notwendig, Task Worker
```

### Einen CronJob anlegen

* * *

1. Öffnen Sie links in der Seitenleiste **Administration** und dann **MetaDB**.
2. Öffnen Sie den Pfad:

    ```auto
    MAIN_MODULE_MANAGEMENT/cronjob/control
    ```

3. Legen Sie eine **Property-Gruppe** an:

    ```auto
    [ <Ihr Konfigurationsprojekt> ]
    ```

4. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAAMCAYAAAC9QufkAAAAaUlEQVQoFWP4/uD0f//MLf8ZMPDh/we+f///HQ9meLBxFxaN2AxDFoMYTKZmqEHk2UyCZv+Nz/5//379fwN6uBBjM1maG05hC+1n/xc0EOFsijTD4p4sZ1NFM8wQDBp38kROUdjYu/4DAJo7vBrmO/P5AAAAAElFTkSuQmCC) ein **Property-Bundle** mit einem beliebigen Namen an.
5. Öffnen Sie das neue **Property-Bundle** mit einem Doppelklick.
6. Legen Sie über ![embedded image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAALCAYAAACgR9dcAAAASklEQVQoFWN4sHHXf4bMLXix/8Zn/79//46BGSjSjM1EYsVIsPn6/4bMLf+RvUCZZmKd+P07Fpsp0owrtCF+g9iGMyopsnnANAMAdi8bRRmARxAAAAAASUVORK5CYII=) jeweils nacheinander folgende [Property-Entrys](#PropertyEntrys) an.**Class**Definiert die Klasse.**CronTime**Bestimmt, um welche Uhrzeit oder in welchen Abständen der CronJob Daten ausgibt und ist frei konfigurierbar.**ParameterNames**Definiert den Namen des Parameters.**ParameterValues**Definiert den Wert des Parameter (hier: Pfad zum verwendeten Skript).
7. Klicken Sie pro Property-Entry auf **Speichern**.
8. Erweitern Sie die Datei **export.yml** Ihres Konfigurationsprojektes um den MetaDB-Eintrag.

#### Property-Entrys

| Name | Datentyp | Wert (String) |
| --- | --- | --- |
| Class | Zeichenkette (String) | agorum.roi.cron.JSCronTaskFactory |
| CronTime | Zeichenkette (String) | Beispiele: Immer um 11 Uhr 0 11 \* \* \* Minütlich \* \* \* \* \* Eingabemöglichkeiten per Generator finden Sie im Web unter dem Stichwort crontime generator. Hinweis: Sollte der CronJob länger laufen als hier angegeben, startet der CronJob seinen Lauf nicht erneut. Wenn Sie etwa eine minütliche Ausführung angeben, der CronJob für die Abarbeitung der Aufgaben jedoch etwa 5 Minuten benötigt, startet der nächste Lauf erst, nachdem der vorherige Lauf beendet wurde. Der CronJob startet also nicht erneut 4 Mal während dieser Zeit. |
| ParameterNames | Zeichenkette (String) | Beispiel JS |
| ParameterValues | Zeichenkette (String) | Beispiel /agorum/roi/customers/agorum/js/<JavaScript-Datei.js> |

### Einen CronJob als Worker-Ersatz verwenden

* * *

Einen CronJob können Sie so verwenden, dass er wie ein QueryScript-Worker funktioniert. Hierfür passen Sie das JavaScript an.

#### Beispiel eines CronJob-JavaScripts

Im folgenden JavaScript für einen CronJob wird ein Worker nachgebildet. Der CronJob soll Objekte erkennen, aus einem Ordner herausnehmen und in einen anderen Ordner ablegen:

**Hinweis**: Bei der Query sollten Sie stets ein nicht vererbtes Metadatum prüfen, da bei vererbten Metadaten aufgrund einer Asynchronität ein zeitlicher Versatz existieren könnte.

```auto
/* global object */

// this is called from a cronjob
let objects = require('common/objects');
let transaction = require('common/transaction');
let metadata = require('common/metadata');

// this is a sample query, put in any query, that should match the objects, that should be handled by this cronjob
// after the cronjob has finished, you have to do something, that marks the object, that it is not found by the
// the query, otherwise it gets handled again.
// This is just an example. You can use any other query, like searching for the existance of a metadata-value or anyhting else...
let query = 'inpath:${ID:/agorum/roi/Files/incoming} NOT agorum_file_processed';

// the output folder
let target = objects.find('/agorum/roi/Files/done');

objects.query(query).iterate('uuid', data => {
  transaction(() => {
    let object = objects.tryFind(data.uuid);

    // check if object still exists
    if (object) {
      // .. do something with the object ..

      // move it away from incoming-folder, so that it is not found next time, the cronjob runs
      // remove from all parents
      objects.remove(object);

      // move to done folder
      objects.add(object, [ target ]);
      metadata({agorum_file_processed: true}).save(object);
    }
  });
});
```

**Hinweis:** Fehlermeldungen, die während der Ausführung des CronJobs auftreten, erscheinen im Serverlog und nicht im *agorum core support tool.*

**Parameter**

| Parameter | Beschreibung |
| --- | --- |
| query | Definiert den Pfad, aus dem das System die Dateien herausholt. |
| target | Definiert den Pfad, in den das System die Dateien verschiebt. |
| object | Definiert das Objekt, das das System durch eine UUID finden soll. |

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/5dcc8890-2a6d-11ec-86a3-005056aa0ecc)

```auto
OCR: Action,Reset action,Description:Query Script Worker,Status:OK,Name,Worker Name,Beispiel_Worker,Concurrency,Worker concurrency level,1,Hidden objects,Include hidden objects (history objects, sub-objects) in the working set,Query,Query,inpath:${ID:/agorum/roi/Files/incoming},Properties,Properties,uuid,JavaScript,JavaScript code,/* global sc, data */,let objects = require('common/objects'),let object = objects. tryFind(data.uuid),let target = objects.find('/agorum/roi/Files/done'),// check if object still exists,if (object) { // .. do something with the object .. ,objects.remove(object),// move to done folder,objects.add(object, [ target ]) },Action,Reset action,Description,Query Script Worker,Status,Name,Worker Name,Beispiel_Worker,Concurrency,Worker concurrency level,Hidden objects,Include hidden objects (history objects, sub-objects) in the working set,Query,Query,inpath:agorum/roi/Files/incoming,Properties,Properties,uuid,JavaScript,JavaScript code,global data,let objects = require('common/objects'),let object = objects.tryFind(data.uuid),let target = objects.find('/agorum/roi/Files/done'),// check if object still exists,if (object) { // .. do something with the object .. ,objects.remove(object),// move to done folder,objects.add(object, [ target ]) }
```

Beispiel-Worker zum Beispiel-CronJob

## JavaScript-Bibliothek agorum.task/js/task

Mithilfe dieser JavaScript-Bibliothek können Sie einmalige oder wiederkehrende Aufgaben planen und ausführen.

* Die Bibliothek verhält sich ähnlich wie ein CronJob innerhalb von *agorum core*, mit dem Unterschied, dass das System den Task auch ausführt, wenn das System zum Ausführungszeitpunkt nicht läuft. In diesem Fall startet der Task zum nächstmöglichen Zeitpunkt.
* Sie können zudem einen Task zu einem Startzeitpunkt in der Zukunft planen.
* Einmalige sowie regelmäßige Ausführungen sind möglich.
* Das System startet keine parallel zueinander laufenden Tasks.**Beispiel zum parallel laufenden Task**Ein Task benötigt 10 Minuten zur Bearbeitung, wird aber laut Skript jede Minute gestartet. Das System startet den nächsten Task erst, wenn der vorhergehende beendet ist. Dadurch können Sie mit try-catch Fehler / Probleme abfangen, und der *agorum task* läuft stabiler durch als etwa Worker.

### Verwendung

* * *

Diese Bibliothek binden Sie stets am Anfang eines Skripts ein:

```auto
let task = require('/agorum/roi/customers/agorum.task/js/task');
```

### agorum.task einrichten

* * *

1. Öffnen Sie den Ordner **js** in Ihrem Konfigurationsprojekt:

    ```auto
    Eigene Dateien/Administration/customers/<Konfigurationsprojekt>/js
    ```

2. Erstellen Sie den Ordner **task**:

    ```auto
    Eigene Dateien/Administration/customers/<Konfigurationsprojekt>/js/task
    ```

3. Erstellen Sie dort eine JavaScript-Datei und benennen Sie diese beliebig.
4. Programmieren Sie in diesem Skript die Aufgabe des *agorum.task*.**Beispiel**: Ausgaben für das Log ausgeben (siehe [Funktionen](#Funktionen)):

    ```auto
    module.exports = {
      run: () => {
        console.log('mein task: ' + new Date());
      }
    };
    ```

5. Öffnen Sie den Ordner **deploy/<pre|post>** Ihres Konfigurationsprojekts:

    ```auto
    Eigene Dateien/Administration/customers/<Konfigurationsprojekt>/deploy/<pre|post>
    ```

6. Erstellen Sie dort eine JavaScript-Datei.
7. Definieren Sie den Startzeitpunkt, die CronTime und welches Skript für diesen *agorum.task* gestartet werden soll:

    ```auto
    let task = require('/agorum/roi/customers/agorum.task/js/task');

    //task.id('<eindeutiger-name-des-tasks>').cron('* * * * *').post('require(\'/agorum/roi/customers/<Konfigurationsprojekt>/js/task/<JavaScript-Datei>\').run();');

    //Beispiel
    task.id('testprojekt123.test.task').cron('* * * * *').post('require(\'/agorum/roi/customers/testprojekt123/js/task/test-task\').run();');
    ```

8. Klicken Sie auf **RUN**, um den *agorum.task* zu registrieren.**Ergebnis**: Je nachdem, welche Einstellungen Sie vorgenommen haben (siehe [Funktionen](#Funktionen)), startet der *agorum.task* automatisch.

    **Tipp**: in dem hier vorgestellten Beispiel wird eine Konsolenausgabe erzeugt:

    ```auto
    console.log('mein task: ' + new Date());
    ```

    Diese Ausgabe erscheint im *support tool* unter *Base System > Schaltfläche „Show Log*“.

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/2ef73900-bf56-11ed-8435-005056aa0ecc)

    ```auto
    OCR: Bitte gib mir den OCR-Text, den ich zusammenfassen soll. Ich werde dann:
    ```

    Anzeige von console.log() im *support tool*

### agorum.task ändern

1. Öffnen Sie den Ordner **js/task** in Ihrem Konfigurationsprojekt:

    ```auto
    Eigene Dateien/Administration/customers/<Konfigurationsprojekt>/js/task
    ```

2. Ändern Sie die JavaScript-Datei für den *agorum.task* nach Bedarf.

    **Hinweis:** Wenn Sie den Namen des Tasks ändern, müssen Sie den Task mit dem alten Namen im Workspace löschen:

    ```auto
    Eigene Dateien/Administration/workspace/agorum.task/tasks
    ```

3. Öffnen Sie den Ordner **deploy/<pre|post>** Ihres Konfigurationsprojekts:

    ```auto
    Eigene Dateien/Administration/customers/<Konfigurationsprojekt>/deploy/<pre|post>
    ```

4. Überprüfen Sie die Einstellungen für die Ausführung dieses *agorum.task*:

    ```auto
    let task = require('/agorum/roi/customers/agorum.task/js/task');

    //task.id('<eindeutiger-name-des-tasks>').cron('* * * * *').post('require(\'/agorum/roi/customers/<Konfigurationsprojekt>/js/task/<JavaScript-Datei>\').run();');

    //Beispiel
    task.id('testprojekt123.test.task').cron('* * * * *').post('require(\'/agorum/roi/customers/testprojekt123/js/task/test-task\').run();');
    ```

5. Klicken Sie auf **RUN**, um den *agorum.task* neu zu registrieren.

### Laufende agorum.tasks einsehen

* * *

Welche *agorum.tasks* gerade aktiv sind, können Sie im Workspace einsehen.

**Achtung**: Datenverlust bei Änderung eines *agorum.task*s im Workspace. Änderungen an dieser Stelle werden durch ein Update des Systems wieder überschrieben. Ändern Sie niemals einen *agorum.task* im Workspace, sondern passen Sie den *agorum.task* im entsprechenden Konfigurationsprojekt an.

1. Öffnen Sie als Super-Administrator **roi** folgenden Pfad:

    ```auto
    Eigene Dateien‎/Administration‎/workspace‎/agorum.task‎/tasks‎
    ```

    **Ergebnis**: Alle aktiven *agorum.tasks* erscheinen.In der Objekt-Info des jeweiligen *agorum.tasks* können Sie etwa den nächsten Startzeitpunkt oder den vorgegebenen Cron-Zeitplan einsehen.

    ![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/b2831b30-bf57-11ed-8435-005056aa0ecc)

    ```auto
    OCR: Weitere Apps, Explorer, docform, Suche, Administration, workspace, agorum.task, tasks, agorum.mail, agorum.mail.filter, Ansicht, Vorschau, Objektinfo, Notizen, Rechte, Wiederherstellen, Audit, Name, agorum.mapping, agorum.metadata.collection, te1896.test.task.js, Metadaten, agorum.pdf, jagorum.pdf.annotate, acbasicarchive_workspace, workspace, acmsg, Cron, Zeitplan, acmsg, Eingang, Workflow, Aufgaben, agorum, core, Dokumentation, Administration, Serverpapierkorb, agorum.sessioninfo, jagorum.stamp.document, agorum.task, tasks, agorum.temporary, agorum.uninstall.manager, save, agorum.user, Audit, Tool, Startzeitpunkt, Area, Area, Freitag, 10., 2023, 16:26:00, workspace, agorum.task, meine_grundlagen_beispiele_, workspace, Ablageorte
    ```

    *agorum.task* im Workspace sichtbar

### Fehlermeldungen einsehen

* * *

Läuft Ihr *agorum.task* in einen Fehler, erscheinen diese Fehler im *agorum core support tool* unter *Base System*:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/e8d8d510-e8c1-11ed-834e-005056aa0ecc)

```auto
OCR: Dashboard, Overview, Show, Log, Configure, Log, Log, Actions, Base, System, Actions, Checks, Configurations, Sub, Statistics, Folders, AdminSync, DocForm, Name, Description, Subsystem, Status, Error, CoreStatistic, agorum, core, base, system, Checks, checks, are running, Updated 2023-05-02 10:17:28, Active, Notifications, Service Status, Task Status, Idle, Warning Count, 3290, Error Count, 8251, Date, Sub, System, Message Count, Object, Severity, 2023-05-02 10:17:02, CoreStatistic, Error, running task, te1896.test.task, Error Details
```

Fehler im *agorum core support tool* einsehen

### Funktionen

* * *

#### id

Initialisiert die Task-Bibliothek für die Einrichtung des Tasks.

**Syntax**

```auto
let aTask = task.id('<eindeutiger-name-des-tasks>');
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Default-Wert |
| --- | --- | --- | --- |
| id | Definiert die ID des Tasks. Die ID muss systemweit eindeutig sein. Stellen Sie das Präfix des Projekts voran. Beispiel ihr.projekt.name.name-des-tasks | ja | – |

**Beispiel**

```auto
let task = require('/agorum/roi/customers/agorum.task/js/task');

let aTask = task.id('agorum.sample.task1');
```

**Rückgabewerte**

Sie erhalten eine Instanz des Tasks zurück, mit der Sie alle weiterführenden Funktionen aufrufen können.

**Verwendung**

Diese Funktion verwenden Sie zur Initialisierung.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### time

Definiert optional ein Datum, ab wann dieser Task das erste Mal laufen soll.

Geben Sie kein Datum an oder lassen den Aufruf von *time* weg, läuft der Task sofort.

**Syntax**

```auto
aTask = aTask.time(new Date('2022-12-31'));
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Default-Wert |
| --- | --- | --- | --- |
| date | Definiert ein date-Objekt, d. h. ab wann der Task das erste Mal laufen soll. | nein | new Date() |

**Beispiel**

```auto
let task = require('/agorum/roi/customers/agorum.task/js/task');

let aTask = task.id('agorum.sample.task1').time(new Date('2022-12-31'));
```

**Rückgabewerte**

Sie erhalten eine Instanz des Tasks zurück, mit der Sie alle weiterführenden Funktionen aufrufen können.

**Verwendung**

Diese Funktion verwenden Sie zum Setzen eines ersten Ausführungszeitpunkts für den Task.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### cron

Definiert das Intervall, mit dem das System diesen Task ausführt.

Lassen Sie *cron* weg, führt das System den Task nur einmal aus und löscht ihn.

**Syntax**

```auto
aTask = aTask.cron('* * * * *);
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Default-Wert |
| --- | --- | --- | --- |
| schedule | Definiert das Ausführungsintervall, mit dem das System den Task ausführt. Die Angabe ist analog zu bekannten Crontabs (siehe Wikipedia-Suche nach Cron). Das System setzt das Intervall zurück und führt den Task nur einmalig aus, wenn der Wert null ist. | nein | null |

**Beispiel**

```auto
let task = require('/agorum/roi/customers/agorum.task/js/task');

// Beispiel: Task ab dem 31.12.2022 ausführen und dann immer jede Minute
let aTask = task.id('agorum.sample.task1').time(new Date('2022-12-31')).cron('* * * * *');
```

**Rückgabewerte**

Sie erhalten eine Instanz des Tasks zurück, mit der Sie alle weiterführenden Funktionen aufrufen können.

**Verwendung**

Diese Funktion verwenden Sie zum Setzen eines Ausführungsintervalls.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### post

Erstellt/ ändert die Einstellungen des definierten Tasks und gibt die JavaScript-Funktion mit, die dieser Task ausführen soll.

Der Task ist eingerichtet und wird vom System verarbeitet, sobald das System *post* aufruft.

**Syntax**

```auto
aTask.post('JavaScript-Code');
```

**Parameter**

| Parameter | Beschreibung | Pflicht | Default-Wert |
| --- | --- | --- | --- |
| script | Definiert den JavaScript-Code, den der Task ausführt. | ja | – |

**Beispiel**

```auto
let task = require('/agorum/roi/customers/agorum.task/js/task');

// Beispiel 1: Task erstellen und ab dem 31.12.2022 immer minütlich laufen lassen
task.id('agorum.sample.task1').time(new Date('2022-12-31')).cron('* * * * *').post('require(\'irgendeine-lib\').run();');

// Beispiel 2: Task erstellen und ab sofort minütlich laufen lassen
task.id('agorum.sample.task1').cron('* * * * *').post('require(\'irgendeine-lib\').run();');

// Beispiel 3: Task erstellen und einmalig ab sofort laufen lassen.
task.id('agorum.sample.task1').post('require(\'irgendeine-lib\').run();');
```

* Der JavaScript-Code kann ein beliebiger *agorum core*\-JavaScript Code sein.
* Geben Sie diesen Code als String an.
* Lagern Sie den Code in eine separate JavaScript-Datei aus, die Sie über *require* laden und ausführen, wie in den obigen Beispielen dargestellt.

**Beispiel für require**

```auto
// Datei /agorum/roi/customers/<Konfigurationsprojekt>/js/task/my-task.js
module.exports = {
  run: () => {
    // Etwas tun ...
  }
};
```

* Rufen Sie den Task folgendermaßen auf:

```auto
let task = require('/agorum/roi/customers/agorum.task/js/task');

task.id('agorum.sample.task1').post('require(\'/agorum/roi/customers/agorum.sample/js/task/my-task\').run();');
```

* Requiern Sie stets den vollständigen Pfad zur JavaScript-Datei.

**Rückgabewerte**

Diese Funktion liefert keine Rückgabewerte zurück.

**Verwendung**

Diese Funktion verwenden Sie, um den Task zu erstellen oder zu ändern und letztlich zu speichern, sodass das System diesen ausführen kann.

**Exceptions**

Zu dieser Funktion existieren keine Exceptions.

#### cancel

Löscht einen vorhandenen Task.

**Syntax**

```auto
task.id('eine-task-id').cancel();
```

**Parameter**

Zu dieser Funktion existieren keine Parameter.

**Rückgabewerte**

Diese Funktion liefert keine Rückgabewerte zurück.

**Verwendung**

Diese Funktion verwenden Sie, um einen vorhandenen Task abzubrechen.

**Exceptions**

Das System wirft eine Exception, wenn der Task mit der ID im System nicht existiert.

## Worker im agorum core support tool verwenden

**Ab welcher Version verfügbar?***• agorum core pro* 7.11

Mit einem Worker suchen und verarbeiten Sie Dateien automatisch. Was der Worker genau mit den Dateien machen soll, können Sie anpassen. Der Worker stimmt sich zeitlich selbst ab und fragt laufend das System ab.

### Unterschied zwischen Worker und CronJob

* * *

Unser Entwicklungsteam zieht einen [CronJob](#) einem Worker vor, da ein Worker das System laufend mit Suchanfragen belastet. Ein CronJob wird dagegen zeitlich eingetaktet. Sie können diesen etwa einmal pro Stunde laufen lassen. Der CronJob führt dann intern eine Query aus, ähnlich wie es der Worker machen würde.

**Wann sollten Sie einen Worker verwenden?**Wenn es zeitnah passieren soll und / oder wenn mehrere Threads parallel arbeiten können /sollen.

**Wann sollten Sie einen CronJob** **verwenden?**Wenn es nicht zeitkritisch ist und es in Ordnung ist, dass die Abarbeitung sequenziell passiert.

### Voraussetzungen

* * *

Sie müssen folgende Voraussetzungen erfüllen, um Worker verwenden zu können:

* Sie können in JavaScript programmieren.
* Sie kennen die [agorum core smart search](#).
* Sie kennen die wichtigsten [JavaScript-Bibliotheken](#) von *agorum core*, etwa [common-objects](#).

Damit die Worker performant laufen, achten Sie auf folgende Punkte:

* Globale Variablen könnten bereits aus vorherigen Durchläufen belegt sein.
* Konstanten (const) dürfen nicht auf der obersten Ebene definiert werden, da diese sonst bei nachfolgenden Durchläufen als Neudefinition gewertet werden.
* Mit *require()* eingebundene externe Skripte werden pro Kontext nur einmal geladen, auch wenn sie sich geändert haben.
* Wird ein externes Skript verändert, muss der Worker per Schaltfläche *Reset worker* zurückgesetzt werden, damit sich die Änderungen auswirken.

### Speicherort der Worker

* * *

Das System speichert die erstellten Worker automatisch in der MetaDb unter einem bestimmten Pfad.

So finden Sie die Worker:

1. Öffnen Sie auf der Startseite von *agorum core* **Administration**.
2. Wählen Sie links im Menü **MetaDb**.
3. Öffnen Sie den Pfad:

    ```auto
    /MAIN_MODULE_MANAGEMENT/workers
    ```

### Anzahl an Workern und Systemressourcen

* * *

**Hinweis**: Die Anzahl an Worker ist abhängig von Ihren Systemressourcen. In der Regel reicht ein Thread pro Worker aus.

### Anwendungsfälle

* * *

Anbei finden Sie drei mögliche Anwendungsfälle für einen Einsatz.

#### Nachträgliche Anpassung an Updates im System

Seit Wochen, Monaten oder auch Jahren werden Dokumente im System abgelegt. Doch wie bei jedem Digitalisierungsprozess werden eines Tages zwei neue Workflows etabliert:

* Workflow für Fragebögen
* Workflow für Feedbackbögen

Damit das System unterscheiden kann, für welches Dokument welcher Workflow greifen soll, wird ein neues Metadatum gesetzt.

Dieses neue Metadatum greift für alle neu im System abgelegten Dokumente. Doch die Benutzer wünschen sich, dass sie auch alte Dokumente mit dem neuen Workflow bearbeiten können. Da diesem das notwendige Metadatum fehlt, wird ein temporären Worker erstellt. Dieser sucht nach diesen Frage- und Feedbackbögen und setzt je das dazu passende Metadatum.

Sobald der Worker durchgelaufen ist, können unsere Benutzer die neuen Workflows auf die alten Dokumente anwenden.

#### Nachträgliche Ablage

Rechnungen sollen für das Finanzamt in einer dazu passenden Ordnerstruktur verlinkt werden. Anstatt Dokumente im Ablageprozess zu verlinken, können Sie auch einen Worker bauen, der nach diesen Rechnungen sucht und diese verlinkt.

#### Falsch angelegte Dokumente

Über Tage oder Monate hinweg werden Ordner und Dokumente mit einem falschen Namen oder einem falschen Metadatum abgelegt. Nach diesen fehlerhaften Einträgen kann gesucht und das zutreffende Objekt entsprechend abgeändert werden.

### Einen Worker öffnen

* * *

1. Öffnen Sie auf der Startseite von *agorum core* **Support tool**.
2. Wählen Sie links im Menü **Workers**.**Ergebnis**: Zwei weitere Einträge (Actions und Sub Statistics) erscheinen. Über diesen Bereich können Sie Worker konfigurieren, starten, stoppen, löschen sowie Statistiken und Logs einsehen.

#### Eintrag „Actions“

Hier haben Sie die Möglichkeit, zwei verschiedene Worker zu erstellen:

**QueryScript-Worker**Ein QueryScript-Worker findet in gut 95 % der Fälle Verwendung. Mit diesem bauen Sie eine Suchfunktion anhand von Metadaten auf. Diese Suche erkennt zu bearbeitende Dateien und reicht diese an ein JavaScript weiter.

[So erstellen Sie einen QueryScript-Worker](#QueryScriptWorker)

**ScriptWorker**Ein ScriptWorker wird selten verwenden. Bei diesem reicht die Suche nach Metadaten nicht aus, um die zu bearbeitenden Dateien zu finden. Stattdessen verwendet ein ScriptWorker ein JavaScript, um die gewünschten Objekte zu finden. Diese werden wiederum zur Bearbeitung an ein JavaScript weitergereicht.

[So erstellen Sie einen ScriptWorker](#ScriptWorker)

#### Eintrag „SubStatictis“

Öffnen Sie den Bereich *SubStatistics*, finden Sie in weiteren Untereinträgen Folgendes:

* Ihre selbst erstellten Worker
* Im Standard mitgelieferte Worker
* Dazugehörige Logausgaben

Die mitgelieferten Worker dienen zur allgemeinen Funktion des Systems, etwa der *MetadataInheritor*, der für die Vererbung von Metadaten benötigt wird.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/262b7510-e3da-11eb-a19b-005056aa0ecc)

```auto
OCR: Dashboard, Base, System, Active, Folders, Sync, Workers, Actions, Statistics, Worker acds_acl_worker, Worker acds_generate_ove, Worker acsoTaskActivateBy, Worker acw_set_metadata, Worker agorum, core, mail
```

Eintrag *SubStatistics*

**Achtung**: Systemschäden durch Löschen der im Standard mitgelieferten Worker. Entfernen Sie die bereits enthaltenen Worker nicht, da das System ansonsten nicht mehr ordnungsgemäß funktioniert. Erstellen Sie eigene Worker, anstatt die mitgelieferten zu löschen. Zur Unterscheidung können Sie etwa im JavaScript einen Kommentar setzen, aus dem hervorgeht, dass Ihr Unternehmen diesen Worker erstellt hat.

### Worker zeitlich aufeinander abstimmen

* * *

Worker, egal ob QueryScript-Worker oder Script-Worker*,* suchen in regelmäßigen Zeitabständen nach Ihrem eigenen Arbeitsvorrat. Haben diese Worker viel zu tun, prüfen diese in schnellen Zeiteinheiten nach neuen Objekten, die bearbeitet werden müssen. Fiel dieser Arbeitsvorrat mehrmals leer aus, kann es bis zu 10 Sekunden dauern, ehe der Worker seine Suche erneut startet.

### Worker von einem Testsystem in ein Produktivsystem überführen

* * *

**Ab welcher Version verfügbar?**

• *agorum core* 8.2.0

Sie können Worker direkt mit der [export.yml](#) exportieren.

### Einen Worker pausieren

* * *

1. Setzen Sie die Threadanzahl (Concurrency) auf 0.

### Einen Worker löschen / aktualisieren /bearbeiten

* * *

Sobald Sie einen eigenen Worker erstellt haben, bekommt dieser wie [oben](#SubStatistics) beschrieben einen eigenen Funktionsbereich. Öffnen Sie ihn und scrollen Sie ganz nach unten, sodass Sie sich unterhalb des (letzten) JavaScriptes befinden. Dort finden Sie drei Schaltflächen:

#### Schaltfläche „Update worker script“

Nehmen Sie Änderungen im Skript oder bei den Einstellungen im *agorum core* *support tool* vor, speichern Sie mit dieser Schaltfläche Ihre Änderungen. Das System führt einen *Reset* des Skripts durch, sodass der Worker mit dem neuen Skript läuft.

Ausgeschlossen ist eine *​*​​​​​​Namensänderung. In diesem Fall erstellen Sie einen neuen Worker und löschen den aktuellen.

#### Schaltfläche „Reset worker“

Wenn ein JavaScript ausgeführt wird, wird es kompiliert, bevor es startet. Damit der Kompiler nicht jedes Mal ausgeführt wird, wird das kompilierte Skript gecacht und gestartet.

Die Schaltfläche löscht den Cache für dieses Skript, sodass das Skript anschließend neu geladen wird. Damit werden auch require-Verweise auf ein anderes Skript aus dem Cache gelöscht und bei erneutem Ausführen wieder neu kompiliert.

Wird der Worker zurückgesetzt, wird auch der aktuell verwendete JavaScript-Kontext verworfen.

#### Schaltfläche „Stop and remove worker“

Diese Schaltfläche stoppt den Worker und löscht ihn anschließend.

### QueryScriptWorker

* * *

Dieser Worker führt regelmäßig eine Suche nach Metadaten aus und übergibt das Ergebnis pro gefundenem Objekt an ein JavaScript. Jeder Aufruf des Skripts wird in einer Transaktion abgearbeitet.

#### Einen QueryScriptWorker erstellen

1. Öffnen Sie auf der Startseite von *agorum core* **Support tool**.
2. Wählen Sie links im Menü **Workers > Actions > QueryScript**.
3. Passen Sie die [Einstellungen](#EinstellungenDesQueryScriptWorkers) des Workers an.
4. Speichern Sie den angelegten Worker und testen Sie, ob der Worker die gewünschte Funktion ausführt.

Ein Worker kann etwa wie folgt aufgebaut werden:

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/5dcc8890-2a6d-11ec-86a3-005056aa0ecc)

```auto
OCR: Action,Reset action,Description:Query Script Worker,Status:OK,Name,Worker Name,Beispiel_Worker,Concurrency,Worker concurrency level,1,Hidden objects,Include hidden objects (history objects, sub-objects) in the working set,Query,Query,inpath:${ID:/agorum/roi/Files/incoming},Properties,Properties,uuid,JavaScript,JavaScript code,/* global sc, data */,let objects = require('common/objects'),let object = objects. tryFind(data.uuid),let target = objects.find('/agorum/roi/Files/done'),// check if object still exists,if (object) { // .. do something with the object .. ,objects.remove(object),// move to done folder,objects.add(object, [ target ]) },Action,Reset action,Description,Query Script Worker,Status,Name,Worker Name,Beispiel_Worker,Concurrency,Worker concurrency level,Hidden objects,Include hidden objects (history objects, sub-objects) in the working set,Query,Query,inpath:agorum/roi/Files/incoming,Properties,Properties,uuid,JavaScript,JavaScript code,global data,let objects = require('common/objects'),let object = objects.tryFind(data.uuid),let target = objects.find('/agorum/roi/Files/done'),// check if object still exists,if (object) { // .. do something with the object .. ,objects.remove(object),// move to done folder,objects.add(object, [ target ]) }
```

Einen QueryScriptWorker erstellen

#### Einstellungen des QueryScriptWorkers

| Einstellung | Beschreibung | Beispiel |
| --- | --- | --- |
| Name | Definiert den Namen des Workers. | – |
| Concurrency | Definiert die Anzahl der verwendeten Threads. Setzen Sie den Wert auf 0, ist dieser Worker inaktiv. | – |
| Hidden Objects | Definiert, dass der Worker auch versteckte Objekte wie die Historie und Versionierung bearbeitet. | – |
| Query | Definiert, welche Objekte durch den Worker bearbeitet werden sollen. Die Suche bauen Sie anhand der agorum core smart search und der Nutzung von etwa Wichtige Metadaten auf. Anhand von Metadaten und ggf. bestimmte Metadatenwerte fangen Sie somit Objekte ab. | Nach dem Ordner incoming suchen inpath:${ID:/agorum/roi/Files/incoming} Hinweis: Sie können auch Metadaten ausschließen, um einen Endlos-Loop zu vermeiden. Hierfür können Sie eine NOT-Formulierung anlegen, etwa: identifier: kundenakte acmf\_kundenname:\* NOT acmf\_kundennamerl:\* Metadaten werden hierbei oft als eine Art Status eingesetzt. Tipp: Kopieren Sie eine Query vorab in das agorum core information center, um zu überprüfen, dass Sie die gewünschten Objekte finden. Schreiben Sie Metadaten stets klein. |
| Properties | Definiert, welche Attribute / Metadaten des durch die Query gefundenen Objekts der Worker an das JavaScript übergibt. Im Standard reicht die UUID, da Sie mit dieser auf alle weiteren Eigenschaften der Objekte zugreifen. Mehrere Attribute trennen Sie mit einem Semikolon (;). | uuid Erklärung Hier wird die uuid des Objekts an das Workerscript übergeben. In dem JavaScript verwenden Sie diese durch den Aufruf data.uuid. |
| JavaScript | Fügt das JavaScript ein. | – |
| Save as a new worker | ​​​​​​Speichert den Worker. | – |

#### JavaScript-Beispiel zum QueryScriptWorker

In dem folgenden Beispiel wird ein JavaScript für einen QueryScriptWorker gezeigt, der ein Objekt aus einem Ordner herausnimmt und in einen anderen Ordner ablegt. Zum Einsatz kommt die JavaScript-Bibliothek [common-objects](#).

```auto
/* global sc, data */

let objects = require('common/objects');

// Objekt anhand der UUID finden

let object = objects.tryFind(data.uuid);

// Ausgabeordner für die Objekte

let target = objects.find('/agorum/roi/Files/done');

// Überprüfen, ob das Objekt noch da ist

if (object) {

  // Etwas mit dem Objekt machen...

  // Objekt aus dem Ordner "incoming" herausnehmen, sodass es nicht mehr in diesem Ordner zu finden ist

  // remove from all parents

  objects.remove(object);

  // Objekt in den Ordner "done" ablegen

  objects.add(object, [ target ]);

}
```

### ScriptWorker

* * *

Beim ScriptWorker wird der Arbeitsvorrat durch ein frei definierbares Skript produziert, dem Producer. Es können daher nicht nur Suchanfragen abgearbeitet werden, sondern etwa auch der Inhalt von Ordnern oder Einträge in einer CSV-Datei.

#### Einen ScriptWorker erstellen

1. Öffnen Sie auf der Startseite von *agorum core* das **Support tool**.
2. Wählen Sie links im Menü **Workers > Actions > ScriptWorker**.
3. Passen Sie die [Einstellungen](#Einstellungen des Script Workers) des Workers an.
4. Speichern Sie den angelegten Worker und testen Sie, ob der Worker die gewünschte Funktion ausführt.

![embedded image](https://agorumdocproxy.agorum.com/api/rest/object/embed/fb6e63e0-e3df-11eb-a19b-005056aa0ecc)

```auto
OCR: Action, Reset action, Name: WorkersStatistic.ScriptWorkerAction, Short description: ScriptWorker, Description:, Status: Name, Script Worker, OK, Worker Name, Name des Workers, Concurrency, Worker concurrency level, Producer, JavaScript code producing work items, 1 /* global sc, limit, idle */, 2, 3 let objects = require('common/objects'), 4, 5, Consumer, JavaScript code consuming work items, 1 /* global sc, data */, Save as new worker, Log, Date, Sub System, Message, Object ID, Severity, There are no events to show at this time
```

Einen ScriptWorker erstellen

#### Einstellungen des ScriptWorkers

| Einstellung | Beschreibung |
| --- | --- |
| Name | Definiert den Namen des Workers. |
| Concurrency | Definiert die Anzahl der verwendeten Threads. Setzen Sie den Wert auf 0, ist dieser Worker inaktiv. |
| Producer | Beim ScriptWorker wird der Arbeitsvorrat durch ein frei definierbares Skript produziert. Definieren Sie an dieser Stelle, welche Objekte das System wiederfinden soll, bevor diese dem Consumer-Skript überreicht werden. Als Rückgabewert des Producers wird ein Array erwartet, dessen Elemente den aktuellen Arbeitsvorrat darstellen. Ein Element kann entweder eine ID oder ein JavaScript-Objekt sein, das mindestens die Eigenschaft "id" besitzt. Diese Elemente werden durch das Worker-Framework aufgeteilt und einzeln als Parameter data an die Consumer-Threads übergeben. Der Wert von id wird außerdem vom Worker-Framework verwendet, um Duplikate automatisch auszufiltern. |
| Consumer | Definiert im Consumer-Skript, was Sie mit den gefundenen Objekten umsetzen möchten. Dieses Skript entspricht dem JavaScript-Feld des QueryWorkers. |
| JavaScript | Fügt das JavaScript ein. |
| Save as a new worker | ​​​​​​Speichert den Worker. |

#### limit und idle im Producer

Dem Producer werden vom Worker-Framework zwei Parameter übergeben.

| Parameter | Beschreibung |
| --- | --- |
| limit (number) | Definiert, wie viele Elemente erzeugt werden. Der Wert ist unter anderem von der konfigurierten Threadanzahl und der aktuellen Länge der Warteschlange abhängig. Bei diesem Wert handelt es sich um einen Richtwert. Darüber hinaus gelieferte Elemente werden nicht verworfen. Es empfiehlt sich folgender Ansatz für die beste Performance: Sind insgesamt weniger als <limit>-Elemente vorhanden, werden alle Elemente zurückgegeben. Sind insgesamt gleich viel oder mehr als <limit>-Elemente vorhanden, werden mindestens <limit>-Elemente zurückgegeben, aber der Wert wird nicht stark überschritten. Gehören die Elemente etwa zu zusammenhängenden Stapeln, sollte der letzte Stapel noch vollständig zurückgegeben und erst danach gestoppt werden. |
| idle (boolean) | Definiert, dass seit dem letzten Aufruf des Producers keine weiteren Elemente verarbeitet wurden. Dieser Parameter kann für Optimierungen, die diese Information benötigen, eingesetzt werden, um etwa gewisse Schritte zu überspringen. |

Die Parameter *idle* und limit werden nicht eingestellt, sondern vorgegeben. Daran kann sich das Producer-Skript orientieren, wenn es darum geht, wie viele Arbeitseinheiten es erzeugen sollte, damit die Consumer-Threads weiterhin beschäftigt sind.

#### Beispiel für die Abarbeitung der Elemente eines Ordners mithilfe des Fileworkflows

**Producer**Der Producer erzeugt ein Array aus den ersten <limit>-Objekten im Ordner */agorum/roi/Files/Eingang*. Das Producer-Skript wird jedes Mal im selben JavaScript-Kontext aufgerufen.

```auto
/* global sc, limit, idle */

let objects = require('common/objects');

objects.find('/agorum/roi/Files/Eingang').items().slice(0, limit).map(item => ({
  id: item.ID,
  object: item
}));
```

**Consumer**Der Consumer ruft für das übergebene Objekt den Fileworkflow auf:

```auto
/* global sc, data */

let workflows = require('common/workflows');

workflows.start('FileWorkflow2', data.object);
```

