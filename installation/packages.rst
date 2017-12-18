Python Pakete installieren
--------------------------

Nach dem Sie sich den ``rdmo-app``-Ordner angesehen haben, mussen Sie die ``rdmo``-Pakete installieren und andere Python-Abhängigkeiten.

Wechslen Sie dazu in den ``rdmo-app``-Ordner und erstellen Sie eine  `virtualenv <https://virtualenv.readthedocs.org>`_ (mit ihrem Benutzer oder ihrem erstellen ``rdmo``-Benutzer, nicht als ``root``):

.. code:: bash

    cd rdmo-app

    python3 -m venv env                                        # for python3
    virtualenv env                                             # for python2.7

    source env/bin/activate                                    # on Linux or macOS
    call env\Scripts\activate.bat                              # on Windows

    pip install --upgrade pip setuptools                       # update pip and setuptools

Nachdem die virtuelle Umgebung aktiviert wurde, kann dort das ``rdmo``-Paket mit Hilfe von ``pip`` installiert werden:

.. code:: bash

    pip install rdmo

Auf Windows wird für die Installation pandoc benötigt:

.. code:: bash

    # only on Windows
    python -c "import pypandoc; pypandoc.download_pandoc()"

Die virtuelle Umgebung schottet die RDMO-Installation vom Rest des Systems ab. Dies ermöglicht es mehrere Anwendungen mit verschiedenen Python-Abhängigkeiten auf einer Machine laufen zu lassen und die Abhängigkeiten ohne Root-Rechte zu installieren.

**Wichtig:** Die virtuelle Umgebung muss jedes Mal mit Hilfe von``source env/bin/activate`` oder ``call env\Scripts\activate.bat`` aktiviert werden , wenn ein neues Terminal benutzt wird mit Hilfe.
