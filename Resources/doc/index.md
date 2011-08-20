OryzoneBoilerplateBundle Documentation
======================================
Hello folks, with OryzoneBoilerplateBundle you can easily create heavily optimized HTML5 twig templates empowered with great features such as CSS resets, CDNed jquery (with offline fallback), asynchronous google analytics script and so on.

Have you ever wondered where to start to create an HTML5 web site by using Symfony2? Yes?! Well, you came in the right place! Let's go on! ;)

If you haven't ever experienced [twig][twig] and its inheritance system I heavily encourage you to [dig further](http://www.twig-project.org/doc/templates.html) before starting out with this bundle.

Installation
------------
The installation process is really straightforward. It follows the Symfony2 bundle setup conventions, so if you ever installed any other bundle it will pretty easy for you to proceed. Otherwise, if this is the first time you try to install a bundle, don't be scared! We promise you will succeed at the first try!

You've to follow only few steps (Scared? You need just 3 steps!)

  1. Download OryzoneBoilerplateBundle
  2. Configure the Autoloader
  3. Enable the Bundle
  4. (optional) Configure google analytics

### Step 1. Download OryzoneBoilerplateBundle ###
Ultimately, the OryzoneBoilerplateBundle files should be downloaded to the `vendor/bundles/Oryzone/BoilerplateBundle` directory.

This can be done at least in two different ways, depending on your preference: by using the symfony vendor script or by using git modules.
The first method is the standard Symfony2 method.

#### Using the vendors script ####
Add the following lines in your deps file:

    [OryzoneBoilerplateBundle]
        git=git://github.com/Oryzone/OryzoneBoilerplateBundle.git
        target=/bundles/Oryzone/BoilerplateBundle

Now, run the vendors script to download the bundle:

    $ php bin/vendors install

#### Using submodules ####
instead, if you prefer using git submodules, just proceed by running the following git commands:

    $ git submodule add git://github.com/Oryzone/OryzoneBoilerplateBundle.git vendor/bundles/Oryzone/BoilerplateBundle
    $ git submodule update --init

### Step 2. Configure the Autoloader ###

Add the Oryzone namespace to your autoloader:

    <?php
    // app/autoload.php
    
    $loader->registerNamespaces( array(
        // ...
        'Oryzone' => __DIR__.'/../vendor/bundles',
    ));

### Step 3. Enable the Bundle ###
Finally, enable the bundle in the kernel:

    <?php
    // app/AppKernel.php
    
    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Oryzone\BoilerplateBundle\OryzoneBoilerplateBundle(),
        );
    }

### Step 4 (optional). Configure Google Analytics ###
Google analytics is disabled by default. You can easily enable it by passing your analytics id within the variable "bp_analytics_id".
Anyway I suggest you to set this variable directly in your configuration file among the twig global variables. This way you have the opportunity to specify an id on the environments you prefer to: for example you may want to not use analytics on development but to use it in production, so just add the following lines on your `config_prod.yml` file

    twig:
        globals:
            bp_analytics_id: UAXXXXXXXX1

Create your own mighty templates as extensions
----------------------------------------------
Now comes the most enjoying part, you've successfully installed the bundle and you're ready to go. Everything starts with a twig template. If you want to create a new HTML5 powered template you've only to extend the `OryzoneBoilerplateBundle::html5.html.twig` template. So you need to put the following line at the beginning of yout template:

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}

By doing so your template had inherited the base HTML5 structure proposed by the HTML5 Boilerplate. You'll have only to declare the content of the various blocks proposed by the template you're extending. A complete list of all the blocks will be described later. Let's see a quick and clear sample to make you hunger.

Quick demo
------------
With the following code we created a simple template for an index page. As you will see we have only extended the basic HTML5 template and redeclared the content of some blocks. The example is merely trivial if you know [twig][twig] a bit.

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}
    
	{% block head_title %}My cool HTML5 website{% endblock %}
    {% block body_header %}<h1>My HTML5 home page is very cool</h1>{% endblock %}
    {% block body_main %}<p>This is the home page of my wild web site!</p>{% endblock %}
	{% block body_footer %}Here we go with copyright infos{% endblock %}

