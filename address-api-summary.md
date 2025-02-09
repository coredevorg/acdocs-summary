# JavaScript Address API summary

Diese Dokumentation gibt einen umfassenden Einblick in die Erstellung von Adressobjekten über eine JavaScript-API.

**Voraussetzungen**

- Sie benötigen JavaScript-Kenntnisse.
- Sie benötigen Verständnis für die verschiedenen Bibliotheken von _agorum core_.

**Hinweis**: Für bestimmte Parameter, etwa _target_ und _path_, siehe [JavaScript-Bibliothek common/objects](#).

### Verwendung

---

Die folgende Bibliothek muss stets zu Beginn eines Skripts stehen:

```javascript
let address = require('address/objects');
```

### Verwendbare Objekte

---

**Adressbuch**

- D4wAddressBook
  - name
  - description
  - items()

**Firma**

- D4wAddressOrganisation
  - name
  - additionalName1
  - additionalName2
  - customerNumber
  - salesTaxIdentificationNumber (USt-Id)
  - taxNumber (Steuernummer)
  - description
  - items()

**Abteilung**

- D4wAddressDepartment
  - name
  - additionalName1
  - additionalName2
  - customerNumber
  - salesTaxIdentificationNumber
  - taxNumber
  - description
  - addressLinks
  - addressPhoneNumbers
  - items()

**Person**

- D4wAddressPerson
  - salutation
  - title
  - givenName
  - familyName
  - familyStatus
  - dateOfBirth
  - description
  - myContainers
  - sex (male (männlich) , female (weiblich), unknown (unbekannt))
  - placeOfBirth
  - maidenName
  - welcomeMessage

**Zusatzinformation zur Person**

- D4wAddressInfo
  - jobTitle
  - activityRate

**Tatsächliche Adresse**

- D4wAddressData
  - street1
  - zip
  - city
  - state
  - country
  - postBox
  - zipPostBox
  - cityPostBox
  - houseNumber1

#### Adress Container

Dieser Container bildet den Link zwischen Person und Adressbuch, Firma oder Abteilung. Auf alle untergeordneten Objekte können Sie ausschließlich _get_ ausführen.

- D4wAddressContainer

  - d4wAddressPerson
  - d4wAddressData (Holt die Adresse, die es für das Objekt gibt.)
  - d4wMyAddressData (Holt ausschließlich die Adresse, die zu dem aktuellen Objekt belegt wurde.)
  - firstAddressImage
  - d4wAddressInfo
  - addressEmails

  - addressLinks

  - addressPhoneNumbers

**Hinweis**: Bei *d4wAddressData* vererbt das System die geholten Adressen. Hat eine Firma eine Adresse, liefert das System diese auch bei Personen zurück, sofern diese unter der Firma verknüpft sind. Hat eine Person eine eigene Adresse, erhalten Sie diese zurück. Wenn die Person unterhalb einer Abteilung mit übergeordneter Firma, also _Firma > Abteilung > Person_, verknüpft ist, erhalten Sie Folgendes zurück:

- die eigene Adresse oder

- die Adresse der Abteilung, sofern diese eine eigene Adresse und die Person keine eigene hat, oder

- die Adresse der Firma, wenn weder die Person noch die Abteilung eine eigene Adresse hat

### Adressobjekte indizieren

---

**Ab welcher Version verfügbar?**

• _agorum core_ 10.0.11

Folgende Adressobjekte indiziert das System automatisch mit den aufgeführten Informationen, um die Adressobjekte gezielter finden zu können:

| Adressobjekt           | Beschreibung                                                                                   |
| ---------------------- | ---------------------------------------------------------------------------------------------- |
| addressname            | Enthält den Namen einer Organisation oder Abteilung.                                           |
| mymailaddresses        | Enthält ausschließlich die E-Mail-Adressen des zugehörigen Adressobjekts, nicht die vererbten. |
| mydefaultmailaddresses | Enthält ausschließlich die Standard-E-Mail-Adressen des zugehörigen Adressobjekts.             |
| mylinks                | Enthält ausschließlich die Links des zugehörigen Adressobjekts, nicht die vererbten.           |
| mydefaultlinks         | Enthält ausschließlich die Standard-Links des zugehörigen Adressobjekts.                       |
| mysubjects             | Enthält ausschließlich die Link-Betreffe des zugehörigen Adressobjekts, nicht die vererbten.   |
| mydefaultsubjects      | Enthält ausschließlich die Standard-Link-Betreffe des zugehörigen Adressobjekts.               |
| myfullnumbers          | Enthält ausschließlich die Telefonnummer des zugehörigen Adressobjekts, nicht die vererbten.   |
| mydefaultfullnumbers   | Enthält ausschließlich die Standard-Telefonnummern des zugehörigen Adressobjekts.              |

**Hinweis**: Wenn Sie _agorum core_ auf [Windows](#) oder [Linux](#) aktualisieren, indiziert das System alle vorhandenen Adressobjekte erneut. Je nach Menge der Adressobjekte erhöht sich kurzfristig die Indizierungsaktivität.

## JavaScript Address API - create

Mit dem Aufruf *create* legen Sie einzelne Objekte an.

### Verwendung

---

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```javascript
let address = require('address/objects');
```

### create.book

---

Mit diesem Aufruf legen Sie ein Adressbuch an.

*data* befüllen Sie wie folgt:

```javascript
let data = {
  name:        '<Name des Addressbuchs>',
  description: '<Beschreibung des Addressbuchs>',
  target:      '<Objekt, in dem das Addressbuch abgelegt wird>',
               // Wenn target null oder nicht vorhanden ist, wird automatisch
               // /agorum/roi/Files verwendet.
  path:        '<relativer oder absoluter Pfad>'
               // Ein relativer Pfad wird an target angehängt und,

               // sofern noch nicht vorhanden, angelegt.
};
```

Zum Anlegen des Adressbuchs existieren folgende Aufrufe:

| Aufruf    | Beschreibung                                                                                                           |
| --------- | ---------------------------------------------------------------------------------------------------------------------- |
| create    | Wenn das Adressbuch bereits vorhanden ist, gibt das System kein Adressbuch zurück, sondern erzeugt eine Fehlermeldung. |
| trycreate | Wenn das Adressbuch bereits vorhanden ist, gibt das System das Adressbuch zurück.                                      |

Bei _target_ handelt es sich um ein Objekt, das entweder früher oder direkt im Aufruf definiert wurde. Das Objekt ist frei wählbar, sofern nicht näher definiert.

- Wenn das Objekt es _null_ oder nicht vorhanden ist, verwendet das System automatisch den Pfad _/agorum/roi/Files_.
- _path_ ist optional.

**Beispiel zu target und path**

```javascript
target: objects.find('/agorum/roi/Files/Lehrpersonal'),
//path: null

//target: null,

path: 'Lehrpersonal'
```

Dieses Beispiel definiert beides Mal dasselbe Ziel:

- Einmal vollständig über _target_
- Einmal über _target : null_, wodurch das System *automatisch /agorum/roi/File*s verwendet. Durch _path_ fügt das System den gewünschten, letzten Teil zum Pfad hinzu.

#### Beispiel

```javascript
let address = require('address/objects');

let data = {
  name:        'Mein erstes Adressbuch',
  description: 'Sammlung aller wichtigen Adressen',
  target:       objects.find('/agorum/roi/Files/Schriftverkehr'),
  // path:      null

};

let book = address.create('book', data);

// oder

// let book = address.tryCreate('book', data);
```

### create.organisation

---

Mit diesem Aufruf legen Sie eine Firma an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  name:            '<Name der Firma/Organisation>',
  additionalName1: '<Zusatzname 1>',
  additionalName2: '<Zusatzname 2>',
  customerNumber:  '<Kundennummer>',
  taxNumber:       '<Steuernummer>',
  description:     '<beliebige Beschreibung>',
  target:          '<Objekt, in dem das Addressbuch abgelegt wird>',
                   // Wenn target null oder nicht vorhanden ist, wird automatisch
                   // /agorum/roi/Files verwendet.
  path:            '<relativer oder absoluter Pfad>',
                   // Ein relativer Pfad wird an target angehängt
                   // und, sofern noch nicht vorhanden, angelegt.
  salesTaxIdentificationNumber: '<Ust-Id>'
};
```

#### Beispiel

```javascript
let address = require('address/objects');

let data = {
  name:            'Unsichtbare Universität',
  additionalName1: '',
  additionalName2: '',
  customerNumber:  '12345',
  taxNumber:       '10 321 654 987',
  description:     'Organisation zur Bewahrung des Wissens',
  target:           null,
  path:            'UU/wirklichwissenswert',
  salesTaxIdentificationNumber: 'DE999999999'
};
// Aufruf:

let organisation = address.create('organisation', data);
```

### create.department

---

Mit diesem Aufruf legen Sie eine Abteilung an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  name:            '<Name der Abteilung>',
  additionalName1: '<Zusatzname 1>',
  additionalName2: '<Zusatzname 2>',
  customerNumber:  '<Departmentnummer>',
  taxNumber:       '<Steuernummer>',
  description:     '<beliebige Beschreibung>',
  target:          '<Objekt, in dem die Abteilung abgelegt wird>',
  path:            '<relativer oder absoluter Pfad>',
                   // Ein relativer Pfad wird an target angehängt und,

                   // sofern noch nicht vorhanden, angelegt.
  salesTaxIdentificationNumber: '<Ust-Id>'
};
```

#### Beispiel

```javascript
let address = require('address/objects');

let data = {
  name:            'Erzkanzlerei',
  additionalName1: '',
  additionalName2: '',
  customerNumber:  '1337',
  taxNumber:       '99 789 456 123',
  description:     'Abteilung des amtierenden Erzkanzlers',
  salesTaxIdentificationNumber: 'DE777777777'
  //path: null

};

//Aufruf:
let department = address.create('department', data);
```

### create.person

---

Mit diesem Aufruf legen Sie eine Person an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  salutation:     '<Anrede>',

                  // Auswahlmöglichkeiten:  'mr; mrs; mrmrs; family'
                  //(Herr, Frau, Herr und Frau, Familie)
  title:          '<Titel>',
  givenName:      '<Vorname>',
  familyName:     '<Familienname>',
  familyStatus:   '<Familienstatus>',
                  // Auswahlmöglichkeiten: 'unmarried (ledig),

                  // married (verheiratet), unknown (-)',
  dateOfBirth:    '<Geburtstag (Datum)>',
  description:    '<beliebige Beschreibung>',
  sex:            '<Geschlecht>',

                  // Auswahlmöglichkeiten: 'male (männlich), female (weiblich),

                  // unknown (unbekannt)',
  placeOfBirth:   '<Geburtsort>',
  maidenName:     '<Geburtsname>',
  welcomeMessage: '<Sehr geehrter Herr Familienname>',
  target:         '<Objekt, in dem das Addressbuch abgelegt wird>',
                  // Wenn target null oder nicht vorhanden ist, wird automatisch

                  // /agorum/roi/Files verwendet.
  path:           '<relativer oder absoluter Pfad>'
                  // Ein relativer Pfad wird an target angehängt und,

                  // sofern noch nicht vorhanden, angelegt.
};
```

#### Beispiel

```javascript
let objects = require('common/objects');
let address = require('address/objects');

