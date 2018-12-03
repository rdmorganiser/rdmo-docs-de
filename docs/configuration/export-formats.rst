Export formate
--------------

RDMO unterstützt das Exportieren in bestimmten Formaten mit Hilfe des ausgezeichneten `Pandoc <https://pandoc.org/>`_ Konvertierers. Die Liste der zur Auswahl stehenden Formate kann über die ``EXPORT_FORMATS``-Einstellung in der ``config/settings/local.py`` angepasst werden.

.. code:: python

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

Die verschienden Formate, die von pandoc unterstützt werden, finden Sie `auf der Pandoc-Homepage <https://pandoc.org/>`_.

Das Seitenformat und verschiedene andere Dinge, die Formatierung und Aussehen von Textdokumenten betreffen, können mit Hilfe von Referenzdokumenten angepasst werden. Die `Pandoc-Dokumentation <https://pandoc.org/MANUAL.html>`_ hält eine ausführliche Liste der unterstützten Einstellungen bereit, die unterhalb des Paragraphen '--reference-doc' eingesehen werden kann. Referenzdokumente können für die Formate ``.docx`` und ``.odt`` verwendet werden. Welche Datei als Referenzdokument dient, wird in der ``config/settings/local.py`` definiert. Wenn diese Einträge nicht in Ihrer Konfiguration sind, werden die Standard-Referenzdokumente aus dem RDMO Paket verwendet.

.. code:: python

    EXPORT_REFERENCE_DOCX='FULL PATH OF YOUR REFERENCE DOCX'
    EXPORT_REFERENCE_ODT='FULL PATH OF YOUR REFERENCE ODT'
