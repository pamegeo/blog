---
layout:     post
title:      Why we published the data behind Hostile Takeover
date:       2016-8-9
summary:	Publishing the data and research tools we used to investigate crony capitalism in Cambodia is key to Global Witness's mission.
categories: open data
---

*This blog post was originally posted on the [Global Witness website](https://www.globalwitness.org/en/blog/why-we-published-data-behind-hostile-takeover/)*

It will come as no shock to Cambodians that their ruling elite has amassed vast fortunes whilst in power. As our report, _[Hostile Takeover](https://www.globalwitness.org/en/reports/hostile-takeover/)_, shows, members of Prime Minister Hun Sen’s family have business interests spanning the majority of the country's major industries. While 40% of Cambodians live below or close to the poverty line, the Hun family have a combined wealth estimated to total between US$ 500 million and US$ 1 billion.

But until fairly recently it has been extremely difficult for activists and campaigners to prove this with hard facts and solid data.

This has enabled the country’s most powerful family to continue to line its pockets behind a wall of secrecy. It has also allowed international companies and investors to establish business relationships with members of Hun Sen’s family, either unaware of or unconcerned by previous allegations of corruption and human rights abuses.

### Limitations of the original dataset

The publication of data by [Cambodia’s Ministry of Commerce](http://www.moc.gov.kh/en-us/) was a step towards greater transparency. The data held the key to the extensive business interests of Cambodia’s ruling elite, exposing just how much of a grip Hun Sen and his family have over the nation’s economy. However, in its original form the data was unusable for investigative purposes.

Whilst we commend the Ministry of Commerce for publishing the data in the first place, the information provided suffered from a number of issues that prevented our researchers from using it effectively:

*   The database was put behind a login, making it difficult to programmatically access  

*   The search portal didn’t allow people to download the dataset in its entirety  

*   The service and availability of information changed from time to time. This posed a risk to our research that data would be taken offline or modified without our knowledge. Since the publication of the [_Hostile Takeover_](https://www.globalwitness.org/en/reports/hostile-takeover/) report - for instance - shareholder information has been removed completely  

*   The Ministry’s servers were slow and unreliable, making it difficult to conduct in-depth research

Given these limitations we extracted the contents of the database and developed our own version with the functionality needed to support in-depth investigation. This is known as "web scraping" by techies, and it is becoming an essential process in a wide-range of investigations at Global Witness.

### Open data and network effects

At Global Witness we passionately believe that our investigations should be a platform for change. We are well aware, however, that the kinds of changes we want to see can only be achieved when we work through networks.

When it comes to data and technology this means enabling a range of actors - from civil society groups to law enforcement - to use the databases we’ve built up and the technology we’ve developed to verify our findings and spot things we haven’t.

This is exactly what we did for _[Hostile Takeover](https://www.globalwitness.org/en/reports/hostile-takeover/)_. We have published both the [dataset that we extracted](https://cambodiacorporates.globalwitness.org/) from the Ministry of Commerce in its entirety and also [the research tool](https://cambodiacorporates.globalwitness.org/) we developed to interrogate this information including the underlying [source code](https://github.com/Global-Witness/cambodia-corporates). We have applied [open licenses](http://opendefinition.org/) to all of these so anyone can freely access, remix and build on our work.

Cambodian newspaper _[The Phnom Penh Post](http://www.phnompenhpost.com/)_ made great use of the data almost immediately after we launched our report. As well as publishing their own analysis of the data we provided, they also produced a [playful interactive](http://www.phnompenhpost.com/national/inside-hun-familys-business-empire#interactive) letting readers explore the wide-ranging business interests of the Hun Sen family.

[![Cambodia Wheel of Fortune](https://www.globalwitness.org/media/images/Screen_Shot_2016-08-19_at_10.17.02.width-500.png)](http://www.phnompenhpost.com/national/inside-hun-familys-business-empire)

By publishing our data openly we also want it to be re-used in some of the game-changing aggregation and search services being built by civic-hackers and tech-for-good enterprises like [OpenCorporates](https://opencorporates.com/). Powerful, free tools for investigative journalists like [data.occrp.org](https://data.occrp.org/) benefit hugely from organisations choosing to open their data post-publication.

These tools and this pooling of information is ever more important for anti-corruption campaigners who - in their attempts to unravel global illicit financial flows - need to be able to join the dots between fragmented and siloed datasets. In the same way that medical researchers across the world leverage the technology, data and methods of their peers to defeat deadly diseases, the fight against corruption could benefit from a far more joined up investigative community.  

But openness isn’t just a practical matter for us, it’s also a principle. As an organisation that asks governments and companies around the world to do more of their work in the open where it can be scrutinised by the public, we believe that once we’ve published a story, and where no risks exist for our sources, we should publish the data we’ve collected as permissibly as possible. We invite others to verify our findings and scrutinise our methodology.  

### Cambodia Corporates functionality

[![Cambodia Corporates screnshot](https://www.globalwitness.org//media/images/Screen_Shot_2016-08-19_at_10.19.11.width-800.png)](https://cambodiacorporates.globalwitness.org/)  

As well as being able to conduct searches for companies and directors, [Cambodia Corporates](https://cambodiacorporates.globalwitness.org/) has a number of functions not available on the original site:  

1.  Fuzzy search for names - It’s a common problem in many datasets that names for the same person are spelt differently on different records. This is particularly problematic in cases where names have been. transliterated from Roman script. [Cambodia Corporates](https://cambodiacorporates.globalwitness.org/) let’s you introduce “fuzziness” into your search by choosing the number of characters that the results can vary from your original search term  

2.  Find the nationality of chairpersons - The Ministry of Commerce website doesn’t allow you to look at the nationality of the chairperson of Cambodian registered companies. This is important information for understanding international investment in the country.  

3.  Download all the data - There are many colleagues and researchers out there who will want to do things with the information that we haven’t anticipated. Perhaps they will want to combine it with other databases they are building. We also want to enable those building excellent registries and search tools like [OpenCorproates](https://opencorporates.com) and OCCRP ([data.occrp.org](http://data.occrp.org)) to connect to this information.  

4.  [Get the source code](https://github.com/Global-Witness/cambodia-corporates) - For the geeks amongst you, you can download, tweak and re-deploy our source code for similar projects.
5.  Following the publication of _[Hostile Takeover](https://www.globalwitness.org/en/reports/hostile-takeover/)_ the Ministry of Commerce database no longer contains the shareholder data that our investigation was built on. The reasons as to why this data is no longer available are [unclear](https://www.cambodiadaily.com/news/government-scrubs-database-exposed-hun-family-riches-116772/). This important information is currently only available from [Cambodia Corporates](https://cambodiacorporates.globalwitness.org/).

You can access the fully functional research tool and the attached database of companies and directors at [https://cambodiacorproates.globalwitness.org](https://cambodiacorproates.globalwitness.org), the underlying source code is available on GitHub [here](https://github.com/Global-Witness/cambodia-corporates).