let  data = {
  salutation:    'mr',
  title:         'Dr.',
  givenName:     'Alberto',
  familyName:    'Malich',
  familyStatus:  'unmarried',
  dateOfBirth:   new Date('1990-03-01T12:00:00.000+02:00'),

                 // 01.03.1990
  description:   'Gründer der UU',
  sex:           'male',
  placeOfBirth:  'Ankh-Morkpork',
  maidenName:    'Malich',
  welcomeMessage:'Sehr geehrter Herr Dr. Malich,',
  target:        objects.find('/agorum/roi/Files/Lehrpersonal'),
                 //path:  null
                 //target: null,
  path:          'Lehrpersonal'
};

//Aufruf:

let person = address.create('person', data);

```

### create.mail

---

Mit diesem Aufruf legen Sie eine E-Mail-Adresse an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  mailAddress:        '<email@adresse.com',
  defaultMailAddress: true/false,
                      //ob Standardmailadresse
  target:             '<Das Objekt, an das data angehängt werden soll>',
                      //Muss ein Objekt von dieser Klasse sein:
                      //'D4WADDRESSCONTAINER',
                      //'D4WADDRESSORGANISATION',
                      //'D4WADDRESSDEPARTMENT',
                      //'D4WADDRESSPERSON'
  path:               '<relativer oder absoluter Pfad>'
                      //Ein relativer Pfad wird an target angehängt und,
                      //sofern noch nicht vorhanden, angelegt.
};
```

#### Beispiel

```javascript
let objects = require('common/objects');
let address = require('address/objects');

let data = {
  mailAddress:        'rolf.lang@agorum.com',
  defaultMailAddress: true,
  target:             objects.find('123005')

};

//Aufruf:
let mail = address.create('mail', data);
```

### create.phone

---

Mit diesem Aufruf legen Sie eine Telefonnummer an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  type:          '<telephone>',
                 // Auswahlmöglichkeiten: telephone/mobile/fax
                 // (siehe csv-Datei: d4w_address_phone_type.csv)
  defaultNumber: true/false,
                 // ob Standardtelefonnummer
  phoneNumber:   '<Telefonnummer>',
                 //Muss so formatiert werden:
                 // +Land Vorwahl Nummer-Durchwahl
                 // +Land Vorwahl Nummer          (Wenn es keine Durchwahl gibt)
  target:        '<Das Objekt, an das data angehängt werden soll>',
                 // Muss ein Objekt von dieser Klasse sein:
                 // 'D4WADDRESSCONTAINER',
                 // 'D4WADDRESSORGANISATION',
                 // 'D4WADDRESSDEPARTMENT',
                 // 'D4WADDRESSPERSON'
                 // Ohne Angabe ist target automatisch: '/agorum/roi/Files/'
  path:          '<relativer oder absoluter Pfad>'
                 // Ein relativer Pfad wird an target angehängt
                 // und, sofern noch nicht vorhanden, angelegt.
};
```

#### Beispiel

```javascript
let address = require('address/objects');

let data = {
  type:          'telephone',
  defaultNumber: true,
  phoneNumber:   '+49 711 34610-60',
  path:          'Telefonnummern'
};

//Aufruf:
let phone = address.create('phone', data);
```

### create.link

---

Mit diesem Aufruf legen Sie eine Verlinkung an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  link:        '<http://www.webseite.com>',
  defaultLink: true/false,
               // ob Standardlink
  subject:     '<Name des Links, etwa Webseitenname>',
  target:      '<Das Objekt, an das data angehängt werden soll>',
               // Muss ein Objekt von dieser Klasse sein:
               // 'D4WADDRESSCONTAINER',
               // 'D4WADDRESSORGANISATION',
               // 'D4WADDRESSDEPARTMENT',
               // 'D4WADDRESSPERSON'
               // Ohne Angabe ist target automatisch: '/agorum/roi/Files/'
  path:        '<relativer oder absoluter Pfad>'
               // Ein relativer Pfad wird an target angehängt und,

               // sofern noch nicht vorhanden, angelegt.
};
```

#### Beispiel

```javascript
let objects = require('common/objects');
let beans = require('common/beans');

let address = require('address/objects');

let data = {
  link:        'http://www.agorum.com',
  defaultLink: true,
  subject:     'agorum Homepage',
  target:      objects.find('258741'),
  //path:      null
};

//Aufruf:
let link = address.create('link', data);

```

### create.info

---

Mit diesem Aufruf legen Sie eine Zusatzinformation zu einer Person an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  jobTitle:     '<Berufsbezeichnung>Softwareentwicklung',
  activityRate: '<100>',
                // Hier eine Integer-Zahl eingeben, mit wie viel Prozent dieser Job gemacht
                // wird
  target:       '<Das Objekt, an das data angehängt werden soll>',
                // Muss ein Objekt von dieser Klasse sein:
                // 'D4WADDRESSCONTAINER',
                // 'D4WADDRESSPERSON'
                // Ohne Angabe ist target automatisch: '/agorum/roi/Files/'
  path:         '<relativer oder absoluter Pfad>'
                // Ein relativer Pfad wird an target angehängt
                // und, sofern noch nicht vorhanden, angelegt.
};
```

#### Beispiel

```javascript
let objects = require('common/objects');
let address = require('address/objects');

let data = {
  jobTitle:     'Softwareentwicklung',
  activityRate: 70,
  target:       objects.find('147852')
};

//Aufruf:
let info = address.create('info', data);
```

### create.data

---

Mit diesem Aufruf legen Sie eine Ortsadresse an.

_data_ befüllen Sie wie folgt:

```javascript
let data = {
  street1:      '<Straßenname>',
  zip:          '<PLZ>',
  city:         '<Ort>',
  state:        '<Bundesland>',
  country:      '<Ländercode>',
                // (siehe CSV-Datei: d4w_address_data_country.csv)
  postBox:      '<Postboxnummer>',
  zipPostBox:   '<PLZ der Postbox>',
  cityPostBox:  '<Ort der Postbox>',
  houseNumber1: '<Hausnummer>',
  target:       '<Das Objekt, an das data angehängt werden soll>',
                // Muss ein Objekt von dieser Klasse sein:
                // 'D4WADDRESSCONTAINER',
                // 'D4WADDRESSORGANISATION',
                // 'D4WADDRESSDEPARTMENT',
                // 'D4WADDRESSPERSON'
                //  Ohne Angabe ist target automatisch: '/agorum/roi/Files/'
  path:         '<relativer oder absoluter Pfad>'
                // Ein relativer Pfad wird an target angehängt und,
                // sofern noch nicht vorhanden, angelegt
};
```

**Hinweis**: Bei _tryCreate_ wird ein bereits vorhandener Datensatz zurückgegeben. Er wird dabei mit den übergebenen Daten aktualisiert.

#### Beispiel

```javascript
let objects = require('common/objects');
let address = require('address/objects');

