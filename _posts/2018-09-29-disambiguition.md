---
layout: page
title: "Disambiguity Workaround"
category: doc
date: 2018-09-29 22:00:00
---

__PyScopus__: An example for author disambiguity

Sometimes Scopus would mix up people with similar names. I recently come up with a not that difficult method to clean author publication profiles, which needs some manual work.

If you can think of a better way, please do let me know!

---


<pre class="prettyprint">
>>> import pyscopus
>>> pyscopus.__version__
    '1.0.2'
</pre>

<pre class="prettyprint">
>>> from pyscopus import Scopus
>>> key = 'YOUR_OWN_APIKEY'
>>> scopus = Scopus(key)
</pre>

---

Wrapper functions for disambiguity:


<pre class="prettyprint">
>>> import requests, time
>>> import pandas as pd
>>> from bs4 import BeautifulSoup as Soup
>>> BASE_URL = "https://api.elsevier.com/content/abstract/scopus_id/"
</pre>


<pre class="prettyprint">
def _check_pub_validity(sid, author_id, author_affil_id_list, apikey):
    global BASE_URL
    r = requests.get(BASE_URL+sid, params={'apikey': apikey})
    soup = Soup(r.content, 'lxml')
    author_list = soup.find('authors').find_all('author')

    ## go through the author list to find the author first, by matching author id
    for au in author_list:
        if au['auid'] == author_id:
            ## find it and break
            break

    ## check the affiliation id: note that an author may have a list of affiliations
    this_affil_id_list = [affil_tag['id'] for affil_tag in au.find_all('affiliation')]
    ## get the affiliation id and check if there are any overlap
    if len(set(author_affil_id_list).intersection(set(this_affil_id_list))) > 0:
        return True
    return False
</pre>


<pre class="prettyprint">
def check_pub_validity(scopus_obj, author_id, author_affil_id_list, apikey):
    ## first find out all pub
    pub_df = scopus_obj.search_author_publication(author_id)
    ## do this for all non-null scopus ids
    pub_df = pub_df[~pub_df.scopus_id.isnull()]
    ## list to save all eligble scopus ids
    eligible_scopus_id_list = list()
    for i, sid in enumerate(pub_df.scopus_id.values):
        if (i+1)%5==0:
            time.sleep(pd.np.random.random()+.3)
        if _check_pub_validity(sid, author_id, author_affil_id_list, apikey):
            ## if true, save it
            eligible_scopus_id_list.append(sid)
    ## finally, get a subset of the original pub_df
    filtered_pub_df = pub_df.query("scopus_id in @eligible_scopus_id_list")
    return filtered_pub_df
</pre>

---

