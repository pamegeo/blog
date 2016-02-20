---
layout:     post
title:      Ingredients of an open data investigation
date:       2016-2-15
summary:	How Global Witness used OpenCorporates data to investigate corruption in the Burmese jade industry
categories: investigations
---

### Background to investigation

The jade industry in Burma was worth a staggering $31 billion in 2014 - equivalent to half of Burma’s official GDP. [Global Witness](https://globalwitness.org) undertook a [year-long investigation](https://www.globalwitness.org/en-gb/campaigns/oil-gas-and-mining/myanmarjade/) to tell the story of this valuable mineral and who really benefits from it. The picture that emerged was a grim one: jade is secretly controlled by Burma's military elite and some of the generals associated with the worst abuses of junta rule. Little or no money flows to the communities who live in jade mining regions where some of Burma’s poorest and most vulnerable people live.

The team working on this used a variety of investigative approaches including field research, interviews and economic analysis.  One important aspect of the work was data analysis conducted using publicly available company data published by [OpenCorporates](https://opencorporates.com/). By combining this data with other sources, we were able to understand the complex webs of ownership of the jade industry and which individuals and groups controlled this valuable mineral.

The approach could in principle be applied to many other investigations. Below is a description of the method used, so that it might give other groups seeking to undertake similar analysis using OpenCorporates a place to start.

### Data acquisition

The research began with a government map of jade concessions and their current license holders. As our goal was to understand who was behind these companies, we needed to get this data in a form that could be linked to a database like OpenCorporates. This needed to be (a) in a structured form that could programatically be linked to another database, and (b) in English. So the first step was to create a simple Excel spreadsheet and translate these names into English using Roman script. 

### Reconciliation with OpenCorporates API

Transliteration always introduces some ambiguity and there are often numerous ways to convert a specific company name from one script to another. Fortunately, OpenCorporates has a service that lets users find company names in the database that are near but not exact matches. This all happens via an [‘endpoint’](https://api.opencorporates.com/documentation/Open-Refine-Reconciliation-API) through which users can load the data they want to reconcile into [OpenRefine](http://openrefine.org/). OpenCorporates will then return a likely set of matches against the company names you have imported. In the case of this investigation, many of the companies returned multiple matches. The mining, gems and trading arms of companies were often separated into different legal entities under the same name. Take for example, Max Burma Company: there is a [general limited company](https://opencorporates.com/companies/mm/733-1993-1994), a [gems and jewellery arm](https://opencorporates.com/companies/mm/903-2007-2008) as well as a [construction company](https://opencorporates.com/companies/mm/958-2005-2006). 

Each set of results was checked by the team of researchers and the best matches were chosen and added to the data, now with a link to the OpenCorporates database. This was a painstaking task even with the suggestions all the automation OpenRefine supplied, there was still a lot of human judgement required.

### Extraction of shareholders and director data

Now that relationships had been established between the jade companies and the OpenCorporates database, we were in a position to extract other properties of those companies held within OpenCorporates. The properties of primary interest were shareholders and directors of those companies.

There are a number of ways to extract this information, one could write a script in a language like Python to programmatically query the [OpenCorporates API](https://api.opencorporates.com/) for instance. The method we opted for was to use the data we already had in OpenRefine and extract the new information we needed into new columns from OpenCorporates.

### Extracting shareholder sand directors from OpenCorporates using OpenRefine

* Load in the company names for which you want to extract shareholders and directors intro OpenRefine;
* Reconcile the names to the OpenCorporates API, you can follow the tutorial available [here](https://api.opencorporates.com/documentation/Google-Refine-Reconciliation-API);
* Once you have reconciled the data and chosen the correct matches, you need to add a column to your data that contains the OpenCorporates ID. This can be achieved by clicking Edit Column > Add column based on this column in the Transform box type `cell.recon.match.id`;
* You should now have a column with the OpenCorporates ID. From this you can construct a URL which returns JSON data for each company on its shareholders and directors;
* You now need to add a column in which we will get data that contains our officers and our shareholders. First, we construct a column that contains the URLs which will return this data;
* For the Burmese company registry you need to construct two different URLs. The director data is contained within the JSON you get from calling `http://api.opencorporates.com + cell.recon.match.id`. The shareholder data on the other hand is contained within the JSON you get from the URL `http://api.opencorporates.com + cell.recon.match.id + "/statements"`;
* We now have two nicely formatted columns containing the URLs we need. Copy and paste one of them into a browser, you should see some data about that company. If it looks messy, install a JSON viewer plug-in in your browser like [JSONView for Chrome](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=en);
* Next we pull all the data returned by each of these URLs by using Refine’s fetch URL function. We can access this by going to one of our URL columns and clicking Edit columns > Add column by fetching URLs;
* Depending on how much data you want to extract, you may need to add an API Token to your URLs. You can request an open data API token from OpenCorporates which lets you request 10,000 URLs a day. When you fetch your URLs you can add it to you URLs by typing value `+ “&api_token=”` in the expression box;
* OpenRefine will then work through you your URLs returning JSON formatted data in the cells in your new column. Once this process has finished you then need to parse this data and extract the relevant bits. In the case of the Burma investigation we were interested in two key pieces of data for directors - their names and their national identifier number. This is the code we used to extract this: 
	`forEach(value.parseJson()
	.get("results").company.officers,v,(v.officer.name + " (" + v.officer.position + ")" + " (" + v.officer.uid + ")"))
	.join(":::")`

### Fuzzy matching of directors against sanctions lists

An important part of the investigation was to understand if any of the directors of jade mining companies or their directors were under sanctions for any reason. By this time we had the names of thousands of companies, directors and shareholders. While there are various proprietary databases for checking this information like LexisNexis or WorldCheck, few of them let you programmatically search for such large numbers of names at once. We therefore opted for our own solution using existing sources of public data [1].

We took a number of recent sanctions lists published by the [EU](http://eeas.europa.eu/cfsp/sanctions/consol-list/index_en.htm), [US](https://www.treasury.gov/resource-center/sanctions/Programs/Pages/Programs.aspx) and [Australia](http://dfat.gov.au/international-relations/security/sanctions/pages/consolidated-list.aspx). We then sought to match these names with the names of company officers and shareholders from OpenCorporates. Names are often spelt differently, so rather than looking for exact matches we used a technique called ‘fuzzy matching’.  There are a number of different ways to fuzzy match names. We opted to use a Python scripts to do this [2], but you can also try to use tools such as [Microsoft Excel’s Fuzzy Lookup](http://www.microsoft.com/en-gb/download/details.aspx?id=15011) addin.

### Checking for politically exposed directors using national identifiers

One of the objectives of the investigation was to look at the extent to which politicians in Burma had interests in the jade industry. Making associations between political figures via name alone was difficult for two main reasons. First, our list of shareholders and officers was already in the hundreds and manual cross checking would be very time consuming. Second, many Burmese individuals share the same surname so a match based on name alone does not guarantee by any means that the two individuals you are looking at are the same.

This is where the national identifiers published first by [DICA](http://dica.gov.mm.x-aas.net/), the Burmese company registry, and re-published by OpenCorporates were so useful. We were able to build up our own lists of Burmese PEPs ("Politically Exposed People") using national identifiers of political candidates published in Burmese newspapers and available online. Historical copies of the newspaper the New Light of Burma Times (for example this issue [published on 13 Nov 2010](https://www.globalwitness.org/en-gb/campaigns/oil-gas-and-mining/myanmarjade/)) proved particularly useful

Again, we used "fuzzy" rather than exact matching. We looked for national identifiers that were the same but with one or two characters difference. We were able to catch those individuals where ID numbers had been put in incorrectly through clerical error, and, more interestingly, associate them with members of their family that had successive ID numbers. On one occasion the spouse of a Burmese politician who had the national identifier after her husband (presumably they had registered together).

### Lessons learned

The methodology above provided us with a number of connections between jade companies and the Burmese military that were later incorporated into the [final report](https://www.globalwitness.org/en-gb/campaigns/oil-gas-and-mining/myanmarjade/) published in November 2015.

There are some key lessons that we have taken from this approach:

* *Open source tools are key for public integrity journalism* - We could not have cleaned and processed the data without tools like OpenRefine that supply simple graphical interfaces, power and flexibility in a way that is affordable to those working in the not-for-profit sector.

* *Unique identifiers are essential*- We would not have been able to conclusively connect members of the military elite to the jade industry without the national identifier numbers.

* *OpenCorporates supports powerful workflows not available for common proprietary databases* - While databases like Orbis may have more complete information they do not support the bulk data operations and flexible workflows required for this investigation. The OpenCorporates API proved invaluable at every step from reconciling the company names to harvesting director data in bulk. [3]

* *The importance of scraped data *- At the time of undertaking the investigation the original source of the company data ([DICA](http://dica.gov.mm.x-aas.net/)) was not available. This is where OpenCorporates again proved its value with its vast archive of scraped data preserving access public interest data even when the original publishers have taken it down. [3]

* *Data journalism projects requires dedication (and perspiration!)* - Even with all the powerful computational tools we had at our disposal, there was still a huge amount of manual data cleaning and reviewing required to get reliable results.

[1] Friedrich Lindenberg has made the first baby steps towards pulling together an open source PEP list that may be useful for those undertaking similar cross-checking exercises: [http://pudo.org/material/opennames/](http://pudo.org/material/opennames/)

[2] Our Python approach to fuzzy matching used a method to this [http://blog.yhat.com/posts/fuzzy-matching-with-yhat.html](http://blog.yhat.com/posts/fuzzy-matching-with-yhat.html)

[3] The team at OpenCorporates explore these issues more fully in their white paper on the subject, ["How open company data was used to uncover the powerful elite benefiting from Burma’s multi-billion dollar jade industry"](https://medium.com/@opencorporates/how-open-company-data-was-used-to-uncover-the-powerful-elite-benefiting-from-myanmar-s-multi-1ef35f88d6bd#.ygcs3g3i9)

