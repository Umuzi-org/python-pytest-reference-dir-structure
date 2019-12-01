# Python and Pytest folder structure

This reference repo is based on http://doc.pytest.org/en/latest/goodpractices.html. The practice described in this repo is a recognised best practice, and it makes certain auto-marking automations easier if ollowed consistently.

## Directory structure

```
├── my_package          the package under test
│   └── thingy.py       you can put submodules and subpackages here
├── README.md           hi there
├── requirements.txt    installation requiremnts
├── setup.py            installation script for the package under test
└── tests               all package tests go in this directory
    └── test_thingy.py  maybe you'll want to test lots of thingies, use this directory to test all your thingies
```

Notice that the setup.py script mentions `my_package`. Make sure that it mentioned the right package when you follow this procedure.

## Usage

First you'll want to install your package in development mode. Ideally you'll be installing this in a virtualenv.

```
python setup.py develop
```

What this does is legit install your package. So now you can import your package from anywhere so long as your venv is active.

Now to run your tests just type `pytest`. Yay, green light.

Now look at the `test_thingie.py`. Things to notice:

- the perfectly normal way we import the thingie under test
- the complete lack of `sys.path` wrangling

## What do the tests run against?

Ok, this part is a little unusual. Basically the tests are running against the installed package. So if you had a different package named my_package installed then the tests would run against that.

When you install a package in development mode, as we did with `python setup.py install develop` then it means that the installed package links to your py files. So if you edit your files then the installed version of the package effectively gets updated automatically.

As an aside, if you were to just install your package with `python setup.py install` then that would also install your package but it wouldn't be in development mode, so if you edit `thingy.py` then you would have to re-install it if you wanted the changes to reflect in the installed package.