When I was collecting data for my own research, I found that [Dr. Vivek K. Singh](http://web.media.mit.edu/~singhv/) has a very [noisy profile in Scopus](https://www.scopus.com/authid/detail.uri?authorId=7404651152). Let's use this as an example.

The basic idea is to match author-affiliation pair:
- For all the paper found in the _mixed profile_
    - Find the focal author (in this case, Dr. Singh)
    - Look at his/her affiliation
        - Keep this paper if the affiliation is indeed where he/she is
        - If not, discard the paper

For Dr. Singh, I manually obtained his affiliation ids by searching through [Scopus affiliation search](https://www.scopus.com/search/form.uri?display=affiliationLookup). Upon obtaining that, create a dictionary containing _name (first/last)_, _affiliation name_, and _a list of affiliation ids_. Author and affiliation names would be used to search for this author. The list of affiliation ids would be used for cleaning papers: 

- UC Irvine `60007278`
- MIT `60022195`
- Rutgers `60030623`


<pre class="prettyprint">
>>> d = {'authfirst': 'Vivek', 'authlastname': 'Singh', 'affiliation': 'Rutgers',
         'affil_id_list': ['60030623', '60022195', '60007278']
        }
>>> d
    {'authfirst': 'Vivek',
     'authlastname': 'Singh',
     'affiliation': 'Rutgers',
     'affil_id_list': ['60030623', '60022195', '60007278']}
>>> query = "AUTHLASTNAME({}) and AUTHFIRST({}) and AFFIL({})".format(d['authlastname'], d['authfirst'], d['affiliation'])
>>> author_search_df = scopus.search_author(query)
>>> author_search_df
    The history saving thread hit an unexpected error (OperationalError('database is locked',)).History will not be written to the database.
</pre>


<div>
<table class="pure-table">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>author_id</th>
      <th>name</th>
      <th>document_count</th>
      <th>affiliation</th>
      <th>affiliation_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7404651152</td>
      <td>Vivek Kumar N. Singh</td>
      <td>491</td>
      <td>Shri Mata Vaishno Devi University</td>
      <td>60017187</td>
    </tr>
  </tbody>
</table>
</div> <br>



Sometimes we would obtain a list of author profiles for each author. In this case, we only have one and it is clear that the author profile is highly noisy.

In the following step, I would use the helper functions in `utils` to screen each paper by this `author_id`


<pre class="prettyprint">
>>> author_id = '7404651152'
>>> author_id, d['affil_id_list']
    ('7404651152', ['60030623', '60022195', '60007278'])
</pre>



The filtering process may take a while, depending on how many documents are mixd up.


<pre class="prettyprint">
>>> filterd_pub_df = check_pub_validity(scopus, author_id, d['affil_id_list'], key)
>>> filterd_pub_df.shape[0], filterd_pub_df.scopus_id.unique().size, filterd_pub_df.scopus_id.isnull().sum()
    (134, 134, 0)
</pre>


Obviously, the number of papers is highly reduced. We can now check a random subset to see if the filtered papers make sense for this author.


<pre class="prettyprint">
>>> filterd_pub_df.iloc[pd.np.random.randint(0, high=134, size=20)][['title', 'publication_name']]
</pre>

<div>
<table class="pure-table">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>publication_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>118</th>
      <td>Effects of high-energy irradiation on silicon ...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Physical-Cyber-Social Computing: Looking Back,...</td>
      <td>IEEE Internet Computing</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Low-stress silicon nitride for mid-infrared mi...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>194</th>
      <td>Mid-infrared silicon waveguide resonators with...</td>
      <td>Materials Research Society Symposium Proceedings</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Effects of high-energy irradiation on silicon ...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>194</th>
      <td>Mid-infrared silicon waveguide resonators with...</td>
      <td>Materials Research Society Symposium Proceedings</td>
    </tr>
    <tr>
      <th>89</th>
      <td>Preface</td>
      <td>Geo-Intelligence and Visualization through Big...</td>
    </tr>
    <tr>
      <th>179</th>
      <td>Demonstration of high-Q mid-infrared chalcogen...</td>
      <td>Optics Letters</td>
    </tr>
    <tr>
      <th>147</th>
      <td>Low-Stress silicon nitride platform for broadb...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>309</th>
      <td>Situation based control for cyber-physical env...</td>
      <td>Proceedings - IEEE Military Communications Con...</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Towards measuring fine-grained diversity using...</td>
      <td>Proceedings of the 11th International Conferen...</td>
    </tr>
    <tr>
      <th>306</th>
      <td>Motivating contributors in social media networks</td>
      <td>1st ACM SIGMM International Workshop on Social...</td>
    </tr>
    <tr>
      <th>146</th>
      <td>Mid-infrared opto-nanofluidics for label-free ...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Gradient Polymer Nanofoams for Encrypted Recor...</td>
      <td>ACS Nano</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Physical-Cyber-Social Computing: Looking Back,...</td>
      <td>IEEE Internet Computing</td>
    </tr>
    <tr>
      <th>336</th>
      <td>Towards environment-to-environment (E2E) multi...</td>
      <td>MM'08 - Proceedings of the 2008 ACM Internatio...</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Low-stress silicon nitride platform for broadb...</td>
      <td>Conference on Lasers and Electro-Optics Europe...</td>
    </tr>
    <tr>
      <th>209</th>
      <td>Anisotropic photoluminescence from Er-TeO&lt;inf&gt;...</td>
      <td>CLEO: Science and Innovations, CLEO_SI 2012</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Physical-Cyber-Social Computing: Looking Back,...</td>
      <td>IEEE Internet Computing</td>
    </tr>
    <tr>
      <th>71</th>
      <td>On-chip mid-infrared gas detection using chalc...</td>
      <td>Applied Physics Letters</td>
    </tr>
  </tbody>
</table>
</div> <br>



However, there may still be noise in it (e.g., papers published in optics/photonics venues). We can manually exclude those as well:


<pre class="prettyprint">
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('optic')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('photonic')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('nano')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('quantum')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('sensor')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('cleo')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('materials')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('physics')")
>>> filterd_pub_df = filterd_pub_df.query("not publication_name.str.lower().str.contains('chip')")
>>> filterd_pub_df.shape
    (59, 16)
</pre>


And let's check again

<pre class="prettyprint">
>>> filterd_pub_df.iloc[pd.np.random.randint(0, high=59, size=20)][['title', 'publication_name']]
</pre>


<div>
<table class="pure-table">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>publication_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>103</th>
      <td>Assessing personality using demographic inform...</td>
      <td>ACM International Conference Proceeding Series</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Examining information search behaviors in smal...</td>
      <td>Proceedings of the Association for Information...</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Examining information search behaviors in smal...</td>
      <td>Proceedings of the Association for Information...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Social bridges in urban purchase behavior</td>
      <td>ACM Transactions on Intelligent Systems and Te...</td>
    </tr>
    <tr>
      <th>62</th>
      <td>If it looks like a spammer and behaves like a ...</td>
      <td>International Journal of Information Security</td>
    </tr>
    <tr>
      <th>152</th>
      <td>EventShop: Recognizing situations in web data ...</td>
      <td>WWW 2013 Companion - Proceedings of the 22nd I...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Are you altruistic? Your mobile phone could tell</td>
      <td>2017 IEEE SmartWorld Ubiquitous Intelligence a...</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Assessing personality using demographic inform...</td>
      <td>ACM International Conference Proceeding Series</td>
    </tr>
    <tr>
      <th>247</th>
      <td>EventShop: From heterogeneous web streams to p...</td>
      <td>Proceedings of the 4th Annual ACM Web Science ...</td>
    </tr>
    <tr>
      <th>61</th>
      <td>LTA 2016 - The first workshop on lifelogging t...</td>
      <td>MM 2016 - Proceedings of the 2016 ACM Multimed...</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Effect of gamma exposure on chalcogenide glass...</td>
      <td>IEEE Radiation Effects Data Workshop</td>
    </tr>
    <tr>
      <th>95</th>
      <td>Physical-Cyber-Social Computing: Looking Back,...</td>
      <td>IEEE Internet Computing</td>
    </tr>
    <tr>
      <th>298</th>
      <td>Structural analysis of the emerging event-web</td>
      <td>Proceedings of the 19th International Conferen...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>New Signals in Multimedia Systems and Applicat...</td>
      <td>IEEE Multimedia</td>
    </tr>
    <tr>
      <th>152</th>
      <td>EventShop: Recognizing situations in web data ...</td>
      <td>WWW 2013 Companion - Proceedings of the 22nd I...</td>
    </tr>
    <tr>
      <th>317</th>
      <td>Adversary aware surveillance systems</td>
      <td>IEEE Transactions on Information Forensics and...</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Toward harmonizing self-reported and logged so...</td>
      <td>Conference on Human Factors in Computing Syste...</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Predicting privacy attitudes using phone metadata</td>
      <td>Lecture Notes in Computer Science (including s...</td>
    </tr>
    <tr>
      <th>89</th>
      <td>Preface</td>
      <td>Geo-Intelligence and Visualization through Big...</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Probing the interconnections between geo-explo...</td>
      <td>UbiComp 2016 - Proceedings of the 2016 ACM Int...</td>
    </tr>
  </tbody>
</table>
</div> <br>


Now it is much better and we can use this cleaned paper list for this focal author.
