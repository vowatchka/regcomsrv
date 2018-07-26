.. meta::
	:description: Всегда выполняйте регистрацию или отмену регистрации COM серверов с правами администратора.
	:keywords: COM сервер регистрация отмена права администратор выполнить

.. _admin-mode:

Регистрация COM сервера с правами администратора
================================================
Если вы заметили, то в разделе :ref:`reg-com-server-py` в окне интерпретатора Python выводилось следующее::

	>>> 
	================ RESTART: C:\Users\VSaltykov\Desktop\test.py ================
	Registering COM servers Python.Dictionary from module win32com.servers.dictionary...
	Requesting elevation and retrying...
	Registering COM servers Python.Dictionary from module win32com.servers.dictionary...
	Registered: Python.Dictionary 
	
	>>> 
	
При регистрации через командную строку на консоль выводилось:

.. figure:: _static/register-python-dictionary.png
	:scale: 100%
	:alt: Регистрация COM сервера Python.Dictionary
	:align: center
	
	Регистрация COM сервера Python.Dictionary
	
Видите разницу? При регистрации COM сервера через скрипт Python в окне интерпретатора присутствует строчка ``Requesting elevation and retrying...``, которой нет на консоли, а также дважды повторяется строка::

	Registering COM servers Python.Dictionary from module win32com.servers.dictionary...
	
Если вы не являетесь администратором на компьютере, где хотите зарегистрировать COM сервер, или там включен **Контроль учетных записей пользователя**, то вы всегда будете видеть строку ``Requesting elevation and retrying...``, и не важно как вы регистрируете COM сервер: через командную строку или нет.

Если в кратце, то модуль Python, выполняющий регистрацию (см. подробнее в ``win32com.server.register``), пытается зарегистрировать COM сервер, но видит, что для этого нужны права администратора. Тогда модуль Python, выполняющий регистрацию COM сервера, запрашивает эти данные и повторяет попытку, выполняя ваш скрипт Python заново. Поэтому при регистрации COM сервера через скрипт Python в окне интерпретатора дублировалась строка::

	Registering COM servers Python.Dictionary from module win32com.servers.dictionary...
	
С консолью все обстаяло иначе, потому что командная строка запускалась с правами администратора.

Все сказанное выше справедливо и для отмены регистрации COM серверов.

Как итог, **всегда выполняйте регистрацию и отмену регистрации COM серверов с правами администратора**.