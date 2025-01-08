What is this project ?
----------------------

This repository is **NOT** the official jinja2-action repository.

It is a fork of jinja2-action sources hosted at https://github.com/cuchi/jinja2-action

It is maintained for the following purposes:
1. As a **GitHub Action** referenced from GitHub workflow (see below for usage details)
2. As a **staging area** for patches that may be contributed back to the official repository.

Why maintain this fork ?
------------------------

As of 2025-01-08, the latest version of `cuchi/jinja2-action` broke due to a breaking change introduced
in poetry 2.0. See https://github.com/cuchi/jinja2-action/pull/21

This fork was created to provide the fix originally contributed by [@OlivierCloudar](https://github.com/OlivierCloudar),
ensuring it is associated with a GitHub organization rather than an individual user account.

What is the branch naming convention ?
--------------------------------------

Each branch is named following the pattern `slicer-YYYY-MM-DD-SHA{N}`

where:

* `YYYY-MM-DD` is the date of the last official commit associated with the branch.
* `SHA{N}` are the first N characters of the last official commit associated with the branch.


How to reference this project in GitHub Actions workflows ?
-----------------------------------------------------------

To deterministically check the spelling, it is recommended to reference this GitHub Action
using a syntax similar to the following by using a specific git hash:

```
- uses: Slicer/jinja2-action@2ea7da6d11a44228eec0dc6b1c0bd6322f869798
```


How to update the version of jinja2-action ?
--------------------------------------------

1. Clone this repository and add a remote to the official project

```
git clone git://github.com/Slicer/jinja2-action
cd jinja2-action
git remote add upstream git://github.com/cuchi/jinja2-action
git fetch upstream
```

2. Checkout base to update the `latest`

```
git checkout -b master upstream/master
```

3. Create a new branch following the convention

```
DATE=$(git show -s --format=%ci HEAD | cut -d" " -f1)
echo "DATE [${DATE}]"
SHA=$(git show -s --format=%h HEAD)
echo "SHA [${SHA}]"
BRANCH_NAME=slicer-${DATE}-${SHA}
echo "BRANCH_NAME [${BRANCH_NAME}]"
git checkout -b ${BRANCH_NAME} ${SHA}
```

4. Cherry-pick the commits not yet integrated into upstream from last branch. Resolve conflict as needed.

5. Publish the branch. (directly in this repo if you have push rights, or on a fork asking maintainer to published it here)


How to be granted push rights ?
-------------------------------

Ask on https://discourse.slicer.org/


Questions
---------

If you have questions, see https://discourse.slicer.org/
