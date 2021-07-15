# GitHub-Action-Ahk2Exe

GitHub Action to compile AutoHotKey scripts using Ahk2Exe

## ⚠️ Precautions for use

Be sure to use Windows as the hosted runner. Otherwise, it will not work.

## ✍ Inputs

The following are the parameters for `step.with`.
Name|Type|Required|Description
-|-|-|-
in|String|True|The path or file name of the AutoHotKey script to compile
out|String|False|The path or file name of the compiled executable (by default, an executable of the same name will be created in the path of the AutoHotKey script specified by the "in" parameter)
icon|String|False|The icon of the executable file is specified

## 📦 Example usage

The following usage example will create a compiled executable of the same name in the path of the AutoHotKey script.

```yaml
name: Example usage of GitHub-Action-Ahk2Exe

on: push

jobs:
  Example:
    name: Example
    runs-on: windows-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Ahk2Exe
        uses: nekocodeX/GitHub-Action-Ahk2Exe@v1
        with:
          in: example.ahk
```

For example, by using [softprops/action-gh-release](https://github.com/marketplace/actions/gh-release), you can take advantage of the compiled executable created above.

```yaml
name: Example usage of GitHub-Action-Ahk2Exe and softprops/action-gh-release

on: push

jobs:
  Example2:
    name: Example2
    runs-on: windows-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Ahk2Exe
        uses: nekocodeX/GitHub-Action-Ahk2Exe@v1
        with:
          in: example.ahk

      - name: Release
        uses: softprops/action-gh-release@v1
        if: startsWith(github.ref, 'refs/tags/')
        with:
          files: example.exe
        env:
          GITHUB_TOKEN: ${{secrets.GITHUB_TOKEN}}
```
