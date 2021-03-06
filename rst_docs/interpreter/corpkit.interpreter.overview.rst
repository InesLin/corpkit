.. _interpreter-page:

Overview
=======================

*corpkit* comes with a dedicated interpreter, which receives commands in a natural language syntax like these:

.. code-block:: bash

   > set mydata as corpus
   > search corpus for pos matching 'JJ.*'
   > call result 'adjectives'
   > edit adjectives by skipping subcorpora matching 'books'
   > plot edited as line chart with title as 'Adjectives'

It's a little less powerful than the full Python API, but it is easier to use, especially if you don't know Python. You can also switch instantly from the interpreter to the full API, so you only need the API for the really tricky stuff.

The syntax of the interpreter is based around *objects*, which you do things to, and *commands*, which are actions performed upon the objects. The example below uses the `search` command on a `corpus` object, which produces new objects, called `result`, `concordance`, `totals` and `query`. As you can see, very complex searches can be performed using an English-like syntax:

.. code-block:: bash

   > search corpus for lemma matching '^t' and pos matching 'VB' \
   ...     excluding words matching 'try' \
   ...     showing word and dependent-word \
   ...     with preserve_case
   > result

This shows us results for each subcorpus:

.. code-block:: none

   .         I/think  I/thought  and/turned  me/told  and/took  I/told   ...
   chapter1        5          3           2        2         1       3   ...
   chapter2        7          2           5        3         0       2   ...
   chapter3        5          5           4        4         1       0   ...
   chapter4        3          7           1        0         3       1   ...
   chapter5        7          7           2        1         4       2   ...
   chapter6        2          0           0        2         1       0   ...
   chapter7        6          2           6        1         1       3   ...
   chapter8        3          1           2        2         1       1   ...
   chapter9        5          7           1        4         6       3   ...


Objects
---------

The most common objects you'll be using are:

+---------------+-----------------------------------------------+
| Object        | Contains                                      |
+===============+===============================================+
| `corpus`      | Dataset selected for parsing or searching     |
+---------------+-----------------------------------------------+
| `result`      | Search output                                 |
+---------------+-----------------------------------------------+
| `edited`      | Results after sorting, editing or calculating |
+---------------+-----------------------------------------------+
| `concordance` | Concordance lines from search                 |
+---------------+-----------------------------------------------+
| `features`    | General linguistic features of corpus         |
+---------------+-----------------------------------------------+
| `wordclasses` | Distribution of word classes in corpus        |
+---------------+-----------------------------------------------+
| `postags`     | Distribution of POS tags in corpus            |
+---------------+-----------------------------------------------+
| `lexicon`     | Distribution of lexis in the corpus           |
+---------------+-----------------------------------------------+
| `figure`      | Plotted data                                  |
+---------------+-----------------------------------------------+
| `query`       | Values used to perform search or edit         |
+---------------+-----------------------------------------------+
| `previous`    | Object created before last                    |
+---------------+-----------------------------------------------+
| `sampled`     | A sampled corpus                              |
+---------------+-----------------------------------------------+
| `wordlists`   | A list of wordlists for searching, editing    |
+---------------+-----------------------------------------------+

When you start the interpreter, these are all empty. You'll need to run commands in order to fill them with data. You can also create your own object names using the ``call`` command.

Commands 
-----------

You do things to the objects via commands. Each command has its own syntax, designed to be as similar to natural language as possible. Below is a table of common commands, an explanation of their purpose, and an example of their syntax

+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| Command         | Purpose                                                      | Syntax                                                                                     |
+=================+==============================================================+============================================================================================+
| `new`           | Make a new project                                           | `new project <name>`                                                                       |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `set`           | Set current corpus                                           | `set <corpusname>`                                                                         |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `parse`         | Parse corpus                                                 | `parse corpus with [options]*`                                                             |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `search`        | Search a corpus for linguistic feature, generate concordance | `search corpus for [feature matching pattern]* showing [feature]* with [options]*`         |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `edit`          | Edit results or edited results                               | `edit result by [skipping subcorpora/entries matching pattern]* with [options]*`           |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `calculate`     | Calculate relative frequencies, keyness, etc.                | `calculate result/edited as operation of denominator`                                      |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `sort`          | Sort results or concordance                                  | `sort result/concordance by value`                                                         |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `plot`          | Visualise result or edited result                            | `plot result/edited as line chart with [options]*`                                         |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `show`          | Show any object                                              | `show object`                                                                              |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `annotate`      | Add annotations to corpus based on search results            | `annotate all with field as <fieldname> and value as m`                                    |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `unannotate`    | Delete annotation fields from corpus                         | `unannotate <fieldname> field`                                                             |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `sample`        | Get a random sample of subcorpora or files from a corpus     | `sample 5 subcorpora of corpus`                                                            |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `call`          | Name an object (i.e. make a variable)                        | `call object '<name>'`                                                                     |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `export`        | Export result, edited result or concordance to string/file   | `export result to string/csv/latex/file <filename>`                                        |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `save`          | Save data to disk                                            | `save object to <filename>`                                                                |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `load`          | Load data from disk                                          | `load object as result`                                                                    |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `store`         | Store something in memory                                    | `store object as <name>`                                                                   |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `fetch`         | Fetch something from memory                                  | `fetch <name> as object`                                                                   |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `help`          | Get help on an object or command                             | `help command/object`                                                                      |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `history`       | See previously entered commands                              | `history`                                                                                  |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `ipython`       | Enter IPython with objects available                         | `ipython`                                                                                  |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `py`            | Execute Python code                                          | `py 'print("hello world")'`                                                                |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+
| `!`             | Run a line of bash shell                                     | `!ls -al data`                                                                             |
+-----------------+--------------------------------------------------------------+--------------------------------------------------------------------------------------------+

In square brackets with asterisks are recursive parts of the syntax, which often also accept `not` operators. `<text>` denotes places where you can choose an identifier, filename, etc.

In the pages that follow, the syntax is provided for the most common commands. You can also type the name of the command with no arguments into the interpreter, in order to show usage examples.

Prompt features
-------------------

* You can use `history`, `clear`, `ls` and `cd` commands as you would in the shell
* You can execute arbitrary bash commands by beginning the line with an exclamation point (e.g. ``!rm data/*``)
* You can use semicolons to put multiple commands on a line (currently needs a space **before and after** the semicolon)
* There is no piping or output redirection (yet), but you can use the `export` and `save` commands to export results
* You can use backslashes to continue writing on the next line
* You can write scripts and pass them to the *corpkit* interpreter

The below is therefore a possible (but terrible) way to write code in *corpkit*:

.. code-block:: bash

   > !du -h data ; set mycorp ; search corpus for words \
   ... matching any \
   ... excluding wordlists.closedclass \
   ... showing lemma and pos ; concordance
