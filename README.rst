==================
python-duckduckgo
==================

A Python 3 library for querying the DuckDuckGo API.

Copyright Michael Stephens <me@mikej.st>, released under a BSD-style license.

Source: http://github.com/crazedpsyc/python-duckduckgo
Original source: http://github.com/mikejs/python-duckduckgo (outdated)

This version has been forked from the modified to support python 3 using the requests library.
All functionality stays the same.

Installation
============

To install run

    ``python setup.py install``

Usage
=====

    >>> import duckduckgo
    >>> r = duckduckgo.query('DuckDuckGo')
    >>> r.type
    'answer'
    >>> r.results[0].text
    'Official site'
    >>> r.results[0].url
    'http://duckduckgo.com/'
    >>> r.abstract.url
    'http://en.wikipedia.org/wiki/Duck_Duck_Go'
    >>> r.abstract.source
    'Wikipedia'
    
    >>> r = duckduckgo.query('Python')
    >>> r.type
    'disambiguation'
    >>> r.related[1].text
    'Python (programming language), a computer programming language'
    >>> r.related[1].url
    'http://duckduckgo.com/Python_(programming_language)'
    >>> r.related[7].topics[0].text # weird, but this is how the DDG API is currently organized
    'Armstrong Siddeley Python, an early turboprop engine'


    >>> r = duckduckgo.query('1 + 1')
    >>> r.type
    'nothing'
    >>> r.answer.text
    '1 + 1 = 2'
    >>> r.answer.type
    'calc'

    >>> print duckduckgo.query('19301', kad='es_ES').answer.text
    19301 es un código postal de Paoli, PA
    >>> print duckduckgo.query('how to spell test', html=True).answer.text
    <b>Test</b> appears to be spelled right!<br/><i>Suggestions: </i>test, testy, teat, tests, rest, yest.

The easiest method of quickly grabbing the best (hopefully) API result is to use duckduckgo.get_zci::
    >>> print duckduckgo.get_zci('foo')
    The terms foobar /ˈfʊːbɑːr/, fubar, or foo, bar, baz and qux are sometimes used as placeholder names in computer programming or computer-related documentation. (https://en.wikipedia.org/wiki/Foobar)
    >>> print ddg.get_zci('foo fighters site')
    http://www.foofighters.com/us/home

Special keyword args for query():
 - useragent   - string, The useragent used to make API calls. This is somewhat irrelevant, as they are not logged or used on DuckDuckGo, but it is retained for backwards compatibility.
 - safesearch  - boolean, enable or disable safesearch.
 - html        - boolean, Allow HTML in responses?

