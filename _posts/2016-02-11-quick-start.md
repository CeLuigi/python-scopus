---
layout: page
title: "Quick Start"
category: doc
date: 2016-02-11 22:37:36
---

### _Note that API keys are hidden. Please get your own API keys._

#### * *A quick example on general search*
{% highlight python %}
from pyscopus.scopus import Scopus
scopus = Scopus(key)
# search for documents
docs = scopus.search("KEY(interdisciplinary collaboration)", count=20)
{% endhighlight %}

By default, the following output will be shown:
<pre class="longoutput"><code>A total number of  1230  records for the query.
Showing 20 of them.
                                          affiliation       aggregation_type  \
0   University of London, Institute of Education, ...                Journal   
1            Simon Fraser University, Burnaby, Canada                Journal   
2         Taipei City Hospital Taiwan, Taipei, Taiwan                Journal   
3   Virginia Polytechnic Institute and State Unive...                Journal   
4            University of Belgrade, Belgrade, Serbia            Book Series   
5                University of Nordland, Bodo, Norway                Journal   
6      Indiana University, Bloomington, United States                Journal   
7   Marquette University School of Dentistry, Milw...                Journal   
8                  Sichuan University, Chengdu, China                Journal   
9           Lulea tekniska Universitet, Lulea, Sweden                Journal   
10  Universitatsklinikum Leipzig und Medizinische ...                Journal   
11  Georgia Southern University, Statesboro, Unite...                Journal   
12  University of South Carolina, Columbia, United...                Journal   
13        Chiang Mai University, Chiang Mai, Thailand                Journal   
14      University of Melbourne, Parkville, Australia                Journal   
15   Valparaiso University, Valparaiso, United States  Conference Proceeding   
16     Karadeniz Teknik Universitesi, Trabzon, Turkey  Conference Proceeding   
17  Fraunhofer Research Institution for Mechatroni...  Conference Proceeding   
18  Indiana University-Purdue University Indianapo...                Journal   
19                 Universitetet i Oslo, Oslo, Norway                Journal   

    citation_count  cover_date                            doi     eissn  \
0                0  2017-02-01              10.1002/asi.23658  23301643   
1                0  2017-01-20  10.1080/14626268.2016.1250013  17443806   
2                0  2017-01-02  10.1080/13561820.2016.1248816  14699567   
3                0  2017-01-01     10.2495/DNE-V12-N2-185-193  17557445   
4                0  2017-01-01   10.1007/978-3-319-49058-8_59      None   
5                0  2017-01-01       10.1177/0020872814559561  14617234   
6                0  2017-01-01      10.1007/s11528-016-0124-6      None   
7                0  2017-01-01     10.1016/j.msec.2016.08.055      None   
8                0  2017-01-01       10.1177/0885328216681893  15308022   
9                0  2017-01-01   10.1016/j.gexplo.2016.09.014      None   
10               0  2017-01-01      10.1007/s00101-016-0247-3  1432055X   
11               0  2016-12-01       10.1177/1049909115613315      None   
12               1  2016-12-01             10.1002/ajcp.12105      None   
13               0  2016-12-01              10.1111/ger.12208  17412358   
14               1  2016-12-01             10.1037/met0000091      None   
15               0  2016-11-28       10.1109/FIE.2016.7757485      None   
16               0  2016-11-28     10.1109/ITHET.2016.7760730      None   
17               0  2016-11-22    10.1109/SysEng.2016.7753141      None   
18               0  2016-11-16  10.1080/10911359.2016.1236000  15403556   
19               0  2016-11-10      10.1007/s10699-016-9509-4  15728471   

             isbn      issn page_range  \
0            None  23301635    378-391   
1            None  14626268       1-16   
2            None  13561820     98-104   
3            None  17557437    185-193   
4   9783319490571  21945357    543-549   
5            None  00208728      45-60   
6            None  87563894      46-52   
7            None  09284931    913-929   
8            None  08853282    901-910   
9            None  03756742    120-132   
10           None  00032417      45-51   
11           None  10499091   996-1012   
12           None  00910562    303-308   
13           None  07340664    545-553   
14           None  1082989X    507-525   
15  9781509017904  15394565              
16  9781509007783      None              
17  9781509007936      None              
18           None  10911359    565-574   
19           None  12331821       1-18   

                                     publication_name    scopus_id  \
