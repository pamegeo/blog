---
layout:     post
title:      Scraping PDF tables using ScraperWiki and Open Refine
date:       2014-12-21
summary:	How to scrape PDFs using ScraperWiki's PDF extract tool and OpenRefine. We use a UK sanctions list of investment targets in Myanmar as an example.
categories: ddj-tips scraping
---
Lots has been written as to why the PDF is inadequate format for data publication.<sup>[1](#1)</sup> PDFs aren't machine readable and information from them often can't even be copy and pasted. Despite this governments, corporations and multi-lateral organisations still release large amounts of public data as PDF. As a result, any organisation or individual wanting to analyse public data will have to extract structured data from PDFs at some point. A fantastic tool for doing this - and which requires no coding knowledge at all - is [ScraperWiki's](http://scraperwiki.com) PDF table extract tool.<sup>[2](#2)</sup> In combination with the data cleaning tool, [Open Refine](http://openrefine.org/), you can wrangle most PDFs into an analysable form within minutes.

The screencast below shows one method to turn the PDF of a UK investment sanctions list for Burmese companies into a spreadsheet. This kind of transformation would be useful if you wanted to automatically reconcile the list of companies with an external database such as [OpenCorporates](https://opencorporates.com/),<sup>[3](#3)</sup> see if any of organsiations appear in another dataset you've been compiling or map the locations of the companies. For this demo, we are aiming to create a spreadsheet that contains one organisation name and address per row. The screencast and instructions below walk through the steps:

<object width="100%"><param name="movie" value="http://www.youtube.com/v/GobC87hVvrQ&hl=en&fs=1"></param><param name="allowFullScreen" value="true"></param><embed src="http://www.youtube.com/v/GobC87hVvrQ&hl=en&fs=1" type="application/x-shockwave-flash" allowfullscreen="true" width="100%" height="500"></embed></object>

&nbsp;

1. Log-in to [ScraperWiki](http://scraperwiki.com) (create a free account if you don't have one already), create a new dataset and choose the PDF Extract tool
2. Upload your PDF or paste in a web link to your PDF if it's available publicly. For the purposes of this demo we will be using the sanctions list at [http://www.betterregulation.com/external/investmentban.pdf](http://www.betterregulation.com/external/investmentban.pdf)
3. Download All Tables as an Excel spreadsheet
4. Open the spreadsheet in Excel, there will be a tab for each page of data in the PDF
5. Remove the header and footer information on each tab from each page
4. Start Open Refine and create a project with your spreadsheet
5. In preview mode, load each of the tabs that contains the data you are interested by ticking them (for brevity I've only turn the first 3 tabs)
6. In preview mode, our data does not have headers so untick the "Parse next X lines(s) as column headers"

	*Open Refine recognises each of our lines from the table as a record despite the fact that it flows over multiple spreadsheet rows. As we are aiming to produce a spreadsheet with one organisation per line, we need to re-shape our data so the rows from our record that display "Organisation name" and "Address" have their own columns.*

7. On "Column 2" choose the "Add a column based on this column function". Insert the following bit of Google Refine Expressions Language (GREL):
		
		row.record.cells["Column 2"][0].value
8. Do this a second time except changing the 0 to a 1:
		
		row.record.cells["Column 2"][1].value

	*The newly created "Address" column retains some extra information that is not useful this time such as "Other information" (you may want to put this data into a new column). We are going to remove it. We would struggle to do this using a normal Find and Replace operation as the string we want to replace is different for every cell, however it does follow a pattern so we are able to use Regular Expressions.*

9. In the "Address" column go to "Edit cells > Transform", insert the following GREL expression that effectively finds all strings in that column that start with "Other information:" and are followed by an indefinite number of further characters. Regular Expressions are bounded by the "/" character is GREL:
		
		value.replace(/\sOther\sInformation.*/,"")
	
	*Now to get remove the extra lines in the records, so that we only have one line for each row of data.*

10. Choose the "Edit Cells > Blank down" function on the "Address" column effectively blanking out all consecutive duplicate rows for that column 
11. Go to "Facet > Text Facet" on the "Address column"
12. Select from the Text Facet box "(blank)", we need to remove all these rows
13. Change the view (top left) to "Rows" from "Records"
14. From the "All" function drop down (top left) select "Edit Cells > Remove all matching rows"
15. Finally, export you project using the button in the top right to either an Excel or CSV file. We now have the one row one record structure we were looking for. You can clean up your data furthers by taking out

<p><a name="1"></a>[1] See for example <a href="https://blog.scraperwiki.com/2013/12/the-tyranny-of-the-pdf/">https://blog.scraperwiki.com/2013/12/the-tyranny-of-the-pdf/</a>.</p>
<p><a name="2"></a>[2] ScraperWiki appears to be spinning this tool out as a separate product called <a href="https://pdftables.com/">PDF Tables</a>, but you can still access the tool through ScraperWiki when this was written.</p>
<p><a name="3"></a>[3] If you're interested in reconciling company names to the OpenCorporates database in order to attach the wealth information held by OpenCorporates to your database (e.g. director names, date of incorporation etc) take a look at <a href="http://vimeo.com/17924204">this</a> tutorial.</p>