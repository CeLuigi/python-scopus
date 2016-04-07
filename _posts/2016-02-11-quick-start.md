---
layout: page
title: "Quick Start"
category: doc
date: 2016-02-11 22:37:36
---

#### The following are some examples. (Note that API keys are hidden. Please get your own API keys.)

<br>
First we search for a spefic author:

{% highlight python %}
from pyscopus.pyscopus import Scopus
scopus = Scopus(key)
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

`kang_info` is a dictionary, containing first name, last name, current/previous affiliations, document count, citation count, cited-by count, journal/conference history, and subject areas.
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

We can also search for a certain publication using its Scopus id:
{% highlight python %}
pub_info = scopus.search_abstract('84905286162')
{% endhighlight %}

The resulting `pub_info` is a dictionary containing the meta data of the specified publication. Similar to previous queries, it will by default print the info as standard output.

<pre class='longoutput'><code>####Retrieved info for publication Finding influential users of online health communities: a new metric based on sentiment influence. (id: 84905286162)####
abstract:  Online health communities (OHCs) have become a major source of support for people with health problems. This research tries to improve our understanding of social influence and to identify influential users in OHCs. The outcome can facilitate OHC management, improve community sustainability, and eventually benefit OHC users. Through text mining and sentiment analysis of users' online interactions, the research revealed sentiment dynamics in threaded discussions. A novel metric--the number of influential responding replies--was proposed to directly measure a user's ability to affect the sentiment of others. Using the dataset from a popular OHC, the research demonstrated that the proposed metric is highly effective in identifying influential users. In addition, combining the metric with other traditional measures further improves the identification of influential users. Published by the BMJ Publishing Group Limited. For permission to use (where not already granted under a licence) please go to http://group.bmj.com/group/rights-licensing/permissions.</code></pre>

If you want to retrieve annual citation counts for your documents of interest, <a href="http://api.elsevier.com/documentation/AbstractCitationAPI.wadl" target="_blank">Citation Overview API</a> is the way to go. However, this API requires authorization. Please contact Elsevier developer team for support.

You can use `retrieve_citation` to obtain one or more documents' citation counts using their Scopus IDs. 
{% highlight python %}
pub_citations = scopus.retrieve_citation('84905286162')
{% endhighlight %}

The output of this function is a dictionary, with keys being Scopus IDs and values being their start year and citation counts. Specifically, Citation Overview API returns three types of citations: citation counts for each year (by default the recent three years); citation counts before the range and after the range. Standard output will also be produced as follows.
<pre><code>Scopus ID     StartYear   Previous    2014        2015        2016        Later
84905286162    2014        0       2       3       1       0
</code></pre>

To write the results to a CSV file, you can set the path to the file as a parameter of the function (here daterange is specified to retrieve a specific year range):

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

