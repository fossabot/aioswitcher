# Contributing to `aioswitcher`

:clap: First off, thank you for taking the time to contribute. :clap:

Contributing is pretty straight-forward:
-   Fork the repository
-   Commit your changes
-   Create a pull request against the `dev` branch
  
Please feel free to contribute, even to this contributing guideline file, if you see fit.

**Content**
-   [Items description](#items-description)
    -   [Configuration files](#configuration-files)
    -   [Python](#python)
    -   [Requirement files](#requirement-files)
    -   [Package management](#package-management)
    -   [Documentation](#documentation)

-   [Continuous Integration](#continuous-integration)
    -   [CircleCi](#circleci)
    -   [CodeCov](#codecov)
    -   [Codacy](#codacy)
    -   [Requires-io](#requires-io)
    -   [David-DM](#david-dm)
    -   [Snyk](#snyk)

-   [Continuous Deployment](#continuous-deployment)
    -   [Read the Docs](#read-the-docs)
    -   [PyPi](#pypi)

-   [Environments and Tools](#environments-and-tools)

-   [Testing](#testing)

-   [Guidelines](#guidelines)
    -   [NPM Scripts](#npm-scripts)

-   [Chat](#chat)

-   [Best Practices](#best-practices)

-   [Code of Conduct](#code-of-conduct)

## Items description
### Configuration files
-   `.circle/config.yml` is the configuration file for [CircleCi Continuous Integration and Deployment Services](https://circleci.com/gh/TomerFi/aioswitcher/tree/dev).

-   `.codecov.yml` is the configuration file for [CodeCov Code Coverage](https://codecov.io/gh/TomerFi/aioswitcher).

-   `.coveragerc` is the configuration file for [Coverage.py](https://coverage.readthedocs.io/en/v4.5.x/)
    creating coverage reports with the [pytest-cov plugin](https://pytest-cov.readthedocs.io/en/latest/).

-   `.yamllint` is the configuration for [yamllint A Linter for YAML Files](https://yamllint.readthedocs.io/en/stable/index.html)
    linting yml files.

-   `.remarkrc` is the configuration file for [remark-lint](https://github.com/remarkjs/remark-lint)
    plugin for [Remark](https://remark.js.org/) linting *markdown* files.

-   `bandit.yml` is the configuration file for [Bandit common security issues finder](https://github.com/PyCQA/bandit)
    checking python scripts.

-   `.spelling` is the dictionary file used by both [markdown-spellcheck](https://www.npmjs.com/package/markdown-spellcheck)
    and [scspell3k](https://pypi.org/project/scspell3k/).
    Case-insensitive words in this file will not raise a spelling mistake error.

### Python
-   `src/aioswitcher` is the *Python* modules making the package.
-   `tests` is where *Python* test-cases are stored and executed with [pytest](https://pypi.org/project/pytest/).
-   `pyscripts` is where *Python* scripts are stored.

### Requirement files
-   `poetry.lock` is the lock file describing the module version tree of the pypi modules. This
    helps locking down working versions of modules, it is part of the
    [poetry](https://poetry.eustace.io/) dependency management.

-   `package-lock.json` is the lock file describing the module version tree of the npm modules.
    This helps locking down working versions of modules, it is part of the
    [npm](https://docs.npmjs.com/files/package.json) dependency management.

-   `requirements.txt` has noting to do directly with the package structure. We use
    [poetry](https://poetry.eustace.io/) for packaging and building. This file is actually being
    manually build with [pyscripts/poetry-to-requirements.py](pyscripts/poetry-to-requirements.py)
    from the content of [poetry.lock](poetry.lock) for legacy support (e.g. [Requires-io](#requires-io)
    and [Snyk](#snyk)).

### Package management
-   The [package.json](package.json) file specified by [npm](https://docs.npmjs.com/files/package.json)
    manages our dependencies, scripts and some metadata.

-   The [pyproject.toml](pyproject.toml) is the main configuration file for the pypi package based
    on [PEP518](https://www.python.org/dev/peps/pep-0518/). Please note, this package is being
    managed, build, packaged and deployed with [poetry](https://poetry.eustace.io/).

### Documentation
-   `docs/sources` is where the *restructuredText* for creating the [Sphinx Documentation](http://www.sphinx-doc.org/en/master/)
    are stored for build, deployment and hosting by [Read the Docs](https://readthedocs.org/).

-   `docs/Makefile` the basic *Makefile* for [Sphinx](http://www.sphinx-doc.org/en/master/)
    documentation generator. From the [docs](docs/) path, type `make html` and
    [sphinx](http://www.sphinx-doc.org/en/master/) will create the documentation site locally in
    `docs/build`.

## Continuous Integration
### CircleCi
By hook configuration, for every pull request, [CircleCi](https://circleci.com/gh/TomerFi/aioswitcher/tree/dev)
will execute the workflows described in [.circleci/config.yml](.circleci/config.yml)
and update the PR conversation with the results.

As a final step, [CircleCi](https://circleci.com/gh/TomerFi/aioswitcher/tree/dev) will push the
[Coverage.py XML Report](https://coverage.readthedocs.io/en/v4.5.x/) to both
[CodeCov](https://codecov.io/gh/TomerFi/aioswitcher) for code coverage analysis and
[Codacy](https://app.codacy.com/project/TomerFi/aioswitcher/dashboard) for code quality
analysis.</br>
Both will of course push their results into the PR conversation.</br>
Please note, [Codacy](https://app.codacy.com/project/TomerFi/aioswitcher/dashboard) is actually
getting notified for the PR by a *GitHub* hook. The report being uploaded is for the
dashboard presentation and does not trigger further action.

Some of the steps are considered required and may prevent the PR from being merged.
But no worries, everything is fixable.

### CodeCov
[CodeCov](https://codecov.io/gh/TomerFi/aioswitcher) is keeping tabs on our code coverage.
When a report is uploaded (by [CircleCi](https://circleci.com/gh/TomerFi/aioswitcher/tree/dev)),
[CodeCov](https://codecov.io/gh/TomerFi/aioswitcher) will check our code coverage and push its
conclusions to the PR conversation.

### Codacy
[Codacy](https://app.codacy.com/project/TomerFi/aioswitcher/dashboard) is here to check the
quality of our code.
When a PR is created or updated, *GitHub* is hooked to notify [Codacy](https://app.codacy.com/project/TomerFi/aioswitcher/dashboard)
that starts checking the quality of our code and push its conclusions to the PR conversation.

### Requires-io
[Requires.io](https://requires.io/github/TomerFi/aioswitcher/requirements/?branch=dev)
is keeping an eye for versions updates upon the *Python* requirements listed in our legacy [requirements.txt](requirements.txt) file.

### David-DM
[David-DM](https://david-dm.org/TomerFi/aioswitcher) is keeping an eye for versions updates upon
the npm requirements listed in the *package.json* file.

### Snyk
[Snyk](https://snyk.io) is keeping an eye out for vulnerabilities and in our
[npm dependencies](https://snyk.io/test/github/TomerFi/aioswitcher?targetFile=package.json),
our [pypi requirements](https://snyk.io/test/github/TomerFi/aioswitcher?targetFile=requirements.txt).

## Continuous Deployment
### Read the Docs
By hook configuration, [Read the Docs](https://readthedocs.org) will build the documentation site
based on [docs/source](docs/source) and host it:
-   `stable` tag [here](https://aioswitcher.readthedocs.io/en/stable/) will be built for every
    release snapshot.

-   `latest` tag [here](https://aioswitcher.readthedocs.io/en/latest/) will be built for every
    push the dev branch, so it'll reflect unreleased changes.

### PyPI
As for now, I'm not auto-deploying anything to [PyPi](https://pypi.org/).
Packages are being deployed manually.

## Environments and Tools
> **Please Note**: Python, poetry and Tox needs to be pre-installed.

-   [Python](https://www.python.org/), CPython interpreter based, although this package supports
    *Python3.5/3.6/3.7*, *Python3.7* is preferred.

-   [Poetry](https://poetry.eustace.io/) is being used for packaging and dependency management.
    -   Please install [Poetry](https://poetry.eustace.io/docs/#installation) if you plan on
        developing or testing the package.

-   [Tox](https://tox.readthedocs.io/en/latest/) for automating unit testing in your
    local environment.
    -   Please install [Tox](https://tox.readthedocs.io/en/latest/) if you want to perform
        local testing automation.

    -   Tox utilizes Python's [virtualenv](https://pypi.org/project/virtualenv/).

    -   Tox is configured with [pyproject.toml](pyproject.toml).

    -   To run tox, simply execute `tox` from the [pyproject.toml](pyproject.toml)'s path.
        It is recommended that you also run `tox --help` to get familiar with the various options
        such as `-e` and `-r` that will help you perform faster and better tests.

> **Please note**: the rest of the steps require no installation on your behalf,
> but knowing them is important seeing they are key elements for testing with `Tox` and/or `CircleCi`.

-   *Python Module*: [nodeenv](https://pypi.org/project/nodeenv/), a tool that enables us to create
    a Node.js virtual environment in resemblance to [virtualenv](https://pypi.org/project/virtualenv/),
    this tool also allows combining [nodeenv](https://pypi.org/project/nodeenv/) within
    [virtualenv](https://pypi.org/project/virtualenv/), which is exactly what we're doing with
    `tox`.

-   *NPM Package*: [package-json-validator](https://www.npmjs.com/package/package-json-validator)
    for validating the [package.json](package.json) file.

-   *Python Package*: [yamllint](https://pypi.org/project/yamllint/) for linting the project yml
    files.
    -   [yamllint](https://pypi.org/project/yamllint/) is configured with [.yamllint](.yamllint.yml).

-   *NPM Package*: [markdown-spellcheck](https://www.npmjs.com/package/markdown-spellcheck)
    for checking the project *markdown* files for spelling errors.
    -   [markdown-spellcheck](https://www.npmjs.com/package/markdown-spellcheck) dictionary file
        is [.spelling](.spelling).

-   *NPM Package*: [remark-lint](https://www.npmjs.com/package/remark-lint) which is a plugin for
    [remark](https://www.npmjs.com/package/remark) and the [remark-cli](https://www.npmjs.com/package/remark-cli)
    command line tool for linting markdown files residing at the `base path` and in `.github`.
    -   [remark-lint](https://www.npmjs.com/package/remark-lint) uses a couple of presets and tools,
        all can be found under the dependencies key in [package.json](package.json).

    -   [remark-lint](https://www.npmjs.com/package/remark-lint) is configured with [.remarkrc](.remarkrc).

-   *Python Module*: [doc8](https://pypi.org/project/doc8/) for checking restructuredText syntax
    for files residing in [docs/source](docs/source) used to create the documentation site.

-   *Python Module*: [scspell3k](https://pypi.org/project/scspell3k/) for spell checking
    restructuredText files residing in [docs/source](docs/source) used to create the documentation
    site.
    -   [scspell3k](https://pypi.org/project/scspell3k/) dictionary file is [.spelling](.spelling).

-   *Python Module*: [sphinx](https://pypi.org/project/Sphinx/) for building the documentation
    site from the restructuredText files residing in [docs/source](docs/source).
    -   It's worth mentioning that [the documentation site](https://aioswitcher.readthedocs.io/en/stable/),
        hosted with [Read the Docs](https://readthedocs.org) is based upon the theme [sphinx-rtd-theme](https://pypi.org/project/sphinx-rtd-theme/).

-   *Python Package*: [bandit](https://pypi.org/project/bandit/) for finding common security
    issues with against the *Python* files.
    -   [bandit](https://pypi.org/project/bandit/) is configured with [bandit.yml](bandit.yml).

-   *Python Package*: [isort](https://pypi.org/project/isort/) for sorting *Python* imports.
    -   [isort](https://pypi.org/project/isort/) is configured with [pyproject.toml](pyproject.toml).

-   *Python Package*: [flake8](https://pypi.org/project/flake8/) for linting *Python* files.

-   *Python Package*: [black](https://pypi.org/project/black/) for formatting *Python* files.
    -   [black](https://pypi.org/project/black/) is configured with [pyproject.toml](pyproject.toml).

-   *Python Package*: [mypy](https://pypi.org/project/mypy/) for checking static typing in *Python*
    files.

-   *Python Package*: [pytest](https://pypi.org/project/pytest/) as testing framework for running
    test-cases written in [tests](tests).

## Testing
Testing is performed with [Pytest, Full-featured Python testing tool](https://docs.pytest.org/en/latest/).</br>
The various test-cases is in [tests](tests).

For automated local tests, use [Tox](https://tox.readthedocs.io/en/latest/).

## Guidelines
> **Please Note**: the project [semver](https://semver.org/) is handled in both [pyproject.toml](pyproject.toml) and [package.json](package.json).

Here are some guidelines (recommendations) for contributing to the `aioswitcher` project:
-   Code docstrings documentation [here](https://aioswitcher.readthedocs.io/en/stable/codedocs.html)

-   For any change in dependencies, please use [pyscripts/poetry-to-requirements.py](pyscripts/poetry-to-requirements.py)
    for creating a valid [requirements.txt](requirements.txt) file and add it to your PR.
    This is also done automatically with the `py37` testenv in `tox`.

-   While not all the test steps in [CircleCi](.circleci/config.yml) and in
    [Tox](pyproject.toml) are parallel to each other, most of them are, so tests
    failing with `Tox` will probably also fail with `CircleCi`.

-   If writing *Python* code, please remember to [static type](https://www.python.org/dev/peps/pep-0484/).

-   You can run npm's script `spell-md-interactive` for handling all spelling mistakes before
    testing.
    You can also choose to run `spell-md-report` to print a full report instead of handling the
    spelling mistakes one-by-one.
    -   [markdown-spellcheck](https://www.npmjs.com/package/markdown-spellcheck) dictionary is the
        file [.spelling](.spelling).

### NPM Scripts
Before using the scrips, you need to install the dependencies.</br>
From the [package.json](package.json) file path, run `npm install`,
Then you can execute the scripts from the same path.
-   `npm run lint-md` will run [remark](https://remark.js.org/) against *markdown* files.

-   `npm run validate-pkg` will run [package-json-validator](https://www.npmjs.com/package/package-json-validator)
    against the [package.json](package.json) file.

-   `npm run spell-md-interactive` will run [markdown-spellcheck](https://www.npmjs.com/package/markdown-spellcheck)
    against *markdown* files in an interactive manner allowing us to select the appropriate action.

-   `npm run spell-md-report` will run [markdown-spellcheck](https://www.npmjs.com/package/markdown-spellcheck)
    against *markdown* files and print the report to stdout.

## Chat
Feel free to join the project's public
[Slack Channel](https://tomfi.slack.com/messages/CK3KRBYDP).</br>
GitHub is integrated with the channel and keep its members updated.

## Best Practices
This project tries to follow the [CII Best Practices](https://bestpractices.coreinfrastructure.org/en/projects/2889) guidelines.

That's not an easy task and I'm not sure achieving 100% is even possible for this specific
project.</br>
At the time writing this, the project has achieved 14% (The writing of this file was actually
according one to those guidelines).</br>
Any contribution bumping up this percentage will be gladly embraced.

## Code of Conduct
The [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) can also be found
[here](https://aioswitcher.readthedocs.io/en/stable/conduct.html).
