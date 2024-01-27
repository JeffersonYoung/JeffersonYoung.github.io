使用Sphinx记录笔记
----------------------

引言
=======
作为第一篇笔记，当然是介绍一下工具的。因为是python用户，对rst比较熟一点，所以选用了sphinx作为工具。
因为是笔记，没有文档那么系统，所以就当作博客托管在GitHub上。

安装Sphinx
===========
.. code:: shell

    pip install sphinx

初始化项目
==========
.. code:: shell

    sphinx-quickstart

- 然后根据提示输入项目名称、作者、版本号、语言等信息。
- 为了更好地管理文件，在 `Separate source and build directories (y/n) [n]` （是否将源码和编译后的文件分开）中一般会选择 y
- 语言选择简体中文的话输入 ``zh_CN``
- 项目名称、作者、版本号就随意

项目初始化之后，文件夹将具有以下结构：
    .. code::

        .
        ├── build/              生成文件的目录
        ├── Makefile            编译脚本, linux 编译时用
        ├── make.bat            Windows 的编译脚本
        └── source/             存放文档源文件
            ├── conf.py         Sphinx 的配置文件
            ├── index.rst       文档的入口
            ├── _static/        静态文件目录，比如图片等
            └── _templates/     模板目录

编译
======

初始化项目后，在该项目的根目录下运行 ``make html`` 就可以生成最基本的静态页面样板，生成的结果可以在 build/html/index.html 中查看。


更改样式主题
============

选择主题
`````````

Sphinx 的默认主题是 alabaster, `Sphinx的官网 <https://sphinx-themes.org>`_ 提供其他主题。
在官网上的主题会提供安装指南。Read the Docs 是一个常用的主题，我们以它为例子介绍一下安装过程

下载
```````
.. code:: shell

    pip install sphinx_rtd_theme

修改配置文件
`````````````

下载完成后，在配置文件 ``source/conf.py`` 中将 ``html_theme`` 修改为 ``sphinx_rtd_theme``
    .. code:: python

        # html_theme = 'alabaster'
        html_theme = 'sphinx_rtd_theme'

.. admonition:: 注意

    主题名称中使用下划线而不是连字符


Bootstrap 主题
```````````````````

Read the Docs 通常是软件的说明文档，对于博客来说不是很适合。
本文使用的是 ``bootstrap`` 主题，安装方法与上文中提到的 ``sphinx-rtd-theme`` 有一定差异，下面简单介绍

下载
~~~~~~

与 ``sphinx-rtd-theme`` 相仿
    .. code:: shell

        pip install sphinx-bootstrap-theme

下载完成后，配置文件需要修改为
    .. code:: python

        # html_theme = 'alabaster'
        
        import sphinx_bootstrap_theme
        html_theme = 'bootstrap'
        html_theme_path = sphinx_bootstrap_theme.get_html_theme_path()

部署
========

可以参考 https://zhuanlan.zhihu.com/p/28321740

为了将项目展示到GitHub上，需要将输出的文件放置在根目录下或者 ``docs`` 目录下。
Windows上可以在 ``make.bat`` 末尾添加以下代码实现

.. code:: 

    del /q /s docs
    xcopy build\html docs /e

.. 这样做欠妥，考虑合理一点的做法

在GitHub上部署时，为了正常显示 ``_`` 开头的文件和目录，需要在根目录和 ``docs`` 目录下添加空白文件 ``.nojekyll`` 。

.. admonition:: 注意

    如果没有 ``.nojekyll`` 文件，静态资源将不能正常显示，因为默认状态下它们会存放在 ``docs/_static`` 目录下

Reference
============

1. https://zhuanlan.zhihu.com/p/384863296?utm_id=0
2. https://chunyu.site/sphinx/
3. https://zhuanlan.zhihu.com/p/618869114
