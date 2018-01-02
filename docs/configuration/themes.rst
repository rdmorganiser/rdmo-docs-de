Themen
------

Eine Anpassung Ihrer RDMO Instanz lässt sich durch Veränderungen an den verschiedenen *templates* sowie den *statischen Assets* (CSS Dateien, Bilder, etc.) erreichen. Das Django-Framework, auf dem RDMO basiert, bietet hierfür eine mächtige Methode. Zunächst legen Sie innerhalb ihres ``rdmo-app``-Verzeichnisses einen ``theme``-Ordner mit einem ``static``- und einem ``templates``-Ordner darin an:

.. code:: python

    mkdir theme theme/static theme/templates

Dann fügen Sie folgendes Ihrer ``config/settings/local.py`` hinzu:

.. code:: python

    THEME_DIR = os.path.join(BASE_DIR, 'theme')

Templates und statische Datein in ihrem ``theme``-Ordner überschreiben dann die entsprechenden original Dateien, solange sie den gleichen relativen Pfad besitzen, z.B. die Datei ``theme/templates/core/base_navigation.html`` überschreibt ``rdmo/core/templates/core/base_navigation.html``.

Normalerweise befinden sich die Templates in Ihrer virtuellen Umgebung, z.B. ``/srv/rdmo/rdmo-app/env/lib/python2.7/site-packages/rdmo/core/static/core/css/variables.scss``. Der konkrete Pfad ist abhängig von Ihrer Python Version und der verwendeten Plattform. Wir empfehlen daher, die Originaldatei aus dem `rdmo repository <https://github.com/rdmorganiser/rdmo>`_ herunterzuladen. Für das Beispiel oben ist dies https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/static/core/css/variables.scss.

Einige Dateien, die Sie vielleicht überschreiben möchten, sind:

SASS Variabeln:
    https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/static/core/css/variables.scss kann zu ``theme/static/css/variables.scss`` kopiert werden und genutzt werden, um Farben anzupassen.

Navigationsleiste
    https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/base_navigation.html kann zu ``theme/templates/core/base_navigation.html`` kopiert werden und genutzt werden, um die Navigationsleiste anzupassen.

Homepage-Text
    https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/home_text_en.html und https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/home_text_de.html können nach ``theme/templates/core/home_text_en.html`` und ``theme/templates/core/home_text_de.html`` kopiert werden und können genutzt werden, um den Text auf der Homepage anzupassen.

Beachten Sie, dass Updates für das RDMO-Paket die Themen inkompatibel werden lassen können und Fehler verursachen können. In diesem Fall müssen die Dateien in ``theme`` so angepasst werden, dass deren RDMO-Gegenstücke auf deren Funktionalität abgestimmt werden.
