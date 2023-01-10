---
layout: post
title: "URLExtract - introduction"
categories: urlextract
tags: urlextract basics
---

Using [urlextract](https://github.com/lipoja/URLExtract) should be straightforward.
In this article I would like to describe the basics of using URLExtract as a library in your project.
First we have to be sure we are using the latest version. It can be easily installed from PyPI using:
```bash
pip install urlextract
```

[![PyPI](https://img.shields.io/pypi/v/urlextract)](https://pypi.org/project/urlextract/)

## How to start?

To use URLExtract in our code we have to import it first and then initialize object with `URLExtract()`.
Let's call the object `extractor`.

```python
from urlextract import URLExtract
extractor = URLExtract()
```

During initialization a list of TLDs is loaded and prepared for matching.
If it is first run and temp directory is writable then URLExtracts downloads
the latest list of TLDs directly from IANA.org site.