let data = {
  street1:      'Vogelsangstrasse',
  zip:          '73760',
  city:         'Ostfildern',
  state:        'Baden Württemberg',
  country:      'de',
  postBox:      '16423',
  zipPostBox:   '73770',
  cityPostBox:  'Denkendorf',
  houseNumber1: '16',
  target:       objects.find('34587')
};

//Aufruf:
let addressData = address.create('data', data);

```

### create.image

---

Mit diesem Aufruf legen Sie ein Bild zu einer Person an. Verwenden Sie folgende Bildformate, idealerweise quadratisch in den Abmessungen 512×512 oder 256×256:

- png
- jpg

_data_ befüllen Sie wie folgt:

```javascript
let data = {

  target: '<Das Objekt, an das data angehängt werden soll>',
          // Muss ein Objekt von dieser Klasse sein:
          // 'D4WADDRESSCONTAINER',
          // 'D4WADDRESSPERSON'
          // Ohne Angabe ist target automatisch: '/agorum/roi/Files/'
  path:   '<relativer oder absoluter Pfad>'
          // Ein relativer Pfad wird an target angehängt und,
          // sofern noch nicht vorhanden, angelegt.
};
```

#### Beispiel

```javascript
let objects = require('common/objects');
let address = require('address/objects');

let data = {
  target: objects.find('123455')
};

//Aufruf:
let image = address.create('image', data);

//Inhalt eines Bilds auf das Image streamen
objects.find('/agorum/roi/Files/neuesBild.png').streamContent(image);

// return: image object
```

#### Das Bild einer Person aktualisieren

```javascript
//Objekt (Person) holen
let image = objects.find('1278388').firstAddressImage;

//Inhalt des neuen Bilds auf das Image streamen
objects.find('/agorum/roi/Files/aktualisiertesBild.png').streamContent(image);
```

## JavaScript Address API - update

Mit dem Aufruf _update_ aktualisieren Sie bestehende Daten.

### Verwendung

---

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```javascript
let address = require('address/objects');
```

### update.book

---

Mit diesem Aufruf aktualisieren Sie ein Adressbuch.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  name:         '<Name des Addressbuchs>',
  description:  '<Beschreibung des Addressbuchs>'
                // optional
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
let name = object.name;
let description = object.description;
```

#### Beispiel

```javascript
let address = require('address/objects');
let objects = require('common/objects');
let object = objects.find('<zu aktualisierendes Objekt>');
let data = {
  name:        'Unsichtbare Universität aktualisiert',
  description: 'Version 2.0'
               // optional

};

//Aufruf:
address.update('book', object, data);
```

### update.organisation

---

Mit diesem Aufruf aktualisieren Sie eine Organisation.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  name:            '<Name der Organisation>',
  additionalName1: '<Zusatzname 1>',
  additionalName2: '<Zusatzname 2>',
  customerNumber:  '<Kundennummer>',
  taxNumber:       '<Steuernummer>',
  description:     '<beliebige Beschreibung>',
  salesTaxIdentificationNumber: '<Ust-Id>'
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.name - set und get,
object.additionalName1 set und get,
object.additionalName2 - set und get,
object.customerNumber - set und get,
object.salesTaxIdentificationNumber - set und get,
object.taxNumber - set und get,
object.description - set und get
```

#### Beispiel

```javascript
let address = require('address/objects');
let objects = require('common/objects');
let object = objects.find('1337');

let data = {
  name:            'Ankh Organisation',
  additionalName1: 'Morkpork',
  additionalName2: ' ',
  customerNumber:  '456987',
  taxNumber:       '10 321 654 988',
  description:     'aktualisierte Beschreibung',
  salesTaxIdentificationNumber: 'DE999999990'
};

//Aufruf:

address.update ('organisation', object, data);
```

### update.department

---

Mit diesem Aufruf aktualisieren Sie eine Abteilung.

*data* befüllen sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  name:            '<Name der Abteilung>',
  additionalName1: '<Zusatzname 1>',
  additionalName2: '<Zusatzname 2>',
  customerNumber:  '<Abteilungsnummer>',
  taxNumber:       '<Steuernummer>',
  description:     '<beliebige Beschreibung>',
  salesTaxIdentificationNumber: '<Ust-Id>'
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.getName(),
object.getAdditionalName1(),
object.getAdditionalName2(),
object.getCustomerNumber(),
object.getSalesTaxIdentificationNumber(),
object.getTaxNumber(),
object.getDescription()
```

#### Beispiel

```javascript
let address = require('address/objects');
let objects = require('common/objects');
let object = objects.find('787844');

let data = {
  name:            'Niederlassung Hamburg',
  additionalName1: 'Z-Name 1 - Hamburg',
  additionalName2: 'Z-Name 2 - Hamburg',
  customerNumber:  'Kundennummer',
  taxNumber:       '10 385 654 568',
  description:     'Abteilung der Qualitätssicherung',
  salesTaxIdentificationNumber: 'DE111111111'
};

//Aufruf
address.update ('department', object, data);
```

### update.person

---

Mit diesem Aufruf aktualisieren Sie eine Person.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  salutation:     '<Anrede>',
                  // Auswahlmöglichkeiten: mr; mrs; mrmrs; family
                  // (Herr, Frau, Herr und Frau, Familie)
  title:          '<Titel>',
  givenName:      '<Vorname>',
  familyName:     '<Familienname>',
  familyStatus:   '<Familienstatus>',
                  // Auswahlmöglichkeiten: unmarried (ledig), married (verheiratet),
                  // unknown (-)
  dateOfBirth:    '<Geburtstag (Datum)>',
  description:    '<beliebige Beschreibung>',
  sex:            '<Geschlecht>',
                  // Auswahlmöglichkeiten: male (männlich), female (weiblich),
                  // unknown (unbekannt)
  placeOfBirth:   '<Geburtsort>',
  maidenName:     '<Geburtsname>',
  welcomeMessage: '<Sehr geehrter Herr Familienname>'
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
let person = object.getD4wAddressPerson();

person.getGivenName(),
person.getFamilyName(),
person.getFamilyState(),
person.getMaidenName(),
person.getTitle(),
person.getSalutation(),
person.getDescription()
```

#### Beispiel

```javascript
let address = require('address/objects');

let objects = require('common/objects');

let object = objects.find('37895');

let data = {
  salutation:     'mr',
  title:          'Dipl.Ing.(FH) Update',
  givenName:      'Rolf Wolf',
  familyName:     'Lang Kurz',
  dateOfBirth:    new Date('1966-08-12T12:00:00.000+02:00'),
  description:    'Neuer Projektleiter',
  sex:            'male',
  placeOfBirth:   'Denkendorf',
  maidenName:     'Geburtsname',
  welcomeMessage: 'Sehr geehrter Herr Lang Kurz'

};

//Aufruf
address.update ('person', object, data);
```

### update.mail

---

Mit diesem Aufruf aktualisieren Sie die E-Mail-Adresse.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  mailAddress:        '<email@adresse.com',
  defaultMailAddress: true/false
                      // ob Standard-E-Mail-Adresse
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.getMailAddress(),
object.getDefaultMailAddress()
```

#### Beispiel

```javascript
let address = require('address/objects');
let objects = require('common/objects');
let object = objects.find('42456');

let data = {
  mailAddress:        'rolf.lang.neu@agorum.de',
  defaultMailAddress: true
};

//Aufruf
address.update ('mail', object, data);
```

### update.phone

---

Mit diesem Aufruf aktualisieren Sie die Telefonnummer.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  type:          '<Art der Nummer>',
                 // Auswahlmöglichkeiten: telephone/mobile/fax
                 // (siehe CSV-Datei: d4w_address_phone_type.csv)
  defaultNumber: true/false,
                 // ob Standardtelefonnummer
  phoneNumber:   'Telefonnummer'
                 // Muss so formatiert werden:
                 //  +Land Vorwahl Nummer-Durchwahl
                 //  +Land Vorwahl Nummer (wenn es keine Durchwahl gibt)
};

```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.getType(),
object.getDefaultNumber(),
object.getCompleteNumberNormalized()
```

#### Beispiel

```javascript
let address = require('address/objects');

let objects = require('common/objects');

let object = objects.find('89894');

let data = {
  type:          'telephone',
  defaultNumber: true,
  phoneNumber:   '+49 711 34610-60'
};

//Aufruf
address.update ('phone', object, data);
```

