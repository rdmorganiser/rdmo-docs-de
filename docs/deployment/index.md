# Betrieb

Wie bereits erwähnt kann RDMO in zwei verschiedenen Setups genutzt werden:

* für [Entwicklung oder Testen](development.html) benutzte Sie den eingebauten Django-Entwicklungsserver.

* für den Betrieb wird ein Webserver und das [wsgi](https://docs.djangoproject.com/en/1.10/howto/deployment/wsgi/) Protokoll verwendet. Wir empfehlen eine der folgenden zwei Setups zu verwenden:
    * [Apache2 und mod_wsgi](apache.html) (nur hier kann Shibboleth verwendet werden)
    * [Nginx, Gunicorn und Systemd](nginx.html)

```eval_rst
----

.. toctree::
   :maxdepth: 2

   development
   apache
   nginx
```
