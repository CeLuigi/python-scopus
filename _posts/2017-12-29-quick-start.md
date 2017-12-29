---
layout: page
title: "Quick Start"
category: doc
date: 2016-02-11 22:37:36
---

### _Note that API keys are hidden. Please get your own API keys._

<hr>
This quick start example is also available in [__Jupyter Notebook__ format](https://nbviewer.jupyter.org/github/zhiyzuo/python-scopus/blob/master/Quick-Start.ipynb).
<hr>

Import `Scopus` class and initialize with your own __API Key__


{% highlight python %}
>>> from pyscopus import Scopus
>>> key = 'xxxxxxxxxx'
>>> scopus = Scopus(key)
{% endhighlight %}

<hr>

#### General Search
{% highlight python %}
>>> search_df = scopus.search("KEY(interdisciplinary collaboration)", count=30)
>>> print(search_df)
{% endhighlight %}

<pre class="longoutput"><code>affiliation       aggregation_type  \
0   [{'name': 'Beijing Normal University', 'city':...                Journal   
1   [{'name': 'University of Nebraska at Omaha', '...                Journal   
2   [{'name': 'Philadelphia University', 'city': '...                Journal   
3   [{'name': 'Technische Universitat Wien', 'city...                Journal   
4   [{'name': 'University of California, San Franc...                Journal   
5   [{'name': 'Monash University', 'city': 'Melbou...                Journal   
6   [{'name': 'Virginia Polytechnic Institute and ...            Book Series   
7   [{'name': 'University of Wisconsin School of M...                Journal   
8   [{'name': 'Swinburne University of Technology'...                Journal   
9   [{'name': 'University of Missouri School of Me...                Journal   
10  [{'name': 'Douglas Mental Health University In...                Journal   
11  [{'name': 'Brigham and Women's Hospital', 'cit...                Journal   
12  [{'name': 'Universite Nice Sophia Antipolis', ...                Journal   
13  [{'name': 'University of South Carolina', 'cit...                Journal   
14  [{'name': 'University of Florida', 'city': 'Ga...                Journal   
15  [{'name': 'Medizinische Hochschule Hannover (M...                Journal   
16  [{'name': 'Children and Screens: Institute of ...                Journal   
17  [{'name': 'National Institute on Aging', 'city...                Journal   
18  [{'name': 'Maimonides Medical Center', 'city':...                Journal   
19  [{'name': 'Universitatea Politehnica din Timis...                Journal   
20  [{'name': 'Universita degli Studi di Milano', ...                Journal   
21  [{'name': 'Baylor College of Medicine', 'city'...                Journal   
22  [{'name': 'Leibniz-Zentrum fur Agrarlandschaft...                Journal   
23  [{'name': 'University of Iceland', 'city': 'Re...  Conference Proceeding   
24  [{'name': 'UT Medical Branch at Galveston', 'c...                Journal   
25  [{'name': 'University of Utah', 'city': 'Salt ...  Conference Proceeding   
26  [{'name': 'DePaul University', 'city': 'Chicag...  Conference Proceeding   
27  [{'name': 'Fachhochschule Munster - Abteilung ...  Conference Proceeding   
28  [{'name': 'Universitatsklinikum Jena und Mediz...                Journal   
29  [{'name': 'Hokkaido University', 'city': 'Sapp...                Journal   

    citation_count  cover_date                                 doi     eissn  \
0                0  2018-05-01     10.1016/j.scitotenv.2017.11.326  18791026   
1                0  2018-02-01           10.1016/j.pcl.2017.08.027  15578240   
2                0  2018-02-01           10.1016/j.pcl.2017.08.020  15578240   
3                0  2018-02-01        10.1016/j.respol.2017.09.010      None   
4                0  2018-02-01          10.1016/j.iccn.2017.07.001      None   
5                0  2018-01-02       10.1080/13561820.2017.1381077  14699567   
6                0  2018-01-01        10.1007/978-3-319-60937-9_27      None   
7                1  2018-01-01          10.1016/j.acra.2017.05.020  18784046   
8                0  2017-12-02       10.1080/09544828.2017.1395395  14661837   
9                0  2017-12-01            10.1177/1049909117693577  19382715   
10               1  2017-12-01           10.1007/s11126-017-9500-4  15736709   
11               0  2017-12-01        10.1016/j.anclin.2017.07.005  22103538   
12               0  2017-12-01           10.1007/s12520-014-0185-4  18669565   
13               0  2017-12-01        10.1016/j.soscij.2017.07.009      None   
14               0  2017-11-01             10.1111/1556-4029.13470  15564029   
15               0  2017-11-01               10.1055/s-0043-119290  14393824   
16               0  2017-11-01             10.1542/peds.2016-1758B  10984275   
17               0  2017-11-01                   10.1111/jgs.15052  15325415   
18               0  2017-11-01              10.1542/peds.2017-1427  10984275   
19               0  2017-11-01  10.1061/(ASCE)SU.1943-5428.0000218      None   
20               0  2017-11-01        10.1016/j.compag.2017.09.030      None   
21               0  2017-11-01              10.1542/peds.2017-0505  10984275   
22               0  2017-10-26                   10.3390/su9111926  20711050   
23               0  2017-10-23             10.1145/3141865.3142467      None   
24               0  2017-10-18        10.1021/acschemneuro.7b00316  19487193   
25               0  2017-10-15             10.1145/3130859.3131333      None   
26               0  2017-10-15             10.1145/3116595.3116600      None   
27               0  2017-10-13          10.1109/ITHET.2017.8067820      None   
28               0  2017-10-12           10.1007/s00063-017-0362-1  21936226   
29               0  2017-10-11                10.2147/JMDH.S144526  11782390   

             isbn      issn page_range  \
0            None  00489697    493-501   
1            None  00313955    143-155   
2            None  00313955      47-57   
3            None  00487333      35-48   
4            None  09643397      18-23   
5            None  13561820      63-68   
6   9783319609362  21945357    352-367   
7            None  10766332       9-17   
8            None  09544828    765-798   
9            None  10499091    901-906   
10           None  00332720    827-838   
11           None  19322275    601-610   
12           None  18669557  1603-1612   
13           None  03623319    458-467   
14           None  00221198  1647-1654   
15           None  03008630    316-321   
16           None  00314005    S51-S56   
17           None  00028614  2441-2445   
18           None  00314005       None   
19           None  07339453       None   
20           None  01681699    424-428   
21           None  00314005       None   
22           None      None       None   
23  9781450355179      None      46-47   
24           None      None  2100-2101   
25  9781450351119      None    405-412   
26  9781450348980      None    291-303   
27  9781538639689      None       None   
28           None  21936218        1-5   
29           None      None    399-407   

                                     publication_name    scopus_id  \
0                    Science of the Total Environment  85036647140   
1                  Pediatric Clinics of North America  85035032871   
2                  Pediatric Clinics of North America  85035066203   
3                                     Research Policy  85033491209   
4                 Intensive and Critical Care Nursing  85028624027   
5                   Journal of Interprofessional Care  85031933779   
6       Advances in Intelligent Systems and Computing  85025807393   
7                                  Academic Radiology  85028323720   
8                       Journal of Engineering Design  85033437283   
9   American Journal of Hospice and Palliative Med...  85032888667   
10                              Psychiatric Quarterly  85013059761   
11                             Anesthesiology Clinics  85034242478   
12        Archaeological and Anthropological Sciences  85036562680   
13                             Social Science Journal  85028332507   
14                       Journal of Forensic Sciences  85018991781   
15                                Klinische Padiatrie  85031940447   
16                                         Pediatrics  85034023085   
17         Journal of the American Geriatrics Society  85034054567   
18                                         Pediatrics  85034103814   
19                   Journal of Surveying Engineering  85018978233   
20           Computers and Electronics in Agriculture  85030118345   
21                                         Pediatrics  85034101645   
22                       Sustainability (Switzerland)  85032380806   
23  SEPS 2017 - Proceedings of the 4th ACM SIGPLAN...  85037139471   
24                          ACS Chemical Neuroscience  85031688464   
25  CHI PLAY 2017 Extended Abstracts - Extended Ab...  85034759003   
26  CHI PLAY 2017 - Proceedings of the Annual Symp...  85034641024   
27  2017 16th International Conference on Informat...  85037077063   
28  Medizinische Klinik - Intensivmedizin und Notf...  85031726522   
29            Journal of Multidisciplinary Healthcare  85034808036   

   subtype_description                                              title  \
0               Review  Climate change and dengue fever transmission i...   
1               Review  Interprofessional Collaborative Practice in Ea...   
2               Review  Supporting Children with Autism and Their Fami...   
3              Article  Gaining insight into interdisciplinary researc...   
4              Article  Impact of surgical intensive care unit interdi...   
5              Article  Translation and psychometric evaluation of the...   
6     Conference Paper  A virtual learning system in environmental mon...   
7               Review  Promoting Collaborations Between Radiologists ...   
8              Article  Implementing shared function modelling in prac...   
9              Article  A Qualitative Analysis of Information Sharing ...   
10             Article  Profiles of mental health care professionals b...   
11              Review        Use of Anesthesiology Services in Radiology   
12             Article  Together in the field: interdisciplinary work ...   
13             Article  Team science: A qualitative study of benefits,...   
14             Article  Skeletal Indicators of Shark Feeding on Human ...   
15    Conference Paper  SICKODevelopment of a Multi-Disciplinary Train...   
16              Review                                       Introduction   
17             Article  Aging Research: Collaborations Forge a Promisi...   
18             Article  Social determinants of health and hospital rea...   
19             Article  Road-structure monitoring with modern geodetic...   
20             Article  Application note: Labelling, a methodology to ...   
21              Review                  Bringing back the term "intersex"   
22             Article  The adoption and implementation of transdiscip...   
23    Conference Paper  Facilitating collaboration in high-performance...   
24             Article  Why I'm Not a Cognitive Psychologist... or a B...   
25    Conference Paper  Design box case study: Facilitating interdisci...   
26    Conference Paper  Leveraging design patterns to support designer...   
27    Conference Paper  Peer review as a quality management tool embed...   
28    Article in Press                          Burnout—a call for action   
29             Article  Establishing community-based integrated care f...   

     volume  
0   622-623  
1        65  
2        65  
3        47  
4        44  
5        32  
6       627  
7        25  
8        28  
9        34  
10       88  
11       35  
12        9  
13       54  
14       62  
15      229  
16      140  
17       65  
18      140  
19      143  
20      142  
21      140  
22        9  
23     None  
24        8  
25     None  
26     None  
27     None  
28     None  
29       10  
</code></pre>

<hr>

#### Search for a specific author


{% highlight python %}
>>> author_result_df = scopus.search_author("AUTHLASTNAME(Zhao) and AUTHFIRST(Kang) and AFFIL(Iowa)")
>>> print(author_result_df)
{% endhighlight %}

<pre><code>     affiliation affiliation_id    author_id  document_count       name
0  University of Iowa       60024324  36635367700              39  Kang Zhao
1  University of Iowa       60024324  57077574400               1  Kang Zhao
</code></pre>


Then we can retrieve more detailed info about the author we are looking for using his/her __author_id__:

{% highlight python %}
>>> kang_info_dict = scopus.retrieve_author('36635367700')
>>> kang_info_dict.keys()
dict_keys(['author-id', 'eid', 'document-count', 'cited-by-count', 'citation-count', 'name', 'last', 'first', 'indexed-name', 'publication-range', 'affiliation-current', 'journal-history', 'affiliation-history'])
{% endhighlight %}

{% highlight python %}
>>> print(kang_info_dict['affiliation-history'])
{% endhighlight %}
<pre class='longoutput'><code>id                                               name parent-id  \
0   60024324                                 University of Iowa      None   
1  104227060  University of Iowa, Department of Management S...  60024324   
2  104227074     University of Iowa, Tippie College of Business  60024324   
3  109230131  University of Iowa, Interdisciplinary Graduate...  60024324   
4  105050101  Pennsylvania State University, College of Info...  60001439   
5   60001439                      Pennsylvania State University      None   

                                         parent-name                    url  \
0                                               None  http://www.uiowa.edu/   
1  {'@source': 'internal-ani', '$': 'University o...  http://www.uiowa.edu/   
2  {'@source': 'internal-ani', '$': 'University o...  http://www.uiowa.edu/   
3  {'@source': 'internal-ani', '$': 'University o...  http://www.uiowa.edu/   
4  {'@source': 'internal-ani', '$': 'Pennsylvania...    http://www.psu.edu/   
5                                               None    http://www.psu.edu/   

                                 address  
0      usa, Iowa City, IA, United States  
1      usa, Iowa City, IA, United States  
2      usa, Iowa City, IA, United States  
3      usa, Iowa City, IA, United States  
4  usa, State College, PA, United States  
5  usa, State College, PA, United States  
</code></pre>

We can also search for his publications explicitly

{% highlight python %}
>>> kang_pub_df = scopus.search_author_publication('36635367700')
>>> kang_pub_df[['title', 'cover_date', 'publication_name']].sort_values('cover_date').reset_index(drop=True)
{% endhighlight %}


<div>
    <style scoped>
        .dataframe tbody tr th:only-of-type {
            vertical-align: middle;
        }

        .dataframe tbody tr th {
            vertical-align: top;
        }

        .dataframe thead th {
            text-align: right;
        }
    </style>
    <table border="1" class="dataframe">
      <thead>
        <tr style="text-align: right;">
          <th></th>
          <th>title</th>
          <th>cover_date</th>
          <th>publication_name</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>0</th>
          <td>Building global bridges: Coordination bodies f...</td>
          <td>2008-01-01</td>
          <td>Proceedings of ISCRAM 2008 - 5th International...</td>
        </tr>
        <tr>
          <th>1</th>
          <td>CyberLab: An online virtual laboratory toolkit...</td>
          <td>2008-09-22</td>
          <td>Proceedings - The 8th IEEE International Confe...</td>
        </tr>
        <tr>
          <th>2</th>
          <td>Effect of topology on the robustness of supply...</td>
          <td>2009-01-01</td>
          <td>19th Workshop on Information Technologies and ...</td>
        </tr>
        <tr>
          <th>3</th>
          <td>A formal model for emerging coalitions under n...</td>
          <td>2009-03-22</td>
          <td>Spring Simulation Multiconference 2009 - Co-lo...</td>
        </tr>
        <tr>
          <th>4</th>
          <td>Sectoral coordination in humanitarian informat...</td>
          <td>2010-01-01</td>
          <td>ISCRAM 2010 - 7th International Conference on ...</td>
        </tr>
        <tr>
          <th>5</th>
          <td>Assessing humanitarian inter-organizational ne...</td>
          <td>2010-01-01</td>
          <td>ISCRAM 2010 - 7th International Conference on ...</td>
        </tr>
        <tr>
          <th>6</th>
          <td>Who blogs what: Understanding behavior, impact...</td>
          <td>2010-01-01</td>
          <td>Proceedings of 20th Annual Workshop on Informa...</td>
        </tr>
        <tr>
          <th>7</th>
          <td>From communication to collaboration: Simulatin...</td>
          <td>2010-11-29</td>
          <td>Proceedings - SocialCom 2010: 2nd IEEE Interna...</td>
        </tr>
        <tr>
          <th>8</th>
          <td>Crossing borders, organizations, levels and te...</td>
          <td>2010-12-01</td>
          <td>16th Americas Conference on Information System...</td>
        </tr>
        <tr>
          <th>9</th>
          <td>Assortativity patterns in multi-dimensional in...</td>
          <td>2010-12-24</td>
          <td>Lecture Notes in Computer Science (including s...</td>
        </tr>
        <tr>
          <th>10</th>
          <td>Identifying leaders in an online cancer surviv...</td>
          <td>2011-01-01</td>
          <td>Proceedings - 21st Workshop on Information Tec...</td>
        </tr>
        <tr>
          <th>11</th>
          <td>Analyzing the Resilience of Complex Supply Net...</td>
          <td>2011-01-17</td>
          <td>IEEE Systems Journal</td>
        </tr>
        <tr>
          <th>12</th>
          <td>Achieving high robustness in supply distributi...</td>
          <td>2011-05-01</td>
          <td>IEEE Transactions on Engineering Management</td>
        </tr>
        <tr>
          <th>13</th>
          <td>Get online support, feel better-sentiment anal...</td>
          <td>2011-12-01</td>
          <td>Proceedings - 2011 IEEE International Conferen...</td>
        </tr>
        <tr>
          <th>14</th>
          <td>Simulating inter-organizational collaboration ...</td>
          <td>2012-01-01</td>
          <td>SIMULATION</td>
        </tr>
        <tr>
          <th>15</th>
          <td>Exploring barriers to coordination between hum...</td>
          <td>2013-02-28</td>
          <td>Information Systems and Modern Society: Social...</td>
        </tr>
        <tr>
          <th>16</th>
          <td>Recommendation in reciprocal and bipartite soc...</td>
          <td>2013-03-14</td>
          <td>Lecture Notes in Computer Science (including s...</td>
        </tr>
        <tr>
          <th>17</th>
          <td>Who blogs what: Understanding the publishing b...</td>
          <td>2013-11-01</td>
          <td>World Wide Web</td>
        </tr>
        <tr>
          <th>18</th>
          <td>Understanding topics and sentiment in an onlin...</td>
          <td>2013-12-01</td>
          <td>Journal of the National Cancer Institute - Mon...</td>
        </tr>
        <tr>
          <th>19</th>
          <td>Making sense of a healthcare forum - Smart key...</td>
          <td>2013-12-01</td>
          <td>International Conference on Information System...</td>
        </tr>
        <tr>
          <th>20</th>
          <td>Social support and user engagement in online h...</td>
          <td>2014-01-01</td>
          <td>Lecture Notes in Computer Science (including s...</td>
        </tr>
        <tr>
          <th>21</th>
          <td>User recommendations in reciprocal and biparti...</td>
          <td>2014-01-01</td>
          <td>IEEE Intelligent Systems</td>
        </tr>
        <tr>
          <th>22</th>
          <td>Social support and user engagement in online h...</td>
          <td>2014-01-01</td>
          <td>Proceedings - Pacific Asia Conference on Infor...</td>
        </tr>
        <tr>
          <th>23</th>
          <td>Finding influential users of online health com...</td>
          <td>2014-01-01</td>
          <td>Journal of the American Medical Informatics As...</td>
        </tr>
        <tr>
          <th>24</th>
          <td>The structure and dynamics of a multi-relation...</td>
          <td>2015-01-01</td>
          <td>25th Annual Workshop on Information Technologi...</td>
        </tr>
        <tr>
          <th>25</th>
          <td>Early prediction of movie success-what, who, a...</td>
          <td>2015-01-01</td>
          <td>Lecture Notes in Computer Science (including s...</td>
        </tr>
        <tr>
          <th>26</th>
          <td>The diffusion of user roles via social network...</td>
          <td>2015-01-01</td>
          <td>25th Annual Workshop on Information Technologi...</td>
        </tr>
        <tr>
          <th>27</th>
          <td>The evolution of user roles in online health c...</td>
          <td>2015-01-01</td>
          <td>Pacific Asia Conference on Information Systems...</td>
        </tr>
        <tr>
          <th>28</th>
          <td>System Informatics: From Methodology to Applic...</td>
          <td>2015-11-01</td>
          <td>IEEE Intelligent Systems</td>
        </tr>
        <tr>
          <th>29</th>
          <td>Leader identification in an online health comm...</td>
          <td>2015-11-01</td>
          <td>Information Systems and e-Business Management</td>
        </tr>
        <tr>
          <th>30</th>
          <td>The evolution and diffusion of user roles in o...</td>
          <td>2015-12-08</td>
          <td>Proceedings - 2015 IEEE International Conferen...</td>
        </tr>
        <tr>
          <th>31</th>
          <td>Investigating regional prejudice in China thro...</td>
          <td>2016-01-01</td>
          <td>Lecture Notes in Computer Science (including s...</td>
        </tr>
        <tr>
          <th>32</th>
          <td>Early Predictions of Movie Success: The Who, W...</td>
          <td>2016-07-02</td>
          <td>Journal of Management Information Systems</td>
        </tr>
        <tr>
          <th>33</th>
          <td>A multirelational social network analysis of a...</td>
          <td>2016-08-01</td>
          <td>Journal of Medical Internet Research</td>
        </tr>
        <tr>
          <th>34</th>
          <td>Analyzing and predicting user participations i...</td>
          <td>2017-04-01</td>
          <td>Journal of Medical Internet Research</td>
        </tr>
        <tr>
          <th>35</th>
          <td>The state and evolution of U.S. iSchools: From...</td>
          <td>2017-05-01</td>
          <td>Journal of the Association for Information Sci...</td>
        </tr>
        <tr>
          <th>36</th>
          <td>A prospective examination of online social net...</td>
          <td>2017-08-01</td>
          <td>PLoS ONE</td>
        </tr>
        <tr>
          <th>37</th>
          <td>A descriptive study of the prevalence and typo...</td>
          <td>2017-09-01</td>
          <td>Journal of Studies on Alcohol and Drugs</td>
        </tr>
        <tr>
          <th>38</th>
          <td>The failure to increase social support: it jus...</td>
          <td>2017-12-01</td>
          <td>Translational Behavioral Medicine</td>
        </tr>
      </tbody>
    </table>
</div>

<hr>
#### Abstract retrieval

{% highlight python %}
>>> pub_info = scopus.retrieve_abstract('84905286162')
>>> print(pub_info)
{'abstract': "Online health communities (OHCs) have become a major source of support for people with health problems. This research tries to improve our understanding of social influence and to identify influential users in OHCs. The outcome can facilitate OHC management, improve community sustainability, and eventually benefit OHC users. Through text mining and sentiment analysis of users' online interactions, the research revealed sentiment dynamics in threaded discussions. A novel metric--the number of influential responding replies--was proposed to directly measure a user's ability to affect the sentiment of others. Using the dataset from a popular OHC, the research demonstrated that the proposed metric is highly effective in identifying influential users. In addition, combining the metric with other traditional measures further improves the identification of influential users. Published by the BMJ Publishing Group Limited. For permission to use (where not already granted under a licence) please go to http://group.bmj.com/group/rights-licensing/permissions.",
 'citedby-count': '29',
 'eid': '2-s2.0-84905286162',
 'prism:aggregationType': 'Journal',
 'prism:coverDate': '2014-01-01',
 'prism:doi': '10.1136/amiajnl-2013-002282',
 'prism:issn': '1527974X',
 'prism:issueIdentifier': 'e2',
 'prism:publicationName': 'Journal of the American Medical Informatics Association : JAMIA',
 'prism:url': 'http://api.elsevier.com/content/abstract/scopus_id/84905286162',
 'prism:volume': '21',
 'pubmed-id': '24449805',
 'scopus-id': '84905286162',
 'source-id': '23600',
 'srctype': 'j',
 'title': 'Finding influential users of online health communities: a new metric based on sentiment influence.'}
{% endhighlight %}

<hr>
__Note that Searching for articles in specific journals (venues) is not supported anymore since this can be easily done by `general search`__
<hr>

#### Citation count retrieval

__Note that the use of `citation overview API` needs to be approved by Elsevier.__

{% highlight python %}
>>> pub_citations_df = scopus.retrieve_citation(scopus_id_array=['84905286162', '0141607824'],
                                            year_range=[2010, 2014])
>>> print(pub_citations_df)
{% endhighlight %}

<pre><code>     scopus_id previous_citation 2010 2011  2012  2013  2014 later_citation  \
0  84905286162                 0    0    0     0     0     3             26   
1   0141607824               905  596  802  1057  1323  1451           5324   

  total_citation  
0             29  
1          11458  
</code></pre>

<hr>
