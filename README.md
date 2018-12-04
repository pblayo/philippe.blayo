# Commands used by Philippe Blayo

## OpenFisca : turn law into software code

https://undraw.co/ & https://www.slidescarnival.com/ : nice Google slides templates for presentations

### Install an Egg locally

pip install --editable git+https://github.com/openfisca/openfisca-core.git@SPECIFIC_BRANCH_NAME#egg=OpenFisca-Core
pip list # (to check that the dependency has been installed successfully

### Debug

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
