gh-fetch-submodules
===================

[GitHub](https://github.com/) automatically creates a release tarball when a version tag gets pushed.
The shortcoming of the feature is that the created tarball does not contain the contents of the submodules.
Some (if not many) tarballs would not work as expected without the the contents of the submodules.

`gh-fetch-submodules` is a tiny script that fixes the problem.
When invoked, it reads `.gitmodules` and uses the [GitHub API](https://developer.github.com/v3/) to fetch and extract the submodules.

In case of [picojson](https://github.com/kazuho/picojson), the script is bundled in the root directory, and a Makefile like the following would automatically fetch the contents of the submodules before the tests are executed.

```
fetch-submodules:
        @if [ ! -e .git ] ; then ./gh-fetch-submodules kazuho/picojson ; fi

test: fetch-submodules
        ...
```
