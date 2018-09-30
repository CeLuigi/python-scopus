---
layout: default
title: "Get Started"
---

#### Last updated 09-29-2018

### NEW!!!
I just upload my workaround for cleaning mixed author profile. See [___Diambiguity Workaround___](doc/disambiguition.html) for more details!


### Citation and Acknowledgement

If you use my code for your own research, it would be courteous of you to cite at least one of our papers below when you use ___PyScopus___:

[1] Zuo, Z., Zhao, K., & Eichmann, D. (2017). The State and Evolution of U.S. iSchools – from Talent Acquisitions to Research Outcome. Journal of the Association for Information Science and Technology, 68(5), 1266–1277. https://doi.org/10.1002/asi.23751

[2] Zuo, Z., & Zhao, K. (2018). The more multidisciplinary the better?–The prevalence and interdisciplinarity of research collaborations in multidisciplinary institutions. Journal of Informetrics, 12(3), 736-756.

---

### Get Acquinted with Scopus API

Please first refer to [Elsevier Developer Portal](http://dev.elsevier.com/index.html) for detailed information before using this wrapper.

---

### Download

PyScopus requires:

+ Python 2.7+ (Compatiable with Python 3)

+ [Numpy](http://www.numpy.org/)

+ [Pandas](http://pandas.pydata.org/)

+ [Requests](http://docs.python-requests.org/en/master/)

##### 1. Using `pip`

The easiest way of installing PyScopus is to use `pip`:

{%highlight bash%}
$ pip install pyscopus==1.0.0a1
{%endhighlight%}

##### 2. Manual installation

You can also clone and install the project from its <a href="https://github.com/zhiyzuo/python-scopus" target="_blank">GitHub homepage</a> like this:

{%highlight bash%}
$ git clone https://github.com/zhiyzuo/python-scopus.git
$ cd python-scopus/
$ python setup.py install
{%endhighlight%}

A tarball can also be downloaded via PyScopus's <a href="https://pypi.python.org/pypi/pyscopus/1.0.0a1" target="_blank">PyPI page</a> or <a href="https://github.com/zhiyzuo/python-scopus/tarball/1.0.0a1" target="_blank">this download link</a>.

{%highlight bash%}
$ tar -xvzf pyscopus-1.0.0a1.tar.gz
$ cd pyscopus-1.0.0a1.tar.gz/
$ python setup.py install
{%endhighlight%}

And then please start to enjoy the easy scraping of data from Scopus.

