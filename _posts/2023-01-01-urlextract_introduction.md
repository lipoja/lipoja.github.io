---
layout: post
title: "URLExtract - introduction"
date: 2023-01-01 08:00:00 +0100
categories: urlextract
tags: urlextract basics
---

Let me introduce you [urlextract](https://github.com/lipoja/URLExtract). Small
python class/library and command line interface which can be used for collecting
(extracting) URLs from given text based on locating TLD.

The latest version can be easily installed using:
```bash
pip install urlextract
```

[![PyPI](https://img.shields.io/pypi/v/urlextract)](https://pypi.org/project/urlextract/)

## regex vs urlextract

To write one regular expression that will cover all formats of URL is impossible.
For example this regex covers only few cases:
```
(http|ftp|https):\/\/([\w_-]+(?:(?:\.[\w_-]+)+))([\w.,@?^=%&:\/~+#-]*[\w@?^=%&\/~+#-])
```

I did not come across any regex that finds URLs which does not have standard schema.
And it is pretty hard to create regex that will match domain only. For example: `example.com`

That was the main reason I've created [URLExtract](https://github.com/lipoja/URLExtract).
It is able to find and extract URLs, emails or IPv4 addresses with only three lines of code.
```python
from urlextract import URLExtract
extractor = URLExtract()
urls = extractor.find_urls("Text with URLs. Let's have URL janlipovsky.cz as an example.")
print(urls) # prints: ['janlipovsky.cz']
```

## How URLs are found by urlextract?

URLExtract tries to find any occurrence of top level domain (TLD) in given text.
[List of top level domains](https://www.iana.org/domains/root/db) is updated
and can be synced from IANA. When TLD is found urlextract starts from that position
to expand boundaries to both sides searching for "stop character"
(usually whitespace, comma, single or double quote).

### Example

> Let's imagine that this is our input text with example.com as URL.

URLExtract have list of all TLDs and tries to find any occurrence in text.
In our example `.com` TLD will be matched and its coordinates will be saved.

Then urlextract will start checking characters on left and right side of `.com` TLD.
When the character on left or right is in the list of stop characters urlextract stops
expanding on that side, and it marks this position as starting or ending resp.

In our example next character on the right from `.com` is `' '` (space) which is
in the list of right stop characters. URLextract marks this position as end position.
However on the left side URLextract goes through the text and checks
all characters one by one: `e, l, p, m, a, x, e, ' '`. Once it hits the space
and confirms that it is in the list of left stop characters it marks this position
as starting position. Finally, everything in between **start** and **end** position
is found URL that is returned to user.


## Use urlextract in your project

URLExtract is not just a class, it has many more features which I will cover
in next posts. In the meantime try to use it in your project.
[Create an issue](https://github.com/lipoja/URLExtract/issues) if you find any
or pick one and help with maintenance.

Thank you and see you around!
