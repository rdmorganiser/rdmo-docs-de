# Themen


## Einleitung

RDMO nutzt Django, welches ein hohes Maß an Anpassungsfähigkeit durch eine eigene mächtige Methode bietet. *Templates* und *statische Assets* (CSS-Dateien, Bilder, etc.) können mit geringem Aufwand eingebunden werden. Dies erreicht man, indem man einen `theme`-Ordner innerhalb von `rdmo-app` erzeugt. Das Framework wird dann die Dateien importieren, die in diesem `theme`-Ordner liegen und nicht die Gegenstücke aus dem Quellcode der RDMO-Installation. Es ist also möglich den Satz der genutzten Dateien zu verändern, solange die Dateistruktur innerhalb von `theme` analog zu der aus der RDMO-Installaion ist. Es gibt zwei Wege Themes zu erstellen.

## Manuell erstellen

Wenn sie ein Theme von Hand erstellen möchten, sollten sie das Folgende tun.

1. Zunächst legen Sie innerhalb ihres `rdmo-app`-Verzeichnisses einen `theme`-Ordner mit einem `static`- und einem `templates`-Ordner darin an:

    ```shell
    mkdir theme theme/static theme/templates
    ```

1. Dann fügen Sie folgendes Ihrer `config/settings/local.py` hinzu:

    ```python
    import os
    from . import BASE_DIR

    THEME_DIR = os.path.join(BASE_DIR, 'theme')
    ```

1. Kopieren Sie die Dateien, die sie modifizieren möchten in den `theme`-Ordner. Achten sie darauf, dass die relativen Pfade denen der Originaldaten der RDMO-Installation entsprechenden. Bitte schauen Sie in den Abschnit weiter unten, in dem sich mehre Informationen finden.

## Automatisch erstellen

Um das Erstellen von Themes zu vereinfachen gibt es ein `manage.py` Skript. Das Skript erstellt die Ordner `theme/static` und `theme/templates`, kopiert ein grundlegenden Satz von Dateien in die Ordner und fügt den nötigen Eintrag der `local.py` Konfiguration hinzu. Wenn Sie andere Dateien anpassen wollen, kopieren sie diese bitte von Hand in die entsprechenden Ordner. Das Skript kann auf so genutzt werden:

```python
python manage.py make_theme
```


## Arbeiten mit Themes

Wenn sie die oben genannten Schritte durchgeführt haben überschreiben Templates und statische Dateien in ihrem `theme`-Ordner die entsprechenden Originaldateien, solange sie den gleichen relativen Pfad besitzen, z.B. die Datei `theme/templates/core/base_navigation.html` überschreibt `rdmo/core/templates/core/base_navigation.html`.

Normalerweise befinden sich die Templates in Ihrer virtuellen Umgebung, z.B. `/srv/rdmo/rdmo-app/env/lib/python2.7/site-packages/rdmo/core/static/core/css/variables.scss`. Der konkrete Pfad ist abhängig von Ihrer Python Version und der verwendeten Plattform. Wir empfehlen daher, die Originaldatei aus dem [rdmo repository](https://github.com/rdmorganiser/rdmo) herunterzuladen. Für das Beispiel oben ist dies <https://raw.githubusercontent.com/rdmorganiser/rdmo/master/rdmo/core/static/core/css/variables.scss>. Wenn Sie von Github runterladen achten Sie bitte darauf, die blanken Text-Dateien zu beziehen. Wenn Sie versehentlich den Quellcode der Website nehmen, wird RDMO nicht mehr funktionieren und einen Fehler ausgeben.

Einige Dateien, die Sie zur Anpassung verändern wollen:

### SASS Variablen:
<https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/static/core/css/variables.scss> kann nach `theme/static/css/variables.scss` kopiert werden und genutzt werden, um Farben anzupassen.

### Navigationsleiste
<https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/base_navigation.html> kann nach `theme/templates/core/base_navigation.html` kopiert werden und genutzt werden, um die Navigationsleiste anzupassen.

### Homepage-Text
<https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/home_text_en.html> und <https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/home_text_de.html> können nach `theme/templates/core/home_text_en.html` und `theme/templates/core/home_text_de.html` kopiert werden und genutzt werden, um den Text der Homepage anzupassen.

### Nutzerbedingungen
Der Inhalt, der in dem Nutzerbedingungen-Fenster erscheint, können durch Templates an der richtigen Stelle gesetzt werden. Für die verschiedenen Sprachen wird jeweils eine Datei benötigt, die sich wie folgt plaziert werden müssen: `theme/templates/account/terms_of_use_de.html` und  `theme/templates/account/terms_of_use_en.html`. Setzen Sie die Variable ACCOUNT_TERMS_OF_USE auf True in Ihrer config/settings/local.py, um die das Erscheinen der Nutzerbedingungen zu aktivieren.

Beachten Sie: Updates für das RDMO-Paket können die Veränderung des `Theme` inkompatibel werden lassen und Fehler verursachen. In diesem Fall müssen die Dateien in `theme` so angepasst werden, dass die veränderten Funktionalitäten von RDMO-Gegenstücken in ihren Dateien ebenfalls bereitgestellt werden.
