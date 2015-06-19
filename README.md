# system_design
*How to prepare for system design questions

#Objective
I collected and studied from a lot of links while preparing for interviews this year and realized that unlike coding questions which has plenty of good repos and combined resources , system design remains elusive. People end up reading from scattered resources and might get pigeon-holed into studying one specific domain and get tongue tied when answering such questions. Hence I collected these links and design techniques for interviews , thought I should share with everyone :).
If you are already familiar with the basics ( given below) it will take you ~2 months to gain a strong foothold over such questions . If you have much less time , scroll down to the bottom for the tl;dr version :)

#Disclaimer 
I am not a system design expert and do not have a ton of experience in this domain , but over the course of giving interviews , reading up from many different sources have a decent idea of what to study and how to answer such questions . This is a domain that can take year to master even one facet of system design , hence I would recommend instead of spending too much time on one topic , try to spread your time , get a broader overview of the entire domain then go into what you might be working on or what interests you more. (Also depends on who are you interviewing with and the level you are interviewing for). Also I have never been in an interview for mobile app dev so dont have much idea on that , feel free to send pull requests with that section also.

#Where to start from?

For a very broad overview please go through these lectures , really useful:
* [david malans cs75 scalability talk](https://www.youtube.com/watch?v=-W9F__D3oY4&list=PLmhRNZyYVpDmLpaVQm3mK5PY5KB_4hLjE&index=10)
Feel free to go through other lectures if needed. 

* [david huffman's talk , scaling up talk](https://www.udacity.com/course/web-development--cs253)

* [scalability for dummies](http://www.lecloud.net/tagged/scalability)
* 
These talks should give you decent ammo to start formulating some architectures yourself . 

##BASICS

But before you begin , here are some topics(in no particular order) which in my opinion you should have a decent idea of before proceeding.

1.Operating system basics: how a file system , virtual memory , paging , instruction execution cycle etc work
(For starters silbershatz should be enough , if you already have decent knowledge try stallings book on OS)
2. Networking basics : 
Should know the TCP/IP stack , basics of how internet , HTTP , TCP/IP work at the minimum . cs75 on youtube (1st lecture ) should give a broad overview . I personally love [networking-a top down approach](http://www.amazon.com/Computer-Networking-Top-Down-Approach-Edition/dp/0132856204) .
3. Concurrency basics : threads , processes , threading in the language you know . Locks , mutex etc . 
4. DB basics: types of DB's (sql vs no sql etc ),hashing and indexing , EAV based dbs . Sharding , caching for dbs , master slave etc
5. A basic idea of how a basic architecture is , say load balancers , proxy , servers , db servers , caching servers , precompute , logging big data etc. Just know broadly what is each layer for.  
6. very basic summary of what the [CAP therem](http://robertgreiner.com/2014/08/cap-theorem-revisited/) is (Have never been asked about the theorem itself , but knowing it will help you in designing large scale systems. 

# How to answer in interviews

I found [hiredintech](http://www.hiredintech.com/system-design) videos an excellent place to start with . The way how to approach a design question as given in the link is really useful . It goes into how we start with clearing the use-cases of the system , then thinking in abstract manner of the various component and the interactions . Think about the bottlenecks of the system and what is more critical for your system ( eg latency vs reliability vs uptime etc) Address those giving the tradeoff of your appraoch. 

[system design in crack the coding interview](http://www.flipkart.com/cracking-coding-interview-150-programming-questions-solutions-english-5th/p/itmdz4pvzbhcv6uv) : good approach on how to begin attacking a problem by first solving for a small usecase then expanding the system .

The best way to prepare for such questions is do mock interviews , pick any topic (given below) try to comeup with a design and then go and see how and why it is designed in that manner. There is absolutely no alternative to practice!! Whiteboarding a system design question is similar to actually writing code and testing it ! Just reading will only take you so far.

# Steps how I approach the system design questions in interviews

These are the steps I go through mentally in the interviews , followed by actual interview experiences:

a) Be absolutely sure you understand the problem being asked , clarify on the onset rather than assuming anything 
b) Use-cases . This is critical , you MUST know what is the system going to be used for , what is the scale it is going to be used for . Also constraints like requests per second, requests types, data written per second, data read per second.
c) Solve the problem for a very small set, say 100 users . This will broadly help you figure out the data structures , components , abstract design of the overall model
d) Write down the various components figured out so far and how will they interact with each other.
e)  As a rule of thumb remember atleast these :
 1.processing and servers
 2.storage 
 3.caching 
 4.concurrency and communication
 5.security 
 6.load balancing and proxy 
 7.CDN 
 8. Monetization : if relevant , how will you monetize?
 eg . What kind of DB (will mysql do ? or nosql fits btr? ) , do you need caching (almost always !) and how much , is security a prime concern? 
f) Special cases for the question asked. Eg say designing a system for storing thumbnails , will a file system suffice ? What if you have to scale for facebook or google? Will a nosql based db work?
g) After I have my components in place , what I generally try to do is look for minor optimization in various places according to the usecases , various tradeoffs that will help in better scaling in 99% cases .
h) [Scaling out or up]  (http://highscalability.com/blog/2014/5/12/4-architecture-issues-when-scaling-web-applications-bottlene.html)
i) Check with the interviewer is there any other special case he is looking to solve ? Also it really helps if you know about the company you are interviewing with , what its architecture is , what will the interviewer have more interest in based on the company and what he works on ? 

