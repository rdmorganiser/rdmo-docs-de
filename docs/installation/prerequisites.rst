Voraussetzungen installieren
----------------------------

Das Installieren der Voraussetzungen für RDMO unterscheidet sich auf den verschiedenen Betriebssystemen und ist daher in einzelnen Abschnitten enthalten.

Linux
~~~~~

Wir empfehlen für die Installtion der Voraussetzungen das Paket-System der Distribution zu verwenden. Bei Debian/Ubunutu verwenden Sie:

.. code:: bash

    sudo apt install build-essential libxml2-dev libxslt-dev zlib1g-dev \
                     python3-dev python3-pip python3-venv \
                     git pandoc

    # optional, for pdf output
    sudo apt install texlive texlive-xetex

Bei RHEL/CentOS verwenden Sie:

.. code:: bash

    sudo yum install gcc gcc-c++ libxml2-devel libxslt-devel \
                     python34-devel python34-pip python34-virtualenv \
                     git pandoc

    # optional, for pdf output
    sudo yum install texlive texlive-xetex texlive-mathspec texlive-euenc \
        texlive-xetex-def texlive-xltxtra

Bei Ubuntu 14.04, ist `python3-venv` nicht verfügbar. Bitte verwenden Sie stattdessen `python3.5-venv`.

Bei RHEL/CentOS ``selinux`` ist standardmäßig aktiviert. Dies führt zu unerwarteten Fehlern abhängig davon wo der RDMO-Sourcecode auf dem System isntalliert ist. Auch wenn die bevorzugte Lösung die richtige Konfiguration ist (was im Rahmen dieser Dokumentation zu weit führen würde), kann ``selinux`` auf ``permissive`` oder ``disabled`` unter ``/etc/selinux/config`` gesetzt werden (erfordert einen Neustart).

Wenn Sie Python 2.7 anstatt Python 3 benutzen möchten, verwenden Sie folgende entsprechende Pakete:

.. code:: bash

    apt install python-dev python-pip python-virtualenv    # Debian/Ubuntu
    yum install python-devel python-pip python-virtualenv  # RHEL/CentOS


macOS
~~~~~

Wir empfehlen die Voraussetzungen mit  `brew <http://brew.sh>`_ zu installieren:

.. code:: bash

    brew install python3                                       # for python 3
    brew install python                                        # for python 2
    brew install git
    brew install pandoc

    # optional, for pdf export
    brew install texlive


Windows
~~~~~~~

Bei Windows müssen die Software-Voraussetzungen von den einzelnen Internetseiten heruntergeladen und isntalliert werden.

Für Python:

* herunterladen von https://www.python.org/downloads/windows/
* wir empfehlen eine Version >= 3.4
* vergessen Sie nicht zu überprüfen, dass währende Des Setups `Python zu den Umgenungsvariabeln hinzufügen` gesetzt ist

Für git:

* herunterladen von https://git-for-windows.github.io/

Für die Microsoft C++ Build Tools:

* herunterladen von http://landinghub.visualstudio.com/visual-cpp-build-tools

Für pdflatex (optional, für pdf-Export):

* herunterladen http://miktex.org/

Alle weiteren Schritte müssen in der Windowsshell ``cmd.exe`` ausgeführt werden. Du kannst diese vom Start-Menü aus öffnen.
