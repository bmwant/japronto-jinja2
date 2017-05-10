## japronto_jinja2

.. image:: https://travis-ci.org/aio-libs/aiohttp-jinja2.svg?branch=master
    :target: https://travis-ci.org/aio-libs/aiohttp-jinja2
.. image:: https://codecov.io/gh/aio-libs/aiohttp-jinja2/branch/master/graph/badge.svg
    :target: https://codecov.io/gh/aio-libs/aiohttp-jinja2
.. image:: https://img.shields.io/pypi/v/aiohttp-jinja2.svg
    :target: https://pypi.python.org/pypi/aiohttp-jinja2
.. image:: https://readthedocs.org/projects/aiohttp-jinja2/badge/?version=latest
    :target: http://aiohttp-jinja2.readthedocs.io/en/latest/?badge=latest


jinja2_ template renderer for `aiohttp.web`__.


.. _jinja2: http://jinja.pocoo.org

.. _aiohttp_web: https://aiohttp.readthedocs.io/en/latest/web.html

__ aiohttp_web_

### Installation

Install from PyPI:
```
pip install japronto-jinja2
```

### Developing

Install requirement and launch tests:
```
pip install -e .[dev]
pytest
```

### Usage

Before template rendering you have to setup *jinja2 environment* first::

    app = web.Application()
    aiohttp_jinja2.setup(app,
        loader=jinja2.FileSystemLoader('/path/to/templates/folder'))


After that you may to use template engine in your *web-handlers*. The
most convenient way is to decorate a *web-handler*.

Using the function based web handlers::

    @aiohttp_jinja2.template('tmpl.jinja2')
    def handler(request):
        return {'name': 'Andrew', 'surname': 'Svetlov'}



On handler call the ``aiohttp_jinja2.template`` decorator will pass
returned dictionary ``{'name': 'Andrew', 'surname': 'Svetlov'}`` into
template named ``tmpl.jinja2`` for getting resulting HTML text.

If you need more complex processing (set response headers for example)
you may call ``render_template`` function.

Using a function based web handler::

    async def handler(request):
        context = {'name': 'Andrew', 'surname': 'Svetlov'}
        response = aiohttp_jinja2.render_template('tmpl.jinja2',
                                                  request,
                                                  context)
        response.headers['Content-Language'] = 'ru'
        return response

### License

`japronto_jinja2` is offered under the Apache 2 license.