# Common Design questions :
It generally depends what you are and you will be working on . Also what your level is but these are some of the more frequent interview questions .

* Design amazon's frequently viewed product page (eg. which shows the last 5 items you saw)
* Design an online poker game for multiplayer . Solve for persistence , concurrency , scale . Draw the ER diagram for this 
* Design a [url compression system] (http://www.hiredintech.com/system-design/the-system-design-process/)
* [Search engine](http://infolab.stanford.edu/~backrub/google.html) ( generally asked with people who have some domain knowledge ) : basic crawling , collection , hashing etc. Dependes on your expertise on this topic
* Design dropbox's architecture . [good talk on this](https://www.youtube.com/watch?v=PE4gwstWhmc)
* Design a [picture sharing website](http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html). How will you store thumbnails , photos? Usage of CDNS? caching at various layers etc .
* * Design a news feed (eg facebook , twitter ) : [news feed](http://www.quora.com/Software-Engineering-Best-Practices/What-are-best-practices-for-building-something-like-a-News-Feed)
* Design a product based on maps , eg hotel / ATM finder given a location. 
* Design malloc , free and [garbage collection system](http://courses.cs.washington.edu/courses/csep521/07wi/prj/rick.pdf) . What data structures to use? decorator pattern over malloc etc
* Design a site like [junglee.com](http://www.junglee.com/) i.e price comparision , availability on ecommerce websites. When and will you cache , how much to query , how to crawl efficiently over ecommerce sites, sharding of dbs , basic db design
* A web application for chatting , eg [whatsapp](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html) , facebook chat . Issues of each , scaling problems , status and availablility notification etc.
* Design a system for collaberating over a document simulataneously (eg [google docs](https://neil.fraser.name/writing/sync/))
* (very common:) top 'n' or most frequent items of a running stream of data
* Design election commission architecture :
 Let's say we work with the Election Commission. On Counting day, we want to collate the votes received at the lakhs of voting booths all over the country. Each booth has a voting machine, which, when connected to the network, returns an array of the form {[party_id, num_votes],[party_id_2, num_votes_2],...}. We want to collect these and get the current scores in real time. The report we need continuously is how many seats is each party leading in. Please design a system f rthis
* Design a logging system
 (For web applications, it is common to have a large number of servers running the same application, with a load balancer in front to distribute the incoming requests. In this scenario, we want to check and alarm in case an exception is thrown in any of the servers. We want a system that checks for appearance of specific words, "Exception", "Disk Full" etc. in the logs of any of the servers. How would you design this system?)

# Architecture and engineering blogs of various companies:

Personally I looked into the following architectures:

* [Google file system](http://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf)
* [facebook haystack needle architecture](https://www.usenix.org/legacy/event/osdi10/tech/full_papers/Beaver.pdf)
* [facebook graph api](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/data-store/tao-facebook-distributed-datastore-atc-2013.pdf)
* [Basics of google search](http://infolab.stanford.edu/~backrub/google.html)
* [youtube architecture and optimizations for video](https://www.youtube.com/watch?v=ZW5_eEKEC28)
* [Twitter scaling](https://www.youtube.com/watch?v=z8LU0Cj6BOU) and facebook feeds
* [Instagram](http://instagram-engineering.tumblr.com/post/13649370142/what-powers-instagram-hundreds-of-instances) and other image based social networks
* [Memcache scaling by facebook](https://cs.uwaterloo.ca/~brecht/courses/854-Emerging-2014/readings/key-value/fb-memcached-nsdi-2013.pdf)
* Broad overview and advantages of Redis , mongodb , cassandra. 
* Basics of messaging frameworks like Kafka , queuing architectures like rabbitmq .
* [Google architecture] (http://highscalability.com/google-architecture)

#company blog links 

courtesy [checkcheckzz](https://github.com/checkcheckzz/system-design-interview#toc)

Depending on where you are interviewing , go through the company blog . VERY USEFUL IN INTERVIEWS! It really helps if you have an idea of the architecture , as the questions asked will generally be of that domain and your prior knowledge will help out here.

* [High Scalability](http://highscalability.com/)
* [The GitHub Blog](https://github.com/blog/category/engineering)
* [Engineering at Quora](http://engineering.quora.com/)
* [Yelp Engineering Blog](http://engineeringblog.yelp.com/)
* [Twitter Engineering](https://engineering.twitter.com/)
* [Facebook Engineering](https://www.facebook.com/Engineering)
* [Yammer Engineering](http://eng.yammer.com/blog/)
* [Etsy Code as Craft](http://codeascraft.com/)
* [Foursquare Engineering Blog](http://engineering.foursquare.com/)
* [Airbnb Engineering](http://nerds.airbnb.com/)
* [WebEngage Engineering Blog](http://engineering.webengage.com/)
* [LinkedIn Engineering](http://engineering.linkedin.com/blog)
* [The Netflix Tech Blog](http://techblog.netflix.com/)
* [BankSimple Simple Blog](https://www.simple.com/engineering/)
* [Square The Corner](http://corner.squareup.com/)
* [SoundCloud Backstage Blog](https://developers.soundcloud.com/blog/)
* [Flickr Code](http://code.flickr.net/)
* [Instagram Engineering](http://instagram-engineering.tumblr.com/)
* [Dropbox Tech Blog](https://tech.dropbox.com/)
* [Cloudera Developer Blog](http://blog.cloudera.com/blog/)
* [Bandcamp Tech](http://bandcamptech.wordpress.com/)
* [Oyster Tech Blog](http://tech.oyster.com/)
* [THE REDDIT BLOG](http://www.redditblog.com/)
* [Groupn Engineering Blog](https://engineering.groupon.com/)
* [Songkick Technology Blog](http://devblog.songkick.com/)
* [Google Research Blog](http://googleresearch.blogspot.com/)
* [Pinterest Engineering Blog](http://engineering.pinterest.com/)
* [Twilio Engineering Blog](http://www.twilio.com/engineering)
* [Bitly Engineering Blog](http://word.bitly.com/)


# Low on time ?

**I would HIGHLY recommend you dont take a shortcut unless you have a week or so for an interview . System design is best learnt by practicing , shortcuts might help you in the short term , but would recommend coming back to this link for an indepth understanding after the interview**

a)Go through cs76 and udacity's links given above for scaling systems. 
b)Go through the engineering blog of the company you are interviewing in (or if its a startup go through the link of the company closest to yours)
c)See this talk : http://www.hiredintech.com/system-design/the-system-design-process/ and develop a process for how to answer such questions .
d) remember these terms , just roll over them in your interview in your mind , and if relevant mention it in the interview 
.1.processing and servers
 2.storage 
 3.caching 
 4.concurrency and communication
 5.security 
 6.load balancing and proxy 
 7.CDN 
 8. Monetization

Best of luck :) , feel free to send pull requests to add more content to this git! Will be updating it from time to time .

