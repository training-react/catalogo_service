########################################
catalogo_service
########################################

.. class:: no-web

    catalogo_service es un microservicio **Resource server** que se autentica y autoriza con el `Authorization server`_.



    .. image:: https://github.com/practian-ioteca-project/catalogo_service/blob/master/media/e2-resource_server_catalogo_service.png
        :alt: catalogo_service
        :width: 100%
        :align: center





.. contents::

.. section-numbering::

.. raw:: pdf

   PageBreak oneColumn


============
Installation
============

--------------
Requirements
--------------

* Python 3.4, 3.5
* Django 1.9, 1.10



-------------------
Development version
-------------------

Clone **latest development version** directly from github_:

.. code-block:: bash
    
    # Universal
    
    E:\dev>git clone https://github.com/practian-ioteca-project/catalogo_service.git

Cree un entorno virtual::

    E:\dev>virtualenv ve_catalogo
    E:\dev>ve_catalogo\Scripts\activate

Instale las dependencias::

    (ve_catalogo) E:\dev>cd catalogo_service
    (ve_catalogo) E:\dev\catalogo_service>pip install -r requirements.txt

También instale `Django OAuth2 Backend`_::

    (ve_catalogo) E:\dev\catalogo_service>pip install https://github.com/practian-reapps/django-oauth2-backend/raw/master/dist/django-oauth2-backend-0.1.zip

y `Django Backend Utils`_::

    (ve_catalogo) E:\dev\catalogo_service>pip install https://github.com/practian-reapps/django-backend-utils/raw/master/dist/django-backend-utils-0.1.zip


Sync your database::

    (ve_catalogo) E:\dev\catalogo_service>manage.py migrate

Si ha creado de cero la base de datos, deberá correr createsupersuer::

    (ve_catalogo) E:\dev\catalogo_service>manage.py createsupersuer

    # también deberás crear las apps en http://localhost:7001/o/applications/ 
    # y en el cliente https://github.com/practian-ioteca-project/catalogo_web/blob/master/app/config.js 
    # actualizar la variable

    oauth2Service.clientId = "tu nuevo client_id";

O en MySQL admin, restrure la DB de https://github.com/practian-ioteca-project/catalogo_service/blob/master/upeu_db.sql ::

	# USER : admin
	# PASSWORD : 12345


Run the app in 8003 port::

    (ve_catalogo) E:\dev\catalogo_service>manage.py runserver 8003



===========
Revise las configuraciones
===========

1. INSTALLED_APPS setting like this:

.. code-block:: bash


	INSTALLED_APPS = [
	    'django.contrib.admin',
	    'django.contrib.auth',
	    'django.contrib.contenttypes',
	    'django.contrib.sessions',
	    'django.contrib.messages',
	    'django.contrib.staticfiles',

	    'django.contrib.admindocs',
	    'rest_framework',
	    'corsheaders',
	    'oauth2_provider',

	    'oauth2_backend',
	    'backend_utils',

	    'catalogo',
	]

2. AUTH_USER_MODEL setting like this::

	AUTH_USER_MODEL = 'oauth2_backend.User' 

3. DATABASES setting like this::

	# Database mysql
	DATABASES = {
	    'default': {
	        'ENGINE': 'django.db.backends.mysql',
	        'OPTIONS': {
	            'read_default_file': 'credentials.cnf',  # read_default_file solo funciona con mysql
	        },
	    },
	}	

4. credentials.cnf file setting like this::

	# my.cnf
	[client]
	database = upeu_db
	user = root
	password = 12345
	host = 127.0.0.1
	port = 3306
	default-character-set = utf8



====
Meta
====


-------
Licence
-------

BSD-3-Clause: `LICENSE <https://github.com/practian-ioteca-project/oauth2_backend_service/blob/master/LICENSE>`_.



-------
Authors
-------

- Angel Sullon Macalupu (asullom@gmail.com)



-------
Contributors
-------

See https://github.com/practian-ioteca-project/catalogo_service/graphs/contributors

.. _github: https://github.com/practian-ioteca-project/catalogo_service
.. _Django: https://www.djangoproject.com
.. _Django REST Framework: http://www.django-rest-framework.org
.. _Django OAuth Toolkit: https://django-oauth-toolkit.readthedocs.io
.. _Django OAuth2 Backend: https://github.com/practian-reapps/django-oauth2-backend
.. _Django Backend Utils: https://github.com/practian-reapps/django-backend-utils
.. _Authorization server: https://github.com/practian-ioteca-project/oauth2_backend_service







