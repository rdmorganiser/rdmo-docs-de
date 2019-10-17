# Export and Import

RDMO bietet Export- und Importfunktionen, die über die rechte Seitenleiste verfügbar sind. Die beiden Kategorien, die die gleichnamigen Funktionen bieten, erscheinen für jeden Datentypen (wie z.B. Fragen oder Optionen). es handelt sich um kontext-sensitive Funktionen. Wenn man sich beispielsweise auf der Seite `Aufgaben` befindet und `Export` oder `Import` nutzt, kann man nur `Aufgaben` ex- beziehungsweise importieren. Besonders beim Import sollte darauf geachtet werden, da dieser fehlschlägt, wenn man eine XML-Datei wählt, die nicht den entsprechend passenden Inhalt hat.

## Export

Das Export-Menü befindet sich auf der rechten Seite des Bildschirms. Es besteht aus einer Liste, der unterstützten Export-Formate. Diese Liste kann je nach Seite auf der man sich befindet unterschiedliche aussehen. Mehr informationen wie die Export-Formate konfiguriert werden, befinden sich [hier](../configuration/export-formats.html).

## Import

Wie bereits erwähnt verhält sich der Import kontext-sensitiv. Er funktioniert nur, wenn eine zur Seite passende XML-Datei importiert wird, die einen validen Datensatz enthält. Ist eine von beiden Bedingungen nicht erfüllt, bricht der Parser den Import ab. Dadurch wird lediglich die Seite neu geladen, während die Daten unverändert bleiben.

Dateien können auf zwei Arten importiert werden. Entweder durch den Auswahldialog, der sich nach Klick auf `XML-Datei wählen` öffnet, oder durch Ziehen und Ablegen (Drag'n'Drop) einer Datei auf die Box, die den erwähnten Text enthält.

Bei einem Projektimport wird immer ein neues Projekt erstellt, in dem die importierten Daten abgelegt werden. *Bei allen anderen Importen (Optionen, Aufgaben etc.) werden die existierenden Daten überschrieben.* Die URI dient dabei als Identifikator. Hat ein zu importierendes Element die URI eines bereits existierenden, wird das existierende überschrieben.
