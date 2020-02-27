LinkFinder
==========

[![Build Status](https://travis-ci.org/yarri/LinkFinder.svg?branch=master)](https://travis-ci.org/yarri/LinkFinder)
[![Downloads](https://img.shields.io/packagist/dt/yarri/link-finder.svg)](https://packagist.org/packages/yarri/link-finder)
[![Codacy Project Certification](https://api.codacy.com/project/badge/Grade/e9ba7e40320b41c9a2caff1bcc85f16f)](https://www.codacy.com/app/jaromir.tomek/LinkFinder?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=yarri/LinkFinder&amp;utm_campaign=Badge_Grade)
[![Coverage](https://api.codacy.com/project/badge/Coverage/e9ba7e40320b41c9a2caff1bcc85f16f)](https://www.codacy.com/app/jaromir.tomek/LinkFinder?utm_source=github.com&utm_medium=referral&utm_content=yarri/LinkFinder&utm_campaign=Badge_Coverage)

In a plain text document the LinkFinder searches for URLs and email addresses and makes them clickable, in a HTML document searches for missing links and makes them clickable too.

Usage
-----

    $text = '
     Welcome at www.example.com!
     Contact us on info@example.com.
    ';
    
    $lf = new LinkFinder();
    echo $lf->process($text);
    
    // ... this prints out
    //  Welcome at <a href="http://www.example.com/">www.example.com</a>!
    //  Contact us on <a href="mailto:info@example.com">info@example.com</a>.

Extra attributes for ```<a>``` and ```<a href="mailto:...">``` elements can be specified in options:

    $lf = new LinkFinder([
      "attrs" => ["class" => "external-link", "target" => "_blank", "rel" => "nofollow"],
      "mailto_attrs" => ["class" => "external-email"]
    ]);
    echo $lf->process($text);
    
    // ... this prints out
    //  Welcome at <a class="external-link" href="http://www.example.com/" target="_blank" rel="nofollow">www.example.com</a>!
    //  Contact us on <a class="external-email" href="mailto:info@example.com">info@example.com</a>.


Escaping of HTML entities is enabled by default:

    $text = '
      Find more at
      <http://www.ourstore.com/>
    ';
    echo $lf->process($text);
    // Find more at
    // &lt;<a href="http://www.ourstore.com/">http://www.ourstore.com/</a>&gt;

Creating missing links on URLs or emails in a HTML document:

    $html_document = '
      <p>
        Visit <a href="http://www.ckrumlov.info/">Cesky Krumlov</a> or Prague.eu.
      </p>
    ';
    $lf = new LinkFinder();
    echo $lf->processHtml($html_document);
    // <p>
    //   Visit <a href="http://www.ckrumlov.info/">Cesky Krumlov</a> or <a href="http://Prague.eu">Prague.eu</a>.
    // </p>

Method $lf->processHtml() is actually an alias for $lf->process($html_document,["escape_html_entities" => false]).

Installation
------------

Just use the Composer:

    composer require yarri/link-finder

Testing
-------

Install required dependencies for development:

    composer update --dev

Run tests:

    ./test/run_tests.sh

License
-------

LinkFinder is free software distributed [under the terms of the MIT license](http://www.opensource.org/licenses/mit-license)

[//]: # ( vim: set ts=2 et: )
