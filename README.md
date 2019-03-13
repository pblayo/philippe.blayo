Commands used by Philippe Blayo

# Setting for a fork in github

To always fetch from the origin and push into the fork, the best setting I've found so far:

```$ git remote -v
origin	https://github.com/IQSS/dataverse.git (fetch)
origin	https://github.com/IQSS/dataverse.git (push)
pblayo	git@github.com:pblayo/dataverse.git (fetch)
pblayo	git@github.com:pblayo/dataverse.git (push)
```


# OpenFisca : turn law into software code

## Local Python environment with pyenv

In my .bashrc, I added at the end:
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

pyenv activate openfisca-core-3.6.7


## Slides' theme used for our demos

https://undraw.co/ & https://www.slidescarnival.com/ : nice Google slides templates for presentations

## Install an Egg locally

pip install --editable git+https://github.com/openfisca/openfisca-core.git@SPECIFIC_BRANCH_NAME#egg=OpenFisca-Core
pip list # (to check that the dependency has been installed successfully

## Debug

Debug with colors (Stop the execution at a specific place in the code and open an interactive console) :
```pip install ipdb```

Then in the location where to put the breakpoint :
```from nose.tools import set_trace
set_trace()
import ipdb
ipdb.set_trace()
```

Then `nosetests core/test_tax_scales.py` from the directory above `tests`
Then `(Pdb) c` in the interactive console to switch from `pdb` to `ipdb`

If you’re using `pytest`, you can add the `-s` option and `import ipdb; ipdb.set_trace()` will work
fpagnoux has a Sublime shortcut to insert this code snippet quickly and use it _a lot_

If you are using this to debug the Web Api, it is convenient to use `openfisca serve -t 0 -w 1`
to disable the timeout and use only one worker.

## Docker

To run a brand new docker on a specific directory like `openfisca-core`, you can run this command: `docker run --rm -it -v $PWD:/openfisca-core -w /openfisca-core python:3.7 bash`

Install manually a recent version of docker : https://fabianlee.org/2017/03/07/docker-installing-docker-ce-on-ubuntu-14-04-and-16-04/
Tested on Ubuntu 14.04 LTS

To install a version as old as 1.13 on a 14.04 LTS : https://docs.docker.com/cs-engine/1.13/
