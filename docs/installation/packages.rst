Python Pakete installieren
--------------------------

Nach dem Sie den ``rdmo-app``-Ordner installiert haben, müssen Sie weitere ``rdmo``-Pakete sowie andere Python-Abhängigkeiten installieren.

Wechslen Sie dazu in den ``rdmo-app``-Ordner und erstellen Sie eine  `virtualenv <https://virtualenv.readthedocs.org>`_ (mit ihrem Benutzer oder ihrem erstellten ``rdmo``-Benutzer, nicht als ``root``):

.. code:: bash

    cd rdmo-app

    python3 -m venv env                                        # for python3
    virtualenv env                                             # for python2.7

    source env/bin/activate                                    # on Linux or macOS
    call env\Scripts\activate.bat                              # on Windows

    pip install --upgrade pip setuptools                       # update pip and setuptools

Nachdem die virtuelle Umgebung aktiviert ist, kann dort das ``rdmo``-Paket mit Hilfe von ``pip`` installiert werden:

.. code:: bash

    pip install rdmo

Auf Windows wird für die Installation pandoc benötigt:

.. code:: bash

    # only on Windows
    python -c "import pypandoc; pypandoc.download_pandoc()"

Die virtuelle Umgebung schottet die RDMO-Installation vom Rest des Systems ab. Dies erlaubt das Betreiben mehrerer Anwendungen mit verschiedenen Python-Abhängigkeiten auf einer Machine laufen zu lassen, und diese Abhängigkeiten ohne Root-Rechte zu installieren.

**Wichtig:** Die virtuelle Umgebung muss jedes Mal mit Hilfe von``source env/bin/activate`` oder ``call env\Scripts\activate.bat`` aktiviert werden, wenn ein neues Terminal benutzt wird.