0   Journal of the Association for Information Sci...  84962866808   
1                                  Digital Creativity  85009973282   
2                   Journal of Interprofessional Care  85006836390   
3   International Journal of Design and Nature and...  85008429090   
4       Advances in Intelligent Systems and Computing  85007284935   
5                           International Social Work  85008654399   
6                                          TechTrends  84994222304   
7                 Materials Science and Engineering C  85010821977   
8                Journal of Biomaterials Applications  85006700597   
9                  Journal of Geochemical Exploration  84992597891   
10                                       Anaesthesist  85003906133   
11  American Journal of Hospice and Palliative Med...  84994104586   
12           American Journal of Community Psychology  85006141494   
13                                      Gerodontology  84940851069   
14                              Psychological Methods  85004097351   
15  Proceedings - Frontiers in Education Conferenc...  85006790217   
16  2016 15th International Conference on Informat...  85007322764   
17  ISSE 2016 - 2016 International Symposium on Sy...  85006511286   
18  Journal of Human Behavior in the Social Enviro...  84991503334   
19                             Foundations of Science  84994791035   

   subtype_description                                              title  \
0              Article  Impact in interdisciplinary and cross-sector r...   
1     Article in Press  Pain matters: outliers in new tribes and terri...   
2              Article  Different perceptions of interprofessional col...   
3              Article  The de Mestral project: Using macro photo-jour...   
4     Conference Paper  Why does architecture need to move? The role o...   
5              Article  Do national welfare systems have an influence ...   
6              Article  Identifying Interdisciplinary Research Collabo...   
7               Review  A current overview of materials and strategies...   
8              Article  Synthesis and characterization of fluorescein-...   
9               Review   Acid rock drainage prediction: A critical review   
10             Article  Practical training for paramedics: Transformat...   
11             Article  Communication Within Hospice Interdisciplinary...   
12                Note  Cultivating Community Psychology for Future Ge...   
13             Article  Development of a community-based oral healthca...   
14             Article  Gaining insights from social media language: M...   
15    Conference Paper  Robotic football dance team: An engineering Fi...   
16    Conference Paper  Performance evaluation of practice courses usi...   
17    Conference Paper  A concept for managing information in early st...   
18             Article  Promoting public health through community enga...   
19    Article in Press  Vibrantly Entangled in Sri Lanka: Food as the ...   

           volume  
0              68  
1            None  
2              31  
3              12  
4             540  
5              60  
6              61  
7              70  
8              31  
9             172  
10             66  
11             33  
12             58  
13             33  
14             21  
15  2016-November  
16           None  
17           None  
18             26  
19           None  
</code></pre>

You can see the results are now ordered by dates. A *TODO* at this moment is to add a sort parameter to allow different sorting schemes.

#### * *An example data collection pipeline*
First we search for a spefic author:

{% highlight python %}
# search for my advisor
query_dict = {'affil': 'University of Iowa', 'authfirst': 'Kang', 'authlast': 'Zhao'}
author_results = scopus.search_author(query_dict)
{% endhighlight %}

This returns `author_results` as a list of dictionary and by default print the following output: 
<pre><code>A total number of  3  records for the query.
             affiliation    author_id  document_count       name
0     University of Iowa  36635367700              24  Kang Zhao
1     University of Iowa  57077574400               1  Kang Zhao
2  Iowa State University  56995506800               1  Kang Zhao
</code></pre>


We can use his unique author id `36635367700` to retrieve some basic information:

{% highlight python %}
kang_info = scopus.retrieve_author('36635367700')
{% endhighlight %}

<pre><code>Name: Kang Zhao
Affiliation: University of Iowa, Department of Management Sciences (n/a,Iowa City,IA,n/a,United States)
</code></pre>

