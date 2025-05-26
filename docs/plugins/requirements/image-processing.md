---
icon: material/image-sync-outline
---

# 图像处理

一些[内置插件]依赖于外部库来进行高效的图像处理，最显著的是用于生成[社交卡片]的[social]插件，以及用于[图像优化]的[optimize]插件。本指南解释了如何在不同环境中安装这些库。

  [built-in plugins]: ../index.md
  [social]: ../social.md
  [social cards]: ../../setup/setting-up-social-cards.md
  [optimize]: ../optimize.md
  [image optimization]: ../../setup/building-an-optimized-site.md

## 依赖项

图像处理库完全是可选的，只有在您想使用[social]插件或[optimize]插件时才需要安装。这些库列在 `imaging` 额外选项中：

```
pip install "mkdocs-material[imaging]"
```

这将安装以下包的兼容版本：

- [Pillow]
- [CairoSVG]

  [Pillow]: https://pillow.readthedocs.io/
  [CairoSVG]: https://cairosvg.org/

### Cairo Graphics

[Cairo Graphics]是一个图形库，也是[Pillow]的依赖项，Material for MkDocs 使用它来生成[社交卡片]和执行[图像优化]。请参阅以下部分，了解如何在您的系统上安装[Cairo Graphics]及其依赖项：

=== ":material-apple: macOS"

    确保已安装[Homebrew]，这是一个现代化的 macOS 包管理器。接下来，使用以下命令安装所有必要的依赖项：

    ```
    brew install cairo freetype libffi libjpeg libpng zlib
    ```

=== ":fontawesome-brands-windows: Windows"

    在 Windows 上使用[Cairo Graphics]库最简单的方法是通过[MSYS2]安装，这是一个 Windows 的软件分发和构建平台。在 MSYS2 shell 中运行以下命令：

    ```
    pacman -S mingw-w64-ucrt-x86_64-cairo
    ```

    MSYS2 在几个不同的环境中提供 Cairo Graphics 库。上述命令使用[UCRT64]环境，这是 MSYS2 开发人员推荐的环境。

=== ":material-linux: Linux"

    Linux 有多个包管理器，每个发行版的可用性各不相同。[安装指南]解释了如何为您的发行版安装[Cairo Graphics]库：

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

以下环境已预装[Cairo Graphics]：

- [x] [Docker 镜像]中无需安装
- [x] [GitHub Actions]（Ubuntu）中无需安装

  [Cairo Graphics]: https://www.cairographics.org/
  [Homebrew]: https://brew.sh/
  [installation guide]: https://www.cairographics.org/download/
  [MSYS2]: https://www.msys2.org/
  [UCRT64]: https://www.msys2.org/docs/environments/
  [Docker image]: https://hub.docker.com/r/squidfunk/mkdocs-material/
  [GitHub Actions]: ../../publishing-your-site.md#with-github-actions

### pngquant

[pngquant]是一个优秀的无损 PNG 压缩库，是[内置优化插件]的直接依赖项。请参阅以下部分，了解如何在您的系统上安装[pngquant]：

=== ":material-apple: macOS"

    确保已安装[Homebrew]，这是一个现代化的 macOS 包管理器。接下来，使用以下命令安装所有必要的依赖项：

    ```
    brew install pngquant
    ```

=== ":fontawesome-brands-windows: Windows"

    在 Windows 上获取[pngquant]最简单的方法是通过[MSYS2]安装，这是一个 Windows 的软件分发和构建平台。在 MSYS2 shell 中运行以下命令：

    ```
    pacman -S mingw-w64-ucrt-x86_64-pngquant
    ```

=== ":material-linux: Linux"

    所有流行的 Linux 发行版，无论使用什么包管理器，都应该允许使用捆绑的包管理器安装[pngquant]。例如，在 Ubuntu 上，可以使用以下命令安装[pngquant]：

    ```
    apt-get install pngquant
    ```

    对于 `yum` 和 `zypper` 也是如此。

以下环境已预装[pngquant]：

