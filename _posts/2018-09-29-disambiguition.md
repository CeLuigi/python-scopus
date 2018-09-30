---
layout: page
title: "Disambiguity Workaround"
category: doc
date: 2018-09-29 22:00:00
---

Sometimes Scopus would mix up people with similar names. I recently come up with a not that difficult method to clean author publication profiles, which needs some manual work.

If you can think of a better way, please do let me know!

---

<pre class="prettyprint">>>> import pyscopus
>>> pyscopus.__version__
'1.0.0a1'
>>> from pyscopus import Scopus
>>> key = 'YOUR_OWN_APIKEY'
>>> scopus = Scopus(key)
>>> import utils
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
      <td>490</td>
      <td>Banaras Hindu University</td>
      <td>60008721</td>
    </tr>
  </tbody>
</table>
</div>

<br>

Sometimes we would obtain a list of author profiles for each author. In this case, we only have one and it is clear that the author profile is highly noisy.

In the following step, I would use the helper functions in `utils` to screen each paper by this `author_id`

<pre class="prettyprint">
>>> author_id = '7404651152'
>>> author_id, d['affil_id_list']
('7404651152', ['60030623', '60022195', '60007278'])
</pre>

The filtering process may take a while, depending on how many documents are mixd up.

<pre class="prettyprint">
>>> filterd_pub_df = utils.check_pub_validity(scopus, author_id, d['affil_id_list'], apikey)
>>> filterd_pub_df.shape[0], filterd_pub_df.scopus_id.unique().size, filterd_pub_df.scopus_id.isnull().sum()
(134, 134, 0)
</pre>


Obviously, the number of papers is highly reduced. We can now check a random subset to see if the filtered papers make sense for this author.

