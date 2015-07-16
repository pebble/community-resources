---
name: pBuild Travis CI Build Tool
creator: Stefano Gerli
link: http://pbuild.igerli.com
---
**pBuild** is a open source Travis CI build tool for Pebble SDK. It helps developers that use the Pebble SDK to test their apps in Travis CI.

How does pBuild works
---------------------
1. pBuild installs all of the Pebble SDK dependencies in Travis CI
2. Then it fetches the SDK from Pebble download servers based on the version you chose to download.
3. Next the SDK gets installed in Travis CI
4. Finally your app gets built, if it fails Travis CI detects it and if it builds succesfully Travis detects a pass.
