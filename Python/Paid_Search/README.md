Creat by: Cathy Xueqing Zhang
This project analyze google search advertisement: Paid Search. Paid search is a form of digital marketing where search engines such as Google and Bing allow advertisers to show ads on their search engine results pages (SERPs). Paid search works on a pay-per-click model.<br/>
<br/><br/>
# Data Acquisition 
- Collect data on the 7 verticals: Auto Insurance, Hotels, Tech, Crowdfunding, Clinical Trials, E-commerce Retail, Local Services.
- Focus on the 4 dimensions of paid search: CPC, Volume, Results, Competition (See the next section for the definition of dimensions.)
<br/><br/>
## 1. Data Source Description 
<br/>
SEMrush database is the source we target to collect the data. It provides two subsets of the database that are valuable.

### 1.1 Keywords Database
<br/>
For each keyword in every vertical, the database provides the data of 8 dimensions related to the target one as listed below:
<br/>
D3443234 | D3443234
---------|---------
A | B


<br/>
Dimensions |	Description
------------ | -------------
Volume | Average times users searched for the keywords related to the selected vertical
Results | The number of URLs displayed for the keywords related to the selected vertical
CPC(USD) | Average Price the advertiser pays for one per click
- Competition : Competitive density of advertiser
- KD : How difficult it would be to rank well in organic search for the keywords in selected vertical
- Trend : Number of Volume for the past 12 months
- A list of related keywords : A list of keywords that are similar to the target one
- A list of phrase-matched keywords : A list of keywords that contain exact keyword or keyword in various order 


A snapshot of the first six dimensions
 
 

#### 1.1.2 A list of related keywords 
<br/>
Based on the algorithm of the SEMrush database, the related keywords are a list of keywords that are similar to the target one. (Similarity is based on the sense of a word)

<br/>Each related keyword has a metric that measure how closely related to the target one. (0 ~100%)

A snapshot of an example of the keywords:

 
#### 1.1.3 A list of phrase-matched keywords 
<br/>
Based on the algorithm of the SEMrush database, the phrase-matched keywords are a list of keywords that contain exact keyword or keyword in various order 
A snapshot of an example of the keywords:
 


### 1.2 Domain Database
<br/>
A snapshot of how the data look like taking one of the car insurance domain as example:

 

The use of this data will be discussed in Future Plan section.
<br/><br/>

## 2. Methods
### 2.1 Rationale
<br/>
In order to acquire the data for every vertical, we intend to collect all keywords which the targeted vertical is using for paid search and use the integrated keywords to calculate the data of the dimensions for each vertical.
<br/>
To collect all keywords of each vertical, we use the related and phrase match algorithm to estimate the totality.

### 2.2 Specific steps:

-Step 1: Set a seed keyword, normally it should be an exclusive keyword that the vertical use in paid search.
-Step 2: Set a threshold for the related metric, then acquire a list of keywords related to the seed.
-Step 3: For each keyword in the list acquired in step 2, collect the list of phrase match keywords.
-Step 4: Integrate all the data from step 3 include columns of keyword, and its dimensions.
-Step 5: Select a subset of the dataset from step 4 to calculate the data for whole vertical.

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
