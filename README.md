* Brandon Lewis
* Information Systems & Business Analytics, Park University
* CIS617: Text Analytics
* Professor: Dr. Dmitry Gimon
* Unit 8: Assignment – Executive Summary / Final Report
* Spring 2: May 10, 2026

# Executive Summary - Analysis Through Text Analytics - Ford Motor Company’s Kansas City Assembly Plant (KCAP)
Ford Motor Company's Kansas City Assembly Plant (KCAP) is a large-scale automotive manufacturing facility located at 8121 US-69, Kansas City, Missouri 64119. As one of Ford's major North American production sites, KCAP is responsible for assembling high-demand vehicles - most notably the Ford F-150 (Beach Automotive Group, 2025). The plant operates on an industrial scale, meaning it handles a continuous flow of inbound and outbound logistics, including the delivery and staging of raw materials, components, and finished vehicles.

This logistical intensity also means that the facility regularly interacts not only with its internal workforce but also with a large external population of commercial truck drivers, contractors, and vendors who arrive to drop off trailers, hook up loads, and pass through security checkpoints. This external-facing dimension (i.e., docking process, gate security, and delivery coordination) appears to drive the overwhelming majority of the public Google Maps reviews captured in this analysis. With 644 total reviews averaging 3.1 out of 5.0 stars as of March 2026, KCAP occupies a middle-to-poor public perception position. This signals meaningful and addressable operational shortcomings.

## Overview of the Dataset
The dataset underlying this analysis consists of Google Maps reviews scraped from Ford KCAP's public listing using SerpApi, a platform that provides programmatic access to search engine results. The Place ID used to locate the business was obtained via Google's PlaceID Finder tool. The resulting dataset (referred to as “reviews.csv”) contained 198 usable reviews after processing, drawn from the broader pool of 644 total reviews available on the platform. Each record in the dataset captures a reviewer's star rating (on a 1-5 scale) and their written text commentary.

The reviews were predominantly submitted by commercial truck drivers and logistics personnel who interact with the plant's loading docks, trailer drop zones, and security gates. The reviews largely document operational and interpersonal encounters during delivery and pickup activities. The mean star rating across the 198 analyzed reviews was approximately 2.08. This is well below the platform-wide average of 3.1, indicating that the subset of reviewers who left written commentary expressed notably stronger dissatisfaction than the overall rating population. 	The dataset was processed using Python-based text analytics tools - primarily the Natural Language Toolkit (NLTK) and VADER sentiment analysis - within Google Colab notebooks. This approach set the stage as the foundation for six successive analytical methods spanning Units 2 through 7.
Executive Summary of Analytical Stages

### Unit 2 - Descriptive Text Analytics (Word Frequency):
The first analytical stage applied descriptive statistics to the review data. The results produced a ranked frequency count of the most commonly occurring words after tokenization and stop word removal. The top ten terms were: place (52), ford (46), trailer (45), drop (39), rude (38), time (36), truck (36), get (34), like (34), and plant (28). Expanding to the top twenty revealed additional high-frequency terms including drivers, hours, people, never, guard, security, go, take, and waiting.

The prominence of words like rude, never, waiting, guard, and security points to a clear pattern that suggests - reviewers are not commenting on vehicle quality or Ford's brand reputation. Instead, they are expressing frustration with the human interactions and wait conditions they encounter at the facility. For KCAP management, this frequency analysis provides a fast, diagnostic where issues are identifiable without reading hundreds of individual reviews. Practically, this should direct attention toward how security personnel and dock staff are trained, how long drivers wait at entry and staging areas, and whether operational processes create unnecessary delays and friction for third-party logistics partners.

### Unit 3 - Named Entity Recognition (NER):
The second phase applied Named Entity Recognition using a pre-trained spaCy model to extract and categorize meaningful entities from the review text. The most frequently occurring named entity was Ford (appearing in 24 unique reviews), confirming the dataset's topical coherence. Beyond that, the entities that emerged were largely temporal and logistical. Terms such as 5 hours, 12 hours, night, 2018, and Sundays were surfaced, rather than named individuals, locations, or products. This is itself significant: the dominant entities are units of time, reinforcing that wait duration is a primary grievance.

The business value of NER in this context is clear: it moves beyond raw word counts to identify what customers are specifically referencing, enabling Ford KCAP to pinpoint whether dissatisfaction is anchored to a process, a time of day, a day of the week, or a particular type of encounter. Knowing that night and Sundays appear as notable temporal entities, for instance, may suggest that staffing or scheduling gaps during off-hours are contributing disproportionately to negative experiences.

