.. meta::
	:description: Пакет regcomsrv предоставляет функцию, читающую параметры командной строки и выполняющую регистрацию COM серверов.
	:keywords: regcomsrv пакет регистрация COM сервер объект командная строка функция отмена

.. _reg-with-python:

Регистрация COM серверов с помошью Python
=========================================
Используя пакет ``regcomsrv``, вы можете регистрировать и отменять регистрацию COM серверов, задавая необходимые параметры командной строки прямо в скрипте Python.


.. _function-reg:

Функция reg
-----------
Пакет ``regcomsrv`` предоставляет функцию, читающую параметры командной строки и выполняющую регистрацию COM серверов.

.. py:function:: reg()

	Функция читает параметры командной строки и выполняет регистрацию COM серверов.
	
	:return: Функция не возврацает данных.
	:rtype: ``None``
	
Подробнее о доступных параметрах коммандной строки см. :ref:`reg-with-command-line`.


.. _reg-com-server-py:

Регистрация COM сервера
-----------------------
Чтобы зарегистрировать COM сервер, создайте скрипт ``*.py``, добавьте в него следующий код и выполните:

.. code-block:: python

	from regcomsrv import reg
	import sys
	
	# set command line attributes
	sys.argv.clear()
	sys.argv.append(__file__)
	sys.argv.append("win32com.servers.dictionary")
	sys.argv.append("DictionaryPolicy")
	
	reg()
	
В окне интерпретатора вы увидите, что COM сервер был успешно зарегистрирован::

	>>> 
	================ RESTART: C:\Users\VSaltykov\Desktop\test.py ================
	Registering COM servers Python.Dictionary from module win32com.servers.dictionary...
	Requesting elevation and retrying...
	Registering COM servers Python.Dictionary from module win32com.servers.dictionary...
	Registered: Python.Dictionary 
	
	>>> 
	
	
.. _unreg-com-server-py:

Отмена регистрации COM сервера
------------------------------
Чтобы отменить регистрацию COM сервера, создайте скрипт ``*.py``, добавьте в него следующий код и выполните:

.. code-block:: python

	from regcomsrv import reg
	import sys
	
	# set command line attributes
	sys.argv.clear()
	sys.argv.append(__file__)
	sys.argv.append("win32com.servers.dictionary")
	sys.argv.append("DictionaryPolicy")
	sys.argv.append("--unregister")
	
	reg()
	
В окне интерпретатора вы увидите, что отмена регистрации COM сервера была успешно выполнена::

	>>> 
	================ RESTART: C:\Users\VSaltykov\Desktop\test.py ================
	Unregistering COM servers Python.Dictionary from module win32com.servers.dictionary...
	Requesting elevation and retrying...
	Unregistering COM servers Python.Dictionary from module win32com.servers.dictionary...
	Unregistered: Python.Dictionary
	
	>>> 