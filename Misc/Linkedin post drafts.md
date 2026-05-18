
## 2026 end of A/Y
### Group project

Wednesday was Demo Day, marking the conclusion of our 8-month-long Software Engineering Group Project, NeuroNarratives: "Stories that read your mind".

In the [University of Nottingham School of Computer Science](https://www.linkedin.com/feed/#), all second-year students must complete a year-long group project. Throughout, I worked as Group Admin for my team of 8. This meant writing the vast majority of the 17,000-word reports, in addition to being the lead and only full-time developer in the backend and AI/ML sub-teams, writing code for the "Narrative Engine", persistent data storage, and designing the API. I even performed the live demonstration to other groups and examiners on Demo Day, which went almost flawlessly!

Our application, written in Python with the Flet framework, communicates with the [Mendi](https://www.linkedin.com/feed/#) fNIRS headband over Bluetooth Low Energy, reading and processing data from the brain’s prefrontal cortex. We derived a focus proxy from this data based on neuroscience research by comparing new activity readings with users' baselines, ingested by the backend system built on the [Cloudflare](https://www.linkedin.com/feed/#) Workers Platform. By then using an LLM, the story users read responds in near-real-time to focus levels: being distracted makes the story take a negative twist, whilst heightened focus leads to positive advances!

A massive thank you to Mendi themselves and sponsor [Mustafa S. Hamada, PhD](https://www.linkedin.com/feed/#), and the supervision by the legendary [Horia Alexandru Maior, PhD](https://www.linkedin.com/feed/#). It was fantastic to see all 49 groups showing off their creations on Demo Day, which was very well organised by the module coordinators.

I am also grateful to have worked with such proactive and continuously hard-working teammates, particularly [Ronan Berridge](https://www.linkedin.com/feed/#) and Roy Ramlugon, in addition to [James R.](https://www.linkedin.com/feed/#) and [Pooja Shah](https://www.linkedin.com/feed/#).


### End of the year reflection


### Senior Mentor application


### Lego Society Treasurer and Publicity


### Website new record 15k users







## misc drafts

### website promo

1.1 million requests in the last 30 days - a new record! My website, iBaguette, was first made to create and organise my exam revision notes, but with a few adjustments and tactical choices, here's how I built it to scale to survive exam season, all for free.


1) **Making good content**
This is (arguably) the hardest part. No matter if you've got the fastest platform with lowest time-to-first-byte, you need to have actually good content that people want to look at. This was relatively easy for me: I made revision "Cheat Sheets" to the highest quality to consolidate my own knowledge, and knew that people across my school wanted to read them. There is no point creating content that real people don't want to read.

These are not AI-generated slop, not huge walls of text that look like it comes from the 1990s, not boring and monotonous paragraphs, rather concise, insightful and somewhat funny resources that had real care and effort put in. I carefully chose what to write and the images to add so that each sentence felt genuinely insightful. Naturally, this led to increased demand and appraisal from staff. 

2) **Using the right platform**
There are many hosting services online but very few come close to how good Cloudflare's free tier is. Using a domain I already had, I coded a Cloudflare Worker that fetches HTML from the GitHub repository that my revision notes are synced to, caching it and returning the result to the user. The result? A beautifully fast website that's highly scalable and efficient. To this day, this single Worker powers all revision material on the site. The free tier allows up to 100,000 requests to each Worker per day which is plenty, even for the day before big exams! 

A single image might be fine to encode directly in your HTML, but this becomes impractical when you are covering entire A Level specifications. I chose an S3-compatibile storage bucket, Cloudflare R2, which allows unlimited, free egress and extremely generous A and B-class operations. In fact, when coupled with the Cloudflare CDN, I was able to achieve cache hit percentages of up to 99% during peak hours by using a custom cache rule on all images and assets in the storage bucket! This results in extremely fast content loading for site viewers, lower B-class operations (since the cache sits in front of the storage bucket) and has cost me... £0.