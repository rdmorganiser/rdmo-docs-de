# Erforderliche Pakete installieren

Das Installieren der erforderlichen Software-Pakete für RDMO unterscheidet sich für verschiedene Betriebssysteme und ist daher in einzelnen Abschnitten dargelegt. Hier müssen Sie den Superuser verwenden.

## Linux

Wir empfehlen für die Installation der Voraussetzungen das Paket-System der Distribution zu verwenden. Bei Debian/Ubunutu verwenden Sie:

```bash
sudo apt install build-essential libxml2-dev libxslt-dev zlib1g-dev \
    python3-dev python3-pip python3-venv \
    git pandoc

# optional, for pdf output
sudo apt install texlive texlive-xetex
```

Bei RHEL/CentOS verwenden Sie:

```
sudo yum install gcc gcc-c++ libxml2-devel libxslt-devel \
    python34-devel python34-pip python34-virtualenv \
    git pandoc

# optional, for pdf output
sudo yum install texlive texlive-xetex texlive-mathspec texlive-euenc \
    texlive-xetex-def texlive-xltxtra
```

Bei Ubuntu 14.04, ist `python3-venv` nicht verfügbar. Bitte verwenden Sie stattdessen `python3.5-venv`.

Bei RHEL/CentOS ist `selinux` standardmäßig aktiviert. Dies führt zu unerwarteten Fehlern, abhängig davon, wo der RDMO-Sourcecode auf dem System isntalliert ist. Auch wenn die bevorzugte Lösung die richtige Konfiguration von `selinux` wäre (was im Rahmen dieser Dokumentation zu weit führen würde), kann `selinux` auf `permissive` oder `disabled` unter `/etc/selinux/config` gesetzt werden (erfordert einen Neustart).

Wenn Sie Python 2.7 anstatt Python 3 benutzen möchten, verwenden Sie die entsprechenden Pakete:

```bash
apt install python-dev python-pip python-virtualenv    # Debian/Ubuntu
yum install python-devel python-pip python-virtualenv  # RHEL/CentOS
```


## macOS

Wir empfehlen die Voraussetzungen mit [brew](http://brew.sh) zu installieren:

```bash
brew install python3             # for python 3
brew install python              # for python 2
brew install git
brew install pandoc

# optional, for pdf export
brew install texlive
```


## Windows

Bei Windows müssen die Software-Voraussetzungen von den einzelnen Internetseiten heruntergeladen und installiert werden.

Für Python:
* herunterladen von <https://www.python.org/downloads/windows/>
* wir empfehlen eine Version >= 3.4
* vergessen Sie nicht zu überprüfen, dass währended des Setups `Python zu den Umgebungsvariablen hinzufügen` gesetzt ist

Für git:
* herunterladen von <https://git-for-windows.github.io>

Für die Microsoft C++ Build Tools:
* herunterladen von <https://wiki.python.org/moin/WindowsCompilers>

Für Pandoc:
* herunterladen von <https://github.com/jgm/pandoc/releases>

Für pdflatex (optional, für pdf-Export):
* herunterladen <http://miktex.org>

Alle weiteren Schritte müssen in der Windows-Shell `cmd.exe` ausgeführt werden. Sie können diese vom Start-Menü aus öffnen.
