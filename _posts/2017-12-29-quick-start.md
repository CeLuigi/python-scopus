---
layout: page
title: "Quick Start"
category: doc
date: 2018-01-05 12:00:00
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
>>> print(search_df.head(10))
{% endhighlight %}

<pre class="longoutput"><code>affiliation aggregation_type  \
0  [{'name': 'Institute of Informatics and Teleco...          Journal   
1  [{'name': 'University of Jinan', 'city': 'Jina...          Journal   
2  [{'name': 'University of South Carolina', 'cit...          Journal   
3  [{'name': 'University of Nottingham', 'city': ...          Journal   
4  [{'name': 'Shenzhen University', 'city': 'Qing...          Journal   
5  [{'name': 'South China University of Technolog...          Journal   
6  [{'name': 'Hopital Tenon', 'city': 'Paris', 'c...          Journal   
7  [{'name': 'Beijing University of Posts and Tel...      Book Series   
8  [{'name': 'Moscow Institute of Physics and Tec...      Book Series   
9  [{'name': 'Indian Institute of Information Tec...      Book Series   

                                             authors  citation_count  \
0                          [57191094398, 8723549900]               0   
1  [56177015500, 56177015500, 7409491657, 7409491...               0   
2  [36519126000, 56937992800, 7801439333, 2408066...               0   
3  [51665107100, 38161915200, 57199156035, 234712...               0   
4  [56349712700, 56349712700, 55739099100, 568013...               0   
5  [57196023747, 57196027721, 55538918200, 710229...               0   
6  [7005233421, 55406676800, 55364211300, 5718548...               0   
7            [57193130741, 55571529600, 57196003124]               0   
8             [57199062408, 57199054340, 6507982932]               0   
9             [49361023900, 8533679400, 57194438376]               0   

   cover_date                              doi     eissn  \
0  2018-04-15       10.1016/j.eswa.2017.11.050      None   
1  2018-03-15       10.1016/j.eswa.2017.10.037      None   
2  2018-02-01  10.1016/j.ijinfomgt.2017.08.002      None   
3  2018-02-01  10.1016/j.prevetmed.2017.11.020      None   
4  2018-01-17     10.1016/j.neucom.2017.08.022  18728286   
5  2018-01-15     10.1016/j.knosys.2017.10.031      None   
6  2018-01-02    10.1080/14737167.2017.1359542  17448379   
7  2018-01-01     10.1007/978-981-10-6445-6_72  18761119   
8  2018-01-01     10.1007/978-3-319-71746-3_16      None   
9  2018-01-01     10.1007/978-3-319-68385-0_11      None   

                                           full_text           isbn      issn  \
0  http://api.elsevier.com/content/article/eid/1-...           None  09574174   
1  http://api.elsevier.com/content/article/eid/1-...           None  09574174   
2  http://api.elsevier.com/content/article/eid/1-...           None  02684012   
3  http://api.elsevier.com/content/article/eid/1-...           None  01675877   
4  http://api.elsevier.com/content/article/eid/1-...           None  09252312   
5  http://api.elsevier.com/content/article/eid/1-...           None  09507051   
6                                               None           None  14737167   
7                                               None  9789811064449  18761100   
8                                               None  9783319717456  18650929   
9                                               None  9783319683843  21945357   

  page_range                                   publication_name    scopus_id  \
0     86-102                   Expert Systems with Applications  85037330308   
1      81-93                   Expert Systems with Applications  85032512464   
2        1-6    International Journal of Information Management  85029596678   
3      60-69                     Preventive Veterinary Medicine  85037636361   
4    133-140                                     Neurocomputing  85031031943   
5    120-133                            Knowledge-Based Systems  85034955336   
6      83-91  Expert Review of Pharmacoeconomics and Outcome...  85026547609   
7    655-662            Lecture Notes in Electrical Engineering  85034022945   
8    181-193  Communications in Computer and Information Sci...  85037536967   
9    123-135      Advances in Intelligent Systems and Computing  85032702838   

  subtype_description                                              title  \
0             Article  Enhanced movie content similarity based on tex...   
1             Article  GIST: A generative model with individual and s...   
2             Article  Characterizing diabetes, diet, exercise, and o...   
3             Article  Analysing the opinions of UK veterinarians on ...   
4             Article     A Topic Drift Model for authorship attribution   
5             Article  Improving user recommendation by extracting so...   
6             Article  Cost-effectiveness of dolutegravir/abacavir/la...   
7    Conference Paper  Tourism Information Search Based on Dynamic At...   
8    Conference Paper  Multi-objective topic modeling for exploratory...   
9    Conference Paper  Topic modeling for unsupervised concept extrac...   

  volume  
0     96  
1     94  
2     38  
3    150  
4    273  
5    140  
6     18  
7    458  
8    789  
9    683  
</code></pre>

<hr>

#### Full text link

{% highlight python %}
>>> full_text_link_arr = search_df.full_text.values
>>> full_text_link_arr
{% endhighlight %}
<pre><code>array(['http://api.elsevier.com/content/article/eid/1-s2.0-S0957417417308059',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0957417417307200',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0268401217306126',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0167587717300223',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0925231217313759',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0950705117305002',
None, None, None, None,
'http://api.elsevier.com/content/article/eid/1-s2.0-S0957417417305948',
None, None,
'http://api.elsevier.com/content/article/eid/1-s2.0-S0020025516313706',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0190962217325847',
None, None, None, None, None, None,
'http://api.elsevier.com/content/article/eid/1-s2.0-S0167923617302130',
None, None,
'http://api.elsevier.com/content/article/eid/1-s2.0-S1532046417302605',
'http://api.elsevier.com/content/article/eid/1-s2.0-S0743731517302174',
None,
'http://api.elsevier.com/content/article/eid/1-s2.0-S0278584617302130',
None,
'http://api.elsevier.com/content/article/eid/1-s2.0-S1386505617304185'], dtype=object)
</code></pre>


For those with full text links, you are able to get all the text by calling `scopus.retrieve_full_text()`:

{% highlight python %}
>>> full_text = scopus.retrieve_full_text(full_text_link_arr[2])
>>> start = 39500
>>> full_text[start:start+10000]
{% endhighlight %}

<pre class='longoutput'><code>"between 1980 and 2014, with more than 1.9 billion adults considered as overweight and over 600 million adults considered as obese in 2014 (World Health Organization Fact Sheet, 2016). Since the 1970s, obesity has risen 37% affecting 25% of the U.S. adults (Flegal, Carroll, Kit, & Ogden, 2012). Similar upward trends of obesity have been found in youth populations, with a 60% increase in preschool aged children between 1990 and 2010 (Harvard HSPH, 2017). Overweight and obesity are the fifth leading risk for global deaths according to the European Association for the Study of Obesity (World Health Organization Fact Sheet, 2016). Excess energy intake and inadequate energy expenditure both contribute to weight gain and diabetes (Hill, Wyatt, & Peters, 2012; Wing et al., 2001).\n                  Obesity can be reduced through modifiable lifestyle behaviors such as diet and exercise (Wing et al., 2001). There are several comorbidities associated with being overweight or obese, such as diabetes (Kopelman, 2000). The prevalence of diabetes in adults has risen globally from 4.7% in 1980 to 8.5% in 2014. Current projections estimate that by 2050, 29 million Americans will be diagnosed with type 2 diabetes, which is a 165% increase from the 11 million diagnosed in 2002 (Boyle et al., 2001). Studies show that there are strong relations among diabetes, diet, exercise, and obesity (DDEO) (Association et al., 2004; Barnard et al., 2009; Hartz, Rupley, Kalkhoff, & Rimm, 1983; Wing et al., 2001); however, the general public's perception of DDEO remains limited to survey-based studies (Tompson et al., 2012).\n                  The growth of social media has provided a research opportunity to track public behaviors, information, and opinions about common health issues. It is estimated that the number of social media users will increase from 2.34 billion in 2016 to 2.95 billion in 2020 (Statista, 2017). Twitter has 316 million users worldwide (Olanoff, 2015) providing a unique opportunity to understand users’ opinions with respect to the most common health issues (Mejova, Weber, & Macy, 2015). Publicly available Twitter posts have facilitated data collection and leveraged the research at the intersection of public health and data science; thus, informing the research community of major opinions and topics of interest among the general population (Nasukawa & Yi, 2003; Wiebe et al., 2003; Zabin & Jefferies, 2008) that cannot otherwise be collected through traditional means of research (e.g., surveys, interviews, focus groups) (Eichstaedt et al., 2015; Wartell, 2015). Furthermore, analyzing Twitter data can help health organizations such as state health departments and large healthcare systems to provide health advice and track health opinions of their populations and provide effective health advice when needed (Mejova et al., 2015).\n                  Among computational methods to analyze tweets, computational linguistics is a well-known developed approach to gain insight into a population, track health issues, and discover new knowledge (Moreland-Russell, Tabak, Ruhr, & Maier, 2014; Paul & Dredze, 2011, 2012; Zhao et al., 2011). Twitter data has been used for a wide range of health and non-health related applications, such as stock market (Bollen, Mao, & Zeng, 2011) and election analysis (Tumasjan, Sprenger, Sandner, & Welpe, 2010). Some examples of Twitter data analysis for health-related topics include: flu (Culotta, 2010; Lampos & Cristianini, 2010, 2012; Lampos, De Bie, & Cristianini, 2010; Ritterman, Osborne, & Klein, 2009; Szomszor, Kostkova, & De Quincey, 2010), mental health (Coppersmith, Dredze, Harman, & Hollingshead, 2015), Ebola (Lazard, Scheinfeld, Bernhardt, Wilcox, & Suran, 2015; Odlum & Yoon, 2015), Zika (Fu et al., 2016), medication use (Buntain & Golbeck, 2015; Hanson, Cannon, Burton, & Giraud-Carrier, 2013; Scanfeld, Scanfeld, & Larson, 2010), diabetes (Harris, Mueller, Snider, & Haire-Joshu, 2013), and weight loss and obesity (Dahl, Hales, & Turner-McGrievy, 2016; Ghosh & Guha, 2013; Harris et al., 2014; Turner-McGrievy & Beets, 2015; Vickey, Ginis, & Dabrowski, 2013).\n                  The previous Twitter studies have dealt with extracting common topics of one health issue discussed by the users to better understand common themes; however, this study utilizes an innovative approach to computationally analyze unstructured health related text data exchanged via Twitter to characterize health opinions regarding four common health issues, including diabetes, diet, exercise and obesity (DDEO) on a population level. This study identifies the characteristics of the most common health opinions with respect to DDEO and discloses public perception of the relationship among diabetes, diet, exercise and obesity. These common public opinions/topics and perceptions can be used by providers and public health agencies to better understand the common opinions of their population denominators in regard to DDEO, and reflect upon those opinions accordingly.\n               \n               \n                  2\n                  Methods\n                  Our approach uses semantic and linguistics analyses for disclosing health characteristics of opinions in tweets containing DDEO words. The present study included three phases: data collection, topic discovery, and topic-content analysis.\n                  \n                     2.1\n                     Data collection\n                     This phase collected tweets using Twitter's Application Programming Interfaces (API) (Twitter, 2017). Within the Twitter API, diabetes, diet, exercise, and obesity were selected as the related words (Wing et al., 2001) and the related health areas (Paul & Dredze, 2011). Twitter's APIs provides both historic and real-time data collections. The latter method randomly collects 1% of publicly available tweets. This paper used the real-time method to randomly collect 10% of publicly available English tweets using several pre-defined DDEO-related queries (Table 1\n                        ) within a specific time frame. We used the queries to collect approximately 4.5 million related tweets between 06/01/2016 and 06/30/2016. The data will be available in the first author's website. Fig. 1\n                         shows a sample of collected tweets in this research.\n                  \n                  \n                     2.2\n                     Topic discovery\n                     To discover topics from the collected tweets, we used a topic modeling approach that fuzzy clusters the semantically related words such as assigning “diabetes”, “cancer”, and “influenza” into a topic that has an overall “disease” theme (Karami, 2015; Karami, Gangopadhyay, Zhou, & Kharrazi, 2017). Topic modeling has a wide range of applications in health and medical domains such as predicting protein-protein relationships based on the literature knowledge (Asou & Eguchi, 2008), discovering relevant clinical concepts and structures in patients’ health records (Arnold, El-Saden, Bui, & Taira, 2010), and identifying patterns of clinical events in a cohort of brain cancer patients (Arnold & Speier, 2012).\n                     Among topic models, Latent Dirichlet Allocation (LDA) (Blei, Ng, & Jordan, 2003) is the most popular effective model (Lu, Mei, & Zhai, 2011; Paul & Dredze, 2011) as studies have shown that LDA is an effective computational linguistics model for discovering topics in a corpus (Hong & Davison, 2010; Mcauliffe & Blei, 2008). LDA assumes that a corpus contains topics such that each word in each document can be assigned to the topics with different degrees of membership (Karami & Gangopadhyay, 2014; Karami, Gangopadhyay, Zhou, & Kharrazi, 2015a, 2015b).\n                     Twitter users can post their opinions or share information about a subject to the public. Identifying the main topics of users’ tweets provides an interesting point of reference, but conceptualizing larger subtopics of millions of tweets can reveal valuable insight to users’ opinions. The topic discovery component of the study approach uses LDA to find main topics, themes, and opinions in the collected tweets.\n                     We used the Mallet implementation of LDA (Blei et al., 2003; McCallum, 2002) with its default settings to explore opinions in the tweets. Before identifying the opinions, two pre-processing steps were implemented: (1) using a standard list for removing stop words, that do not have semantic value for analysis (such as “the”); and, (2) finding the optimum number of topics. To determine a proper number of topics, log-likelihood estimation with 80% of tweets for training and 20% of tweets for testing was used to find the highest log-likelihood, as it is the optimum number of topics (Wallach, Murray, Salakhutdinov, & Mimno, 2009). The highest log-likelihood was determined 425 topics.\n                  \n                  \n                     2.3\n                     Topic content analysis\n                     The topic content analysis component used an objective interpretation approach with a lexicon-based approach to analyze the content of topics. The lexicon-based approach uses dictionaries to disclose the semantic orientation of words in a topic. Linguistic Inquiry and Word Count (LIWC) is a linguistics analysis tool that reveals thoughts, feelings, personality, and motivations in a corpus (Karami & Zhou, 2014a, 2014b, 2015). LIWC has accepted rate of sensitivity, specificity, and English proficiency measures (Golder & Macy, 2011). LIWC has a health related dictionary that can help to find whether a topic contains words associated with health. In this analysis, we used LIWC to find health related topics.\n                  \n               \n               \n                  3\n                  Results\n                  Obesity and Diabetes showed the highest and the lowest number of tweets (51.7% and 8.0%). Diet and Exercise formed 23.7% and 16.6% of the tweets (Table 1).\n"
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