- [x] [Docker 镜像]中无需安装

  [pngquant]: https://pngquant.org/
  [built-in optimize plugin]: ../../plugins/optimize.md
  [pngquant-winbuild]: https://github.com/jibsen/pngquant-winbuild

## 故障排除

### 未找到 Cairo 库

按照上述安装指南操作后，您可能仍然会遇到以下错误：

```bash
no library called "cairo-2" was found
no library called "cairo" was found
no library called "libcairo-2" was found
cannot load library 'libcairo.so.2': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo.so.2'
cannot load library 'libcairo.2.dylib': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo.2.dylib'
cannot load library 'libcairo-2.dll': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo-2.dll'
```

这意味着[`cairosvg`][PyPi CairoSVG]包已安装，但底层的[`cairocffi`][PyPi CairoCFFI]依赖项无法[找到][cffi-dopen]已安装的库。根据操作系统的不同，库查找过程也不同：

!!! tip
    在继续之前，请记住完全重启任何打开的终端窗口及其父主机（如 IDE），以重新加载在安装过程中更改的任何环境变量。这可能就是快速解决方案。

=== ":material-apple: macOS"

    在 macOS 上，库查找会检查[dyld][osx-dyld]中定义的路径。此外，每个库`name`都会以`libname.dylib`、`name.dylib`和`name.framework/name`格式[检查三个变体][find-library-macOS]。

    [Homebrew]应该设置每个需要的变量指向已安装的库目录，但如果这没有发生，您可以使用下面的调试脚本来查看查找了哪些路径。

    一个[已知的解决方法][cffi-issue]是在运行 MkDocs 之前直接添加 Homebrew lib 路径：

    ```bash
    export DYLD_FALLBACK_LIBRARY_PATH=/opt/homebrew/lib
    ```

    查看[cairo-lookup-macos.py]的源代码

    ```bash title="Python Debug macOS Script"
    curl "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-macos.py" | python -
    ```

=== ":fontawesome-brands-windows: Windows"

    在 Windows 上，库查找会检查环境`PATH`变量中定义的路径。此外，每个库`name`都会以`name`和`name.dll`格式[检查两个变体][find-library-Windows]。

    使用上述命令安装包的[MSYS2]的[UCRT64]环境的默认二进制文件和共享库路径是：

    ```powershell
    C:\msys64\ucrt64\bin
    ```

    使用下面的调试脚本检查是否包含该路径。如果没有，则：

    1. 按 ++windows+r++。
    2. 运行`SystemPropertiesAdvanced`小程序。
    3. 在底部选择"环境变量"。
    4. 将上述目录的完整路径添加到您的`Path`变量中。
    5. 在所有打开的窗口上点击确定以应用更改。
    6. 完全重启任何打开的终端窗口及其父主机（如 IDE）。

    ```powershell title="您也可以使用 PowerShell 列出路径"
    $env:Path -split ';'
    ```

    查看[cairo-lookup-windows.py]的源代码

    ```powershell title="PowerShell - Python Debug Windows Script"
    (Invoke-WebRequest "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-windows.py").Content | python -
    ```

=== ":material-linux: Linux"

    在 Linux 上，库查找[差异很大][find-library-Linux]，并且取决于已安装的发行版。对于测试过的 Ubuntu 和 Manjaro 系统，Python 运行 shell 命令来检查[`ldconfig`][ubuntu-ldconfig]、[`gcc`][ubuntu-gcc]/`cc`编译器和[`ld`][ubuntu-ld]中可用的库。

    您可以使用包含`libcairo.so`等的库目录的绝对路径扩展`LD_LIBRARY_PATH`环境变量。在运行 MkDocs 之前直接运行：

    ```bash
    export LD_LIBRARY_PATH=/absolute/path/to/lib:$LD_LIBRARY_PATH
    ```

    您也可以修改`/etc/ld.so.conf`文件。

    下面的 Python 脚本显示了正在运行哪个函数来查找已安装的库。您可以查看源代码以了解正在运行的具体命令。

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
