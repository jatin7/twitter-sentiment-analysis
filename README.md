Twitter Sentiment Analysis
==========================

Retrieve tweets using Spark Streaming,    
language detection & sentiment analysis (StanfordNLP),    
live dashboard using Kibana.
Ingest the tweets to MapR-DB
Index tweets in Elasticsearch
Live dashboard using Kibana

Launch:

    # Compile the Twitter Sentiment Analysis jar
    JAVA_OPTS=-Xmx2G sbt clean package assembly

    # Create a table in MapR-DB to store the Twitter messages plus the sentiment analysis result
    su - mapr
    hbase shell
    create 'twitter_sentiment', 'TwitterSentiment'


    Create ElasticSearch Index
        chmod a+x insert.dashboard.sh
        ./insert.dashboard.sh
        
    # Launch the Twitter capture and store the messages in MapR-DB & Elasticsearch
    su - mapr

    #In order to run the job, you have to clone the project and compile it with sbt as usual.
    git clone https://github.com/jatin7/twitter-sentiment-analysis.git
    cd twitter-sentiment-analysis

    /opt/mapr/spark/spark-*/bin/spark-submit \
    --class com.github.vspiewak.TwitterSentimentAnalysis \
    --master local[2] \
    target/twitter-sentiment-analysis-0.1-SNAPSHOT.jar \
    <consumer_key> \
    <consumer_secret> \
    <access_token> \
    <access_token_secret> \
    <maprdbandelastic|maprdbjsonandelastic|maprdbonly|maprdbjsononly|elasticonly> \
    </path/to/maprdb-binary-table> \
    <ColumnFamily> \
    /user/mapr/out \
    [<filters>]
    
    Do you want to know what is going on with BigData and MapR?
    i.e. 
    
    /opt/mapr/spark/spark-2.1.0/bin/spark-submit \
    --class com.github.vspiewak.TwitterSentimentAnalysis \
    --master local[2] \
    target/twitter-sentiment-analysis-0.1-SNAPSHOT.jar \
    <consumer_key> \
    <consumer_secret> \
    <access_token> \
    <access_token_secret> \
    <maprdbandelastic|maprdbjsonandelastic|maprdbonly|maprdbjsononly|elasticonly> \
    twitter_sentiment \
    TwitterSentiment \
    /user/mapr/out \
    Hadoop MapR



Original Author : https://github.com/vspiewak/twitter-sentiment-analysis 
