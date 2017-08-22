Conda Environment Buildpack
===========================

Update (Aug-21, 2017): Updated the origin conda-buildpack to use Python 3.6 by default. 


This is the [Heroku Buildpack][] for [Conda][] using it's new
[environment spec][].  Anything you can install with `conda install` can be
installed using this, including the entire data science stack.  Be careful of
slug sizes, though.  Heroku does have limits.

## Usage
To control what gets installed, create an `environment.yml` file in the root
of your repository.  For example, if you wanted to install Flask, you would add
this:

```yaml
name: myproject  # overridden at install, so this is for your use with conda env
dependencies:
  - flask
```

Once that's created, you need to create a new Heroku app using this buildpack
like this:

```console
$ heroku create --buildpack https://github.com/conda/conda-buildpack.git
```

You can also add it to upcoming builds of an existing application:

```console
$ heroku config:add BUILDPACK_URL=https://github.com/conda/conda-buildpack.git
```

You can test that this is running conda managed Python like this:

```console
$ heroku run python
Running `python` attached to terminal... up, run.7018
Python 2.7.9 |Continuum Analytics, Inc.| (default, Dec 15 2014, 10:33:51)
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
Anaconda is brought to you by Continuum Analytics.
Please check out: http://continuum.io/thanks and https://binstar.org
>>>
```


## Fair Warning

Heroku limits the final application footprint (slug) size to 300MB. Start small.

[Conda]: http://conda.io
[environment spec]: https://github.com/conda/conda-env#environmentyml
[Heroku Buildpack]: https://devcenter.heroku.com/articles/buildpacks