`kang_info` is a dictionary, containing first name, last name, current/previous affiliations, document count, citation count, cited-by count, journal/conference history, and subject areas. By default, `PyScopus` will save the results from `retrieve_author()` to a folder named `author_xmls/` in the current working directory. You can set `save_xml=False` when calling this function to disable this feature.
<pre class='longoutput'><code>{'current-affiliation': [{'address': 'n/a,Iowa City,IA,n/a,United States', 'id': '104227060', 'name': 'University of Iowa, Department of Management Sciences'}], 'citation-count': 73, 'last-name': 'Zhao', 'subject-areas': ['Applied Mathematics', 'Information Systems', 'Artificial Intelligence', 'Electrical and Electronic Engineering', 'Modeling and Simulation', 'Medicine (all)', 'Software', 'Computer Science (all)', 'Oncology', 'Control and Systems Engineering', 'Education', 'Human-Computer Interaction', 'Strategy and Management', 'Hardware and Architecture', 'Cancer Research', 'Computer Graphics and Computer-Aided Design', 'Computer Science Applications', 'Safety, Risk, Reliability and Quality', 'Library and Information Sciences', 'Computer Networks and Communications', 'Statistics, Probability and Uncertainty', 'Theoretical Computer Science'], 'affiliation-history': [{'address': 'n/a,Iowa City,IA,n/a,United States', 'id': '104227060', 'name': 'University of Iowa, Department of Management Sciences'}, {'address': 'n/a,Iowa City,IA,n/a,United States', 'id': '104227074', 'name': 'University of Iowa, Tippie College of Business'}, {'address': 'n/a,Iowa City,IA,n/a,United States', 'id': '60024324', 'name': 'University of Iowa'}, {'address': 'n/a,State College,PA,n/a,United States', 'id': '105050101', 'name': 'Pennsylvania State University, College of Information Sciences and Technology'}, {'address': 'n/a,State College,PA,n/a,United States', 'id': '60001439', 'name': 'Pennsylvania State University'}], 'cited-by-count': 59, 'first-name': 'Kang', 'journal-history': ['Proceedings - 21st Workshop on Information Technologies and Systems, WITS 2011', 'Proceedings - Pacific Asia Conference on Information Systems, PACIS 2014', 'Journal of the National Cancer Institute. Monographs', 'Proceedings - The 8th IEEE International Conference on Advanced Learning Technologies, ICALT 2008', 'ISCRAM 2010 - 7th International Conference on Information Systems for Crisis Response and Management: Defining Crisis Management 3.0, Proceedings', 'Information Systems and e-Business Management', 'Lecture Notes in Computer Science (including subseries Lecture Notes in Artificial Intelligence and Lecture Notes in Bioinformatics)', '16th Americas Conference on Information Systems 2010, AMCIS 2010', 'Proceedings - 2011 IEEE International Conference on Privacy, Security, Risk and Trust and IEEE International Conference on Social Computing, PASSAT/SocialCom 2011', 'IEEE Transactions on Engineering Management', 'Lecture Notes in Computer Science (including subseries Lecture Notes in Artificial Intelligence and Lecture Notes in Bioinformatics)', 'World Wide Web', '19th Workshop on Information Technologies and Systems, WITS 2009', 'IEEE Intelligent Systems', 'Proceedings of ISCRAM 2008 - 5th International Conference on Information Systems for Crisis Response and Management', 'Proceedings - SocialCom 2010: 2nd IEEE International Conference on Social Computing, PASSAT 2010: 2nd IEEE International Conference on Privacy, Security, Risk and Trust', 'Journal of the National Cancer Institute - Monographs', 'Simulation', 'IEEE Systems Journal', 'Proceedings of 20th Annual Workshop on Information Technologies and Systems', 'International Conference on Information Systems (ICIS 2013): Reshaping Society Through Information Systems Design', 'Journal of the American Medical Informatics Association : JAMIA'], 'document-count': 24}
</code></pre>

The author id can also be used to search for his publication records:

{% highlight python %}
kang_pubs = scopus.search_author_publication('36635367700')
{% endhighlight %}

`kang_pubs` is also a list of dictionaries and again the search will yield a list of publication names to standard ouput:
<pre class='longoutput'><code>A toal number of  24  records for author  36635367700
0 Leader identification in an online health community for cancer survivors:...
1 Early prediction of movie success-what, who, and when...
2 Social support and user engagement in online health communities...
3 Finding influential users of online health communities: a new metric based...
4 User recommendations in reciprocal and bipartite social networks-An online...
5 Social support and user engagement in online health communities...
6 Making sense of a healthcare forum - Smart keyword and user navigation...
7 Understanding topics and sentiment in an online cancer survivor community...
8 Who blogs what: Understanding the publishing behavior of bloggers...
9 Recommendation in reciprocal and bipartite social networks - A case study...
10 Simulating inter-organizational collaboration network: A multi-relational...
11 Get online support, feel better-sentiment analysis and dynamics in an...
12 Achieving high robustness in supply distribution networks by rewiring...
13 Analyzing the Resilience of Complex Supply Network Topologies Against...
14 Identifying leaders in an online cancer survivor community...
15 Assortativity patterns in multi-dimensional inter-organizational networks:...
16 Crossing borders, organizations, levels and technologies: IS collaboration...
17 From communication to collaboration: Simulating the emergence of...
18 Sectoral coordination in humanitarian information management: The...
19 Who blogs what: Understanding behavior, impact and types of bloggers...
20 Assessing humanitarian inter-organizational network effectiveness: The...
21 Effect of topology on the robustness of supply networks - Metrics and...
22 CyberLab: An online virtual laboratory toolkit for non-programmers...
23 Building global bridges: Coordination bodies for improved information...
</code></pre>

