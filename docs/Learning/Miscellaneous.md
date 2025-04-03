# Miscellaneous

## Module Import in Python

For a package structure as following: 

```
package
├── __init__.py
├── subpackage1
│   ├── __init__.py
│   ├── moduleX.py
│   └── moduleY.py
├── subpackage2
│   ├── __init__.py
│   └── moduleZ.py
└── moduleA.py
```

Assuming you execute the following command under `package`

``` 
1. python subpackage1/moduleX.py   
2. python -m subpackage1.moduleX
```

The first one will import modules from `sys.path`. A `ModuleNotFound` error raises if the desired one is not in `sys.path`. So if `moduleX.py` import function in `moduleZ.py`, it may cause error since the `sys.path` may only contains `xxx/package/subpackage1`

Instead, the second one will first import the desired package or module, then execute the script.