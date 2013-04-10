Heroku buildpack: Python
========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps with Node.js, powered by [pip](http://www.pip-installer.org/) and [npm](http://npmjs.org/).
[![Build Status](https://secure.travis-ci.org/heroku/heroku-buildpack-python.png?branch=master)](http://travis-ci.org/heroku/heroku-buildpack-python)

Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  packages.json web.py

    $ heroku create --stack cedar --buildpack git://github.com/fivethreeo/heroku-buildpack-python-nodejs.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> No runtime.txt provided; assuming python-2.7.3.
    -----> Preparing Python runtime (python-2.7.3)
    -----> Installing Distribute (0.6.34)
    -----> Installing Pip (1.2.1)
    -----> Installing dependencies using Pip (1.2.1)
           Downloading/unpacking Flask==0.7.2 (from -r requirements.txt (line 1))
           Downloading/unpacking Werkzeug>=0.6.1 (from Flask==0.7.2->-r requirements.txt (line 1))
           Downloading/unpacking Jinja2>=2.4 (from Flask==0.7.2->-r requirements.txt (line 1))
           Installing collected packages: Flask, Werkzeug, Jinja2
           Successfully installed Flask Werkzeug Jinja2
           Cleaning up...
    Node.js
    -----> Resolving engine versions
           Using Node.js version: 0.10.3
           Using npm version: 1.2.15
    -----> Fetching Node.js binaries
    -----> Vendoring node into slug
    -----> Installing dependencies with npm
           npm WARN package.json nordtun@0.0.2 No README.md file found!
           npm http GET https://registry.npmjs.org/less/1.3.3
           npm http 200 https://registry.npmjs.org/less/1.3.3
           npm http GET https://registry.npmjs.org/less/-/less-1.3.3.tgz
           npm http 200 https://registry.npmjs.org/less/-/less-1.3.3.tgz
           npm http GET https://registry.npmjs.org/ycssmin
           npm http 200 https://registry.npmjs.org/ycssmin
           npm http GET https://registry.npmjs.org/ycssmin/-/ycssmin-1.0.1.tgz
           npm http 200 https://registry.npmjs.org/ycssmin/-/ycssmin-1.0.1.tgz
           less@1.3.3 node_modules/less
           ÔööÔöÇÔöÇ ycssmin@1.0.1
           npm WARN package.json nordtun@0.0.2 No README.md file found!
           less@1.3.3 /tmp/build_2oes14d16al8r/node_modules/less
           ycssmin@1.0.1 /tmp/build_2oes14d16al8r/node_modules/less/node_modules/ycssmin
           Dependencies installed
           
You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/fivethreeo/heroku-buildpack-python-nodejs.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug. 

This buildpack also checks for Node.js, for usage see:

https://github.com/heroku/heroku-buildpack-nodejs

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.3.0
    
Runtime options include:

- python-2.7.3
- python-3.3.0
- pypy-1.9 (experimental)