<pre class="prettyprint">
>>> filterd_pub_df.iloc[utils.pd.np.random.randint(0, high=134, size=20)][['title', 'publication_name']]
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
      <th>117</th>
      <td>Effects of high-energy irradiation on silicon ...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>34</th>
      <td>"They basically like destroyed the school one ...</td>
      <td>Proceedings of the ACM Conference on Computer ...</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Situation recognition from multimodal data</td>
      <td>MM 2016 - Proceedings of the 2016 ACM Multimed...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>On-chip mid-infrared gas detection using chalc...</td>
      <td>Applied Physics Letters</td>
    </tr>
    <tr>
      <th>212</th>
      <td>Mid-infrared As&lt;inf&gt;2&lt;/inf&gt;Se&lt;inf&gt;3&lt;/inf&gt; chal...</td>
      <td>IEEE International Conference on Group IV Phot...</td>
    </tr>
    <tr>
      <th>88</th>
      <td>Geo-intelligence and visualization through big...</td>
      <td>Geo-Intelligence and Visualization through Big...</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Effects of high-energy irradiation on silicon ...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>206</th>
      <td>Low loss mid-infrared silicon waveguides by us...</td>
      <td>Frontiers in Optics, FIO 2012</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Predicting spending behavior using socio-mobil...</td>
      <td>Proceedings - SocialCom/PASSAT/BigData/EconCom...</td>
    </tr>
    <tr>
      <th>154</th>
      <td>Generation of two-cycle pulses and octave-span...</td>
      <td>Optics Letters</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Predicting privacy attitudes using phone metadata</td>
      <td>Lecture Notes in Computer Science (including s...</td>
    </tr>
    <tr>
      <th>259</th>
      <td>Novel designs for on-chip mid-infrared detecto...</td>
      <td>Optics InfoBase Conference Papers</td>
    </tr>
    <tr>
      <th>204</th>
      <td>Engineering spectral variation of FSR by tailo...</td>
      <td>Integrated Photonics Research, Silicon and Nan...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Toward harmonizing self-reported and logged so...</td>
      <td>Conference on Human Factors in Computing Syste...</td>
    </tr>
    <tr>
      <th>316</th>
      <td>Adversary aware surveillance systems</td>
      <td>IEEE Transactions on Information Forensics and...</td>
    </tr>
    <tr>
      <th>194</th>
      <td>Situation recognition: An evolving problem for...</td>
      <td>MM 2012 - Proceedings of the 20th ACM Internat...</td>
    </tr>
    <tr>
      <th>209</th>
      <td>Trimming of athermal silicon resonators</td>
      <td>Integrated Photonics Research, Silicon and Nan...</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Nonreciprocal racetrack resonator based on vac...</td>
      <td>Optics Express</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Assessing personality using demographic inform...</td>
      <td>ACM International Conference Proceeding Series</td>
    </tr>
    <tr>
      <th>265</th>
      <td>Visible light trimming of coupled ring-resonat...</td>
      <td>2011 Conference on Lasers and Electro-Optics E...</td>
    </tr>
  </tbody>
</table>
</div>

<br>

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
>>> filterd_pub_df.iloc[utils.pd.np.random.randint(0, high=59, size=20)][['title', 'publication_name']]
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
      <th>94</th>
      <td>Physical-Cyber-Social Computing: Looking Back,...</td>
      <td>IEEE Internet Computing</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Situation recognition from multimodal data</td>
      <td>MM 2016 - Proceedings of the 2016 ACM Multimed...</td>
    </tr>
    <tr>
      <th>151</th>
      <td>Predicting spending behavior using socio-mobil...</td>
      <td>Proceedings - SocialCom/PASSAT/BigData/EconCom...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Toward multimodal cyberbullying detection</td>
      <td>Conference on Human Factors in Computing Syste...</td>
    </tr>
    <tr>
      <th>61</th>
      <td>If it looks like a spammer and behaves like a ...</td>
      <td>International Journal of Information Security</td>
    </tr>
    <tr>
      <th>134</th>
      <td>Cyber bullying detection using social and text...</td>
      <td>SAM 2014 - Proceedings of the 3rd Internationa...</td>
    </tr>
    <tr>
      <th>45</th>
      <td>From sensors to sense-making: Opportunities an...</td>
      <td>Proceedings of the Association for Information...</td>
    </tr>
    <tr>
      <th>45</th>
      <td>From sensors to sense-making: Opportunities an...</td>
      <td>Proceedings of the Association for Information...</td>
    </tr>
    <tr>
      <th>297</th>
      <td>Structural analysis of the emerging event-web</td>
      <td>Proceedings of the 19th International Conferen...</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Using cognitive dissonance theory to understan...</td>
      <td>Proceedings of the Association for Information...</td>
    </tr>
    <tr>
      <th>88</th>
      <td>Geo-intelligence and visualization through big...</td>
      <td>Geo-Intelligence and Visualization through Big...</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Preface</td>
      <td>Geo-Intelligence and Visualization through Big...</td>
    </tr>
    <tr>
      <th>34</th>
      <td>"They basically like destroyed the school one ...</td>
      <td>Proceedings of the ACM Conference on Computer ...</td>
    </tr>
    <tr>
      <th>152</th>
      <td>EventShop: Recognizing situations in web data ...</td>
      <td>WWW 2013 Companion - Proceedings of the 22nd I...</td>
    </tr>
    <tr>
      <th>73</th>
      <td>Predicting privacy attitudes using phone metadata</td>
      <td>Lecture Notes in Computer Science (including s...</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Introduction to the special issue on advances ...</td>
      <td>ACM Transactions on Internet Technology</td>
    </tr>
    <tr>
      <th>74</th>
      <td>Situation recognition using eventShop</td>
      <td>Situation Recognition Using EventShop</td>
    </tr>
    <tr>
      <th>301</th>
      <td>From microblogs to social images: Event analyt...</td>
      <td>MIR 2010 - Proceedings of the 2010 ACM SIGMM I...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Toward harmonizing self-reported and logged so...</td>
      <td>Conference on Human Factors in Computing Syste...</td>
    </tr>
    <tr>
      <th>94</th>
      <td>Physical-Cyber-Social Computing: Looking Back,...</td>
      <td>IEEE Internet Computing</td>
    </tr>
  </tbody>
</table>
</div>

<br>

Now it is much better and we can use this cleaned paper list for this focal author.
