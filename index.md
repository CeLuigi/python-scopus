---
layout: default
title: "Get Started"
---

### Reference

Please consider citating one or both of our papers below when you use PyScopus:

[1] Zhiya Zuo, Kang Zhao, andd David Eichmann. The State and Evolution of U.S. iSchools -- from Talent Acquisitions to Research Outcome. *Journal of the Association for Information Science and Technology* (JASIST). (*Forthcoming*)

[2] Zhiya Zuo, Xi Wang, David Eichmann, and Kang Zhao. 2016. Research Collaborations in Multidisciplinary Institutions: a Case Study of iSchools. *In Proceedings of the 25th International Conference Companion on World Wide Web* (WWW '16 Companion). International World Wide Web Conferences Steering Committee, Republic and Canton of Geneva, Switzerland, 443-448. DOI=http://dx.doi.org/10.1145/2872518.2890522

### Get Acquinted with Scopus API

Please first refer to [Elsevier Developer Portal](http://dev.elsevier.com/index.html) for detailed information before using this wrapper.

### Download

PyScopus requires:

+ [Python 2.7](https://www.python.org/download/releases/2.7/)

+ [Numpy](http://www.numpy.org/)

+ [Pandas](http://pandas.pydata.org/)

+ [BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/)

##### 1. Using `pip` or `easy_install`

The easiest way of installing PyScopus is to use `pip`:

{%highlight bash%}
$ pip install pyscopus
{%endhighlight%}

 or `easy_install`

{%highlight bash%}
$ easy_install pyscopus
{%endhighlight%}

##### 2. Manual installation

You can also clone and install the project from its <a href="https://github.com/zhiyzuo/python-scopus" target="_blank">GitHub homepage</a> like this:

{%highlight bash%}
$ git clone https://github.com/zhiyzuo/python-scopus.git
$ cd python-scopus/
$ python setup.py install
{%endhighlight%}

A tarball can also be downloaded via PyScopus's <a href="https://pypi.python.org/pypi?name=pyscopus&version=0.7.2.post4&:action=display" target="_blank">PyPI page</a> or <a href="https://github.com/zhiyzuo/python-scopus/tarball/0.7.2.post4" target="_blank">this download link</a>.

{%highlight bash%}
$ tar -xvzf zhiyzuo-python-scopus-0.7.2.post4-0-ge4fd2dd.tar.gz
$ cd zhiyzuo-python-scopus-0.7.2.post4-0-ge4fd2dd/
$ python setup.py install
{%endhighlight%}

And then please start to enjoy the easy scraping of data from Scopus.