Available blocks
----------------
The basic template structure is made of nested blocks. This template proposes a default structure, so you have to rewrite only the blocks you really need to modify (or populate). Generally, as shown in the quick demo, you'll rewrite only few of them like `head_title` and the `body_main`. The template has been tought to be flexible enough to handle most of the cases. However, if you wish to apply deep modification to the whole structure you can totally rewrite higher level blocks like `head` or `body`.
Follows a representation of the blocks tree. Note that every block name is prefixed with the name of his ancestor blocks.

  * <strong>head</strong>
    * <strong>head\_meta</strong>
       * <strong>head\_meta\_description</strong>
       * <strong>head\_meta\_keywords</strong>
       * <strong>head\_meta\_author</strong>
    * <strong>head\_title</strong>
    * <strong>head\_css</strong>: Contains a reference to the basic css reset
    * <strong>head\_js</strong>: adds modernizr script. All the other script should be added inside the <strong>body\_js</strong> block
  * <strong>body</strong>
    * <strong>body\_header</strong>
    * <strong>body\_main</strong>
    * <strong>body\_footer</strong>
    * <strong>body\_js</strong>: to handle js at the end of the page
      * <strong>body\_js\_jquery</strong>: handles jquery 1.6.2 (from google CDN with local fallback if offline)
        * <strong>body\_js\_jquery\_onlineSrc</strong>: allows you to change the url of the cdn hosted script
        * <strong>body\_js\_jquery\_offlineSrc</strong>: allows you to change the path of the local jQuery script
      * <strong>body\_js\_analytics</strong>: handles google analytics script
      * <strong>body\_js\_chromeframe</strong>: handles google chrome frame for internet explorer

Available variables
-------------------
The template uses some variables that you can optionally redefine to customize its behaviour. Here's the complete list:

  * <strong>bp_language</strong>: allows you to set the language of your html file. ("en" by default)
  * <strong>bp_analytics_id</strong>: allows you to specify your google analytics id. If you don't provide a value for this variable the whole Google analytics script won't be added on the resulting page.

Two different approaches: overwrite and extend
----------------------------------------------
If you're alredy experienced with twig this paragraph would be pointless, so feel free to skip it on if you are confortable with twig inheritance based paradigm.

Basically there are two ways to deal with a block: by complete overwriting the content of its parent block or by reusing and extending it.

For example suppose you don't want to use the default css reset included in the basic parent template and want to use your own stylesheet files. In this case you have to rewrite the whole `head_css` block. So would have something like that:

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}
    
	{% block head_css %}
		<link rel="stylesheet" href="myWonderful.css">
		<link rel="stylesheet" href="someMoreBeautiful.css">
	{% endblock %}
    
    {# ... #}

You can use the overwrite even to "remove" an entire block. E.g. suppose you want no stylesheet, you can just create an empty `head_css` blocks:

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}
    
	{% block head_css %}{% endblock %}
    
    {# ... #}

This would be pretty useful even if, for example, you want to remove a default feature. Suppose you don't want to use jQuery. It's quite simple:

    {% block body_js_jquery %}{% endblock %}

Instead if you want to add some more stylesheet to the default one you can use the special twig function `parent()` that gets the content of the block from the parent template.

	{% extends "OryzoneBoilerplateBundle::html5.html.twig" %}
    
	{% block head_css %}
	    {{ parent() }}
		<link rel="stylesheet" href="myWonderful.css">
		<link rel="stylesheet" href="someMoreBeautiful.css">
	{% endblock %}
    
    {# ... #}

Note that if you overwrite an higher level block as `head` you'll automatically overwrite all it's nested blocks as `head_title` and `head_css`. This makes twig pretty flexible because you have the full control of everything you wish to change or extend. Blocks can be considered just as starting points or suggestions on which you can build upon.

Setting the page language
-------------------------
If you want to redefine the `lang` attribute of the `html` tag you just only have to define the `bp_language` variable from your controller.
If you want your templates to reflect your global locale configuration you can provide a global value for bp_language by doing this way:

    # Twig Configuration
    twig:
        globals:
            bp_language: %locale%

Is that all?
------------
Yes. This should be quite enough to get you started. Anyway if you are still in trouble or if you have any question feel free to contact us at [ORYZONE](http://oryzone.com).

[twig]: http://www.twig-project.org/ "The TWIG project home page"