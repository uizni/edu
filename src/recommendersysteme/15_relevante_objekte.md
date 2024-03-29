F: *Nennen und erklären Sie die Funktionalität der drei Hauptkomponenten einer Suchmaschine wie Google* (9 Punkte)

A:

Nach @brin_anatomy_1998 [S. 3828]:

1. **Komponenten zum Crawling**: Der URL-Server schickt eine Liste mit zu suchenden Webseiten an die Crawler. Verteilte Crawler laden Webseiten herunter. Der Store-Server komprimiert die Webseiten und legt sie im Webpage-Repository mit einer doc id ab.

2. **Komponenten zum Indexieren von Daten**: Der Indexer liest das Repository, dekomprimiert die Webseiten und extrahiert aus den Webseiten Wort-Treffer mit Informationen zu Schriftgröße, Großschreibung etc. (hits) und speichert sie in den *barrels* ab. Weiterhin werden alle Links extrahiert und Linkziel, der Linktext und die Linkquelle in *Anchors Files* gespeichert. Der URL-Resolver liest die Anchor Files, konvertiert die Links in absolute Links und generiert doc Ids. Die Anchor-Texts werden ebenfalls mit abgelegt im Forward Index. Der Sorter sortiert die Barrels nach wordIDs, um einen invertierten Index zu erstellen. Weiterhin besteht ein Lexikon, das neu aus dem Indexer generiert wird. Es wird dann vom *Searcher* verwendet, um mit dem invertierten Index und PageRank Suchanfragen zu beantworten.

3. **Komponenten zum Bewerten der Wichtigkeit**: Anhand der Links wird eine Link-Datenbank aufgebaut, woraus dann der Page-Rank für alle Dokumente ermittelt wird.

![Google Infrastruktur [@brin_anatomy_1998 S. 3.828] ](../.gitbook/assets/google_infrastructure.jpg)

---

F: *Wie wird die Gewichtungsmatrix von PageRank aus der Adjazenzmatrix aufgebaut? Erklären Sie die PageRank Formel für die Gewichtungsmatrix* (9 Punkte)

A: Die PageRank Formel lautet wie folgt: 

$$
M = \left( 1 - m \right) \times A + m \times S
$$

$$A$$ ist dabei die Matrix, die aus der Linkstruktur abgeleitet wird. Sie enthält **Stimmenverteilung**. Die Matrix $$A$$ enthält in einer Zeile $$k$$, die Stimmanteile, die k von anderen Seiten erhält. Und in Spalte $$k$$, die Stimmanteile, die $$k$$ an die anderen Spalten verteilt (Folie 11 + 18). Die positiven Werte in Spalte k stellen die Wahrscheinlichkeit dar, dass ein Surfer von Seite k auf eine Seite $$j$$ durch Anklicken des Links zwischen $$k$$ und $$j$$ wechselt.

Die Matrix $$S$$ ist eine $$n \times n$$ Matrix mit $$s_{\text{ij}} = \frac{1}{n}$$. Sie enthält **Gleichverteilung**. Die Annahme ist, dass ein Surfer z. B. durch Eingeben eines Links in den Browser auf irgendeine Seite wechselt. Die Wahrscheinlichkeit von $$k$$ nach $$j$$ zu wechseln ist damit $$\frac{1}{n}$$.

Der Faktor $$m$$ gewichtet also den Einfluss beider Verhaltensmodi (zufälliges Klicken vs. Weiternavigieren in Linkstruktur) des Random Surfers. Behebt damit das Problem nicht verbundener Nodes, Dangling Nodes (und Spidertraps). [@geyer-schulz_relevante_2020 S. 19]

---

F: *Wie wird der PageRank Index aus der Gewichtungsmatrix berechnet? Beschreiben Sie den Berechnungsalgorithmus*

A: 
Es wird die Power-Methode verwendet. Siehe hierzu @geyer-schulz_relevante_2020 [S. 20]:
```powershell
Power(M, z, k)
M: PageRank Linkmatrix
z: Startvektor aus n Einsen (x_j = 1)
k: Anzahl der Iterationen
x <- z;
For i in 1 to k
    Do x <- Mx;
Return(x)
```

**Erklärung**:

Der Vektor $$x$$ wird mit $$z=\vec{1}$$ initialisiert. Es wird $$k$$-fach eine Matix $$M$$ von links an den Vektor $$x$$ multipliziert. Das Ergebnis des Matrix-Vektorprodukts wird im Vektor $$x$$ gespeichert. Aus $$x$$ lässt sich nach $$k$$ Iterationen der Index ableiten.

## Quellen:
