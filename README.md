# ![](https://i.imgur.com/Bz4ThRE.jpg)
<h4> <p align="center">
  <img src="https://i.imgur.com/7uTPL2g.gif" alt="npm version" data-canonical-src="https://i.imgur.com/7uTPL2g.gif" width="75" height="75" style="max-width:100%;"></a>
  <html>
<body> <div>
			<td bgcolor="#ffffcc">
<!-- Begin MailChimp Signup Form -->
<br><span aria-hidden="true" class="icon-search"> </span><label class="screen-reader-text" for="id-search-field"> </label><input id="id-search-field" name="q" type="search" role="textbox" class="search-field" placeholder="Search" value="" tabindex="1"><button type="submit" name="submit" id="submit" class="search-button" title="Submit this Search" tabindex="3">GO</button> </br>
<p align="center">
        <div class='container'>
          <div class='wrapper'>
<span class='close'></span>
<h2 class='blue'>
</h2>
<form class='req-check signup-check' method='post' action='{#url}'>
<div class='form'>
<div class='row'><input req='1' type='text' name='txtName' placeholder='Name' /></div>
<div class='row'><input req='1' type='text' name='txtCompany' placeholder='Email' /></div>
<div class='row'><input req='1' type='email' name='txtEmail' placeholder='Password' /></div>
<div class='row'>
<span class='req-error red bold'>
</span>
<input type='submit' value='REGISTER NOW!' />
<!--End mc_embed_signup--> 

</details>
<details>
<summary> <img src="https://www.codeaffine.com/wp-content/uploads/2014/07/travis-ci.png" width="1000" height="250" alt="travis-ci"> </summary>       

# About this repository [![Build Status](https://travis-ci.org/travis-ci/docs-travis-ci-com.svg?branch=master)](https://travis-ci.org/travis-ci/docs-travis-ci-com)

