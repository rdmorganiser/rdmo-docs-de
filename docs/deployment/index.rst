Deployment
==========

Wie bereits erwähnt kann RDMO in zwei verschiedenen Setups genutzt werden:

* für :doc:`Entwicklung oder zum Test <development>` wird der eingebaute Django-Entwicklungsservers genutzt.

* für den Betrieb wird ein Webserver und das `wsgi <https://docs.djangoproject.com/en/1.11/howto/deployment/wsgi/>`_ Protokoll verwendet. Wir empfehlen eines der folgenden Setups zu verwenden:

    * :doc:`Apache2 und mod_wsgi <apache>` (Nur hier kann Shibboleth verwendet werden.)
    * :doc:`nginx, gunicorn und systemd <nginx>`

.. toctree::
   :caption: Index
   :maxdepth: 2

   development
   apache
   nginx
