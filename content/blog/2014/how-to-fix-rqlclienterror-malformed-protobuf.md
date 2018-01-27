+++
date = "2014-09-28 18:54:00"
title = "How to fix \"RqlClientError: MALFORMED PROTOBUF\""
draft = "false"
categories = ["Technology"]
author = "edavis215"
original_url = "https://ttboj.wordpress.com/2014/09/28/how-to-fix-rqlclienterror-malformed-protobuf/"
+++


<p> If you encounter a <code>RqlClientError: MALFORMED PROTOBUF</code> exception (example below) when using RethinkDB's Python driver, it's because the server version and driver version don't match. </p>

<p> Sync the versions up and everything should start working. </p>

[sourcecode language="python" title=""]
&gt;&gt;&gt; r.db('test').table('authors').filter(r.row['name'] == 'William Adama').run()
Traceback (most recent call last):
  File &quot;&lt;stdin&gt;&quot;, line 1, in &lt;module&gt;
  File &quot;/Users/eric/virtualenvs/river/lib/python2.7/site-packages/rethinkdb/ast.py&quot;, line 95, in run
    return c._start(self, **global_optargs)
  File &quot;/Users/eric/virtualenvs/river/lib/python2.7/site-packages/rethinkdb/net.py&quot;, line 238, in _start
    return self._send_query(query, global_optargs)
  File &quot;/Users/eric/virtualenvs/river/lib/python2.7/site-packages/rethinkdb/net.py&quot;, line 339, in _send_query
    self._check_error_response(response, query.term)
  File &quot;/Users/eric/virtualenvs/river/lib/python2.7/site-packages/rethinkdb/net.py&quot;, line 320, in _check_error_response
    raise RqlClientError(message, term, frames)
rethinkdb.errors.RqlClientError: RqlClientError: MALFORMED PROTOBUF (Illegal Term type 170). in:
r.db('test').table('authors').filter(lambda var_2: (r.row['name'] == r.expr('William Adama')))
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
[/sourcecode]

<p> Happy hacking! </p>


