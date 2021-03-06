<!--
{% comment %}
Copyright 2018-2021 IBM Corporation

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}
-->

# Making a release

We are using the bumpversion (more specifically bump2version active fork) to help with
some updates during the release steps.

* Update the release version (e.g. 0.1.0)

```bash
bump2version release
sed -i'.bak' -e 's/master/0.5.0/g' notebook/pipeline/_notebook_op.py
rm notebook/pipeline/_notebook_op.py.bak
git commit -a -m"Airflow Notebook release 0.1.0"
git tag v0.1.0
```

Note: Use `bump2version suffix` when releasing from a `dev` suffixed version.

* Build the release artifacts

```bash
make clean dist
twine upload --sign --repository ibm dist/*
```

Note: the repository **ibm** should be a valid section in the config file (~/.pypirc)

* Preparing to the next development iteration

```bash
bump2version minor
git commit -a -m"Prepare for next development iteration"
```