### Unit 4 - Sentiment Analysis:
The next phase applied VADER's polarity scoring method to each review, generating four sentiment metrics per entry: negative, neutral, positive, and compound. The mean scores were: neutral (0.755), negative (0.137), positive (0.108), and compound (-0.116). The compound score - a normalized aggregate of the other three - averaged mildly negative across the dataset, consistent with the below-average star ratings.

The most analytically interesting finding from this stage was the high standard deviation of the compound sentiment score (0.583), compared to the relatively low variability in the individual positive, negative, and neutral scores. This indicates that while most reviews share a similar internal composition of sentiment components, the overall tone of individual reviews varies wildly - some are harshly negative, others surprisingly positive. 

This variability implies that the quality of the experience at KCAP is highly inconsistent, likely dependent on which staff members a driver encounters, what time of day they arrive, or how backed up the docking process is on a given day. For management, this inconsistency is arguably more actionable than a uniformly negative average as it suggests that good experiences are possible at KCAP.

### Unit 5 - Topic Modeling (LDA):
The following phase applied Latent Dirichlet Allocation (LDA) to the review corpus, generating five latent themes after a set of stop words was removed. The five themes identified were:
* Safety and Worker Conduct - centered on terms like rude, trailer, workers, never, and security, suggesting negative interpersonal experiences at entry points.
* Facility Operations and Logistics - keywords bad, facility, delivery, open, and staff pointed to concerns about operational efficiency and staff responsiveness.
* Entry/Exit and Security Delays - time, never, drivers, gate, and security collectively described bottlenecks at access points, especially relevant to truck drivers.
* Professionalism and Work Environment - drop, trailer, take, hook, and unprofessional reflected complaints about loading/unloading procedures and workforce conduct.
* Waiting Experience and Customer Service Quality - long, waiting, driver, rude, and time reinforced the dominant theme of excessive wait times combined with poor service.

Topic modeling added a layer of interpretive depth that word frequency alone could not provide. LDA revealed that these terms cluster together in coherent thematic patterns, confirming that poor interpersonal behavior and extended wait times are structurally linked experiences. 	Ford KCAP leadership can see that addressing gate security behavior and wait time management is about correcting a shared negative experience that appears across multiple review clusters.

### Unit 6 - Text Summarization (Extractive vs. Abstractive):
The fifth phase explored two automated summarization techniques applied to individual reviews. An extractive summarization approach, which selects the most important sentences directly from the source text. This method successfully preserved the meaning and emotional tone of scathing reviews describing a discourteous interaction with an employee. The second approach being the abstractive summarization approach, which attempts to generate a paraphrased synthesis. Unfortunately, method produced incoherent output, failing to meaningfully represent the review's.

The business application here is straightforward and scalable. For a facility receiving hundreds of reviews over time, manually reading each one to identify actionable feedback is impractical. Extractive summarization offers a reliable automated tool for distilling the most important complaints from individual reviews. This allows management to quickly triage feedback, escalate serious incidents (such as the named-employee complaint in the sample), and track recurring grievances over time.

### Unit 7 - Text Visualization (Bigram Network Graphs):
The final analytical stage introduced NLTK-based Bigram Network Graphs as a visualization tool for mapping word co-occurrence relationships across the review corpus. By plotting nodes (individual words) and edges (connections between words that appear together), the network graph allows patterns invisible in tabular outputs to emerge spatially. Two-word phrases like "long wait," "poor management," "great place," or "good pay" become visible as connected pairs, offering a more contextually grounded picture of how concepts relate in reviewer language.

The primary business value of this approach is communicability. Network graphs translate findings into an accessible visual format that can be shared with plant managers, HR teams, and operations leads who may not be versed in data science.

### The Intersection of Text Analytics and Numerical Analysis
The most fitting demonstrations of how textual analytics gains power when combined with numerical, non-textual analysis appears in Unit 4. Sentiment polarity scores derived from review text were merged with the numerical star ratings submitted by the same reviewers. This combined dataset, containing both a sentiment compound score and a 1-5 integer rating per review enabled a comparative statistical analysis that neither source alone could provide. Sentiment scores derived from review text, by contrast, are richer but less precise. A compound score of -0.40 is meaningful in context but lacks the intuitive scale of a star rating. When these two data streams are merged, each compensates for the other's weakness. The numerical rating provides a stable, comparable anchor; the sentiment score adds emotional granularity and directional nuance.

