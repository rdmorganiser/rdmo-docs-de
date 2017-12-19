Einsatz
========


Wie bereits erwähnt kann RDMO in zwei verschiedenen Setups ausgeführt werden:

* für :doc:`Entwicklung oder Testen <development>` benutzte Sie den eingebauten Django-Entwicklungsserver.

* für den Betrieb wird ein Webserver und das `wsgi <https://docs.djangoproject.com/en/1.10/howto/deployment/wsgi/>`_ Protokoll verwendet. Wir empfehlen eine der folgenden zwei Setups zu verwenden: 
    * :doc:`Apache2 und mod_wsgi <apache>`
    * :doc:`nginx, gunicorn und systemd <nginx>`

.. toctree::
   :caption: Index
   :maxdepth: 2

   development
   apache
   nginx