### update.link

---

Mit diesem Aufruf aktualisieren Sie einen Link.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  link:        '<URL>',
  defaultLink: '<Standardlink true/false>',
  subject:     'Webseite 2'
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.getLink(),
object.getDefaultLink(),
object.getSubject()
```

#### Beispiel

```javascript
let address = require('address/objects');

let objects = require('common/objects');

let object = objects.find('8457');

let data = {
  link:        'http://www.agorum.com/2',
  defaultLink: true,

               // true oder false
  subject:     'Webseite 2'
};

//Aufruf
address.update ('link', object, data);
```

### update.info

---

Mit diesem Aufruf aktualisieren Sie die Zusatzinformation zu einer Person.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<Zu aktualisierendes Objekt>');

let data = {
  jobTitle:     '<Berufsbezeichnung>',
  activityRate: '<Integer-Zahl, mit wie viel Prozent der Job gemacht wird>'
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.getJobTitle(),
object.getActivityRate()
```

#### Beispiel

```javascript
let address = require('address/objects');
let objects = require('common/objects');
let object = objects.find('85947');

let data = {
  jobTitle:     'Softwareentwicklung',
  activityRate: 100
};

//Aufruf
address.update ('info', object, data);
```

### update.data

---

Mit diesem Aufruf aktualisieren Sie die Ortsadresse.

*data* befüllen Sie wie folgt:

```javascript
let object = objects.find('<zu aktualisierendes Objekt>');

let data = {
  street1:      '<Straßenname>',
  zip:          '<PLZ>',
  city:         '<Ort>',
  state:        '<Bundesland>',
  country:      '<Ländercode>',
                // (siehe CSV-Datei: d4w_address_data_country.csv)
  postBox:      '<Postboxnummer>',
  zipPostBox:   '<PLZ der Postbox>',
  cityPostBox:  '<Ort der Postbox>',
  houseNumber1: '<Hausnummer>'
};
```

**Bestehende Daten auslesen**

Wenn das Objekt bekannt ist, lesen Sie die bestehenden Daten folgendermaßen aus:

```javascript
object.getStreet1(),
object.getStreet2(),
object.getStreet3(),
object.getZip(),
object.getCity(),
object.getState(),
object.getCountry(),
object.getPostBox(),
object.getZipPostBox(),
object.getCityPostBox(),
object.getHouseNumber1()
object.getHouseNumber2()
object.getHouseNumber3()
```

#### Beispiel

```javascript
let address = require('address/objects');
let objects = require('common/objects');
let object = objects.find('963582');

let data = {
  street1:      'Vogelsangstrasse',
  zip:          '73760',
  city:         'Ostfildern',
  state:        'Baden Württemberg',
  country:      'de',
  postBox:      '16423',
  zipPostBox:   '73770',
  cityPostBox:  'Denkendorf',
  houseNumber1: '16'
};

//Aufruf
address.update ('data', object, data);
```

## JavaScript Address API - query

**Ab welcher Version verfügbar?**

_• agorum core_ 9.5.0

