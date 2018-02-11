Themen
------

Eine Anpassung Ihrer RDMO Instanz lässt sich durch Veränderungen an den verschiedenen *Templates* sowie den *statischen Assets* (CSS-Dateien, Bilder, etc.) erreichen. Das von RDMO genutzte Django-Framework bietet hierfür eine mächtige Methode. Zunächst legen Sie innerhalb ihres ``rdmo-app``-Verzeichnisses einen ``theme``-Ordner mit einem ``static``- und einem ``templates``-Ordner darin an:

.. code:: python

    mkdir theme theme/static theme/templates

Dann fügen Sie folgendes Ihrer ``config/settings/local.py`` hinzu:

.. code:: python

    THEME_DIR = os.path.join(BASE_DIR, 'theme')

Templates und statische Dateien in ihrem ``theme``-Ordner überschreiben dann die entsprechenden originalen Dateien, solange sie den gleichen relativen Pfad besitzen, z.B. die Datei ``theme/templates/core/base_navigation.html`` überschreibt ``rdmo/core/templates/core/base_navigation.html``.

Normalerweise befinden sich die Templates in Ihrer virtuellen Umgebung, z.B. ``/srv/rdmo/rdmo-app/env/lib/python2.7/site-packages/rdmo/core/static/core/css/variables.scss``. Der konkrete Pfad ist abhängig von Ihrer Python Version und der verwendeten Plattform. Wir empfehlen daher, die Originaldatei aus dem `rdmo repository <https://github.com/rdmorganiser/rdmo>`_ herunterzuladen. Für das Beispiel oben ist dies https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/static/core/css/variables.scss.

Einige Dateien, die Sie zur Anpassung verändern wollen:

SASS Variabeln:
    https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/static/core/css/variables.scss kann nach ``theme/static/css/variables.scss`` kopiert werden und genutzt werden, um Farben anzupassen.

Navigationsleiste
    https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/base_navigation.html kann nach ``theme/templates/core/base_navigation.html`` kopiert werden und genutzt werden, um die Navigationsleiste anzupassen.

Homepage-Text
    https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/home_text_en.html und https://github.com/rdmorganiser/rdmo/blob/master/rdmo/core/templates/core/home_text_de.html können nach ``theme/templates/core/home_text_en.html`` und ``theme/templates/core/home_text_de.html`` kopiert werden und genutzt werden, um den Text der Homepage anzupassen.

Beachten Sie: Updates für das RDMO-Paket können die Veränderung des `Theme` inkompatibel werden lassen und Fehler verursachen. In diesem Fall müssen die Dateien in ``theme`` so angepasst werden, dass die veränderten Funktionalitäten von RDMO-Gegenstücken in ihren Dateien ebenfalls bereitgestellt werden.
