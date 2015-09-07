[![Build Status](https://travis-ci.org/ncclient/ncclient.svg?branch=master)](https://travis-ci.org/ncclient/ncclient)
[![Coverage Status](https://coveralls.io/repos/leopoul/ncclient/badge.svg)](https://coveralls.io/r/leopoul/ncclient)
[![Documentation Status](https://readthedocs.org/projects/ncclient/badge/?version=latest)](https://readthedocs.org/projects/ncclient/?badge=latest)

ncclient: Python library for NETCONF clients
--------------------------------------------

ncclient is a Python library that facilitates client-side scripting
and application development around the NETCONF protocol. `ncclient` was
developed by [Shikar Bhushan](http://schmizz.net). It is now maintained
by [Leonidas Poulopoulos (@leopoul)](http://ncclient.org)

**Docs**: [http://ncclient.readthedocs.org](http://ncclient.readthedocs.org)

**PyPI**: [https://pypi.python.org/pypi/ncclient](https://pypi.python.org/pypi/ncclient)

#### Requirements:
* Python 2.6 <= version < 3.0
* setuptools 0.6+
* Paramiko 1.7+
* lxml 3.0+
* libxml2
* libxslt

If you are on Debian/Ubuntu install the following libs (via aptitude or apt-get):
* libxml2-dev
* libxslt1-dev

#### Installation:

    [ncclient] $ sudo python setup.py install
    
or via pip:

    pip install ncclient

#### Examples:

    [ncclient] $ python examples/juniper/*.py

### Usage
####Get device running config
Use either an interactive Python console (ipython)
or integrate the following in your code:

    from ncclient import manager

    with manager.connect(host=host, port=830, username=user, hostkey_verify=False) as m:
        c = m.get_config(source='running').data_xml
        with open("%s.xml" % host, 'w') as f:
            f.write(c)

As of 0.4.1 ncclient integrates Juniper's and Cisco's forks, lots of new concepts
have been introduced that ease management of Juniper and Cisco devices respectively.
The biggest change is the introduction of device handlers in connection paramms.
For example to invoke Juniper's functions annd params one has to re-write the above with ***device_params={'name':'junos'}***:

    from ncclient import manager

    with manager.connect(host=host, port=830, username=user, hostkey_verify=False, device_params={'name':'junos'}) as m:
        c = m.get_config(source='running').data_xml
        with open("%s.xml" % host, 'w') as f:
            f.write(c)

Device handlers are easy to implement and prove to be futureproof.

####Supported device handlers

* Juniper: device_params={'name':'junos'}
* Cisco CSR: device_params={'name':'csr'}
* Cisco Nexus: device_params={'name':'nexus'}
* Huawei: device_params={'name':'huawei'}


### Changes | brief

* Nexus exec_command operation
* Allow specifying multiple cmd elements in Cisco Nexus
* Update rpc for nested rpc-errors
* Prevent race condition in threading
* Prevent hanging in session close

### Acknowledgements
* v0.4.3: Thanks to all contributors and bug hunters; [Jeremy Schulman](https://github.com/jeremyschulman), [Ray Solomon](https://github.com/rsolomo), [Rick Sherman](https://github.com/shermdog), [subhak186](https://github.com/subhak186)
* v0.4.2: Thanks to all contributors; [katharh](https://github.com/katharh), [Francis Luong (Franco)](https://github.com/francisluong), [Vincent Bernat](https://github.com/vincentbernat), [Juergen Brendel](https://github.com/juergenbrendel), [Quentin Loos](https://github.com/Kent1), [Ray Solomon](https://github.com/rsolomo), [Sebastian Wiesinger](https://github.com/sebastianw), [Ebben Aries](https://github.com/earies) 
* v0.4.1: Many thanks, primarily to [Jeremy Schulman](https://github.com/jeremyschulman) (Juniper) for providing his precious feedback, to [Ebben Aries](https://github.com/earies) (Juniper) for his contribution, to Juergen Brendel (Cisco) for the Cisco fork and to all contributors from Cisco and Juniper.

