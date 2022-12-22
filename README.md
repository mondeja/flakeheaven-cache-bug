# Cache bug in flakeheaven

## How to reproduce (Unix)

```
python3 -m virtualenv venv
. venv/bin/activate
pip install -r requirements.txt

# the next command will fail
flakeheaven lint file.py
# so change the configuration to make it pass
sed -i s/false/true/ pyproject.toml
# and run it again, doesn't work
flakeheaven lint file.py

# but if you disable the cache, it works
pysetenv FLAKEHEAVEN_CACHE_TIMEOUT=0 flakeheaven lint file.py
```

Perhaps the cache is not invalidated when the configuration of
*pyproject.toml* changes?
