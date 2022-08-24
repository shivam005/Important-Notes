# Twitter-System-Design-Notes

![twitter](https://user-images.githubusercontent.com/38420375/186358760-895be707-f3e1-482b-a33c-eadc9bdfca19.png)

Apache Lucene™ is a technology suitable for nearly any application that requires structured search, full-text search, faceting, nearest-neighbor search across high-dimensionality vectors, spell correction or query suggestions.

Heron is a real-time analytics platform to process streaming. It is a distributed stream processing engine developed at Twitter. Apache storm is also serves similar purpose. 

Fanout service basically put all the latest tweet of a person into the cache memory of their follower so that whenever it has to find the data in timeline, it will retrived faster. But the scene becomes different in case of celibrity tweet, in this scenerio it is not put into the cache of all the millions or billions followers instead when they load their timeline, first of all other tweets are shown which has already been cahced and at the same time, the list of all the celebrity which is being followed is checked and their tweet is load in the cache. 

Zookeeper is the master node for all the nodes available in the redis. 
