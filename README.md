Make Theano compatible with Python3.12.

For versioneer.py line 334-347
```python
# configparser.NoOptionError (if it lacks "VCS="). See the docstring at
# the top of versioneer.py for instructions on writing your setup.cfg .
setup_cfg = os.path.join(root, "setup.cfg")
#parser = configparser.SafeConfigParser()   SafeConfigParser nolonger used in Python3.12
parser = configparser.ConfigParser()
with open(setup_cfg, "r") as f:
	#parser.readfp(f)
	parser.read_file(f)
VCS = parser.get("versioneer", "VCS")  # mandatory

def get(parser, name):
```

For theano/configparser.py line75-89  
```python
config_files = config_files_from_theanorc()
theano_cfg = (ConfigParser.ConfigParser if PY3
			#else ConfigParser.SafeConfigParser)(
            else ConfigParser.ConfigParser)(
    {'USER': os.getenv("USER", os.path.split(os.path.expanduser('~'))[-1]),
     'LSCRATCH': os.getenv("LSCRATCH", ""),
     'TMPDIR': os.getenv("TMPDIR", ""),
```
