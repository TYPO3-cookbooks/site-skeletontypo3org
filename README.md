Cookbook site-skeletontypo3org
==============================

This cookbook provides a skeleton for TYPO3 site-cookbooks. The following sections describe the usage of the skeleton.

## Cookbook Structure

````
├── Berksfile                       # Cookbook dependencies for Berkshelf
├── Gemfile                         # Ruby Gems dependencies for Bundler
├── README.md                       # The cookbook documentation - automatically generated, DO NOT TOUCH!
├── attributes                      # Chef's attributes directory
│   └── ...
├── doc                             # Directory containing Markdown documents that will automatically be rendered into the README file
│   └── ...
├── files                           # Chef's files directory
│   └── ...
├── .kitchen.yml                    # Configuration for TestKitchen (integration testing)
├── metadata.rb                     # The cookbook's metadata file
├── recipes                         # The cookbook's recipes
│   ├── _privat_cookbook.rb         # Private recipes start with a '_'
│   ├── public_cookbook.rb          # Public recipes (reusable recipes, must be well documented)
│   └── ...
├── spec                            # Directory for ChefSpec tests (unit tests)
│   └── ...
└── templates                       # Chef's template directory
    └── ...
````



## Gemfile

The `Gemfile` describes the dependencies to Ruby Gems, which we need for some meta tasks (e.g. rendering the documentation or dependency management for cookbooks).

To resolve the Gem dependencies that you need to work with the cookbook, run

````
bundle install
````

from the cookbook's root directory. Make sure to have Bundler installed with `gem install bundler`.



### Gem Dependencies

Here's a brief description of the dependencies defined in the Gemfile:

* `berkshelf` - the cookbook dependency manager, see [berkshelf.com](http://berkshelf.com)
* `chefspec` - the unit testing framework for Chef cookbooks, see [ChefSpec's Github page](https://github.com/sethvargo/chefspec)
* `knife-cookbook-doc` - a plugin for knife that let's you generate the README, see [knife-cookbook-doc's Github page](https://github.com/realityforge/knife-cookbook-doc)
* `foodcritic` - a linting tool for Chef cookbooks, see [foodcritic.io](http://foodcritic.io/)
* `serverspec` - an integration testing framework, see [serverspec.org](http://serverspec.org/)
* `guard` - a file watcher tool, see [Guard's Github page](https://github.com/guard/guard)
* `thor-scmversion` - a versioning utility handling the cookbook versions, see [thor-scmversion's Github page](https://github.com/RiotGamesMinions/thor-scmversion)

The usage of the tools is described below if necessary.



## Berkshelf

We use [Berkshelf](http://berkshelf.com) as a dependency manager for our cookbooks. Since most of our cookbooks have dependencies to other cookbooks (community cookbooks or other TYPO3 cookbooks) it is a requirement for the cookbook development to resolve those cookbooks in a consistent manner. Berkshelf does this job for us.



### The Berksfile

Within the `Berksfile` we can configure the dependencies of our cookbook. Therefore we create a `Berksfile` with the following content in the root directory of our cookbook:

```` ruby
source 'https://supermarket.chef.io'

metadata

cookbook 'apache22'
cookbook 't3-zabbix', github: 'TYPO3-cookbooks/t3-zabbix'
cookbook 't3-megabook', path: '../cookbooks/t3-megabook'
````


Generally there are three different sources from where we get our cookbooks:

1. From the [Chef Supermarket](https://supermarket.chef.io/)
2. From (TYPO3's cookbook repositories on Github)[https://github.com/TYPO3-cookbooks]
3. From a local directory in our development environment

As you can see in the given example above, Berkshelf can handle all three of these locations for us.

The `metadata` keyword indicates that the dependencies of the cookbook should automatically be read from our `metadata.rb` file in which we have to declare the dependencies for Chef. Berkshelf will then automatically resolve those dependencies (from the Chef Supermarket unless an different location is given in the `Berksfile`).



## Rendering README Documentation

The README file for the cookbook is automatically generated by [knife-cookbook-doc](https://github.com/realityforge/knife-cookbook-doc). Here is a brief description of how it works.



### File and Directory Structure for Automated README Rendering

Regarding the following file / directory structure of a cookbook (files that are not relevant for the README rendering are not shown):

````
├── README.md                       # This file is generated automatically
├── attributes                      # Comments in attribute files are rendered as documentation
│   └── ...
├── doc                             # Every file in here is rendered into the README file
│   └── ...
├── metadata.rb                     # Certain content of `metadata.rb` is used for the README (e.g. authors and dependencies)
└── recipes                         # For each recipe in the `recipes` folder, a documentation section is rendered
    ├── _privat_cookbook.rb         # Documentation for prive recipes is NOT rendered into the README
    ├── public_cookbook.rb          # Public recipes should be well-annotated as there is a documentation section in the README for them
    └── ...
````

you will get a README rendered by running the following command from the cookbook root directory:

````
bundle exec knife cookbook doc . --template README.md.erb
````

If any error occurs, use the `-VV` switch to get some debug information.



### Template for README rendering

The template for the README rendering is currently part of this repository but should be put in a separate, global project since we want to re-use it in multiple cookbooks. It is planned to create a command line tool for common tasks concerning cookbook maintenance into which the template could be integrated later on.



### Documentation of Recipes

TODO



### Documentation of Attributes

TODO





Requirements
============

Platform:
---------

* debian

Cookbooks:
----------

*No dependencies defined*



Attributes
==========


### `node['skeleton']['sample_attribute']`
Sample attribute for showing how documentation of attributes works

**Default Value:** `[ ... ]`
### `node['email_adress']`
email address for the TYPO3 cookbook maintainers

**Default Value:** `cookbooks@typo3.org`




Recipes
=======

* [site-skeletontypo3org::sample](#site-skeletontypo3orgsample) - Provides a sample recipe for the TYPO3 skeleton cookbook.

site-skeletontypo3org::sample
-----------------------------

Provides a sample recipe for the TYPO3 skeleton cookbook.



TODOs
=====

## Documentation

* email address and metadata information in `metadata.rb`
* agree upon which platforms we want to support



## Testing

* Add basic TestKitchen configuration
* Agree upon whether or not we want to use Chefspec



## Tools

* Discuss usage / implementation of our own CLI helper tool (Thor?)
* Introduce Guard





License and Maintainer
======================

Maintainer:: The TYPO3 DevOps Team (<cookbooks@typo3.de>)

License:: All rights reserved
