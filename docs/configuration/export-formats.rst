Formate exportieren
-------------------

RDMO unterstützt das Exportieren zu bestimmten Formaten mit Hilfe vom großartigen `pandoc <https://pandoc.org/>`_ Konvertierer. Die Liste der zur Auswahl stehenden Formate kann angepasst werden indem die ``EXPORT_FORMATS``-Einstellung in ihrem ``config/settings/local.py`` konfiguriert wird.

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

Die verschienden Formate, die von pandoc unterstützt werden, finden Sie `auf der pandoc Homepage <https://pandoc.org/>`_.
