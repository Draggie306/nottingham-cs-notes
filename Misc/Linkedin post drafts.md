
## Group project

Wednesday marked the conclusion and  of our 8-month-long Software Engineering Group Project, NeuroNarratives, sponsored by Mendi.

In the University of Nottingham School of Computer Science, second year students must take part in a year-long group project.

We 

Over the year, I worked as Team Admin for my team. This meant writing the vast majority of the group’s 17,000-word reports over the year, in addition to being only full-time developer across the back-end and AI/ML sub-teams. 

Our application, written in Python with the Flet framework, communicates with the Mendi fNIRS headband over Bluetooth Low Energy, processing data from the brain’s prefrontal cortex as a proxy for focus levels. This is sent to my back-end system, built with Cloudflare Workers, to ingesting focus data and create user sessions. By using an LLM, we are able to use changes in neural activity to write a story that changes and branches depending on if the user becomes more or less focused, relative to a sliding window.

A massive thank you to Mendi themselves and sponsor Mustafa Hamada, leaders in neurotechnology, and supervision by the legendary Horia Maior. It was fantastic to see all 47 groups showing off their creations on Demo Day.

I am also grateful to have worked with such proactive and hard-working teammates, particularly Ronan Berridge and Roy Ramlugon





## website promo

1.1 million requests in the last 30 days - a new record! My website, iBaguette, was first made to create and organise my exam revision notes, but with a few adjustments and tactical choices, here's how I built it to scale to survive exam season, all for free.


1) **Making good content**
This is (arguably) the hardest part. No matter if you've got the fastest platform with lowest time-to-first-byte, you need to have actually good content that people want to look at. This was relatively easy for me: I made revision "Cheat Sheets" to the highest quality to consolidate my own knowledge, and knew that people across my school wanted to read them. There is no point creating content that real people don't want to read.

These are not AI-generated slop, not huge walls of text that look like it comes from the 1990s, not boring and monotonous paragraphs, rather concise, insightful and somewhat funny resources that had real care and effort put in. I carefully chose what to write and the images to add so that each sentence felt genuinely insightful. Naturally, this led to increased demand and appraisal from staff. 

2) **Using the right platform**
There are many hosting services online but very few come close to how good Cloudflare's free tier is. Using a domain I already had, I coded a Cloudflare Worker that fetches HTML from the GitHub repository that my revision notes are synced to, caching it and returning the result to the user. The result? A beautifully fast website that's highly scalable and efficient. To this day, this single Worker powers all revision material on the site. The free tier allows up to 100,000 requests to each Worker per day which is plenty, even for the day before big exams! 

A single image might be fine to encode directly in your HTML, but this becomes impractical when you are covering entire A Level specifications. I chose an S3-compatibile storage bucket, Cloudflare R2, which allows unlimited, free egress and extremely generous A and B-class operations. In fact, when coupled with the Cloudflare CDN, I was able to achieve cache hit percentages of up to 99% during peak hours by using a custom cache rule on all images and assets in the storage bucket! This results in extremely fast content loading for site viewers, lower B-class operations (since the cache sits in front of the storage bucket) and has cost me... £0.