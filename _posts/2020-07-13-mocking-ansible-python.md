---
layout: post
title: "Isolating the Network Role: How to mock the Ansible runtime"
tags: gsoc linux-system-roles floss
author:
- Elvira G.
meta: "GSOC"
---

My main task in the GSoC project is to add Pytest to the Network Role at Linux
System Roles. This will lead to a better coverage of tests, since all the
utilities of pytest will be available for testing the module, instead of being
limited to the execution from a playbook. This does not mean that playbooks
will not be used anymore (it is still useful to see how Ansible reacts to the
different tasks!), it means that a more in-depth testing will be possible.

In order to achieve this, I had to mock some objects. This is necessary because
the module is meant to be executed only from Ansible, and thus some
dependencies go missing. Furthermore, the available system paths also change
depending on where you execute the module from, so it was also necessary to
mock this attribute.

## The code

```
 with mock.patch.object(                                                         
     sys,                                                                        
     "path",                                                                     
     [parentdir, os.path.join(parentdir, "module_utils/network_lsr")] + sys.path,
 ):                                                                              
     with mock.patch.dict(                                                       
         "sys.modules",                                                          
         {"ansible": mock.Mock(), "ansible.module_utils": __import__("module_utils")},
     ):                                                                          
         import library.network_connections as nc 
```

### Changing sys.path 

Thanks to the [mock object
library](https://docs.python.org/3/library/unittest.mock.html#module-unittest.mock),
patching the value of an attribute from the object we need (in this case,
`sys.path`) is not a difficult task, using
[`patch.object`](https://docs.python.org/3/library/unittest.mock.html#patch-object).
This function can take up to three arguments: 
1. The object to be patched, (`sys`)
2. the attribute that we want to change, (`path`)
3. and the object used to replace the current value of the attribute.

The object to that will be used is a list consisting of the current `sys.path`
but adding the main directory of the project and the `module_utils/network_lsr`
folder. This last folder is the one that is  usually imported through Ansible
instead of locally, but since we need to execute the project directly from
Python, we need a workaround.

### Using mock modules

Similarly to the previous description, now that we have network_lsr in the path
we want to import it in a way that the module thinks it's from the Ansible
library. This time, we use
[`mock.patch.dict`](https://docs.python.org/3/library/unittest.mock.html#patch-dict)
to patch `sys.modules`. Ansible gets imported as a Mock object and
`ansible.module_utils` as `module_utils`.  

_(Note that we can import module_utils thanks to the path workaround we did
before.)_

### Importing the library

Thanks to the previous mocking, everything is ready to import the Network Role.
Once it is imported, we can alreadycreate a custom RunEnvironment for the
testing and therefore running tests without the need of executing them from
Ansible.

