Themen
------

RDMO erlaubt es Hochlevel-Anpassungen mit Hilfe von Django *templates* (Vorlagen) sowie mit statischen Inhalten (CSS Datei, Bilder, etc.) vorzunehmen. Django, worauf RDMo basiert, bietet eine mächtige Methode dafür. Innerhalb ihres ``rdmo-app``-Verzeichnisses können Sie einen ``Themen``-Ordner mit einem ``static``- und einem ``templates``-Ordner anlegen:

.. code:: python

    mkdir theme
    mkdir theme/static
    mkdir theme/templates

Dann fügen Sie folgendes ihrer ``config/settings/local.py`` hinzu:

.. code:: python

    THEME_DIR = os.path.join(BASE_DIR, 'theme')

Templates und statische Datein in ihrem ``theme``-Ordner können Dateien von RDMO überschreiben solange sie einen relativen Pfad besitzen, z.B. die Datei ``theme/templates/core/base_navigation.html`` überschreibt ``rdmo/core/templates/core/base_navigation.html``.

Einige Dateien, die Sie vielleicht überschreiben möchten, sind:

SASS Variabeln:
    ``rdmo/core/static/core/css/variables.scss`` kann zu ``theme/static/css/variables.scss`` kopiert werden und genutzt werden, um Farben anzupassen.

Navigationsleiste
    ``rdmo/core/templates/core/base_navigation.html`` kann zu ``theme/templates/core/base_navigation.html`` kopiert werden und genutzt werden, um die Navigationsleiste anzupassen. 

Homepage-Text
    ``rdmo/core/templates/core/home_text_en.html`` und ``rdmo/core/templates/core/home_text_de.html`` können nach ``theme/templates/core/home_text_en.html`` und ``theme/templates/core/home_text_de.html`` kopiert werden und können genutzt werden, um den Text auf der Homepage nazupassen. 
    
Beachten Sie, dass Updates für das RDMO-Paket die Themen inkompatiblel werden lassen können und Fehler verursachen können. In diesem Fall müssen die Dateien in ``theme`` so angepasst werden, dass deren RDMO-Gegenstücke auf deren Funktionalität abgestimmt werden.
