---
icon: material/image-sync-outline
---

# 图像处理

一些[内置插件]依赖于外部库来获得高效的图像
处理，最值得注意的是生成[社交卡]的[社交]插件，以及
用于应用[图像优化]的[optimization]插件。本指南解释了如何
在不同的环境中安装这些库。

  [built-in plugins]: ../index.md
  [social]: ../social.md
  [social cards]: ../../setup/setting-up-social-cards.md
  [optimize]: ../optimize.md
  [image optimization]: ../../setup/building-an-optimized-site.md

## 依赖关系

用于图像处理的库是完全可选的，只需要
如果你想使用[社交]插件或[优化]插件，请安装。这个
库列在“图像”附加项下：

```
pip install "mkdocs-material[imaging]"
```

这将安装以下软件包的兼容版本：

- [Pillow]
- [CairoSVG]

  [Pillow]: https://pillow.readthedocs.io/
  [CairoSVG]: https://cairosvg.org/

### 开罗图形

[Cairo Graphics]是[Phillow]的图形库和依赖项
MkDocs的材料用于生成[社交卡]和执行
[图像优化]。请参阅以下部分，了解如何安装
[Cairo Graphics]及其对您系统的依赖性：

=== ":material-apple: macOS"

    Make sure [Homebrew] is installed, which is a modern package manager for
    macOS. Next, use the following command to install all necessary
    dependencies:

    ```
    brew install cairo freetype libffi libjpeg libpng zlib
    ```

=== ":fontawesome-brands-windows: Windows"

    The easiest way to get up and running with the [Cairo Graphics] library is
    by installing it via [MSYS2], which is a software distribution and building
    platform for Windows. Run the following command inside of a MSYS2 shell:

    ```
    pacman -S mingw-w64-ucrt-x86_64-cairo
    ```

    MSYS2 provides the Cairo Graphics library in several different environments.
    The above command uses the [UCRT64] environment, as recommended by the MSYS2
    developers.

=== ":material-linux: Linux"

    There are several package managers for Linux with varying availability per
    distribution. The [installation guide] explains how to install the [Cairo
    Graphics] library for your distribution:

    === ":material-ubuntu: Ubuntu"

        ```
        apt-get install libcairo2-dev libfreetype6-dev libffi-dev libjpeg-dev libpng-dev libz-dev
        ```

    === ":material-fedora: Fedora"

        ```
        yum install cairo-devel freetype-devel libffi-devel libjpeg-devel libpng-devel zlib-devel
        ```

    === ":fontawesome-brands-suse: openSUSE"

        ```
        zypper install cairo-devel freetype-devel libffi-devel libjpeg-devel libpng-devel zlib-devel
        ```

以下环境附带了预装的[Caroo Graphics]版本：

- [x] No installation needed in [Docker image]
- [x] No installation needed in [GitHub Actions] (Ubuntu)

  [Cairo Graphics]: https://www.cairographics.org/
  [Homebrew]: https://brew.sh/
  [installation guide]: https://www.cairographics.org/download/
  [MSYS2]: https://www.msys2.org/
  [UCRT64]: https://www.msys2.org/docs/environments/
  [Docker image]: https://hub.docker.com/r/squidfunk/mkdocs-material/
  [GitHub Actions]: ../../publishing-your-site.md#with-github-actions

### pngquant

[pngquant]是一个优秀的有损PNG压缩库
[内置优化插件]的依赖关系。请参阅以下部分
解释了如何安装[pngquant]系统：

=== ":material-apple: macOS"

    Make sure [Homebrew] is installed, which is a modern package manager for
    macOS. Next, use the following command to install all necessary
    dependencies:

    ```
    brew install pngquant
    ```

=== ":fontawesome-brands-windows: Windows"

    The easiest way to get [pngquant] is by installing it via [MSYS2], which is
    a software distribution and building platform for Windows. Run the following
    command inside of a MSYS2 shell:

    ```
    pacman -S mingw-w64-ucrt-x86_64-pngquant
    ```

=== ":material-linux: Linux"

    All popular Linux distributions, regardless of package manager, should
    allow to install [pngquant] with the bundled package manager. For example,
    on Ubuntu, [pngquant] can be installed with:

    ```
    apt-get install pngquant
    ```

    The same is true for `yum` and `zypper`.

以下环境预装了[pngquant]版本：

- [x] No installation needed in [Docker image]

  [pngquant]: https://pngquant.org/
  [built-in optimize plugin]: ../../plugins/optimize.md
  [pngquant-winbuild]: https://github.com/jibsen/pngquant-winbuild

## 故障排除

### 找不到开罗图书馆

按照上面的安装指南进行操作后，可能会出现以下情况：
以下错误：

```bash
no library called "cairo-2" was found
no library called "cairo" was found
no library called "libcairo-2" was found
cannot load library 'libcairo.so.2': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo.so.2'
cannot load library 'libcairo.2.dylib': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo.2.dylib'
cannot load library 'libcairo-2.dll': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo-2.dll'
```

