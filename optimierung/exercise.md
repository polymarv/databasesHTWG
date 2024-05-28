

1) Wenden Sie Transformationsregeln an, um einen optimalen Auswertungsplan zu
finden. Geben Sie die zwei erfolgsversprechendsten Auswertungsbäume an.




2) Geben Sie Kostenabschätzungen für diese Auswertungspläne ohne Pipelining an
und vergleichen Sie das Ergebnis.

Siehe S.37 ff.

Berechne Anzahl Tupel S.37 oben (und ab S.40)
Tupel pro Seite = Seitengröße/Tupelgröße abgerundet

Berechne Blöcke (b in diesem Block):
Anzahl Seiten = Tupel / Tupel pro Seite

sh als join ist dann = s + h (bei "Durchschnittliche Tupelgrößen")


// Nur Lese und Schreibzugriffe wichtig
Kostenschätzung S.37 unten
Jeder Operator hat Lese- und Schreibkosten
 -> ohne Pipelining

Alle Kosten addieren sind dann die Gesamtkosten (Lesen und Schreiben)


Klausur relevant in abgespeckter Form

3) Wenn Sie genau einen Index erstellen sollten, auf welchem Attribut würden Sie ihn
definieren?