This method could help Ford KCAP’s management eventually build a monitoring dashboard that tracks both metrics over time. Statistical trends in star ratings could be used as a leading indicator and sentiment analysis as a diagnostic tool to understand what is driving those trends. Furthermore, combining these methods with topic modeling and NER for identifying who and what the sentiment is directed toward results in a multi-layered feedback system. For a business this outcome is much more actionable than a single measurement.
Operational Steps and Conclusion

The textual analytics conducted across six analytical phases consistently revealed two interconnected operational failures at Ford Motor Company's Kansas City Assembly Plant: excessive and unpredictable wait times at entry and staging areas, and pervasive unprofessional conduct by security personnel and dock staff toward visiting truck drivers and logistics contractors. These are not minor complaints as they appear across every method applied, from raw word frequency counts to LDA topic modeling, and they cluster together in ways that suggest a compounded, systemic experience rather than isolated incidents. 

To address the wait time problem specifically, KCAP leadership should conduct a formal audit of its gate entry and trailer drop procedures, establishing measurable service-level benchmarks (i.e., maximum gate processing time, and increased staffing at entry points). The staff’s conduct issues require an equally structured response. The recurrence of words like rude, unprofessional, and never signals that the problem extends beyond occasional bad days and reflects a gap in culture, accountability, and customer-service training for roles that interact with external partners. 

Ford KCAP should implement mandatory service standards training for all security, gate, and dock personnel who regularly interact with third-party drivers and vendors, framing these workers not as incidental to the plant's mission but as frontline representatives of the Ford brand. Given that the facility's public Google rating of 3.1 stars is driven substantially by this external logistics population rather than traditional consumers, improving the driver experience is not merely a hospitality concern; it is a reputational and operational priority that directly reflects on Ford's ability to attract and retain reliable logistics partnerships.

















References
Google. (n.d.). Ford Kansas City Assembly Plant (KCAP). Google Maps. https://www.google.com/maps/place/Ford+Kansas+City+Assembly+Plant/@39.20451,-94.4833593,16z/data=!4m16!1m9!3m8!1s0x87c0f8e555555555:0xcb1a8a8252a8e119!2sFord+Kansas+City+Assembly+Plant!8m2!3d39.2045059!4d-94.4784884!9m1!1b1!16zL20vMGY3OHli!3m5!1s0x87c0f8e555555555:0xcb1a8a8252a8e119!8m2!3d39.2045059!4d-94.4784884!16zL20vMGY3OHli?entry=ttu&g_ep=EgoyMDI2MDMxOC4xIKXMDSoASAFQAw%3D%3D 
Google. (n.d.). Place ID Finder. Google Maps Platform. https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder 
Google Search API. SerpApi. (n.d.). https://serpapi.com/ 
Keraghel, I., Morbieu, S., & Nadif, M. (2024, December 20). Recent Advances in Named Entity Recognition: A Comprehensive Survey and Comparative Study. arXiv.org. https://arxiv.org/abs/2401.10825 
Text Analytics with Python. Business Analytics Review. (2024, October 4). https://businessanalytics.substack.com/p/text-analytics-with-python 
Text Data Labeling: Techniques for Named Entity Recognition and Sentiment Analysis. Sapien. (2024, April 16). https://www.sapien.io/blog/text-data-labeling-techniques-for-named-entity-recognition-and-sentiment-analysis 
The Legacy of Ford: A Look at the Brand’s History and Innovation. Beach Automotive Group. (2025, July 22). https://www.beachford.net/blogs/5597/the-legacy-of-ford-a-look-at-the-brands-history-and-innovation 
Transformers in Machine Learning. GeeksforGeeks. (2026, April 14). https://www.geeksforgeeks.org/machine-learning/getting-started-with-transformers/ 
Visualizing Text Data: Techniques and Applications. GeeksforGeeks. (2025, July 23). https://www.geeksforgeeks.org/data-visualization/visualizing-text-data-techniques-and-applications/ 
Watson, E. (2024, May 13). A Beginner’s Guide to Performing Sentiment Analysis on Text with Python. Medium. https://medium.com/@eleanor.watson/a-beginners-guide-to-performing-sentiment-analysis-on-text-with-python-3ce80dcac22e 

