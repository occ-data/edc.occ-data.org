# Repositiory for edc.occ-data.org


## About

Website Powered by [Hugo](https://gohugo.io/) with generous support from the [Kube theme](https://github.com/jeblister/kube). 

## Usage

For more information read the official [setup guide](//gohugo.io/overview/installing/) for Hugo.

## Installation

Inside the folder of your Hugo site run:

    $ mkdir themes
    $ cd themes
    $ git clone https://github.com/jeblister/kube.git

Copy custom archetypes to your site:

```shell
cp themes/kube/archetypes/* archetypes
```


Next, take a look in the `exampleSite` folder at. This directory contains an example config file and the content for the demo. It serves as an example setup for your blog. 

Copy at least the `config.toml` in the root directory of your website. Overwrite the existing config file if necessary. 

Hugo includes a development server, so you can view your changes as you go :

``` sh
hugo server -w
```

Now you can go to [localhost:1313](http://localhost:1313) and the `kube`
theme should be visible.


## License

MIT

## Credit 

- [kube framework](https://imperavi.com/kube/)
- [after dark theme](https://github.com/comfusion/after-dark)

