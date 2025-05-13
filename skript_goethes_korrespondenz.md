Übungsbeispiel Goethes Briefkorrespondenz
=========================================

Dieses Tutorial führt anhand eines Beispielszenarios in die wichtigsten Funktionen von OpenRefine
ein.

Das Portal [CorrespSearch](https://correspsearch.net) aggregiert Daten zu Korrespondenzen zwischen 
historischen Persönlichkeiten aus verschiedenen Editionen und Datenquellen. Über eine API können 
alle verzeichneten Korrespondenzen zu einer Person abgefragt und heruntergeladen werden.

Diese Informationen wollen wir so zusammenstellen und anreichern, dass wir auf einer Landkarte
die Orte von Goethes Korrespondenzpartnern in Abhängigkeit von der Zeit einzeichnen können.

Über diese URL erhalten wir eine XML-Datei mit der Korrespondenz von Goethe:
https://correspsearch.net/api/v1.2/tei-xml.xql?correspondent=http://d-nb.info/gnd/118540238
Neben Metadaten unter anderem zu den Quellen der einzelnen Korrespondenzen werden die Briefe selbst
in je einem Element correspDesc gelistet. Dabei werden ein oder mehrere Absender und Empfänger 
genannt, sowie deren Aufenthaltsorte und das Versendedatum --- sofern bekannt.

Anmerkung: die Daten enthalten für die Personen Verweise in die GND und für Orte nach Geonames. Wir
werden diese interessante Information allerdings aus didaktischen Gründen ignorieren.


1. Anlegen eines neuen Projekts:
  - Über die Startseite kann ein bestehendes Projekt geöffnet oder importiert sowie ein neues
    angelegt werden.
  - OpenRefine unterstützt eine ganze Reihe von Datenquellen und Quellformaten, die nicht zwingend 
    tabellarisch organisiert sein müssen. In einem Mappingschritt werden die Daten in das 
    tabellarische Format von OpenRefine überführt.
  - Import der Daten über URL: https://correspsearch.net/api/v1.2/tei-xml.xql?correspondent=http://d-nb.info/gnd/118540238
  - Auswählen der geeigneten Ebene, in unserem Fall das Element `correspDesc`
  - Über Preview erhalten wir einen Eindruck, wie die Daten mit den aktuellen Einstellungen
    ins tabellarische Format überführt würden. 
  - Wir setzen den Projektnamen auf "Goethes Korrespondenz"

2. Überblick über die Oberfläche
  - Im Hauptbereich befindet sich die Tabelle mit den Daten.
    OpenRefine arbeitet spaltenbasiert, d.h. Operationen werden in der Regel auf die Werte 
    bestimmter Spalten angewandt; es unterscheidet einen Zeilen- und einen "Record"-Modus (oben
    links kann man zwischen beiden umschalten)
    - Im Record-Modus werden zusammengehörige Zeilen zu einem "Record"/Datensatz zusammengefasst. 
      In unserem Fall ist die Zusammengehörigkeit über das gemeinsame correspDesc-XML-Element
      definiert.
    - Den Unterschied kann man sich leicht klarmachen, wenn man zwischen beiden Modi wechselt und
      anhand der Hintergrundfarbe beobachtet, wie OpenRefine die Zeilen gruppiert.
  - Die linke Seitenleiste enthält erstellte Filter und Facetten sowie die Änderungshistorie
  - Oben rechts befindet sich noch ein Export-Button, woebi OpenRefine zahlreiche 
    Exportmöglichkeiten bietet, die hier nicht näher besprochen werden.
  - Jede Spalte besitzt ein Spaltenmenü (Button mit Dreieck), über das die auf der Spalte möglichen
    Operationen aufgerufen werden können. Dies sind
    - Facetten/Filter auf den Werten der Spalte definieren
    - Transformationen auf den Daten in der Spalte
    - Ansichten
    - Abgleich/Anreicherung (Reconcile) mit Fremddaten

3. Spalten reduzieren, entfernen, umbenennen und verschieben
  - Man kann einzelne Spalten einklappen, wenn man sie aktuell nicht benötigt. Dies befindet sich im
    Menü unter `View`. Dies geht auch für mehrere Spalten gleichzeitig, indem man die Option wählt, 
    alle Spalten nach links/rechts einzuklappen.
  - Man kann einzelne Spalten löschen, wenn man sie definitiv nicht mehr benötigt. Dies befindet 
    sich im Mneü unter `Edit column`
  - Man kann über das Menü der All-Spalte mehrere Spalten gleichzeitig löschen und verschieben.
    Dazu wählt man im All-Menü `Edit columns > Re-order / remove columns...` und führt die 
    Änderungen im Dialogfenster per Drag-n-Drop druch.
  - Die ersten vier Spalten enthalten Identifikatoren für den einzelnen Brief.
    Da wir sie erstmal nicht brauchen, klappen wir sie ein.
  - Die Spalten, die auf ref, cert oder evidence enden, benötigen wir für dieses Beispiel nicht und
    löschen sie daher.
  - Wir werden hauptsächlich mit den Spalten arbeiten, die auf type, persName und placeName enden
    und verkürzen daher ihre Namen entsprechend.
    
4. Facetten und Datenbereinigung
  - Jede Zelle der Tabelle kann einzeln Editiert werden über den Edit-Button, der erscheint, wenn 
    man mit der Maus über die Zelle hovert.
  - Facetten bieten einen Überblick über die Werte in einer Spalte und man kann die Tabelle nach
    bestimmten Werten filtern. Es gibt verschiedene Arten von Facetten, die je einen anderen
    Blick auf die Daten werfen. Das Filtern geschieht über die Auswahl bestimmer Werte oder eines
    Wertebereichs
  - Facetten werden über das Spaltenmenü `Facets` erstellt und in der linken Seitenleiste angezeigt.
    In der Leiste bleiben die Facetten bestehen, bis man sie aktiv schließt (über das x). Es können 
    also mehrere Facetten (über mehrere Spalten) gelistet sein und auch aktiv filtern.
  - Wir verschaffen uns einen Überblick über die Werte in der persName-Spalte. Wir erstellen eine
    Text-Facette. In dem Facetten-Fenster in der Seitenleiste werden alle Namen mit ihren
    Häufigkeiten alphabetisch gelistet. 
  - Klicken wir einen Wert an, wird die Tabelle entsprechend gefiltert. Dabei macht es einen 
    Unterschied, ob  man im row- oder record-Modus ist: Bei ersterem werden nur die Zeilen 
    angezeigt, die diesen Wert enthalten. Bei letzterem werden alle Zeilen eines Records angezeigt,
    in dem mindestens eine Zeile den gesuchten Wert enthält.
    Operation auf der Tabelle werden nur die von den aktiven Facetten gefilterten Zeilen angewandt.
  - Wir erkennen, dass einige Einträge Fehler enthalten oder Varianten existieren, z.B. für Goethe.
    Hovern wir über einen Wert, erscheint ein "edit"-Button, mit dem wir alle diese Werte auf einmal
    ändern können. Zum Beispiel haben einige Ansetzungen von Goethe einen Zeilenumruch im Namen und
    das "von" steht in einer eigenen Zeile. Diese Vorkommen können wir auf einmal Korrigieren.
  - Über den Button Cluster können automatisiert Kandidaten für Namensvarianten gefunden und 
    vereinheitlicht werden. OpenRefine bietet dafür verschiedene Verfahren an, die sich je nach 
    Datenlage unterschiedlich gut eignen. Eine manuelle Kontrolle ist sinnvoll! Wichtig: Zum 
    Clustern auf allen Werten, dürfen in der Facette keine Werte ausgewählt sein, sonst werden nur 
    diese geclustert! 
    
5. Spalten und Zellen vereinen und auftrennen
  - OpenRefine bietet mehrere Möglichkeiten, Werte zu vereinen oder zu trennen. Das Trennen und
    Vereinen geht jeweils über die Angabe von Trennzeichen.
  - Über `Edit cells > Join/Split multi-values cells` können Zeilen eines Records mit 
    unterschiedlichen Werten in einer Zelle vereint oder entsprechend auf mehrere Zeilen 
    aufgespalten werden.
  - Über die `Transpose`-Befehle können komplizierte Umformungen zwischen Spalten und Zeilen 
    durchgeführt werden. Ein einfaches Verbinden oder Auftrennen von Spalten geht über
    `Edit column > Split/Join columns`.
  - Aus unseren zahlreichen Datumsspalten wollen wir eine einzige Spalte mit einer Jahresangabe 
    extrahieren. Der Ansatz ist, alle Werte der bestehenden Spalten zu vereinen. In dieser fischen 
    wir dann die erstbeste Jahresangabe heraus:
  - Wir gehen auf `Join columns...`. Im Dialog wählen wir alle Date-Spalten aus und geben als
    Separator ein Komma an. Wir wählen "Write result in new column named" und nennen diese "year". 
    Schließlich haken wir noch an "Delete joined columns", da wir die Originalspalten nicht mehr 
    benötigen.
  - Wir schauen uns über eine Textfacette die WErte der year-Spalte an und erkennen, dass 
    vierstellige Zahlen immer Jahreszahlen sind und diese auch immer vorhanden sind.
    Wir gehen auf `Edit cells > Replace`. In diesem Ersetzen-Dialog können wir mit regulären
    Ausdrücken arbeiten, was uns erlaubt, eine Jahreszahl zu finden und alles andere zu löschen.
    Der entsprechende Suchstring ist `^.*(\d{4}).*$` und als Ersetzung `$1`.
    
6. Reconcile: Abgleichen und Verknüpfen
  - Mit `Reconcile > Start reconciling` wird der automatische Abgleich mit einer externen 
    Datenquelle gestartet. Vorinstalliert ist die Verbindung zu Wikidata. Andere Datenquellen wie
    Normdateien können ebenfalls installiert werden, sofern sie eine bestimmte Schnittstelle 
    unterstützen. Man muss sich für jeden Reconcile-Vorgang auf eine Datenquelle festlegen. 
    OpenRefine wird dann die Datenquelle nach geeigneten Treffern (Matches) durchsuchen und Zellen, 
    für die ein hinreichend sicherer Match gefunden wurde, inhaltlich aufbereiten: Für diese Zelle 
    sieht man und verwendet OpenRefine nicht mehr den ursprünglichen Wert, sondern die Normansetzung
    der Datenquelle.
  - Im Dialogfenster kann man den Suchraum für OpenRefine auf bestimmte Kategorien/Types eingrenzen.
    Außerdem kann man Spalten angeben, die für eine Bewertung von Treffern hilfreich sein können.
    So könnte etwa beim Reconcilen der Personendaten die Spalte year hilfreich sein, da sie mit den
    Lebensdaten der Person vergeglichen werden kann. Dies hängt jedoch auch maßgeblich von den
    Möglichkeiten der Fremddatenquelle ab.
  - Wir werden die Ortsdaten mit Wikidata abgleichen. Wir schränken die Suche auf den type "city"
    ein. Zusätzliche Information in weiteren Spalten haben wir nicht. Der Reconcile-Vorgang selbst
    kann einige Zeit in Anspruch nehmen. Daher gibt OpenRefine oben mittig den Fortschritt an.
  - Nachdem Reconcile fertig ist, zeigt OpenRefine im Kopf der Spalte einen Fortschrittsbalken an,
    der dem Anteil der Zellen entspricht, die mit einem Datensatz aus Wikidata gematcht wurden. 
    Gematchte Werte werden als Link angezeigt, der zu den Fremddaten führt. Beim Hovern darüber, 
    wird ein Vorschau-Popup eingeblendet. Findet OpenRefine mehrere Kandidaten, wird es diese als
    Liste einblenden, die nach bester Übereinstimmung sortiert ist. Man hat dann die Möglichkeit 
    einen Treffer entweder nur für diese eine Zelle oder für alle gleichlautenden Werte zu matchen. 
    Weiterhin kann man über "Search for match" die Fremddaten manuell durchsuchen.
    Die Funktion `Reconcile > Actions > Match each cell to its best candidate` kann die mühsame
    manuelle Auswahl abkürzen.
  - Reconcile bringt seine eigenen Facets unter `Reconcile > Facets`. Mit er Facette `By judgment`
    kann man sich einen Blick darüber verschaffen, wieviele und welche Werte gematcht wurden oder 
    nicht.
  - Wir matchen also alle noch offenen Felder. Wir können dazu die oben beschriebe Action benutzen.
    Danach bleiben allerdings immernoch Felder übrig, für die wir händisch eine Lösung finden 
    müssen. Sollten wir beim Durchsuchen von Wikidata keinen passenden Eintrag finden, können wir
    einen neuen erstellen ("Create new item").
    Hinweis: Bei letzterem erstellen wir nicht automatisch einen neuen Eintrag in Wikidata. Vielmehr
    merkt sich OpenRefine, dass es diesen Ort noch nicht in Wikidata gibt. Diese Funktionalität ist
    nur oder vor allem sinnvoll, wenn man Daten für einen Upload in Wikidata vorbereitet.
    
7. Reconcile: Anreichern
  - Da nun alle Ortsdaten mit Wikidata verknüpft sind, können wir unsere Daten mit Informationen aus
    Wikidata anreichern. Für uns sind die Geo-Koordinaten wichtig, um die Orte auf einer Karte 
    anzeigen zu können.
  - Wir gehen auf `Edit column > Add columns from reconciled values...`. Im Dialog können wir nach 
    beliebigen Wikidata-Eigenschaften suchen oder aus der vorgeschlagenen Liste auswählen.
    In der Preview können Sie abgleichen, ob die gefundenen Werte Ihren Erwartungen entsprechen.
    Es sollte nicht schwer sein, eine entsprechende Eigenschaft zu finden...
    Es ist auch möglich, mehrere Spalten auf einmal auszuwählen und zu laden.
    Das Laden der Zusatzinfos kann je nach Umfang ebenfalls einige Zeit in Anspruch nehmen.

8. Spaltenwerte auffüllen
  - Da der XML-Import Records angelegt hat, sind in "übergeordneten" Spalten die Werte immer nur in
    der ersten Zeile eingetragen, obwohl sie auch für darunterstehende Werte gelten. Über dieses
    Verhalten erkennt OpenRefine zusammenhängende Zeilen, also Records. Records können in OpenRefine
    von Vorteil für die Bearbeitung sein, manchmal aber auch hinderlich. Die leeren Felder sind bei 
    einer Weiterverarbeitung in anderen Programmen ebenfalls eventuell nachteilig.
    OpenRefine stellt daher die Funktionen `Fill down` und `Blank down` bereit, die entweder auf
    einer einzelnen Spalte (dann unter `Edit cells`) oder die gesamte Tabelle (im All-Menü unter 
    `Edit columns`) angewandt werden können. Sie füllen die leere Zellen mit dem vorhergehenden Wert
    aus bzw. tilgen wiederholte Werte. 
  - Wir können dies auf unsere gesamte Tabelle anwenden.

9. Export
  - Wir haben nun einen Datensatz, den wir als CSV exportieren und in ein GIS oder eine App integrieren 
    können.
  - Im Menü `Export` kann dabei aus mehreren Exportformaten und -modi gewählt werden. 

Weitere mögliche Schritte zum Üben wären:
- Die Koordinaten in zwei Spalten für lat und long aufspalten oder als WKT formatieren. 
- Die Personendaten ebenfalls mit Wikidata reconcilen und die Tabelle mit Lebensdaten oder 
  (Links zu) Thumbnails der Personen anreichern. 
- Die Bearbeitungshistorie kopieren und auf die Korrespondenz von Alexander von Humboldt anwenden.
  