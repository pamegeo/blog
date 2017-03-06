---
layout:     post
title:      Mining the UK register of beneficial ownership
date:       2016-11-22
summary:	Insights from our dive into the world's first register of who corporate control.
categories: open data
---

UK companies with hidden owners lie behind some of the worst problems of our time. Amongst other things they have been used to breach UN sanctions, evade taxes and rip off ordinary citizens. That’s why Global Witness has been calling for an end to these getaway cars for crime and corruption for years (see this [TED-Ed animation](http://ed.ted.com/lessons/how-exposing-anonymous-companies-could-cut-down-on-crime-global-witness) for a short introduction to the issue). Now, we’re seeing the first seeds of change - in June, the [UK government started publishing](https://companieshouse.blog.gov.uk/2016/04/13/the-new-people-with-significant-control-register/) the world’s first open data register of the real owners and controllers of companies – known as “beneficial owners”.  

It is a big step forward for transparency in this country, and a potential treasure trove of information - but we need to make sense of it first. Which is why we’ve collaborated with [DataKind UK](http://www.datakind.org/chapters/datakind-uk), [OpenCorporates](https://opencorporates.com/), [Spend Network](https://www.spendnetwork.com/) and [OCCRP](https://www.occrp.org/en), to probe it in detail, and give feedback on how useful it is. So on a grey autumn weekend in London, we brought together thirty volunteer data scientists, including the head of software for a Formula 1 team, an astrophysicist and a former consultant to the UK tax authority.

We had three aims for the weekend. Firstly, we wanted to get some basic insights into this data and what it could tell us about companies in the UK. Secondly, it was important to understand the flaws and gaps in the new register. Finally, we were curious to see whether the register could yield investigative leads.  

Here’s a snapshot of what we found:

*   Almost 3,000 companies listed their beneficial owner as a company with a tax haven address - something that is not allowed under the rules. There are problems with how the data has been inputted. For example, you can write anything in the nationality field and we found over 500 ways of putting “British”, including ten people who wrote “Cornish”.

*   76 beneficial owners share the same name and birthday as someone on the U.S. sanctions list. We have to do more digging to find out whether these are actually the same people, but it’s an insight into what is possible with this new information.

*   Most beneficial owners are from the UK, followed by a number from other European countries and India and China.

### Insights

The data allows us to start to understand the complex ecosystem of companies and their owners in the UK - where they’re from, and what other companies they own. In theory, law enforcement agencies, journalists and civil society being able to map this stuff out will make it much harder for those with something to hide to do so behind layers and layers of secret companies.

Under the new system, companies have to provide ownership information once a year when they send in their annual return or “confirmation statement”. Out of 3.5 million companies, 1.3 million have already filed beneficial ownership information as of 17 November. Most beneficial owners (1.2 million) are British. Perhaps unsurprisingly when you take the British out of the mix, Irish is the next biggest nationality, followed by a mix of European countries (Italy and Poland) and the two mega-economies of China and India.  

![Beneficial Owners Nationality](https://www.globalwitness.org//media/images/Screen_Shot_2016-11-19_at_22.07.18.width-1280.png)
*Nationality of beneficial owners in the UK register*

On top of nationality, we also have information on where beneficial owners live. The vast majority are based in the UK, with 183,000, or 13% of the total, living overseas.

One of the arguments made against creating these registers is that companies would find it very difficult to identify their beneficial owners, but this doesn’t appear to be the case. In only 2% of cases did companies say that they were struggling to identify a beneficial owner or collect the right information.

Just under ten percent of companies claimed to have no beneficial owner. This is possible under the legislation, because you have to own at least 25 percent of a company to be considered its beneficial owner. We think that’s quite a high threshold, which could be exploited by people looking to stay under the radar So we will be digging a bit deeper to see whether companies are trying to avoid disclosing information that they should be.

<div style="max-width:900px"><iframe id="datawrapper-chart-EVcm0" src="//datawrapper.dwcdn.net/EVcm0/1/" frameborder="0" allowtransparency="true" allowfullscreen="allowfullscreen" webkitallowfullscreen="webkitallowfullscreen" mozallowfullscreen="mozallowfullscreen" oallowfullscreen="oallowfullscreen" msallowfullscreen="msallowfullscreen" width="100%" height="196"></iframe><script type="text/javascript">"undefined"==typeof window.datawrapper&&(window.datawrapper={}),window.datawrapper["EVcm0"]={},window.datawrapper["EVcm0"].embedDeltas={"100":196,"200":196,"300":196,"400":196,"500":196,"600":196,"700":196,"800":196,"900":196,"1000":196},window.datawrapper["EVcm0"].iframe=document.getElementById("datawrapper-chart-EVcm0"),window.datawrapper["EVcm0"].iframe.style.height=window.datawrapper["EVcm0"].embedDeltas[Math.min(1e3,Math.max(100*Math.floor(window.datawrapper["EVcm0"].iframe.offsetWidth/100),100))]+"px",window.addEventListener("message",function(a){if("undefined"!=typeof a.data["datawrapper-height"])for(var b in a.data["datawrapper-height"])"EVcm0"==b&&(window.datawrapper["EVcm0"].iframe.style.height=a.data["datawrapper-height"][b]+"px")});</script></div>


Approximately 30 beneficial owners have been successfully granted the right to keep their name off the register due to concerns about their security.

We were also able to build up a picture of company networks. These were only partial insights as we were working with just three months’ worth of data, but it gave us an idea of what was possible, and to start to understand complex corporate structures. Complexity doesn’t necessarily indicate wrongdoing. For example below is a partial map of Reckitt Benckiser, the healthcare company that makes Durex condoms among other things. However, it will provide a much better map of how UK companies structure themselves, and in some cases connections between companies may raise further questions about what they have been up to.

![Reckitt Benckiser](https://www.globalwitness.org//media/images/Screen_Shot_2016-11-18_at_14.31.23.width-1280.png)
*The UK control structure of Reckitt Benckiser*

### Flaws

Inevitably with a bold experiment like this, there will be problems with the data, despite the generally excellent job that Companies House has done. The flaws that we identified split into two categories: messy data due to how it was collected, and examples of what look like non-compliance with the law.

One of the big problems we found was that Companies House allows for free text entry for a number of fields. For example, we found over 500 different ways of putting “British”. Our favourite were the 10 beneficial owners who described themselves as Cornish. We were able to get around this by creating a nationality mapping table. However, an easy way to avoid this would be for Companies House to use drop down menus for fields such as nationality or title, with a potential “other box”.  

![Many ways of spelling British](https://www.globalwitness.org/media/images/Screen_Shot_2016-11-18_at_14.19.07.width-1280.png)
*The many ways of spelling "British" in the UK beneficial ownership register*

Another big challenge is the lack of unique identifiers for individuals and some companies. We were relying on using name and day and month of birth to try and identify individuals. This is fine if you’re someone with an unusual name, but proves more tricky for the John Smiths or Mohammed Iqbals of this world. We’d like to work with Companies House on thinking about how they could get around this problem. One solution could be to assign beneficial owners a unique number to allow better cross-matching.

There were also 2,160 beneficial owners born in 2016\. Now either these are a very precocious bunch of toddlers or the data has been entered incorrectly. We also had people who listed 9988 as their year of birth - clearly a visitor from the future.

On top of these data validation issues, we found a number of signs of non-compliance with the law. For example, 9,800 companies listed their beneficial owner as a foreign company. Now this is possible if the foreign company was listed on one of the stock exchanges deemed equivalent to the UK system (e.g. the US, EU and Japanese exchanges). However, we found almost 3,000 companies with tax haven addresses listed as beneficial owners. This is not allowed under the rules. We’ll be handing this list of companies over to Companies House to investigate further.

<div style="max-width:900px"><iframe id="datawrapper-chart-OpOKm" src="//datawrapper.dwcdn.net/OpOKm/1/" frameborder="0" allowtransparency="true" allowfullscreen="allowfullscreen" webkitallowfullscreen="webkitallowfullscreen" mozallowfullscreen="mozallowfullscreen" oallowfullscreen="oallowfullscreen" msallowfullscreen="msallowfullscreen" width="100%" height="351"></iframe><script type="text/javascript">"undefined"==typeof window.datawrapper&&(window.datawrapper={}),window.datawrapper["OpOKm"]={},window.datawrapper["OpOKm"].embedDeltas={"100":485,"200":418,"300":385,"400":385,"500":351,"600":351,"700":351,"800":351,"900":351,"1000":351},window.datawrapper["OpOKm"].iframe=document.getElementById("datawrapper-chart-OpOKm"),window.datawrapper["OpOKm"].iframe.style.height=window.datawrapper["OpOKm"].embedDeltas[Math.min(1e3,Math.max(100*Math.floor(window.datawrapper["OpOKm"].iframe.offsetWidth/100),100))]+"px",window.addEventListener("message",function(a){if("undefined"!=typeof a.data["datawrapper-height"])for(var b in a.data["datawrapper-height"])"OpOKm"==b&&(window.datawrapper["OpOKm"].iframe.style.height=a.data["datawrapper-height"][b]+"px")});</script></div>

With all of these examples it’s not clear whether this is because the people filing the information didn’t understand the new system, or whether there’s something more sinister going on.

### Investigation

One of the key arguments in favour of creating this register was that law enforcement, civil society and journalists could use it to uncover wrongdoing. We didn’t expect to find any slam dunk cases in just a weekend, but we did find a few interesting leads. Because the UK register is available as open data, we could compare it to other data sets.

Initial findings suggest 19 senior politicians (known as politically exposed persons), 76 people from the U.S. sanctions list and 267 disqualified directors were listed as beneficial owners.

However, these matches were based on name and month and year of birth. This means that it’s hard to be certain that the matches are good ones. Any leads coming out of the new register will have to be followed up with more traditional investigative digging.

We also had an initial look at comparing the beneficial ownership to government spending information. It was challenging given that a lot of the spending information doesn’t have proper identification for companies (for example it would be good to include company numbers). But we did find a number of recipients of government contracts who had beneficial owners based in tax havens.

### Reflections

As campaigners who have worked for years to get this information out in the public domain, the weekend was an exciting first opportunity to get our hands dirty and start to tell some stories. The work was only possible because the UK government made the decision to make the register free and accessible to all as open data. This is an important lesson for other countries who are thinking about creating similar registers.

Inevitably the data was messy, partly due to how the register is set up and partly due to confusion from those providing data. We’re going to be working with Companies House on ironing out some of these issues. Hopefully as the register beds in, these kinks will get ironed out.

A big question that we weren’t able to answer was whether people had lied to the register or provided inaccurate information. This is going to be a serious challenge for the credibility of the register, and the government will have to provide more reassurances on how they’re going to ensure data accuracy.

Finally, we’re hoping that other governments will see the potential of what the UK has done. The process will be difficult, but if our weekend showed us anything, it’s that this is incredibly useful information to have.  
