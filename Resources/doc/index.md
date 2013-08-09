OryzoneBoilerplateBundle Documentation
======================================
Hello folks, with OryzoneBoilerplateBundle you can easily create heavily optimized HTML5 Twig templates empowered with great features such as CSS resets, CDNed jQuery (with offline fallback), asynchronous google analytics script and so on.

Have you ever wondered where to start to create an HTML5 web site by using Symfony2? Yes?! Well, you came in the right place! Let's go on! ;)

If you haven't ever experienced [Twig][twig] and its inheritance system I heavily encourage you to [dig further](http://www.twig-project.org/doc/templates.html) before starting out with this bundle.

<a name="toc"></a>
## Table of contents

  * [Installation](#installation)
    * [Step 1. Download OryzoneBoilerplateBundle](#installation-step1)
      * [If you are using Symfony 2.0](#installation-step1a)
        * [Using the vendors script](#installation-step1a1)
        * [Using submodules](#installation-step1a2)
      * [If you are using Symfony 2.1](#installation-step1b)
        * [Using composer script](#installation-step1b1)
        * [Using submodules](#installation-step1b2)
    * [Step 2. Configure the Autoloader](#installation-step2)
    * [Step 3. Enable the Bundle](#installation-step3)
    * [Step 4. Configure Assetic](#installation-step4)
  * [Create your own mighty templates as extensions](#create-your-own-mighty-templates-as-extensions)
  * [Quick demo](#quick-demo)
  * [Available blocks](#available-blocks)
  * [Available variables](#available-variables)
  * [Two different approaches: overwrite and extend](#two-different-approaches)
  * [Configure Google Analytics](#configure-google-analytics)
  * [Setting the page language](#setting-the-page-language)
  * [Adding classes to the html tag](#adding-classes-to-the-html-tag)
  * [Is this all?](#is-this-all)

<a name="installation"></a>
## Installation ##
The installation process is really straightforward. It follows the Symfony2 bundle setup conventions, so if you ever installed any other bundle it will pretty easy for you to proceed. Otherwise, if this is the first time you try to install a bundle, don't be scared! We promise you will succeed at the first try!

You've to follow only few steps (Scared? You need just 4 steps!)

  1. Download OryzoneBoilerplateBundle
  2. Configure the Autoloader
  3. Enable the Bundle
  4. Configure Assetic
  5. (optional) Configure google analytics

<a name="installation-step1"></a>
### Step 1. Download OryzoneBoilerplateBundle

<a name="installation-step1a"></a>
#### If you are using Symfony 2.0
Ultimately, the OryzoneBoilerplateBundle files should be downloaded to the `vendor/bundles/Oryzone/Bundle/BoilerplateBundle` directory.

This can be done at least in two different ways, depending on your preference: by using the symfony vendor script or by using git modules.
The first method is the standard Symfony 2.0 method.

<a name="installation-step1a1"></a>
##### Using the vendors script
Add the following lines in your deps file:

    [OryzoneBoilerplateBundle]
        git=git://github.com/Oryzone/OryzoneBoilerplateBundle.git
        target=/bundles/Oryzone/Bundle/BoilerplateBundle

Now, run the vendors script to download the bundle:

    $ php bin/vendors install

<a name="installation-step1a2"></a>
##### Using submodules
instead, if you prefer using git submodules, just proceed by running the following git commands:

    $ git submodule add git://github.com/Oryzone/OryzoneBoilerplateBundle.git vendor/bundles/Oryzone/Bundle/BoilerplateBundle
    $ git submodule update --init

<a name="installation-step1b"></a>
#### If you are using Symfony 2.1
With Symfony 2.1, the OryzoneBoilerplateBundle files should be downloaded to the `vendor/oryzone/boilerplate-bundle/Oryzone/Bundle/BoilerplateBundle` directory.

This can be done at least in two different ways, depending on your preference: by using the [Composer](http://getcomposer.org/) script or by using git modules.
The first method is the standard Symfony 2.1 method.

<a name="installation-step1b1"></a>
##### Using the Composer script
Add the following to your composer.json file:

    {
        "require": {
            "oryzone/boilerplate-bundle": "dev-master"
        }
    }

Update the vendor libraries:

    $ php composer.phar update

<a name="installation-step1b2"></a>
##### Using submodules
Instead, if you prefer using git submodules, just proceed by running the following git commands:

    $ git submodule add git://github.com/Oryzone/OryzoneBoilerplateBundle.git vendor/oryzone/boilerplate-bundle/Oryzone/Bundle/BoilerplateBundle
    $ git submodule update --init

<a name="installation-step2"></a>
### Step 2. Configure the Autoloader
Add the Oryzone namespace to your autoloader:

    <?php
    // app/autoload.php

    $loader->registerNamespaces( array(
        // ...
        'Oryzone' => __DIR__.'/../vendor/bundles',
    ));

<a name="installation-step3"></a>
### Step 3. Enable the Bundle
Finally, enable the bundle in the kernel:

    <?php
    // app/AppKernel.php

    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Oryzone\Bundle\BoilerplateBundle\OryzoneBoilerplateBundle(),
        );
    }

<a name="installation-step4"></a>
### Step 4. Configure Assetic
Make sure Assetic is configured to scan OryzoneBoilerplateBundle:

    <?php
    // app/config/config.yml

    assetic:
        // ...
        bundles:        ["OryzoneBoilerplateBundle"]

<a name="create-your-own-mighty-templates-as-extensions"></a>
Create your own mighty templates as extensions
----------------------------------------------
Now comes the most enjoying part, you've successfully installed the bundle and you're ready to go. Everything starts with a Twig template. If you want to create a new HTML5 powered template you've only to extend the `OryzoneBoilerplateBundle::html5.html.twig` template. So you need to put the following line at the beginning of your template:

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}

By doing so your template had inherited the base HTML5 structure proposed by the HTML5 Boilerplate. You'll have only to declare the content of the various blocks proposed by the template you're extending. A complete list of all the blocks will be described later. Let's see a quick and clear sample to make you hunger.

<a name="qucik-demo"></a>
Quick demo
------------
With the following code we created a simple template for an index page. As you will see we have only extended the basic HTML5 template and redeclared the content of some blocks. The example is merely trivial if you know [Twig][twig] a bit.

    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}

	{% block head_title %}My cool HTML5 website{% endblock %}
    {% block body_container_header %}<h1>My HTML5 home page is very cool</h1>{% endblock %}
    {% block body_container_main %}<p>This is the home page of my wild web site!</p>{% endblock %}
	{% block body_container_footer %}Here we go with copyright infos{% endblock %}

<a name="available-blocks"></a>
Available blocks
----------------
The basic template structure is made of nested blocks. This template proposes a default structure, so you have to rewrite only the blocks you really need to modify (or populate). Generally, as shown in the quick demo, you'll rewrite only few of them like `head_title` and the `body_main`. The template has been thought to be flexible enough to handle most of the cases. However, if you wish to apply deep modification to the whole structure you can totally rewrite higher level blocks like `head` or `body`.
Follows a representation of the blocks tree. Note that every block name is prefixed with the name of his ancestor blocks.

  * <strong>head</strong>
    * <strong>head\_meta</strong>
       * <strong>head\_meta\_description</strong>
       * <strong>head\_meta\_keywords</strong>
       * <strong>head\_meta\_viewport\_tag</strong>
         * <strong>head\_meta\_viewport\_tag\_content</strong>
    * <strong>head\_title</strong>
    * <strong>head\_css</strong>: Contains a reference to the basic css reset
    * <strong>head\_js</strong>: adds modernizr script. All the other script should be added inside the <strong>body\_js</strong> block
  * <strong>body</strong>
    * <strong>body\_chromeframe</strong>: handles google chrome frame for internet explorer
    * <strong>body\_container</strong>
      * <strong>body\_container\_header</strong>
      * <strong>body\_container\_main</strong>
      * <strong>body\_container\_footer</strong>
    * <strong>body\_js</strong>: to handle js at the end of the page
      * <strong>body\_js\_jquery</strong>: handles jQuery (from google CDN with local fallback if offline)
        * <strong>body\_js\_jquery\_onlineSrc</strong>: allows you to change the url of the cdn hosted script
        * <strong>body\_js\_jquery\_offlineSrc</strong>: allows you to change the path of the local jQuery script
      * <strong>body\_js\_analytics</strong>: handles google analytics script
        * <strong>body\_js\_analytics\_extra</strong>: allows you to add additional code (configuration) to your google analytics tracking code
        * <strong>body\_js\_analytics\_track</strong>: allows you to easily customize the track instruction on specific templates

<a name="available-variables"></a>
Available variables
-------------------
The template uses some variables that you can optionally redefine to customize its behaviour. Here's the complete list:

  * <strong>bp_language</strong>: allows you to set the language of your html file. ("en" by default)
  * <strong>bp_analytics_id</strong>: allows you to specify your google analytics id. If you don't provide a value for this variable the whole Google analytics script won't be added on the resulting page.
  * <strong>bp_analytics_domain</strong>: allows you to specify your google analytics domain. Will add a `_gaq.push(['_setDomainName', '{{ bp_analytics_domain }}']);` to your google analytics tracking code.
  * <strong>bp_html_classes</strong>: allows you to add classes to the `html` tag.
  * <strong>bp_html_attributes</strong>: allows you to add custom attributes to the `html` tag (e.g. `xmlns:fb="http://www.facebook.com/2008/fbml`)
  * <strong>bp_head_attributes</strong>: allows you to add custom attributes to the `head` tag (e.g. facebook `prefix` attribute)
  * <strong>bp_body_attributes</strong>: allows you to add custom attributes to the `body` tag

<a name="two-different-approaches"></a>
Two different approaches: overwrite and extend
----------------------------------------------
If you're already experienced with Twig this paragraph would be pointless, so feel free to skip it on if you are comfortable with Twig inheritance based paradigm.

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

Instead if you want to add some more stylesheet to the default one you can use the special Twig function `parent()` that gets the content of the block from the parent template.

	{% extends "OryzoneBoilerplateBundle::html5.html.twig" %}

	{% block head_css %}
	    {{ parent() }}
		<link rel="stylesheet" href="myWonderful.css">
		<link rel="stylesheet" href="someMoreBeautiful.css">
	{% endblock %}

    {# ... #}

Note that if you overwrite an higher level block as `head` you'll automatically overwrite all its nested blocks as `head_title` and `head_css`. This makes Twig pretty flexible because you have the full control of everything you wish to change or extend. Blocks can be considered just as starting points or suggestions on which you can build upon.

<a name="configure-google-analytics"></a>
Configure Google Analytics
--------------------------
Google analytics is disabled by default. You can easily enable it by passing your analytics id within the variable `bp_analytics_id`.
Optionally, if track subdomains or different domains, it would be good to even set the variable `bp_analytics_domain` to the current domain you are tracking.
Anyway I suggest you to set these variables directly in your configuration file among the Twig global variables. This way you have the opportunity to specify an id on the environments you prefer to: for example you may want to not use analytics on development but to use it in production, so just add the following lines on your `config_prod.yml` file

    twig:
        globals:
            bp_analytics_id: "UA-XXXXX-X"
            bp_analytics_domain: "example.com"

If you need to pass additional configuration to your google analytics tracking code you can use the block `body_js_analytics_extra`. Follows an example:

    {% block body_js_analytics_extra %}
        _gaq.push(['_setAllowLinker', true]);
    {% endblock %}

<a name="setting-the-page-language"></a>
Setting the page language
-------------------------
If you want to redefine the `lang` attribute of the `html` tag you just only have to define the `bp_language` variable from your controller.
If you want your templates to reflect your global locale configuration you can provide a global value for bp_language by doing this way:

    # Twig Configuration
    twig:
        globals:
            bp_language: %locale%

<a name="adding-classes-to-the-html-tag"></a>
Adding classes to the html tag
------------------------------
Sometimes is quite useful to add a class on the `html` tag. Modernizr does this all the time to let you build your css and being aware of the capabilities of the current browser.
It's also a common practice adding classes that specify, for example, the current section, the language or other useful attributes that can be useful to provide specific style variations on your css files.
Suppose you want to have the navigation bar with a different background color on each page of your website. You can add a specific class on the `html` tag of every page (e.g.`class="section-home"` or `class="section-contacts"`) and then provide some css rules of this kind:

    html.section-home nav
    {
        background-color: white;
    }

    html.section-contacts nav
    {
        background-color: yellow;
    }

To specify additional classes for your head tag you must assign a value to the `bp_html_classes` variable.
You can do so by passing a value from the controller, but, in my opinion this is not a controller duty. So it would be fairly better to set a value directly the template (which extends the boilerplate template). So you do something like this in your templates.

    {% set bp_html_classes = "section-home" %}

<a name="is-this-all"></a>
Is this all?
------------
Yes. This should be quite enough to get you started. Anyway if you are still in trouble or if you have any question feel free to contact us at [ORYZONE](http://oryzone.com).

[twig]: http://www.twig-project.org/ "The TWIG project home page"
