---
share: true
uuid: 7ad5ebd2-06f0-4a20-b9c6-20394ebed346
---
#### Description

These notes are created using [Obsidian](https://obsidian.md/) and are stored in [this git repo](https://github.com/Memex-Working-Group/collective-memex) and published using [this one](https://github.com/Memex-Working-Group/pauls-obsidian-publisher-for-memex.mememaps.net). If you would like access to this the raw markdown notes to add to your Obsidian Vault, or to add your own pull requests, please message [[Jordy from mememaps.net|Jordy]], [[Paul Mullins from mememaps.net|Paul Mullins]], or [[Zoravur from mememaps.net|Zoravur]] on the mememaps.net Discord which you can find in [[mememaps.net community links]].

#### Integrating with your existing Git Based Obsidian Vault

``` bash

git submodule add git@github.com:Memex-Working-Group/collective-memex.git

git submodule update --init --recursive

```

**To update the submodule**

pullSubmodule.sh
``` bash
#!/bin/bash
git submodule update --init --recursive
```