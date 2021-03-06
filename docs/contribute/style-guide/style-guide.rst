ASP.NET Docs Style Guide
========================
By `Steve Smith`_ | Originally Published: 15 April 2015 

.. _`Steve Smith`: Author_

This document provides an overview of how articles published on `docs.asp.net <http://docs.asp.net>`_ should be formatted. You can actually use this file, itself, as a template when contributing articles.

This article covers the following topics:
	- Article Structure
	- ReStructuredText Syntax
	- Additional Reading

Article Structure
^^^^^^^^^^^^^^^^^

Articles should be submitted as individual text files with a **.rst** extension. Authors should be sure they are familiar with the `Sphinx Style Guide <http://documentation-style-guide-sphinx.readthedocs.org/en/latest/style-guide.html>`_, but where there are disagreements, this document takes precedence. The article should begin with its title on line 1, followed by a line of === characters. Next, the author and publication date should be displayed. The author name appears in 3 places in an article document: line 3, line 5 (an alias to the Author_ target), and on the very last line, where the appropriate author.rst file is included (e.g. steve-smith.rst).

Articles should typically begin with a brief abstract describing what will be covered, followed by a bulleted list of topics, if appropriate. If the article has associated sample files, a link to the samples should be included following this bulleted list. 

Articles should typically include a Summary section at the end, and optionally additional sections like Next Steps or Additional Resources. These should not be included in the bulleted list of topics, however.

Headings
--------

Typically articles will use at most 3 levels of headings. The title of the document is the highest level heading and must appear on lines 1-2 of the document. The title is designated by a row of === characters.

Section headings should correspond to the bulleted list of topics set out after the article abstract. `Article Structure`, above, is an example of a section heading. A section heading should appear on its own line, followed by a line consisting of ^^^ characters.

Subsection headings can be used to organize content within a section. `Headings`, above, is an example of a subsection heading. A subsection heading should appear on its own line, followed by a line of --- characters.

For section headings, only the first word should be capitalized:
- This heading follow the style
- This Heading Does Note



ReStructuredText Syntax
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following ReStructuredText elements are commonly used in ASP.NET documentation articles. Note that **indentation and blank lines are significant!**

Inline Markup
-------------

Surround text with:

- One asterisk for \*emphasis\* (*italics*)
- Two asterisks for \**strong emphasis\** (**bold**)
- Two backticks for \``code samples``\ (an ``<html>`` element)

..note:: Inline markup cannot be nested, nor can surrounded content start or end with whitespace (``* foo*`` is wrong).

Escaping is done using the ``\`` backslash.

Format specific items using these rules:

- *Italics* (surround with \*)
	- Files, folders, paths (for long items, split onto their own line)
	- New terms
	- URLs (unless rendered as links, which is the default)
- **Strong** (surround with \**)
	- UI elements
- ``Code Elements`` (surround with \``)
	- Classes and members
	- Command-line commands
	- Database table and column names
	- Language keywords

Links
-----

Inline hyperlinks are formatted like this:

.. code-block:: rst

	Learn more about `ASP.NET <http://www.asp.net>`_.
	
Learn more about `ASP.NET <http://www.asp.net>`_.
	
Surround the link text with backticks. Within the backticks, place the target in angle brackets, and ensure there is a space between the end of the link text and the opening angle bracket. Follow the closing backtick with an underscore.

In addition to URLs, documents and document sections can also be linked by name:

.. code-block:: rst

	For example, here is a link to the `Inline Markup`_ section, above.
	
For example, here is a link to the `Inline Markup`_ section, above.

Any element that is rendered as a link should not have any additional formatting or styling.

Lists
-----

Lists can be started with a ``-`` or ``*`` character:

.. code-block:: rst

	- This is one item
	- This is a second item

Numbered lists can start with a number, or they can be autonumbered by starting each item with the \# character.

.. code-block:: rst

	1. Numbered list item one.
	2. Numbered list item two.

	#. Auto-numbered one.
	#. Auto-numbered two.

Source Code
-----------

Of course, source code is very commonly included in these articles. Images should never be used to display source code - instead use ``code-block`` or ``literalinclude``. You can refer to it using the ``code-block`` element, which must be declared precisely as shown, including spaces, blank lines, and indentation:

.. code-block:: rst

	.. code-block:: c#
	
	public void Foo()
	{
		// Foo all the things!
	}

This results in:

.. code-block:: c#

	public void Foo()
	{
		// Foo all the things!
	}

