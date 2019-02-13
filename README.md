# User journey through semantic analysis informed probabilistic modelling

Language is the primary method for users to interact with a website, especially during their early engagements.  Combining text analysis and site metrics, the Analytics team intend to quantitatively map how users interact with government services and information during various life events across the digital environment. Key terms associated with life events will be extracted from documents to form a lexicon*. An algorithm will use this lexicon to rank internal search queries, identifying users who may be undertaking that life event. The pages that users accessed after the query will be identified using Google Analytics and brought together to form a network of webpages that correlate to that life event.  The Analytics team will then apply network analytics methods to identify core nodes in that network for investigation.

If the experiment provides meaningful results, the Analytics team will expand the methodology to identify features that will underpin a machine learning analysis.    

# Methodology:
People’s initial engagement with a website is predominantly through text, mediated through a search engine.  Preliminary investigations have shown that organic search, and Google in particular, is a major traffic source to the .gov.au domain (Image 1).  

This use of language, rather than clicking on links, provides an opportunity to analyse the text that entered into internal search functions and correlate those queries to life events. may allow a quantitative analysis of life event journeys across the .gov.au domain.  A life events are “common, crucial moments or stages in the lives of citizens or the lifespan of a business. For the user, accessing the services they want … typically involves multiple contacts with more than one administration”. As these services are defined, there are terms that users may have a tendency to enter into a search function, both external and internal to the website.

Image 1. A network map of websites linked by referring domain.  Highlighted is Google and its links across the government’s digital domain.

An automated way of identifying these terms is by applying Zpif’s law to documents associated with the life event. Zipf’s law states that there is a power law relationship between a term’s rank in a document is inversely proportional to its frequency (Chart 1).  Thus the word “the” may have the highest frequency but the lowest rank, whereas a name may have the lowest frequency but the highest rank, or value.  Applying Zipf’s law to a large number of documents associated with a life event should identify an associated group of key terms terms.  These words will then be used as a vector to rank a large collection of search queries.  Each word in the query compared to the vector and given a score of one.  This is then totaled across the search query to give it a score.  

Chart 1. Term frequency - inverse document frequency analysis of carersgateway.gov.au webpages identifying words that may form the carers lexicon.

Search queries are filtered based on a chosen score or ratio. The webpages users accessed after the search query and additional pages will be downloaded from Google Analytics.  A directed network will then be constructed based on this data for visualisation and further analysis. 

# What does failure look like in Google Analytics?
Hypotheses:
Building upon Wildebeest phase one work, identifying user journey language and network maps we will:
Develop a simple, binary classification model that will group user journeys through the .gov.au domain space into ‘unsuccessful’ and ‘not-unsuccessful’ clusters.
Explore the use of multilevel logistic regression to create a model that identifies unsuccessful and undefined user journeys.
Benefits
Understanding the user breakpoints (failures) in the .gov.au domain space.
Enhancing dashboard’s value to agencies and ministers through greater use of a consistent reporting.  
Provide additional value to GA360 subscribers by reducing agency reporting burden. 

# Assumptions
The initial model assumes that a user only has a single query when coming to a .gov.au website, and is only actioning one task.
The initial model assumes that taking a long time to action a task is ‘unsuccessful’, and that a long time in internet terms is 2 minutes or more spent on one page
The initial model assumes that seeking out a contacts page, after looking at (at least) one other page is ‘unsuccessful’. It also assumes that should a user go directly to a contacts page, this was their original intention and is ‘not-unsuccessful’
The initial model assumes that Lostness factor will provide equal value across multiple websites, despite being created for single website (and single purpose) use based on what known steps a user would take that are fastest (which we do not know for every website that we have data for).
This model only applies to unauthenticated web browsing as google analytics does not collect data from authenticated activity.

# Methodology
Identify suitable Google Analytics dimensions and metrics to be used in the test/train time series dataset
Apply Google Analytics Dimensions and Metrics to Lostness factor equation: 

L = Lostness
N = The number of different screens visited during the task
S = The total number of screens visited during the task
R = the minimum number of screens that must be visited to complete the task
Determine how we view Lostness within Google Analytics and download a small dataset to test train methodology
We will create a data model using K-fold cross validation to support a multivariable regression:

We will randomly sample a download of one weeks data for humanservices.gov.au for a hundred and fifty thousand records. Then
We will run a function across that random set that queries each of the columns with a true false query based around our indicators for unsuccessful. 
Another algorithm will sum this query and if the total is 3 or greater we will mark the observation as unsuccessful. 
We will then apply a k-fold cross validation model across the random set to build a model of unsuccessful or not-successful. 
Finally we will apply the model to the residual 600,000 observation in our DHS extract.

Initial Google Dimensions and  Metrics and unsuccessful characteristic

# Dimension & Metric 
unsuccessful characteristic

Source
ExitPathPage page contains “contact”
SearchUsed “Visits With Site Search”
PageDepth value > 3
Date  Used to create Time series
Hour  Used to create Time series
Minute Used to create Time series
Users
timeOnPage value < 45 & or value > 121
SearchDepth value > 3
SearchRefinement
SearchDuration value > 12
SearchExits value > 0