We can also retrieve the abstract of a certain publication using its Scopus id:
{% highlight python %}
pub_info = scopus.retrieve_abstract('84905286162')
{% endhighlight %}

The resulting `pub_info` is a dictionary containing the meta data of the specified publication. Similar to previous queries, it will by default print the info as standard output. Similar to `retrieve_author()`, this function will also export the corresponding XML file to `abstract_xmls/` in the current directory. You can set `save_xml` to `False` to prevent it from outputing.

<pre class='longoutput'><code>####Retrieved info for publication Finding influential users of online health communities: a new metric based on sentiment influence. (id: 84905286162)####
abstract:  Online health communities (OHCs) have become a major source of support for people with health problems. This research tries to improve our understanding of social influence and to identify influential users in OHCs. The outcome can facilitate OHC management, improve community sustainability, and eventually benefit OHC users. Through text mining and sentiment analysis of users' online interactions, the research revealed sentiment dynamics in threaded discussions. A novel metric--the number of influential responding replies--was proposed to directly measure a user's ability to affect the sentiment of others. Using the dataset from a popular OHC, the research demonstrated that the proposed metric is highly effective in identifying influential users. In addition, combining the metric with other traditional measures further improves the identification of influential users. Published by the BMJ Publishing Group Limited. For permission to use (where not already granted under a licence) please go to http://group.bmj.com/group/rights-licensing/permissions.</code></pre>

Sometimes you may want to search for articles within a specific venue (journal, conference, book, or report) -- the function `search_venue` comes to you! For example, we are interested in finding some papers in <a href='http://www.jmlr.org/' target='_blank'>Journal of Machine Learning Research</a> from 2013 to 2015, we can run the following code:
{% highlight python %}
mlpapers = scopus.search_venue('journal of machine learning research', year_range=(2013,2015))
{% endhighlight %}

<pre><code>A total number of  925  records for the venue journal of machine learning research from 2013 to 2015.
Showing 10 of them as requested ordered by relevency.
0) A topic modeling approach to ranking...
1) Efficient sparse clustering of high-dimensional non-spherical Gaussian...
2) Similarity-based clustering by left-stochastic matrix factorization...
3) Estimating the accuracies of multiple classifiers without labeled data...
4) Sparse activity and sparse connectivity in supervised learning...
5) Random Bayesian networks with bounded indegree...
6) Random projections for support vector machines...
7) A direct estimation of high dimensional stationary vector autoregressions...
8) Parallel MCMC with generalized elliptical slice sampling...
9) Online passive-aggressive algorithms for non-negative matrix factorization...
</code></pre>


If you want to retrieve annual citation counts for your documents of interest, <a href="http://api.elsevier.com/documentation/AbstractCitationAPI.wadl" target="_blank">Citation Overview API</a> is the way to go. However, this API requires authorization. __Please contact Elsevier developer team for support before trying this out__.

You can use `retrieve_citation` to obtain one or more documents' citation counts using their Scopus IDs. 
{% highlight python %}
pub_citations = scopus.retrieve_citation(['84905286162'])
{% endhighlight %}

The output of this function is a dictionary, with keys being Scopus IDs and values being their start year and citation counts. Specifically, Citation Overview API returns three types of citations: citation counts for each year (by default the recent three years); citation counts before the range and after the range. Standard output will also be produced as follows.
<pre><code>Scopus ID     StartYear   Previous    2014        2015        2016        Later
84905286162    2014        0       2       3       1       0
</code></pre>

To write the results to a CSV file, you can set the path to the file as a parameter of the function (here daterange is specified to retrieve a specific year range):

(*Please note that if you are searching the citation record for only one publication, you still need to put it in a list or numpy array.*)

{% highlight python %}
pub_citations = scopus.retrieve_citation(['84905286162', '0141607824'],\
     daterange=(2014,2015), write2file='citations.csv')
{% endhighlight %}

Standard output and `citations.csv` are displayed as follows.

<pre><code>Scopus ID     StartYear   Previous    2014        2015        Later
84905286162  2014        0       2       3       1
0141607824   2003        4517        1400        1327        141
</code></pre>

<table class="table table-bordered table-hover table-condensed">
<tbody><tr><td align="center">Scopus ID</td>
<td align="center">previous</td>
<td align="center">2014</td>
<td align="center">2015</td>
<td align="center">later</td>
</tr>
<tr><td align="center">84905286162</td>
<td align="center">0</td>
<td align="center">2</td>
<td align="center">3</td>
<td align="center">1</td>
</tr>
<tr><td align="center">0141607824</td>
<td align="center">4517</td>
<td align="center">1400</td>
<td align="center">1327</td>
<td align="center">141</td>
</tr>
</tbody></table>