这意味着安装了[`cairosvg`][PyPi-cairosvg]包，但
基础[`cairocffi`][PyPi-cairocffi]依赖项无法[找到][cffi dopen]
已安装的库。根据操作系统，库查找
过程不同：

!!! tip
    在继续之前，请记住完全重新启动任何打开的终端窗口，以及
    它们的父主机像IDE一样重新加载任何环境变量，这
    在安装过程中被更改。这可能是快速解决方案。

=== ":material-apple: macOS"

    在macOS上，库查找会检查[dyld][osx-dyld]中定义的路径内部。
    此外，每个库“名称”都在[三个变体][查找库macOS]中检查
    使用`libname.dylib`、`name.dylib `和`name.framework/name`格式。

    [Homebrew]应将所有需要的变量设置为指向已安装的
    库目录，但如果没有发生这种情况，您可以使用调试脚本
    下面查看查找的路径。

    一个[已知的解决方法][cffi问题]是直接添加Homebrew库路径
    在运行MkDocs之前：

    ```bash
    export DYLD_FALLBACK_LIBRARY_PATH=/opt/homebrew/lib
    ```

    查看[cairo lookup macos.py的源代码]

    ```bash title="Python Debug macOS Script"
    curl "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-macos.py" | python -
    ```

=== ":fontawesome-brands-windows: Windows"

    在Windows上，库查找检查中定义的路径内部
    环境变量“PATH”。此外，还会检查每个库的“名称”
    在[两种变体][查找库窗口]中，使用“name”和“name.dll”格式。

    [UCRT64]环境的默认二进制和共享库路径
    [MSYS2]是使用上述命令安装软件包的：

    ```powershell
    C:\msys64\ucrt64\bin
    ```

    使用下面的调试脚本检查是否包含路径。如果不是，那么：

    1. 按++窗口+r++。
    2. 运行“SystemPropertiesAdvanced”小程序。
    3. 选择底部的“环境变量”。
    4. 将上述目录的整个路径添加到“path”变量中。
    5. 在所有打开的窗口上单击“确定”以应用更改。
    6. 完全重新启动任何打开的终端窗口及其父主机，如IDE。

    ```powershell title="You can also list paths using PowerShell"
    $env:Path -split ';'
    ```

    查看[cairo查找窗口.py]的源代码

    ```powershell title="PowerShell - Python Debug Windows Script"
    (Invoke-WebRequest "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-windows.py").Content | python -
    ```

=== ":material-linux: Linux"

    在Linux上，库查找可以[差异很大][查找库Linux]
    取决于已安装的分发。适用于经过测试的Ubuntu和Manjaro
    系统Python运行shell命令来检查哪些库在
    在[`gcc][ubuntu-gcc]/`cc`编译器中的[`ldconfig][ubuntu ldconfig]，以及
    在[ld][ubuntu-ld]中。

    您可以使用绝对值扩展“LD_LIBRARY_PATH”环境变量
    包含“libcairo.so”等的库目录的路径。直接运行此命令
    在MkDocs之前：

    ```bash
    export LD_LIBRARY_PATH=/absolute/path/to/lib:$LD_LIBRARY_PATH
    ```

    您还可以修改`/etc/ld.so.conf`文件。

    下面的Python脚本显示了正在运行哪个函数来查找已安装
    图书馆。您可以查看源代码以了解具体命令是什么
    在库查找期间在您的系统上执行。

    查看[cairo-lookup linux.py的源代码]

    ```bash title="Python Debug Linux Script"
    curl "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-linux.py" | python -
    ```

  [PyPi CairoSVG]: https://pypi.org/project/CairoSVG
  [PyPi CairoCFFI]: https://pypi.org/project/CairoCFFI
  [osx-dyld]: https://www.unix.com/man-page/osx/1/dyld/
  [ubuntu-ldconfig]: https://manpages.ubuntu.com/manpages/focal/en/man8/ldconfig.8.html
  [ubuntu-ld]: https://manpages.ubuntu.com/manpages/xenial/man1/ld.1.html
  [ubuntu-gcc]: https://manpages.ubuntu.com/manpages/trusty/man1/gcc.1.html
  [cffi-issue]: https://github.com/squidfunk/mkdocs-material/issues/5121
  [cffi-dopen]: https://github.com/Kozea/cairocffi/blob/f1984d644bbc462ef0ec33b97782cf05733d7b53/cairocffi/__init__.py#L24-L49
  [find-library-macOS]: https://github.com/python/cpython/blob/4d58a1d8fb27048c11bcbda3da1bebf78f979335/Lib/ctypes/util.py#L70-L81
  [find-library-Windows]: https://github.com/python/cpython/blob/4d58a1d8fb27048c11bcbda3da1bebf78f979335/Lib/ctypes/util.py#L59-L67
  [find-library-Linux]: https://github.com/python/cpython/blob/4d58a1d8fb27048c11bcbda3da1bebf78f979335/Lib/ctypes/util.py#L92
  [cairo-lookup-macos.py]: https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-macos.py
  [cairo-lookup-windows.py]: https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-windows.py
  [cairo-lookup-linux.py]: https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-linux.py