Mit dem Aufruf _query_ bauen Sie eine Solr-Suche auf, die Addressobjekte über den Suchindex findet. Verwenden Sie dazu den Aufbau der [smart search](#), die das Verwenden von [regulären Ausdrücken](#) erlaubt.

### Verwendung

---

Binden Sie die Bibliothek stets am Anfang eines Skripts ein:

```javascript
let address = require('address/objects');
let search = address.query(type, data);
```

### Parameter

---

#### type

Stellt folgende Addressobjekte zur Verfügung:

```javascript
'book', 'organisation', 'department', 'person', 'mailaddresses', 'fullnumbers'
```

**Beispiele**

- mailaddresses: 'rolf.lang@agorum.com'
- fullnumbers: '+497113461060'

**Hinweis**: Das System speichert eine Telefonnummer immer in diesem Format im Index.

#### data

Übergibt Metadaten oder Attribute, die während des Anlegens eines Adressobjekts übergeben werden. Das System sucht die Inhalte der Parameter dann genau in den Attributen oder Metadaten.

- Sie können alle Metadaten übergeben, die auf den Addressobjekten sitzen.
- Wenn Sie den Parameter _data_ leer lassen und nicht füllen, selektiert das System alle Objekte des übergebenen _types_.

**Metadaten verwenden**

Sie können in den einzelnen Parametern die solr-Syntax ([smart search](#)) verwenden:

```javascript
zip: '73*'
name: "agorum Software GmbH"
```

Bei Arrays übergeben Sie die internen Werte:

```javascript
country: 'de' //ist ok
country: 'Deutschland' //ist nicht ok
```

Ein Datum übergeben Sie als Datum oder als Datumsrange:

```javascript
dateofbirth: new Date() // Datum

dateofbirth: { start: new Date(), end: new Date() } // Datumsrange

```

Auch „Subobjekte“ von Adressen gelten und ermöglichen eine Art Hierarchie-Suche:

addressbook  addressorganisation    addressdepartment        person

**Beispiele**

**addressbookIds: \[<Objket-ID1>, <Objket-ID2>\]**

- Setzen Sie in das übergebene Array \[\] die IDs Ihrer Adressbücher ein.
- Lesen Sie die IDs aus über den JavaScript-Befehl _require('common/objetcs').find(id)_ (siehe [JavaScript-Bibliothek common-objects](#)).

**addressorganisation**Sucht nach einer Person oder nach einer Abteilung aus einer Organisation. Der Inhalt ist der Name der Organisation, etwa _addressorganisation: 'agorum Software GmbH'._

**addressdepartment**:

Sucht nach einer Person aus einer bestimmten Abteilung. Der Inhalt ist der Name der Abteilung, etwa _addressdepartment: 'Entwicklung'._

**Tipp**: Sie können in allen Suchen den Parameter *rawquery* übergeben. In diesem Parameter können Sie die Suche für den gewählten *type* komplett selbst steuern.

```javascript
Beispiel: rawquery: 'name:xx*' // Alle Adressobjekte holen, deren Name mit xx beginnt.
```

#### Returnwerte

Durch _address.query()_ leiten Sie eine erweiterte Suchanfrage ein und können die Anzahl an Ergebnissen einschränken, ähnlich wie bei der [JavaScript-Bibliothek common-objects](#).

**Beispiele**

```javascript
// Liefert ein Ergebnis mit maximal 10 Einträgen, bestehend aus rows und total.
let result = address.query('person', { givenname: 'Rolf' }).limit(10).search('id');

// Liefert ein Array von Objekten mit maximal 10 Einträgen.
let persons = address.query('person', { givenname: 'Rolf' }).limit(10).find();
```

Je nach Suchanfrage erhalten Sie folgende Objekte zurück:

**type === 'book'**\--> return D4wAddressBook

**type === 'organisation'**\--> return D4wAddressOrganisation

**type === 'department'**\--> return D4wAddressDepartment

**type === 'person'**\--> return D4wAddressContainer

Eine Person holen Sie per *container.d4wAddressPerson* und erhalten darüber etwa den _fullName_.

### Beispiele

---

In folgendem Abschnitt finden Sie Skripte, die Sie herauskopieren und für Ihr Testsystem anpassen müssen, ehe Sie diese ausführen.

```javascript
let address = require('address/objects');

// Adressbuch mit dem Namen 'xxbook02' holen und den Namen ausgeben
address.query('book', {
  name: 'xxbook02'
}).find().map(m => m.name);

// Alle Adressbücher holen
address.query('book').find().map(m => m.name);

// Alle Adressbücher, die mit xx* starten, holen via rawquery
address.query('book', {
  rawquery: 'name:xx*'
}).find().map(m => m.name);

// Alle Personen suchen und direkt familyName und givenName aus dem Index liefern lassen
address.query('person', {}).search('familyname', 'givenname').rows;

// Verschiedenen Beispiele
address.query('person', {
  // Suche nach Vor- und Nachname
  // givenName: 'petra pau*',
  // familyName: '*demo*',

  // Suche nach E-Mail-Adresse
  // mailaddresses: 'anne.klein@agorum.com',

  // Suche nach einem Datum
  // dateOfBirth: new Date('1982-06-20T11:00:00.000Z')

  //
  // dateOfBirth: {

  //   start: new Date('1982-06-18T11:00:00.000Z'),

  //   end: new Date('1982-06-20T11:00:00.000Z')

  // },

  // Suche nach allen Klein in einer bestimmten Organisation und Abteilung
  // familyName: 'Klein',
  // givenName: 'Anne',
  // addressorganisation: 'agorum Software GmbH',
  // addressdepartment: 'Geschäftsleitung',

  // 1 Adressbuch durchsuchen
  // addressbookIds: '/agorum/roi/Files/Musterfirma GmbH/Musterfirma GmbH/Kunden/a/ag/agorum Software GmbH/Adressen/xxbook'

  // 2 Adressbücher durchsuchen
  // addressbookIds: ['/agorum/roi/Files/Musterfirma GmbH/Musterfirma GmbH/Kunden/a/ag/agorum Software GmbH/Adressen/xxbook',
  //                 '/agorum/roi/Files/Musterfirma GmbH/Musterfirma GmbH/Kunden/xxbook02'],
  // familyName: 'Klein'

  // fullnumbers: '+497113461060',
  // title: 'd*'   // Alle Titel, die mit d beginnen

})
.find()
.map(m => m.d4wAddressPerson)  // Die Person holen
.map(m => m.fullName);         // Die Daten der Person ausgeben

// Alle Organisationen holen
address.query('organisation').find().map(m => m.name);

// Alle Abteilungen holen und mit der Organisation ausgeben
address.query('department').find().map(m => { return {organisation: m.organisation.name, department: m.name};});

// Alle Personen holen und mit der Organisation und der Abteilung ausgeben
address.query('person').find().map(m => {

  let org = address.getPersonOrganisation(m);
  let dep = address.getPersonDepartment(m);
  return {organisation: org && org.name || '-', department: dep && dep.name || '-', person: m.d4wAddressPerson.fullName};});

// Person holen und dann die Adressbücher holen, in denen diese enthalten ist
let p = address.query('person', {givenName: 'Test'}).find()[0];
address.getBooks(p).map(m => m.name);
```

## JavaScript Address API - get

Mit dem Aufruf _get_ erhalten Sie einzelne Objekte.

### getEmails

---

Mit diesem Aufruf erhalten Sie E-Mail-Adressen.

- Das Ergebnis ist ein Array aus E-Mail-Adressen.
- Die E-Mail-Adressen können entweder bei der Firma, der Abteilung oder bei der Person hinterlegt sein.

#### Beispiel

```javascript
// Aufruf
address.getEmails(object [, own [, def ]]);

// object kann sein:  D4wAddressContainer, D4wAddressOrganisation, D4wAddressDepartment und D4wAddressPerson

// own = true/false: Liefert die Werte, bei denen own === true oder own === false ist.
// def = true/false: Liefert die Werte, bei denen default === true oder

// default === false ist.

// Beispiel
let aes = address.getEmails(organisation, true, true);

// Das Ergebnis ist ein Array mit folgender Struktur:
[

  {
    "default" :   true,                // true === ist die Standard-E-Mail-Adresse des Objekts, auf das belongTo verweist.
    "address" :   "info3@agorum.com",  // Definiert die E-Mail-Adresse.
    "completeAddress" : "\"agorum Software GmbH\" <info3@agorum.com>"  // Definiert die E-Mail-Adresse inkl. Namen (ab agorum core 10.0.4).
                                                                       // Kann etwa für eine E-Mail verwendet werden.
    "own" :       false,               // true = Standard-E-Mail-Adresse des übergebenen Objekts
    "id" :        "1144789",           // Definiert die id des Objekts.
    "uuid" :      "a-uuid",            // Definiert die uuid des Objekts (ab agorum core 10.0.7).
    "type" :      "mail",              // Definiert den type (immer mail).
    "belongsTo" : "1139314"            // Definiert das Objekt, an dem dieses Objekt verknüpft ist.
  }
]
```

**Ergebnis**

```javascript
[

  {
    "default" :   true,
    "address" :   "info3@agorum.com",
    "completeAddress" : "\"agorum Software GmbH\" <info3@agorum.com>",
    "own" :       false,
    "id" :        "1144789",
    "uuid" :      "c2341d40-070c-11ec-ae43-02420a0a000f",
    "type" :      "mail",
    "belongsTo" : "1139314"
  },

  {
    "default" :   false,
    "address" :   "info.developer@agorum.com",
    "completeAddress" : "\"Abteilung Entwicklung\" <info.developer@agorum.com>"
    "own" :       false,
    "id" :        "1144794",
    "uuid" :      "c2341d40-070c-11ec-ae43-02420a0a000f",
    "type" :      "mail",
    "belongsTo" : "1139373"
  },

  {
    "default" :   true,
    "address" :   "rolf.lang@agorumcore.de",
    "completeAddress" : "\"Dipl. Ing. (FH) Rolf Lang\" <rolf.lang@agorumcore.com>"
    "own" :       true,
    "id" :        "1144799",
    "uuid" :      "c2341d40-070c-11ec-ae43-02420a0a000f",
    "type" :      "mail",
    "belongsTo" : "1139405"
  }
]
```

### getPhoneNumbers

---

Mit diesem Aufruf erhalten Sie eine Telefonnummer.

Die Telefonnummer kann entweder bei der Firma, der Abteilung oder bei der Person hinterlegt sein.

#### Beispiel

```javascript
// Aufruf
address.getPhoneNumbers(object, type [, own [, def ]]);

// object kann sein:  D4wAddressContainer, D4wAddressOrganisation, D4wAddressDepartment und D4wAddressPerson
// type kann sein: 'fax', 'telephone', 'mobile', null === alle

//Beispiel

let als =  address.getPhoneNumbers(organisation, null, true, true);

// Das Ergebnis ist ein Array mit folgender Struktur:
[

  {
    "number" :         "3461062",        // Definiert die Hauptnummer.
    "default" :        true,             // true === Standard-E-Mail-Adresse des Objekts, auf das belongTo verweist.
    "directAccess" :   " ",              // Definiert die Durchwahl.
    "countryCode" :    "+49",            // Definiert die Länderkennung.
    "prefix" :         "711",            // Definiert die Vorwahl.
    "own" :            false,            // true = Standard-E-Mail-Adresse des übergebenenen Objekts
    "id" :             "1144809",        // Definiert die id des Objekts.
    "uuid" :           "a-uuid",         // Definiert die uuid des Objekts (ab agorum core 10.0.7).
    "type" :           "fax",            // Definiert den type der Nummer.
    "belongsTo" :      "1139373",        // Definiert das Objekt, an dem dieses Objekt verknüpft ist.

    "completeNumber" : "+49 711 3461062" // Definiert die komplette Nummer.
  }

]
```

**Ergebnis**

```javascript
[

  {
    "number" :         "3461062",
    "default" :        true,
    "directAccess" :   " ",
    "countryCode" :    "+49",
    "prefix" :         "711",
    "own" :            false,
    "id" :             "1144809",
    "uuid" :           "c2341d40-070c-11ec-ae43-02420a0a000f",
    "type" :           "fax",
    "belongsTo" :      "1139373",
    "completeNumber" : "+49 711 3461062"
  },

  {
    "number" :         "34610",
    "default" :        true,
    "directAccess" :   "61",
    "countryCode" :    "+49",
    "prefix" :         "711",
    "own" :            false,
    "id" :             "1144804",
    "uuid" :           "c2341d40-070c-11ec-ae43-02420a0a000f",
    "type" :           "telephone",
    "belongsTo" :      "1139314",
    "completeNumber" : "+49 711 34610-61"
  },

  {
    "number" :         "34610",
    "default" :        true,
    "directAccess" :   "60",
    "countryCode" :    "+49",
    "prefix" :         "711",
    "own" :            true,
    "id" :             "1144814",
    "uuid" :           "c2341d40-070c-11ec-ae43-02420a0a000f",
    "type" :           "telephone",
    "belongsTo" :      "1139405",
    "completeNumber" : "+49 711 34610-60"
  }
]
```

### getLinks

---

Mit diesem Aufruf erhalten Sie einen Link.

Der Link kann entweder bei der Firma, der Abteilung oder bei der Person hinterlegt sein.

#### Beispiel

```javascript
// Aufruf

address.getLinks(objct [, own [, def ]]);

// object kann sein:  D4wAddressContainer, D4wAddressOrganisation, D4wAddressDepartment und D4wAddressPerson

//Beispiel

let link =  address.getLinks(organisation, true, true);

// Das Ergebnis ist ein Array mit folgender Struktur:
[

  {

    "default" :   true,                       // true === Standard-E-Mail-Adresse des Objekts, auf das belongTo verweist.
    "subject" :   "Webseite 2",               // Definiert die Beschreibung des Links.
    "own" :       false,                      // true = Standard-E-Mail-Adresse des übergebenen Objekts
    "link" :      "http://www.agorum.com/2",  // Definiert den Link.
    "id" :        "1144824",                  // Definiert die id des Objekts.
    "uuid" :      "a-uuid",                   // Definiert die uuid dieses Objekts. (ab agorum core 10.0.7).
    "belongsTo" : "1139373"                   // Definiert das Objekt, an dem dieses Objekt verknüpft ist.

  }
]
```

**Ergebnis**

```javascript
[

  {
    "default" :   true,
    "subject" :   "Webseite 2",
    "own" :       false,
    "link" :      "http://www.agorum.com/2",
    "id" :        "1144824",
    "uuid" :      "c2341d40-070c-11ec-ae43-02420a0a000f",
    "belongsTo" : "1139373"
  },

  {
    "default" :   true,
    "subject" :   "Webseite",
    "own" :       false,
    "link" :      "http://www.agorum.com/1",
    "id" :        "1144819",
    "uuid" :      "c2341d40-070c-11ec-ae43-02420a0a000f",
    "belongsTo" : "1139314"
  },

  {
    "default" :   true,
    "subject" :   "Webseite 3",
    "own" :       true,
    "link" :      "http://www.agorum.com/3",
    "id" :        "1144829",
    "uuid" :      "c2341d40-070c-11ec-ae43-02420a0a000f",
    "belongsTo" : "1139405"
  }

]
```

### getMyData

---

Mit diesem Aufruf erhalten Sie die in *data* definierten Werte des Objekts.

Das System ignoriert vererbte Informationen.

#### Beispiel

```javascript
// Aufruf

address.getMyData(object);

// object kann sein: 'D4wAddressContainer','D4wAddressOrganisation',
// 'D4wAddressDepartment' oder 'D4wAddressPerson'

//Beispiel
let dataDepartment = address.getMyData(departmentZSB);

// Das Ergebnis ist ein Array mit folgender Struktur:
[

  {

    "description":  "Beschreibung der Adresse",
    "street1":      "Straßenname",
    "zip":          "PLZ",
    "city":         "Stadt",
    "state":        "Bundesstaat",
    "country":      "Ländercode",                    // siehe CSV-Datei: d4w_address_data_country.csv
    "postBox":      "Postfach Nr",
    "houseNumber1": "Hausnummer",
    "zippostbox": "PLZ Postfach Nr",
    "citypostbox": "Stadt Postfach Nr",
    "id" : "1144829",                                // ab agorum core 10.0.7
    "uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f", // ab agorum core 10.0.7
​​​​​​​  }
]
```

**Ergebnis**

```javascript
[
  {

    "description":  "Beschreibung der Adresse",
    "street1":      "Huberstrasse",
    "zip":          "65432",
    "city":         "Kulgow",
    "country":      "de",
    "postBox":      "12233",
    "houseNumber1": "28",
    "id" : "1144829", // ab agorum core 10.0.7
​   ​​​​​​ "uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f", // ab agorum core 10.0.7
  }
]
```

### getPerson

---

Mit diesem Aufruf erhalten Sie die Daten einer Person.

Wenn das System keine Person findet, erhalten Sie _null_ zurück.

#### Beispiel

```javascript
// Aufruf
address.getPerson(object [, data ]);

// object kann sein: FolderObject, 'D4wAddressOrganisation', 'D4wAddressDepartment'
// data sind Vorname und Nachname der Person

Oder
object kann sein: D4wAddressContainer
// data wird dann nicht benötigt, sondern es wird direkt die Person des Containers ausgelesen.

//Beispiel
let os = address.getPerson(departmentGL, {givenName: 'Vorname OS', familyName:'Nachname OS' });

//Beispiel 2
let rl = address.getPerson(container);

// Das Ergebnis ist ein Array mit folgender Struktur:
[
  {
    "salutation":     "Anrede",                              // Auswahl aus mr, mrs, mrmrs, family
    "title":          "titel",                               // Definiert den Titel der Person, sofern vorhanden.
    "givenName":      "Bob",                                 // Definiert den Vornamen.
    "familyName":     "Müller",                              // Definiert den Nachnamen.
    "dateOfBirth":    "1978-09-17T12:00:00.000+02:00",       // Definiert das Geburtsdatum.
    "sex":            "male",                                // Definiert das Geschlecht.
    "maidenName":     "Kurz",                                // Definiert den Geburtsnamen.
    "description":    "Beschreibung",                        // Definiert eine optionale Beschreibung der Person.
    "welcomeMessage": "Sehr geehrter Herr Nachname",         // Definiert eine Willkommensnachricht.
 ​​​​​​​   "id" :            "1144829",                             // ab agorum core 10.0.7
    ​​​​​​"uuid" :          "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7
  }
]
```

**Ergebnis**

```javascript
[

  {

    "salutation":     "mr",

    "title":          "Dipl.Ing.(FH)",
    "givenName":      "Bob",
    "familyName":     "Müller",
    "dateOfBirth":    "1978-09-17T12:00:00.000+02:00",
    "sex":            "male",
    "maidenName":     "Kurz",
    "description":    "Herr Müller ist Softwareentwickler bei Firma Y.",
    "welcomeMessage": "Sehr geehrter Herr Müller",
 ​​​​​​​   "id" : "1144829", // ab agorum core 10.0.7
    ​​​​​​"uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7

  }
]
```

### getInfo

---

Mit diesem Aufruf erhalten Sie Informationen zu einer Person.

Wenn das System keine Person findet, erhalten Sie _null_ zurück.

#### Beispiel

```javascript
// Aufruf
address.getInfo(object);

// object kann sein: Person oder Containerobject, von dem die Information geholt werden soll.

//Beispiel
let osInfo = address.getInfo(os);

// Das Ergebnis ist ein Array mit folgender Struktur:
[
  {
    "jobTitle":     "Job Bezeichnung",                     // Definiert die Jobbezeichnung der Person.
    "activityRate": 100,                                   // Definiert, mit wie viel Prozent der Job ausgeübt wird.
 ​​​​​​​   "id" :          "1144829",                             // ab agorum core 10.0.7
    ​​​​​​"uuid" :        "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7
  }
]
```

**Ergebnis**

```javascript
[
  {
    "jobTitle":     "Softwareentwickler",
    "activityRate": 100,
 ​​​​​​​   "id" : "1144829", // ab agorum core 10.0.7
    ​​​​​​"uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7
  }
]
```

### getOrganisation

---

Mit diesem Aufruf erhalten Sie Informationen zu einer Organisation.

Wenn das System keine Organisation findet, erhalten Sie _null_ zurück.

#### Beispiel

```javascript
// Aufruf
address.getOrganisation(object);

// object kann sein: 'D4WADDRESSCONTAINER', 'D4WADDRESSPERSON', 'D4wAddressOrganisation', 'D4wAddressDepartment'

//Beispiel
let orga = address.getOrganisation(os);

// Das Ergebnis ist ein Objekt mit folgender Struktur:

 {
    name: 'Name  Organisation',
    additionalName1: 'Zusatzname 1',
    additionalName2: 'Zusatzname 2',
    customerNumber: 'Kundennummer',
    salesTaxIdentificationNumber: 'Ust-Id',
    taxNumber: 'Steuernummer',
    description: 'beliebige Beschreibung',
 ​​​​​​​   "id" : "1144829", // ab agorum core 10.0.7
    ​​​​​​"uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7
  }
```

#### Ergebnis (Beispiel)

```javascript
{
  "additionalName1" : "",
  "salesTaxIdentificationNumber" : "DE198023952",
  "name" : "agorum Software GmbH",
  "taxNumber" : "",
  "description" : "Hersteller des DMS agorum core",
  "customerNumber" : "1221",
  "additionalName2" : "",
​​​​​  "id" : "1144829", // ab agorum core 10.0.7
​​​​​​  "uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7

}
```

### getDepartment

---

Mit diesem Aufruf erhalten Sie Informationen zu einem Department (Abteilung).

Wenn das System kein Department findet, erhalten Sie _null_ zurück.

#### Beispiel

```javascript
// Aufruf
address.getDepartment(object);

// object kann sein: 'D4WADDRESSCONTAINER', 'D4WADDRESSPERSON', 'D4wAddressDepartment'

//Beispiel
let depart = address.getDepartment(os);

// Das Ergebnis ist ein Objekt mit folgender Struktur:

  {
     name:            '<Name der Abteilung>',
     additionalName1: '<Zusatzname 1>',

     additionalName2: '<Zusatzname 2>',
     customerNumber:  '<Abteilungsnummer>',
     taxNumber:       '<Steuernummer>',
     description:     '<beliebige Beschreibung>',
     salesTaxIdentificationNumber: '<Ust-Id>',
 ​​​​​​​    "id" : "1144829", // ab agorum core 10.0.7
     ​​​​​​"uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7
  }
```

**Ergebnis**

```javascript
{
  "additionalName1" : "",
  "salesTaxIdentificationNumber" : "",
  "name" : "Gesch\u00E4ftsleitung",
  "taxNumber" : "",
  "description" : "",
  "customerNumber" : "",
  "additionalName2" : "",
 ​​​​​​​ "id" : "1144829", // ab agorum core 10.0.7
  ​​​​​​"uuid" : "c2341d40-070c-11ec-ae43-02420a0a000f" // ab agorum core 10.0.7

}
```

### getBooks

---

**Ab welcher Version verfügbar?**• _agorum core_ 9.5.0

Mit diesem Aufruf erhalten Sie alle Adressbücher, in denen eine Person enthalten ist.

```javascript
Aufruf: let books = address.getBooks(<object>);

  object:  Muss eines der folgenden Objekttypen sein:
           D4wAddressOrganisation, D4wAddressDepartment, D4wAddressContainer, D4wAddressPerson

   return: [ D4wAddressBook, .... ]

           [ 0 ... n ] Adressbücher, in denen "object" enthalten ist.
```

#### Beispiel

```javascript
let address = require('address/objects');

// Person holen und dann die Adressbücher holen, in denen die Person enthalten ist.
let person = address.query('person', {givenName: 'Rolf', familyName: 'Lang'}).limit(1).find()[0];

let books = address.getBooks(person);
```

### getPersonOrganisation

---

**Ab welcher Version verfügbar?**• _agorum core_ 9.5.0

Mit diesem Aufruf erhalten Sie alle Organisation, in der eine Person enthalten ist.

Wenn das System keine Organisation findet, in der die Person enthalten ist, erhalten Sie _null_ zurück.

```javascript
Aufruf: let organisation = address.getPersonOrganisation(person);

  person:  D4wAddressContainer, D4wAddressPerson
           Hinweis: Wenn D4wAddressPerson übergeben wird, wird nur dann etwas zurückgeliefert, wenn nur 1 Container vorhanden ist.

  return: Die Organisation (D4wAddressOrganisation), in der die Person enthalten ist.
```

#### Beispiel

```javascript
let address = require('address/objects');

// Person holen und dann die Organisation holen, in der die Person enthalten ist.

let person = address.query('person', {givenName: 'Rolf', familyName: 'Lang'}).limit(1).find()[0];
let books = address.getPersonOrganisation(person);
```

### getPersonDepartment

---

**Ab welcher Version verfügbar?**• _agorum core_ 9.5.0

Mit diesem Aufruf erhalten Sie alle Abteilungen, in denen eine Person enthalten ist.

Wenn das System keine Abteilung findet, in der die Person enthalten ist, erhalten Sie _null_ zurück.

```javascript
Aufruf: let department = address.getPersonDepartment(person);

  person:  D4wAddressContainer, D4wAddressPerson
           Hinweis: Wenn D4wAddressPerson übergeben wird, wird nur dann etwas zurückgeliefert, wenn nur 1 Container vorhanden ist.

   return: Die Abteilung (D4wAddressDepartment), in der die Person enthalten ist.
```

#### Beispiel

```javascript
let address = require('address/objects');

// Person holen und dann die Organisation holen, in der die Person enthalten ist.

let person = address.query('person', {givenName: 'Rolf', familyName: 'Lang'}).limit(1).find()[0];

let department = address.getPersonDepartment(person);
```

### getPersonContainer

---

**Ab welcher Version verfügbar?**• _agorum core_ 9.5.0

Mit diesem Aufruf erhalten Sie den Container, in dem eine Person enthalten ist.

Wenn eine Person mehreren Containern zugeordnet ist, erhalten Sie keinen Container zurück.

```javascript
Aufruf: let container = address.getPersonContainer(person);

  Object kann sein:  D4wAddressContainer, D4wAddressPerson
                     Hinweis: Wenn D4wAddressPerson übergeben wird, wird nur dann etwas zurückgeliefert, wenn nur 1 Container vorhanden ist.

   return: Der Container (D4wAddressContainer), in dem die Person zugeordnet ist.
```

#### Beispiel

```javascript
let address = require('address/objects');

// Person holen und dann den Container holen, in dem die Person enthalten ist.

let person = address.query('person', {givenName: 'Rolf', familyName: 'Lang'})
             .limit(1)
             .find()[0]
             .d4wAddressPerson; // D4wAddressPerson - Object holen

let container = address.getPersonContainer(person);
```

## Beispielskript zur JavaScript Address API

Mit dem nachfolgenden Skript erstellen Sie ein Adressbuch. Dabei finden alle in der Dokumentation beschriebenen Funktionen Verwendung und werden kombiniert:

- [JavaScript Address API - Create](#)
- [JavaScript Address API - Update](#)
- [JavaScript Address API - query](#)
- [JavaScript Adress API - Get](#)

```javascript
/* global sc */
let address = require('address/objects');
let objects = require('common/objects');

let folder = objects.find('/agorum/roi/Files').createPath('Test-My-First-Address-JS');

let book = address.tryCreate('book', {
  name: 'Mein erstes Adressbuch',
  description: 'Beschreibung des Addressbuches',
  target: folder
});

let organisation = address.tryCreate('organisation', {
  name: 'agorum Software GmbH',
  additionalName1: 'additionalName1',
  additionalName2: 'additionalName2',
  customerNumber: '1234567890',
  salesTaxIdentificationNumber: 'DE12345654321',
  taxNumber: '1098754311',
  description: 'Beschreibung der Firma',
  target: book
});

// Prüfen ob es Data schon gibt für die Organisation
let dataOrganisation = address.getMyData(organisation);

if (!(dataOrganisation && dataOrganisation[0])) {
  dataOrganisation = address.create('data', {
    street1: 'Vogelsangstrasse',
    zip: '73760',
    city: 'Ostfildern',
    state: 'Baden Württemberg',
    country: 'de',  // siehe csv-Datei: d4w_address_data_country.csv
    postBox: '16423',
    zipPostBox: '73760',
    cityPostBox: 'Ostfildern',
    houseNumber1: '22',

    target : organisation
  });
}

// Hier prüfen, ob es eine Telefonnummer gibt
let apns = address.getPhoneNumbers(organisation, 'telephone', true, true);
let telephoneOrganisation = null;

if (apns.length > 0) {
  telephoneOrganisation = objects.find(apns[0].id);
}

else {
  telephoneOrganisation = address.create('phone', {
    type: 'telephone',
    phoneNumber: '+49 711 3461060',
    defaultNumber: true, // true oder false

    target: organisation
  });
}

// Hier prüfen, ob es eine Faxnummer gibt
apns = address.getPhoneNumbers(organisation, 'fax', true, true);
let faxOrganisation = null;

if (apns.length > 0) {
  faxOrganisation = objects.find(apns[0].id);
}

else {
  faxOrganisation = address.create('phone', {
    type: 'fax',
    phoneNumber: '+49 711 3461063',
    defaultNumber: true, // true oder false

    target: organisation
  });
}

// Hier prüfen, ob es eine Mailadresse gibt
let aes = address.getEmails(organisation, true, true);
let mailOrganisation = null;

if (aes.length > 0) {
  mailOrganisation = objects.find(aes[0].id);
}

else {
  mailOrganisation = address.create('mail', {
    mailAddress: 'info2@agorum.com',
    defaultMailAddress: true, // true oder false

    target: organisation
  });
}

let als =  address.getLinks(organisation, true, true);
let linkOrganisationOwnTrue = null;

if (als.length > 0) {
  linkOrganisationOwnTrue = objects.find(als[0].id);
}
else {
  linkOrganisationOwnTrue = address.create('link', {
    link: 'https://www.agorum.com',
    defaultLink: true, // true oder false
    subject: 'Homepage',

    target: organisation
  });
}

let alsn =  address.getLinks(organisation, true, false);
let linkOrganisationOwnFalse = null;

if (alsn.length > 0) {
  linkOrganisationOwnFalse = objects.find(alsn[0].id);
}
else {
  linkOrganisationOwnFalse = address.create('link', {
    link: 'https://www.desk4web.de',
    defaultLink: false, // true oder false
    subject: 'desk4web',

    target: organisation
  });
}

let departmentZSB = address.tryCreate('department', {
  name: 'Zweigstelle Belgien',
  target: organisation
});

// prüfen ob es data schon gibt für das Department
let dataDepartment = address.getMyData(departmentZSB);
if (!dataDepartment) {
  // Durch tryAdd wird data nur einmal angelegt
  dataDepartment = address.create('data', {
    description: 'Beschreibung der Adresse',
    street1: 'Huberstrasse',
    zip: '65432',
    city: 'Kulgow',
    // state: 'Baden Württemberg',
    country: 'be',  // siehe csv-Datei: d4w_address_data_country.csv
    postBox: '12233',
    houseNumber1: '28',

    target: departmentZSB
  });
}

// Hier prüfen, ob es eine Telefonnummer gibt
apns = address.getPhoneNumbers(departmentZSB, 'telephone', true, true);
let telephonedepartmentZSB = null;

if (apns.length > 0) {
  telephonedepartmentZSB = objects.find(apns[0].id);
}

else {
  telephonedepartmentZSB = address.create('phone',  {
    type: 'telephone',
    phoneNumber: '+32 873 87876876',
    defaultNumber: true, // true oder false

    target: departmentZSB
  });
}

// Hier prüfen, ob es eine Faxnummer gibt
apns = address.getPhoneNumbers(departmentZSB, 'fax', true, true);
let faxdepartmentZSB = null;

if (apns.length > 0) {
  faxdepartmentZSB = objects.find(apns[0].id);
}

else {
  faxdepartmentZSB = address.create('phone',  {
    type: 'fax',
    phoneNumber: '+49 711 3461062',
    defaultNumber: true, // true oder false

    target: departmentZSB
  });
}

// Hier prüfen, ob es eine Mailadresse gibt
aes = address.getEmails(departmentZSB, true, true);
let maildepartmentZSB = null;

if (aes.length > 0) {
  maildepartmentZSB = objects.find(aes[0].id);
}

else {
  maildepartmentZSB = address.create('mail',  {
    mailAddress: 'infobelgien@agorum.com',
    defaultMailAddress: true, // true oder false

    target: departmentZSB
  });
}

let departmentZSBMB = address.tryCreate('department', {
  name: 'Marketing Belgien',
  target: departmentZSB
});

let departmentGL = address.tryCreate('department', {
  name: 'Geschäftsleitung',
  target: organisation
});

let departmentDEV = address.tryCreate('department', {
  name: 'Entwicklung',
  target: organisation
});

// Personen anlegen
// prüfen ob es die Person schon gibt
let os = address.getPerson(departmentGL, {givenName: 'Vorname OS', familyName:'Nachname OS' });
if (!os) {
  os = address.create('person', {
    salutation: 'mr', // Hier gibt es folgende Auswahl:  mr; mrs; mrmrs; family (Herr, Frau, Herr und Frau, Familie)
    title: 'Dipl.Ing.(FH)',
    givenName: 'Vorname OS',
    familyName: 'Nachname OS',
    dateOfBirth: new Date('1978-09-17T12:00:00.000+02:00'),
    sex: 'male',
    maidenName: 'Kurz',
    description: 'Beschreibung der Person',
    welcomeMessage: 'Sehr geehrter Herr Nachname OS',
    target: departmentGL
  });
}

let osInfo = address.getInfo(os);
if (!osInfo) {
  osInfo = address.create('info', {
    jobTitle: 'Hier steht der Job-Title OS',
    activityRate: 100,  // Hier eine Integer eingeben, mit wieviel Prozent dieser Job gemacht wird

    target:  os
  });
}

// Hier prüfen, ob es eine Mailadresse gibt
aes = address.getEmails(os, true, true);
let mailOS = null;

if (aes.length > 0) {
  mailOS = objects.find(aes[0].id);
}

else {
  mailOS = address.create('mail',  {
    target: os,
    mailAddress: 'os@agorum.com',
    defaultMailAddress: true // true oder false
  });
}

// Hier prüfen, ob es eine Telefonnummer gibt
apns = address.getPhoneNumbers(os, 'mobile', true, true);
let mobileOS = null;

if (apns.length > 0) {
  mobileOS = objects.find(apns[0].id);
}

else {
  mobileOS = address.create('phone',  {
    target: os,
    type: 'mobile',
    phoneNumber: '+49 171 1234567',
    defaultNumber: true // true oder false
  });
}

// RL
// prüfen ob es die Person schon gibt
let rl = address.getPerson(departmentGL, { givenName: 'Vorname RL', familyName: 'Nachname RL' });

if (!rl) {
  rl = address.create('person', {
    salutation: 'mr', // Hier gibt es folgende Auswahl:  mr; mrs; mrmrs; family (Herr, Frau, Herr und Frau, Familie)
    title: 'Dipl.Ing.(FH)',
    givenName: 'Vorname RL',
    familyName: 'Nachname RL',
    dateOfBirth: new Date('1978-09-20T12:00:00.000+02:00'),
    sex: 'male',
    maidenName: 'Kurz',
    description: 'Beschreibung der Person',
    welcomeMessage: 'Sehr geehrter Herr Nachname RL',
    target: departmentGL
  });
}

let rlInfo = address.getInfo(rl);
if (!rlInfo) {
  rlInfo = address.create('info',  {
    target: rl,
    jobTitle: 'Hier steht der Job-Title von RL',
    activityRate: 100  // Hier eine Integer eingeben, mit wieviel Prozent dieser Job gemacht wird
  });
}

// Hier prüfen, ob es eine Mailadresse gibt
aes = address.getEmails(rl, true, true);
let mailRL = null;

if (aes.length > 0) {
  mailRL = objects.find(aes[0].id);
}

else {
  mailRL = address.create('mail', {
    target: rl,
    mailAddress: 'rl@agorum.com',
    defaultMailAddress: true // true oder false
  });
}

// Hier prüfen, ob es eine Telefonnummer gibt
apns = address.getPhoneNumbers(rl, 'mobile', true, true);
let mobileRL = null;

if (apns.length > 0) {
  mobileRL = objects.find(apns[0].id);
}

else {
  mobileRL = address.create('phone', {
    target:  rl,
    type: 'mobile',
    phoneNumber: '+49 173 22334455',
    defaultNumber: true // true oder false
  });
}

// SG
// prüfen ob es die Person schon gibt
let sg = address.getPerson(departmentZSBMB, { givenName: 'Vorname SG', familyName: 'Nachname SG' });

if (!sg) {
  sg = address.create('person', {
    salutation: 'mr', // Hier gibt es folgende Auswahl:  mr; mrs; mrmrs; family (Herr, Frau, Herr und Frau, Familie)
    title: 'Dipl.Ing.(FH)',
    givenName: 'Vorname SG',
    familyName: 'Nachname SG',
    dateOfBirth: new Date('1978-09-20T12:00:00.000+02:00'),
    sex: 'male',
    maidenName: 'Kurz',
    description: 'Beschreibung der Person',
    welcomeMessage: 'Sehr geehrter Herr Nachname SG',
    target: departmentZSBMB
  });
}

let sgInfo = address.getInfo(sg);
if (!sgInfo) {
  sgInfo = address.create('info', {
    target:  sg,
    jobTitle: 'Hier steht der Job-Title von SG',
    activityRate: 100  // Hier eine Integer eingeben, mit wieviel Prozent dieser Job gemacht wird
  });
}
sgInfo;

// Hier prüfen, ob es eine Mailadresse gibt
aes = address.getEmails(sg, true, true);
let mailSG = null;

if (aes.length > 0) {
  mailSG = objects.find(aes[0].id);
}

else {
  mailSG = address.create('mail', {
    target:  sg,
    mailAddress: 'sg@agorum.com',
    defaultMailAddress: true // true oder false
  });
}

// Hier prüfen, ob es eine Telefonnummer gibt
apns = address.getPhoneNumbers(sg, 'mobile', true, true);
let mobileSG = null;

if (apns.length > 0) {
  mobileSG = objects.find(apns[0].id);
}

else {
  mobileSG = address.create('phone', {
    target:  sg,
    type: 'mobile',
    phoneNumber: '+49 171 1234567',
    defaultNumber: true // true oder false
  });
}

// FS
// prüfen ob es die Person schon gibt
let fs = address.getPerson(departmentDEV, { givenName: 'Vorname FS', familyName: 'Nachname FS' });

if (!fs) {
  fs = address.create('person', {
    salutation: 'mr', // Hier gibt es folgende Auswahl:  mr; mrs; mrmrs; family (Herr, Frau, Herr und Frau, Familie)
    title: 'Dipl.Ing.(FH)',
    givenName: 'Vorname FS',
    familyName: 'Nachname FS',
    dateOfBirth: new Date('1978-09-20T12:00:00.000+02:00'),
    sex: 'male',
    maidenName: 'Kurz',
    description: 'Beschreibung der Person',
    welcomeMessage: 'Sehr geehrter Herr Nachname FS',
    target: departmentDEV
  });
}

let fsInfo = address.getInfo(fs);
if (!fsInfo) {
  fsInfo = address.create('info', {
    target: fs,
    jobTitle: 'Hier steht der Job-Title von FS',
    activityRate: 100  // Hier eine Integer eingeben, mit wieviel Prozent dieser Job gemacht wird
  });
}

// Hier prüfen, ob es eine Mailadresse gibt
aes = address.getEmails(fs, true, true);
let mailFS = null;

if (aes.length > 0) {
  mailFS = objects.find(aes[0].id);
}

else {
  mailFS = address.create('mail', {
    target:  fs,
    mailAddress: 'fs@agorum.com',
    defaultMailAddress: true // true oder false
  });
}

// Hier prüfen, ob es eine Telefonnummer gibt
apns = address.getPhoneNumbers(fs, 'mobile', true, true);
let mobileFS = null;

if (apns.length > 0) {
  mobileFS = objects.find(apns[0].id);
}

else {
  mobileFS = address.create('phone', {
    target:  fs,
    type: 'mobile',
    phoneNumber: '+49 171 1234567',
    defaultNumber: true // true oder false
  });
}
```
