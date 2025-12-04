# databricks-assetbundle

#### installation
https://docs.databricks.com/aws/en/dev-tools/cli/install

#### config file and command
```sh
~/.databrickscfg
databricks configure
```
- config file example
```sh
cat ~/.databrickscfg                                                                                                                                                                              1 ↵
# The profile defined in the DEFAULT section is to be used as a fallback when no profile is explicitly specified.
[DEFAULT]

[databricks-playground]
host  = https://dbc-dec...dswe.cloud.databricks.com/
token = dap......

[eurostar-dev]
host  = https://adb-....95.15.azuredatabricks.net/
token = dap.......
```

#### virtual enev
```sh
python3.11 -m venv .venv_dab
source .venv_dab/bin/activate
pip install --upgrade pip
pip list
pip install databricks-connect==15.1
pip install uv
pip freeze > requirements.txt
pip install -r requirements.txt
deactivate
```

#### Databricks CLI
```sh
# Databricks Right Version
which -a databricks # find all versions
/usr/local/bin/databricks -v # select one
export PATH="/usr/local/bin:$PATH" # set this version
databricks -v / --version
databricks -h / --help

# Authenticate
databricks configure -h
databricks configure --host https://dbc-26546341-69b4.cloud.databricks.com/ --profile databricks-playground
databricks auth profiles
databricks auth describe --profile databricks-playground

# To Modify
nano ~/.databrickscfg # edit config file
databricks auth profiles # show profiles

# Bundle
databricks bundle -h
cd citibike_dab
databricks bundle summary --profile databricks-playground # show location where bundle will be deployed
databricks bundle validate --profile databricks-playground # setup bundle .toml file
databricks bundle deploy --profile databricks-playground # deploy the bundle
databricks bundle deploy --target stg --profile databricks-playground # deploy to specific enev, based on databricks.yml
databricks bundle deploy --target prod --profile databricks-playground
databricks bundle destroy --target prod --profile databricks-playground # delete all resources, jobs, etc..
```
