OryzoneBoilerplateBundle Documentation
======================================
Hello folks, with OryzoneBoilerplateBundle you can easily create heavily optimized HTML5 twig templates empowered with great features such as CSS resets, CDNed jquery (with offline fallback), asynchronous google analytics script and so on.

Have you ever wondered where to start to create an HTML5 web site by using Symfony2? Well you came in the right place! Let's go on! ;)

Installation
------------
The installation process is really straightforward. It follows the Symfony2 bundle setup conventions, so if you ever installed any other bundle it will pretty easy for you to proceed. If this is the first time you try to install a bundle don't be scared! We promise you will succeed at the first try!

You've to follow only few steps (Scared? There are just 4!)

  1. Download OryzoneBoilerplateBundle
  2. Configure the Autoloader
  3. Enable the Bundle
  4. Create your own mighty templates as extensions

### Step 1. Download OryzoneBoilerplateBundle ###
Ultimately, the OryzoneBoilerplateBundle files should be downloaded to the `vendor/bundles/Oryzone/BoilerplateBundle` directory.

This can be done at least in two different ways, depending on your preference. The first method is the standard Symfony2 method.

#### Using the vendors script ####
Add the following lines in your deps file:

    [OryzoneBoilerplateBundle]
        git=git://github.com/Oryzone/OryzoneBoilerplateBundle.git
        target=bundles/Oryzone/BoilerplateBundle

Now, run the vendors script to download the bundle:

    $ php bin/vendors install

#### Using submodules ####
If you prefer instead to use git submodules, the run the following:

    $ git submodule add git://github.com/Oryzone/OryzoneBoilerplateBundle.git vendor/bundles/Oryzone/BoilerplateBundle
    $ git submodule update --init

### Step 2. Configure the Autoloader ###

Add the Oryzone namespace to your autoloader:

<?php
// app/autoload.php

$loader->registerNamespaces(array(
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

Quick sample
------------
Once you've added OryzoneBoilerplateBundle to your project it will be truly damn easy for you to produce an HTML5 enabled template. Here's a quick a fresh served appetizer to disclose what are you going to taste by using this bundle.

    {# yourMainBundle/Resources/views/Default/index.html.twig #}
    
    {% extends "OryzoneBoilerplateBundle::html5.html.twig" %}
    
	{% block head_title %}My cool HTML5 website{% endblock %}
    {% block body_header %}<h1>My HTML5 home page is very cool</h1>{% endblock %}
    {% block body_main %}<p>This is the home page of my wild web site!</p>{% endblock %}
	{% block body_footer %}Here we go with copyright infos{% endblock %}

Available blocks
----------------
  * *head*
    * *head_meta*
       * *head_meta_description*
       * *head_meta_keywords*
       * *head_meta_author*
    * *head_title*
    * *head_css* contiene un riferimento al reset di base
    * *head_js* contiene un riferimento a modernizer. Tutti gli altri javascript dovrebbero essere inseriti in *body_js*
  * *body*
    * *body_header*
    * *body_main*
    * *body_footer*
    * *body_js* to handle js at the end of the page
      * *body_js_jquery* handles jquery 1.6.2 (from google cdn with local fallback if offline)
        * *body_js_jquery_onlineSrc* allows you to change the url of the cdn hosted script
        * *body_js_jquery_offlineSrc* allows you to change the path of the local jQuery script
      * *body_js_analytics* handles google analytics script
        * *body_js_analytics_id* uset to set the analytics id inside the script
      * *body_js_chromeframe* handles google chrome frame for internet explorer

Adding assets (a.k.a. *javascripts* and *stylesheets* )
-------------------------------------------------------
To be written

What the hell if i want to change the main structure of the page?
-----------------------------------------------------------------
To be written

Disable features
----------------
To be written

Going by extension
------------------