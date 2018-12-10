# Formate exportieren

RDMO unterstützt das Exportieren zu bestimmten Formaten mit Hilfe vom großartigen [Pandoc](https://pandoc.org/) Konvertierer. Die Liste der zur Auswahl stehenden Formate kann angepasst werden indem die `EXPORT_FORMATS`-Einstellung in ihrem `config/settings/local.py` konfiguriert wird.

```python
EXPORT_FORMATS = (
    ('pdf', _('PDF')),
    ('rtf', _('Rich Text Format')),
    ('odt', _('Open Office')),
    ('docx', _('Microsoft Office')),
    ('html', _('HTML')),
    ('markdown', _('Markdown')),
    ('mediawiki', _('mediawiki')),
    ('tex', _('LaTeX'))
)
```

Die verschienden Formate, die von pandoc unterstützt werden, finden Sie [auf der Pandoc-Homepage](https://pandoc.org/).

Das Seiten-Format und verschiedene andere Dinge, die Formatierung und Aussehen von Textdokumenten betreffen, können mit Hilfe von Referenzdokumenten angepasst werden. Die [Pandoc-Dokumentation](https://pandoc.org/MANUAL.html) hält eine ausführliche Liste der unterstützten Einstellungen bereit, die unterhalb des Paragraphen '--reference-doc' eingesehen werden kann. Referenzdokumente können für die Formate `.docx` und `.odt` verwendet werden. Welche Datei als Referenzdokument dient, wird in der `config/settings/local.py` definiert. Wenn diese Einträge nicht in Ihrer Konfiguration sind, werden die Standard-Referenzdokumente aus der RDMO-Installation verwendet.

```python
EXPORT_REFERENCE_DOCX='FULL PATH OF YOUR REFERENCE DOCX'
EXPORT_REFERENCE_ODT='FULL PATH OF YOUR REFERENCE ODT'
```
