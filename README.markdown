OryzoneBoilerplateBundle
========================
The OryzoneBoilerplateBundle allows you to use a twig template based on the great [HTML5 ★ Boilerplate](http://html5boilerplate.com/) 4.* by [Paul Irish](http://paulirish.com/), [Divya Manian](http://nimbupani.com/) and many other great guys.
So with this bundle you can easily create heavily optimized HTML5 twig templates empowered with great features such as CSS resets, CDNed jQuery (with offline fallback), asynchronous google analytics script and so on.

A little appetizer
------------------
Once you've added OryzoneBoilerplateBundle to your project it will be truly damn easy for you to produce an HTML5 enabled template. Here's a quick a fresh served appetizer to disclose what are you going to taste by using this bundle.

    {# yourMainBundle/Resources/views/Default/index.html.twig #}

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}

	{% block head_title %}My cool HTML5 website{% endblock %}
    {% block body_container_header %}<h1>My HTML5 home page is very cool</h1>{% endblock %}
    {% block body_container_main %}<p>This is the home page of my wild web site!</p>{% endblock %}
	{% block body_container_footer %}Here we go with copyright infos{% endblock %}

Documentation
-------------
The bulk of the documentation is stored in the [Resources/doc/index.md][documentation] file in this bundle.

Installation
------------
All the installation instructions are located in [documentation][documentation].

License
-------
This bundle is under the MIT license. See the complete [license][license] in the bundle: `Resources/meta/LICENSE`

This bundle includes parts of HTML5 ★ Boilerplate under the MIT license. See the complete [license][h5bp.license] in the bundle: `Resources/meta/H5BP.LICENSE`

About
-----
OryzoneBoilerplateBundle is an [ORYZONE][oryzone] initiative.

Reporting an issue or a feature request
---------------------------------------
Issues and feature requests are tracked in the [Github issue tracker](https://github.com/Oryzone/OryzoneBoilerplateBundle/issues).

When reporting a bug, it may be a good idea to reproduce it in a basic project built using the Symfony Standard Edition to allow developers of the bundle to reproduce the issue by simply cloning it and following some steps.

[documentation]: Resources/doc/index.md  "Extended bundle documentation"

[license]: https://github.com/Oryzone/OryzoneBoilerplateBundle/blob/master/Resources/meta/LICENSE "MIT license"

[h5bp.license]: https://github.com/Oryzone/OryzoneBoilerplateBundle/blob/master/Resources/meta/H5BP.LICENSE "HTML5 ★ Boilerplate MIT license"

[oryzone]: http://oryzone.com "ORYZONE web site"