This is the documentation site for Travis CI! (<http://docs.travis-ci.com/>)

## How to contribute

Fork the repository, read the rest of this README file and make some changes.
Once you're done with your changes send a pull request. Thanks!

## How to check your edit before sending PR

You can inspect how your edits will be reflected by the documentation site.

### Install dependencies

1. Make sure you have Ruby and RubyGems installed.

1. Install [bundler](http://bundler.io/):

    ```sh-session
    $ gem install bundler
    ```

1. Install application dependencies:

    ```sh-session
    $ bundle install --binstubs
    ```

### Generate documentation

Run

```sh-session
$ ./bin/jekyll build
```


### Run application server

You are now ready to start your documentation site, using Jekyll or Puma.
For documentation edits, Jekyll is sufficient.

#### Starting and inspecting edits with Jekyll

1. Run Jekyll server:

    ```sh-session
    $ ./bin/jekyll serve
    ```

1. Open [localhost:4000](http://localhost:4000/) in your browser.

#### Starting and inspecting edits with Puma

For more programmatical PRs (such as handling webhooks notification
via POST), Puma is necessary.

1. Run Puma server:

    ```sh-session
    $ ./bin/puma
    ```

1. Open [localhost:9292](http://localhost:9292/) in your browser.

### API V2 documentation

API V2 (and 2.1) documentation is maintained in `slate/source` and updated is now generated at build time from source.

## License

Distributed under the [MIT license](https://opensource.org/licenses/MIT); the same as other Travis CI projects.
</details>
<details>
<summary> <img src="https://eysz7x.imgur.com/PMMdfyN.gif" width="200" height="50" alt="Python Project"> Python Project </summary>       
       
title: Building a Python Project
layout: en

---

### What This Guide Covers
<div>
	<tbody>
		<tr>
			<td bgcolor="#ffffcc">
				<p>
<aside markdown="block" class="ataglance">
|Python ||Default|

|:--------------------------------------------
|:------------------------------------------
|
     
     |[Default `install`](#dependency-management)
     | `pip install -r requirements.txt` 
     |
     | [Default `script`](#default-build-script)   
     | N/A                               
     |
     | [Matrix keys](#build-matrix)       
     | `python`, `env`                    
     |
     | Support                            
     | [Travis CI](mailto:support@travis-ci.com) 
     |
____

Minimal example:

```yaml
  language: python
  python:
    - "3.6"
  script:
    - pytest
```
{: data-file=".travis.yml"}
</aside>

{{ site.data.snippets.trusty_note_no_osx }}

Python builds are not available on the macOS environment.

The rest of this guide covers configuring Python projects in Travis CI. If you're
new to Travis CI please read our [Tutorial](/user/tutorial/) and
[build configuration](/user/customizing-the-build/) guides first.

## Specifying Python versions

Specify python versions using the `python` key. As we update the Python build
images, aliases like `3.6` will point to different exact versions or patch
levels.

```yaml
language: python
python:
  - "2.6"
  - "2.7"
  - "3.3"
  - "3.4"
  - "3.5"
  - "3.5-dev"  # 3.5 development branch
  - "3.6"
  - "3.6-dev"  # 3.6 development branch
  - "3.7-dev"  # 3.7 development branch
# command to install dependencies
install:
  - pip install -r requirements.txt
# command to run tests
script:
  - pytest
```
{: data-file=".travis.yml"}

You can also specify the stable release of Python 3.7 on our Xenial build images:

```yaml
dist: xenial
language: python
python: 3.7
```
{: data-file=".travis.yml"}


### Travis CI Uses Isolated virtualenvs

The CI Environment uses separate virtualenv instances for each Python
version. This means that as soon as you specify `language: python` in `.travis.yml` your tests will run inside a virtualenv (without you having to explicitly create it).
System Python is not used and should not be relied on. If you need
to install Python packages, do it via pip and not apt.

If you decide to use apt anyway, note that for compatibility reasons, you'll only be able to use the default Python versions that are available in Ubuntu (e.g. for Trusty, this means 2.7.6 and 3.4.3).
To access the packages inside the virtualenv, you will need to specify that it should be created with the `--system-site-packages` option.
To do this, include the following in your `.travis.yml`:

```yaml
language: python
python: 
  - "2.7"
  - "3.4" 
virtualenv:
  system_site_packages: true
```
{: data-file=".travis.yml"}


### PyPy Support

Travis CI supports PyPy and PyPy3.

To test your project against PyPy, add "pypy3.5" to the list of Pythons
in your `.travis.yml`:

```yaml
language: python
python:
  - "2.7"
  - "3.4"
  - "3.5"
  - "3.6"
  # PyPy versions
  - "pypy3.5"
   
# command to install dependencies
install:
  - pip install -r requirements.txt
  - pip install .
# command to run tests
script: pytest
```
{: data-file=".travis.yml"}

### Nightly build support

Travis CI supports a special version name `nightly`, which points to
a recent development version of [CPython](https://github.com/python/cpython) build.

### Development releases support

From Python 3.5 and later, Python In Development versions are available.

You can specify these in your builds with `3.5-dev`, `3.6-dev`,
`3.7-dev` or `3.8-dev`.

{: .warning}
> Recent Python branches [require OpenSSL 1.0.2+](https://github.com/travis-ci/travis-ci/issues/9069).
> As this library is not available for Trusty,  `3.7`, `3.7-dev`, `3.8-dev`, and `nightly`
> do not work (or use outdated archive).

## Default Build Script

Python projects need to provide the `script` key in their `.travis.yml` to
specify what command to run tests with.

For example, if your project uses pytest:

```yaml
# command to run tests
script: pytest
```
{: data-file=".travis.yml"}

if it uses `make test` instead:
```yaml
script: make test
```
{: data-file=".travis.yml"}

If you do not provide a `script` key in a Python project, Travis CI prints a
message (_"Please override the script: key in your .travis.yml to run tests."_)
and fails the build.

## Using Tox as the Build Script

Due to the way Travis is designed, interaction with [tox](https://tox.readthedocs.io/en/latest/) is not straightforward.
As described [above](/user/languages/python/#travis-ci-uses-isolated-virtualenvs), Travis already runs tests inside an isolated virtualenv whenever `language: python` is specified, so please bear that in mind whenever creating more environments with tox. If you would prefer to run tox outside the Travis-created virtualenv, it might be a better idea to use `language: generic` instead of `language: python`.

If you're using tox to test your code against multiple versions of python, you have two options:
  * use `language: generic` and manually install the python versions you're interested in before running tox (without the manual installation, tox will only have access to the default Ubuntu python versions - 2.7.6 and 3.4.3 for Trusty)
  * use `language: python` and a build matrix that uses a different version of python for each branch (you can specify the python version by using the `python` key). This will ensure the versions you're interested in are installed and parallelizes your workload.

A good example of a `travis.yml` that runs tox using a Travis build matrix is [twisted/klein](https://github.com/twisted/klein/blob/master/.travis.yml).

## Dependency Management

### pip

By default Travis CI uses `pip` to manage Python dependencies. If you have a
`requirements.txt` file, Travis CI runs `pip install -r requirements.txt`
during the `install` phase of the build.

You can manually override this default `install` phase, for example:

```yaml
install: pip install --user -r requirements.txt
{: data-file=".travis.yml"}

Please note that the `--user` option is mandatory if you are not using `language: python`, since no virtualenv will be created in that case.

### Custom Dependency Management

To override the default `pip` dependency management, alter the `before_install`
step as described in [general build
configuration](/user/job-lifecycle/#customizing-the-installation-phase) guide.

### Testing Against Multiple Versions of Dependencies (e.g. Django or Flask)

If you need to test against multiple versions of, say, Django, you can instruct
Travis CI to do multiple runs with different sets or values of environment variables.

Use *env* key in your .travis.yml file, for example:

```yaml
env:
  - DJANGO_VERSION=1.10.8
  - DJANGO_VERSION=1.11.5
```
{: data-file=".travis.yml"}

and then use ENV variable values in your dependencies installation scripts, test
cases or test script parameter values. Here we use ENV variable value to instruct
pip to install an exact version:

```yaml
install:
  - pip install -q Django==$DJANGO_VERSION
  - python setup.py -q install
```
{: data-file=".travis.yml"}

The same technique is often used to test projects against multiple databases and so on.
For a real world example, see [getsentry/sentry](https://github.com/getsentry/sentry/blob/master/.travis.yml) and [jpvanhal/flask-split](https://github.com/jpvanhal/flask-split/blob/master/.travis.yml).

## Examples

- [tornadoweb/tornado](https://github.com/tornadoweb/tornado/blob/master/.travis.yml)
- [simplejson/simplejson](https://github.com/simplejson/simplejson/blob/master/.travis.yml)
- [fabric/fabric](http://github.com/fabric/fabric/blob/master/.travis.yml)
- [dstufft/slumber](https://github.com/dstufft/slumber/blob/master/.travis.yml)
- [dreid/cotools](https://github.com/dreid/cotools/blob/master/.travis.yml)
- [twisted/klein](https://github.com/twisted/klein/blob/master/.travis.yml)
</body>
</html>
</p>

</details>
<details>
<summary> <img src="https://i.imgur.com/3tFTS1u.png" width="110" alt="Travis Api"> REQUIRMENTS </summary>
# Requirments


[![Build Status](https://travis-ci.org/travis-ci/travis-api.svg?branch=master)](https://travis-ci.org/travis-ci/travis-api)

You will need the following packages to get travis-api to work:

1. PostgreSQL 9.3 or higher
2. Bundler
3. Redis
4. *Optional:* RabbitMQ Server
5. *Optional:* Nginx -
    *If working in Ubuntu please install nginx manually from source: Download and extract latest nginx version, open a terminal in extracted folder and then run the following:*
```sh-session
    $ sudo apt-get install libpcre3 libpcre3-dev
    $ auto/configure --user=$USER
    $ make
    $ sudo make install
    $ sudo ln -s /usr/local/nginx/sbin/nginx /bin/nginx
```

## Installation

### Setup
```sh-session
$ bundle install
```
### Main Database & Logs Database setup

*You might need to create a role first. For this you should run the following:*

```sh-session
$ sudo -u postgres psql -c "CREATE USER yourusername WITH SUPERUSER PASSWORD 'yourpassword'"
```

Databases are set up with a Rake task that uses the database schemas (`structure.sql`) in `travis-migrations`. Details can be found in the `Rakefile`.
You can override the `travis-migrations` branch that is being used by setting the environment variable `TRAVIS_MIGRATIONS_BRANCH`.


To create and migrate the Databases:

```sh-session
$ ENV=development bundle exec rake db:create
$ ENV=test bundle exec rake db:create
```

Please Note: The database names are configured using the environment variable ENV. If you are using a different configuration you will have to make your own adjustments. The default environment is `test`.


### Run tests
```sh-session
$ bundle exec rake
```

### Run the server (development)
```sh-session
ENV=development bundle exec ruby -Ilib -S rackup
```

### To test your branch locally:
- checkout your branch
- run the local server:
```sh-session
ENV=development bundle exec ruby -Ilib -S rackup
```

- get the correct token in another window:
```sh-session
travis login --api-endpoint=http://localhost:9292
travis token --api-endpoint=http://localhost:9292
```
- run a request:
```sh-session
curl -H "Travis-API-Version: 3" \
     -H "Authorization: token xxxxxxxxxxxx" \
     http://localhost:9292/repos
```

(The database connection can be overwritten by setting a DATABASE_URL env var. Please ensure you also set ENV to the corresponding env and add encryption key config to `config/travis.yml`)

### Test billing locally:
To test billing locally add the following code to the config/travis.yml:

```
development:
  billing:
    url: "http://localhost:9292"
    auth_key: "auth_keys"
```
go to your local api repo and make sure API is running on port 9293:

```
ENV=development  bundle exec ruby -Ilib -S rackup -p 9293
```

go to your local billing repo and run which runs on 9292:
```
make start
```
and then you can run:

```
curl -H "Travis-API-Version: 3" \
     -H "content-type: application/json" \
     -H "Authorization: token <your-token>" \
     http://localhost:9293/subscriptions
```
and get:
```  
{
  "@type": "subscriptions",
  "@href": "/subscriptions",
  "@representation": "standard",
  "subscriptions": [

  ]
}
```



### Run the server (production)
```sh-session
$ bundle exec script/server
```
If you have problems with Nginx because the websocket is already in use, try restarting your computer.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

### API documentation

v3 documentation can be found at https://developer.travis-ci.org which is a repository that can be found at https://github.com/travis-pro/developer

### Adding V3 Endpoints Developer Documentation
Start with the find/get spec (for example: spec/v3/services/caches/find_spec.rb) for your new endpoint. If you don't have a find route start with whatever route you want to add first. Run the test and add the files you need to clear the errors. They should be:
 - A service (lib/travis/api/v3/services/caches/find.rb)
 - A query (lib/travis/api/v3/queries/caches.rb)
 - Register the service in v3/services.rb (alphabetical order please)
 - Add a route (v3/routes.rb)
 Re-run the test at this point. Depending on what objects you are returning you may also need to add:
 - Add a model (either pulls from the DB or a wrapper for the class of the objects returned from another source (s3 for example), or that structures the result you will be passing back to the client)
 - Add a renderer (if needed to display your new model/object/collection).
</details>
<details>
<summary> <img src="https://i.imgur.com/Mqza0wb.jpg" width="115" alt="CODE OF CONDUCT"> CODE OF CONDUCT</summary>
<div>
	<tbody>
      <td>
			<td bgcolor="#ffffcc">
# <code>[Contributor Covenant Code of Conduct](https://www.contributor-covenant.org)</code>

## <code>Our Pledge</code>

<br>In the interest of fostering an open and welcoming environment, we as
contributors and maintainers pledge to making participation in our project and
our community a harassment-free experience for everyone, regardless of age, body
size, disability, ethnicity, gender identity and expression, level of experience,
nationality, personal appearance, race, religion, other beliefs, or sexual identity and
orientation.</br>

## <code>Our Standards</code>
<br>
Examples of behavior that contributes to creating a positive environment
include:</br>

* Using welcoming and inclusive language
* Being respectful of differing viewpoints and experiences
* Being constructive and proportionate when criticizing
* Gracefully accepting constructive criticism
* Focusing on what is best for the community
* Showing empathy towards other community members

<code>Examples of unacceptable behavior by participants include:</code>

* The use of sexualized language or imagery and unwelcome sexual attention or
  advances
* Trolling, insulting/derogatory comments, and personal or political attacks
* Public or private harassment
* Publishing others' private information, such as a physical or electronic
  address, without explicit permission
* Other conduct which could reasonably be considered inappropriate in a
  professional setting

## <code>Our Responsibilities</code>

<br>Project maintainers are responsible for clarifying the standards of acceptable
behavior and are expected to take appropriate and fair corrective action in
response to any instances of unacceptable behavior.

Project maintainers have the right and responsibility to remove, edit, or
reject comments, commits, code, wiki edits, issues, and other contributions
that are not aligned to this Code of Conduct, or to ban temporarily or
permanently any contributor for other behaviors that they deem inappropriate,
threatening, offensive, or harmful.</br>

## <code>Scope</code>
<br>
This Code of Conduct applies both within project spaces and in public spaces
when an individual is representing the project or its community. Examples of
representing a project or community include using an official project e-mail
address, posting via an official social media account, or acting as an appointed
representative at an online or offline event. Representation of a project may be
further defined and clarified by project maintainers.</br>

## <code>Enforcement</code>
<br>
Instances of abusive, harassing, or otherwise unacceptable behavior may be
reported by contacting the project team at the following email address: conduct@travis-ci.org. All
complaints will be reviewed and investigated and will result in a response that
is deemed necessary and appropriate to the circumstances. The project team is
obligated to maintain confidentiality with regard to the reporter of an incident.
Further details of specific enforcement policies may be posted separately.</br>

<br>Project maintainers who do not follow or enforce the Code of Conduct in good
faith may face temporary or permanent repercussions as determined by other
members of the project's leadership.</br>

## <code>Attribution</code>

<br>This Code of Conduct is adapted from the [Contributor Covenant][homepage], version 1.4,
available at https://www.contributor-covenant.org/version/1/4/code-of-conduct.html</br>

<a href="homepagehttps://www.contributor-covenant.org"/>[Homepage]</a>
</tbody>
      </td>
      </details>
	<tbody>
      <td>
			<td bgcolor="#ffffcc">
<details>
<summary> <img src="https://img.icons8.com/color/48/000000/repository.png" width="50" alt="CONTRIBUTING"> CONTRIBUTING</summary>
	
<code>Issues for any Travis-CI repo should be submitted to</code>
## [Contributing to Travis-CI](https://github.com/travis-ci/travis-ci/issues) 

#### Security Issues
***Any security issues should be submitted directly to [security@travis-ci.org](mailto:security@travis-ci.org)***

#### Reporting Issues
<code>
- Explain what you expected to happen vs the actual results
- Include a screenshot if it helps illustrate the issue. https://github.com/blog/1347-issue-attachments
- What steps are required to reproduce the issue
- An example build that shows the issue
</code>
#### Submitting a PR to Travis-API
See testing and setup notes in the base <a href="https://github.com/travis-ci/travis-api"/>README</a>
	</tbody>
      </td>
</details>
	<tbody>
      <td>
			<td bgcolor="#ffffcc">
</summary>

<code>title: Travis CI Tutorial
layout: en
redirect_from:
  - /user/getting-started/
</code>
<code>
This is a very short guide to using Travis CI with your GitHub hosted code repository.
If you're new to continuous integration or would like some more information on
what Travis CI does, start with [Core Concepts for Beginners](/user/for-beginners)
instead.</code>
</details>
______
<br>
## Prerequisites
</br>
<br>To start using Travis CI, make sure you have:</br>
<br>
 * A [GitHub](https://github.com/) account.
 * Owner permissions for a project [hosted on GitHub](https://help.github.com/categories/importing-your-projects-to-github/).
</br>
<br>
## To get started with Travis CI
</br>
<br>
1. Go to [Travis-ci.com](https://travis-ci.com) and [*Sign up with GitHub*](https://travis-ci.com/signin).</br>
<br>
2. Accept the Authorization of Travis CI. You'll be redirected to GitHub.</br>
<br>
3. Click the green *Activate* button, and select the repositories you want to use with Travis CI.
<br>
4. Add a `.travis.yml` file to your repository to tell Travis CI what to do.</br>
<br>
   The following example specifies a Ruby project that should
   be built with Ruby 2.2 and the latest versions of JRuby.</br>

   ```yaml
   language: ruby
   rvm:
    - 2.2
    - jruby
   ```
   {: data-file=".travis.yml"}

   The defaults for Ruby projects are `bundle install` to [install dependencies](/user/job-lifecycle/#customizing-the-installation-phase),
   and `rake` to build the project.

5. Add the `.travis.yml` file to git, commit and push, to trigger a Travis CI build:

   > Travis only runs builds on the commits you push *after* you've added a `.travis.yml` file.

6. Check the build status page to see if your build [passes or fails](/user/job-lifecycle/#breaking-the-build), according to the return status of the build command by visiting the [Travis CI](https://travis-ci.com/auth) and selecting your repository.


## Selecting a different programming language

Use one of these common languages:

```yaml
language: ruby
```
{: data-file=".travis.yml"}

```yaml
language: java
```
{: data-file=".travis.yml"}
</tbody>
      </td>
			</body>
            </html>