The code block ends when you begin a new paragraph without indentation. `Sphinx supports quite a few different languages <http://pygments.org/docs/lexers/>`_. Some common language strings that are available include:

- ``c#``
- ``javascript``
- ``html``

.. _Captions: 

Code blocks also support line numbers and emphasizing or highlighting certain lines, as well as captions and names. Captions are displayed, names can be used as link targets (e.g. `Foo Method`_):

.. code-block:: rst

	.. code-block:: c#
	   :linenos:
	   :emphasize-lines: 3
	   :caption: The Foo() method
	   :name: Foo Method
	
	public void Foo()
	{
		// Foo all the things!
	}

This results in:

.. code-block:: c#
   :linenos:
   :emphasize-lines: 3
   :caption: The Foo() method
   :name: Foo Method

	public void Foo()
	{
		// Foo all the things!
	}


Images
------

Images such as screen shots and explanatory figures or diagrams should be placed in a ``_static`` folder at the same level as the article file. References to images should therefore always be made using relative references, e.g. ``_static/asp-net.png``. Note that images should always be saved as all lower-case file names, using hyphens to separate words, if necessary.

.. note:: Do not use images for code. Use ``code-block`` or ``literalinclude`` instead.

To include an image in an article, use the ``.. image`` directive:

.. code-block:: rst

	.. image:: _static/asp-net.png
	
.. note:: No quotes are needed around the file name.

Here's an example using the above syntax:

.. image:: _static/asp-net.png

Images are responsively sized according to the browser viewport when using this directive. Currently the maximum width supported by the http://docs.asp.net theme is 697px.

Notes
-----

To add a note callout, like the ones shown in this document, use the ``.. note::`` directive.

.. code-block:: rst

	.. note:: This is a note.
	
This results in:

.. note:: This is a note.

Including External Source Files
-------------------------------

One nice feature of ReStructuredText is its ability to reference external files. This allows actual sample source files to be referenced from documentation articles, reducing the chances of the documentation content getting out of sync with the actual, working code sample (assuming the code sample works, of course). However, if documentation articles are referencing samples by filename and line number, it is important that the documentation articles be reviewed whenever changes are made to the source code, otherwise these references may be broken or point to the wrong line number. For this reason, it is recommended that samples be specific to individual articles, so that updates to the sample will only affect a single article (at most, an article series could reference a common sample). Samples should be committed to ``/aspnet/docs/samples/`` in a folder named to correspond with the article referencing the sample.

External file references can specify a language, emphasize certain lines, display line numbers (recommended), similar to `Source Code`_. Remember that these line number references may need to be updated if the source file is changed.

.. code-block:: rst

	.. literalinclude:: _static/startup.cs
		:language: c#
		:emphasize-lines: 19,25-27
		:linenos:

.. literalinclude:: _static/startup.cs
	:language: c#
	:emphasize-lines: 19,25-27
	:linenos:

You can also include just a section of a larger file, if desired:

.. code-block:: rst
   :emphasize-lines: 3

	.. literalinclude:: _static/startup.cs
		:language: c#
		:lines: 1,4,20-
		:linenos:

This would include the first and fourth line, and then line 20 through the end of the file.

Literal includes also support `Captions`_ and names, as with ``code-block`` elements. If the ``caption`` is left blank, the file name will be used as the caption.

Tables
------

Tables can be constructed using grid-like "ASCII Art" style text. In general they should only be used where it makes sense to present some tabular data. Rather than include all of the syntax options here, you will find a detailed reference at `<http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#grid-tables>`_.

UI navigation
-------------

When documenting how a user should navigate a series of menus, use the ``:menuselection:`` directive:

.. code-block:: rst

	:menuselection:`Windows --> Views --> Other...`
	
This will result in :menuselection:`Windows --> Views --> Other...`.

Additional Reading
^^^^^^^^^^^^^^^^^^

Learn more about Sphinx and ReStructuredText:
	- `Sphinx documentation <http://sphinx-doc.org/contents.html>`_
	- `RST Quick Reference <http://docutils.sourceforge.net/docs/user/rst/quickref.html>`_


Summary
^^^^^^^

This style guide is intended to help contributors quickly create new articles for `docs.asp.net <http://docs.asp.net>`_. It includes the most common RST syntax elements that are used, as well as overall document organization guidance. If you discover mistakes or gaps in this guide, please `submit an issue <https://github.com/aspnet/docs/issues>`_.

.. include:: /_authors/steve-smith.rst
