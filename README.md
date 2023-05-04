Download Link: https://assignmentchef.com/product/solved-csci572-homework2-web-crawling
<br>
In this assignment, you will work with a simple web crawler to measure aspects of a crawl, study the characteristics of the crawl, download web pages from the crawl and gather webpage metadata, all from pre-selected news websites.

<h1>2.  Preliminaries</h1>




To begin we will make use of an existing open source Java web crawler called crawler4j. This crawler is built upon the open source crawler4j library which is located on github. For complete details on downloading and compiling see  <a href="https://github.com/yasserg/crawler4j">https://github.com/yasserg/crawler4j</a>

Also see the document “Instructions for Installing Eclipse and Crawler4j” located on the Assignments web page for help.

<strong>Note</strong>:  You can use any IDE of your choice. But we have provided installation instructions for Eclipse IDE only

<h1>3.  Crawling</h1>

Your task is to configure and compile the crawler and then have it crawl a news website. In the interest of distributing the load evenly and not overloading the news servers, we have pre-assigned the news sites to be crawled according to your USC ID number, given in the table below.

The maximum pages to fetch can be set in crawler4j and it should be set to <strong>20,000</strong> to ensure a reasonable execution time for this exercise. Also, maximum depth should be set to <strong>16</strong> to ensure that we limit the crawling.

<em>You should crawl only the news websites assigned to you, and your crawler should be configured so that it does not visit pages outside of the given news website! </em>

<table width="615">

 <tbody>

  <tr>

   <td width="133"><strong>USC ID ends with</strong></td>

   <td width="145"><strong>News Sites to Crawl</strong></td>

   <td width="109"><strong>NewsSite </strong><strong>Name </strong></td>

   <td width="228"><strong>Root URL</strong></td>

  </tr>

  <tr>

   <td width="133">01~20</td>

   <td width="145">NY Times</td>

   <td width="109">nytimes</td>

   <td width="228">https://www.nytimes.com</td>

  </tr>

  <tr>

   <td width="133">21~40</td>

   <td width="145">Wall Street Journal</td>

   <td width="109">wsj</td>

   <td width="228">https://www.wsj.com</td>

  </tr>

  <tr>

   <td width="133">41~60</td>

   <td width="145">Fox News</td>

   <td width="109">foxnews</td>

   <td width="228">https://www.foxnews.com</td>

  </tr>

  <tr>

   <td width="133">61~80</td>

   <td width="145">USA Today</td>

   <td width="109">usatoday</td>

   <td width="228">https://www.usatoday.com</td>

  </tr>

  <tr>

   <td width="133">81~00</td>

   <td width="145">Los Angeles Times</td>

   <td width="109">latimes</td>

   <td width="228">https://www.latimes.com</td>

  </tr>

 </tbody>

</table>




<strong><em>Limit your crawler so it only visits HTML, doc, pdf and different image format URLs and record the meta data for those file types </em></strong>

<h1>4.  Collecting Statistics</h1>




Your first task is to enhance the crawler so it collects information about:

<ol>

 <li><em>the URLs it attempts to fetch</em>, a two column spreadsheet, column 1 containing the URL and column 2 containing the HTTP status code received; name the file <strong>csv </strong></li>

</ol>

(where the name “NewsSite” is replaced by the news website name in the table above that you are crawling). The number of rows should be no more than 20,000 as that is our pre-set limit.

<ol start="2">

 <li><em>the files it successfully downloads</em>, a four column spreadsheet, column 1 containing the URLs successfully downloaded, column 2 containing the size of the downloaded file (in Bytes, or you can choose your own preferred unit (bytes,kb,mb)), column 3 containing the # of outlinks found, and column 4 containing the resulting content-type; name the file <strong>csv</strong>; clearly the number of rows will be less than the number of rows in fetch_NewsSite.csv</li>

 <li><em>all of the URLs (including repeats) that were discovered</em> and processed in some way; a two column spreadsheet where column 1 contains the encountered URL and column two an indicator of whether the URL resides in the website (<strong>OK</strong>), or <strong>b.</strong> points outside of the website (<strong>N_OK</strong>). (A file points out of the website if its URL does not start with the initial domain name, e.g. when crawling USA Today news website all inside URLs must start with <a href="https://www.usatoday.com/">www.usatoday.com</a><a href="https://www.usatoday.com/">.</a>) Name the file <strong>urls_NewsSite.csv</strong>. This file will be much larger than fetch_*.csv and visit_*.csv.</li>

</ol>

For example for New York Times- the URL <a href="https://www.nytimes.com/section/sports">http://www.nytimes.com/section/sports</a> and the URL <a href="https://nytimes.com/section/sports">http://nytimes.com/section/sports</a> are both considered as residing in the same website whereas the following URL is <strong><em>not</em></strong> considered to be in the same website, http://store.nytimes.com/




<strong>Note1: </strong>you should modify the crawler so it outputs the above data into three separate csv files; you may use them for processing later;

<strong>Note2:</strong> all uses of NewsSite above should be replaced by the name given in the column labeled <strong>NewsSite Name</strong> in the table on page 1.

<strong> </strong>

As you should use multiple threads, then based on the information recorded by the crawler in its output files, you are to collate the following statistics for a crawl of your designated news website:




<ul>

 <li>Fetch statistics:

  <ul>

   <li># fetches attempted:</li>

  </ul></li>

</ul>

The total number of URLs that the crawler attempted to fetch. This is usually equal to the

MAXPAGES setting if the crawler reached that limit; less if the website is smaller than that.

<ul>

 <li># fetches succeeded:</li>

</ul>

The number of URLs that were successfully downloaded in their entirety, i.e. returning a HTTP status code of 2XX.

<ul>

 <li># fetches failed or aborted:</li>

</ul>

The number of fetches that failed for whatever reason, including, but not limited to: HTTP redirections (3XX), client errors (4XX), server errors (5XX) and other network-related errors.<sub>1</sub>

<ul>

 <li>Outgoing URLs: statistics about URLs extracted from visited HTML pages o Total URLs extracted:</li>

</ul>

The grand total number of URLs extracted (including repeats) from all visited pages o # unique URLs extracted:

The number of <em>unique</em> URLs encountered by the crawler o # unique URLs within your news website:

The number of <em>unique</em> URLs encountered that are associated with the news website,

i.e. the URL begins with the given root URL of the news website, but the remainder of the

URL is distinct o # unique URLs outside the news website:

The number of <em>unique</em> URLs encountered that were <em>not</em> from the news website.




<ul>

 <li>Status codes: number of times various HTTP status codes were encountered during crawling, including (but not limited to): 200, 301, 401, 402, 404, etc.</li>

 <li>File sizes: statistics about file sizes of visited URLs – the number of files in each size range (See Appendix A).</li>

</ul>

o 1KB = 1024B; 1MB = 1024KB

<ul>

 <li>Content Type: a list of the different content-types encountered</li>

</ul>




These statistics should be collated and submitted as a plain text file whose name is CrawlReport_domain.txt, following the format given in Appendix A at the end of this document. Make sure you understand the crawler code and required output before you commence collating these statistics.




For efficient crawling it is a good idea to have multiple crawling threads. crawler4j supports multi-threading and our examples show setting the number of crawlers to seven (see the line in the code int numberOfCrawlers = 7;). However, if you do a naive implementation the threads will trample on each other when outputting to your statistics collection files. Therefore you need to be a bit smarter about how to collect the statistics, and crawler4j documentation has a good example of how to do this. See both of the following links for details:




<a href="https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java">https://github.com/yasserg/crawler4j/blob/master/crawler4j</a><a href="https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java">–</a><a href="https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java">examples/crawler4j</a><a href="https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java">–</a><a href="https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java">examples</a><a href="https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java">base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/MultipleCrawlerController.java</a> and <u>https://github.com/yasserg/crawler4j/blob/master/crawler4j-examples/crawler4j-examplesbase/src/test/java/edu/uci/ics/crawler4j/examples/localdata/LocalDataCollectorCrawler.java</u>




<u>All the information that you are required to collect can be derived by processing the crawler</u> <u>output.</u>




1 Based purely on the success/failure of the fetching process. Do not include errors caused by difficulty in parsing content <em>after</em> it has already been successfully downloaded.

<h1>5.  FAQ</h1>




<strong>Q: </strong>For the purposes of counting unique URLs, how to handle URLs that differ only in the query string? For example: https://www.nytimes.com/page?q=0 and https://www.nytimes.com/page?q=1

<strong>A:  </strong>These can be treated as different URLs.







<strong>Q: </strong>URL case sensitivity: are these the same, or different URLs?

https://www.nytimes.com/foo and https://www.nytimes.com/FOO

<strong>A:  </strong>The path component of a URL is considered to be case-sensitive, so the crawler behavior is correct according to RFC3986. Therefore, these are different URLs.

The page served may be the same because:

<ul>

 <li>that particular web server implementation treats path as case-insensitive (some server implementations do this, especially windows-based implementations)</li>

 <li>the web server implementation treats path as case-sensitive, but aliasing or redirect is being used.</li>

</ul>

This is one of the reasons why deduplication is necessary in practice.







<strong>Q: </strong>Attempting to compile the crawler results in syntax errors.

<strong>A:  </strong>Make sure that you have included crawler4j as well as all its dependencies.

Also check your Java version; the code includes more recent Java constructs such as the typed collection List&lt;String&gt; which requires at least Java 1.5.0.




<strong>Q: </strong>I get the following warnings when trying to run the crawler:




log4j: WARN No appenders could be found for logger log4j: WARN Please initialize the log4j system properly.

<strong>A:  </strong>You failed to include the log4j.properties file that comes with crawler4j.




<strong>Q:  </strong>On Windows, I am encountering the error: Exception_Access_Violation

<strong>A:  </strong>This is a Java issue. See: <a href="https://java.com/en/download/help/exception_access.xml">http://java.com/en/download/help/exception_access.xml</a>







<strong>Q: </strong>I am encountering multiple instances of this info message:




INFO [Crawler 1] I/O exception (org.apache.http.NoHttpResponseException) caught when processing request: The target server failed to respond INFO [Crawler 1] Retrying request

<strong>A:  </strong>If you’re working off an unsteady wireless link, you may be battling network issues such as packet losses – try to use a better connection. If not, the web server may be struggling to keep up with the frequency of your requests.

As indicated by the info message, the crawler will retry the fetch, so a few isolated occurrences of this message are not an issue. However, if the problem repeats persistently, the situation is not likely to improve if you continue hammering the server at the same frequency. Try giving the server more room to breathe:




<table width="576">

 <tbody>

  <tr>

   <td width="576">/**         Be polite: Make sure that we don’t send more than*         1 request per second (1000 milliseconds between requests).*/ config.setPolitenessDelay(2500);         /**         READ ROBOTS.TXT of the website – Crawl-Delay: <sup>10</sup>  * Multiply that value by 1000 for millisecond value*/</td>

  </tr>

 </tbody>

</table>







<strong>Q: </strong>The crawler seems to choke on some of the downloaded files, for example:




java.lang.StringIndexOutOfBoundsException: String index out of range: -2




java.lang.NullPointerException: charsetName




<strong>A:  </strong>Safely ignore those. We are using a fairly simple, rudimentary crawler and it is not necessarily robust enough to handle all the possible quirks of heavy-duty crawling and parsing. These problems are few in number (compared to the entire crawl size), and for this exercise we’re okay with it as long as it skips the few problem cases and keeps crawling everything else, and terminates properly – as opposed to exiting with fatal errors.




<strong>Q:</strong> While running the crawler, you may get the following error:

SLF4J: Failed to load class “org.slf4j.impl.StaticLoggerBinder”.

SLF4J: Defaulting to no-operation (NOP) logger implementation

SLF4J: See <a href="https://urldefense.proofpoint.com/v2/url?u=http-3A__www.slf4j.org_codes.html-23StaticLoggerBinder&amp;d=DwMFaQ&amp;c=clK7kQUTWtAVEOVIgvi0NU5BOUHhpN0H8p7CSfnc_gI&amp;r=5nz01Hxlw4vO4-NAa0g_Sg&amp;m=nu7oJEazZTnlDpvc9WMZ1qQ-WidO6_7bENFuWKhQKmA&amp;s=yMejVsVULqKz5a14dlVS0GFyMqeakYxVSoOHDu__hjQ&amp;e=">http://www.slf4j.org/codes.html#StaticLoggerBinder</a> for further details.




<ol>

 <li>Download slf4j-simple-1.7.25.jar from <a href="https://urldefense.proofpoint.com/v2/url?u=https-3A__repo1.maven.org_maven2_org_slf4j_slf4j-2Dsimple_1.7.25_&amp;d=DwMFaQ&amp;c=clK7kQUTWtAVEOVIgvi0NU5BOUHhpN0H8p7CSfnc_gI&amp;r=5nz01Hxlw4vO4-NAa0g_Sg&amp;m=nu7oJEazZTnlDpvc9WMZ1qQ-WidO6_7bENFuWKhQKmA&amp;s=ehRGdS6BP0KaclIGP6XkakQTYK23euSQ1ZZ6vAGQ6V8&amp;e=">https://repo1.maven.org/maven2/org/slf4j/slf4j</a><a href="https://urldefense.proofpoint.com/v2/url?u=https-3A__repo1.maven.org_maven2_org_slf4j_slf4j-2Dsimple_1.7.25_&amp;d=DwMFaQ&amp;c=clK7kQUTWtAVEOVIgvi0NU5BOUHhpN0H8p7CSfnc_gI&amp;r=5nz01Hxlw4vO4-NAa0g_Sg&amp;m=nu7oJEazZTnlDpvc9WMZ1qQ-WidO6_7bENFuWKhQKmA&amp;s=ehRGdS6BP0KaclIGP6XkakQTYK23euSQ1ZZ6vAGQ6V8&amp;e=">simple/1.7.25/</a> add this as an external JAR to the project in the same way as the crawler-4j JAR will make the crawler display logs now.</li>

</ol>




<strong>Q:</strong> What should we do with URL if it contains comma ?

A: Replace the comma with “-” or “_”, so that it doesn’t throw an error.




<strong>Q: </strong>Should the number of 200 codes in the fetch.csv file have to exactly match with the number of records in the visit.csv?

<strong>A:  </strong>Yes, it should be same




<strong>Q:</strong> “CrawlConfig cannot be resolved to a type” ?

A: import edu.uci.ics.crawler4j.crawler.CrawlConfig;




<strong>Q:</strong> What’s the difference between aborted fetches and failed fetches? A: failed:  Can be due to HTTP errors and other network related errors     aborted:  Client decided to stop the fetching. (ex: Taking too much time to fetch)  You may sum up both the values and provide the combined result in the write up.




<strong>Q:</strong> For some reason my crawler attempts 19,999 fetches, even though max pages is set to 20,000, does this matter?

A: It can be possible because 20,000 is the limit that you will try to fetch (it may contain successful status code like 200 and other like 301). But the visit.csv will contain only the URL’s for which you are able to successfully download the files.




<strong>Q: </strong>How to differentiate fetched pages and downloaded pages?

A: In this assignment we do not ask you to save any of the downloaded files to the disk. Visiting a page means crawler4j processing a page (it will parse the page and extract relevant information like outgoing URLs ). That means all visited pages are downloaded.

You must make sure that your crawler crawls both http and https pages of the given domain




<strong>Q: </strong>How much time should it approximately take to crawl a website using n crawlers?

A: (i) Depends on your parameters set for the crawler

(ii) Depends on the politeness you set in the crawler program

Therefore, it can vary for everyone




<strong>Q:</strong> For third CSV, should the discovered URLs include redirect URLs?

A: YES, if the redirect URL is the one that gets status code 300, then the url that redirects the URL to point to will be added to the scheduler of the crawler and waits to be visited.




<table width="628">

 <tbody>

  <tr>

   <td width="24"><strong>Q:</strong></td>

   <td width="343">When the URL ends with “/”, what needs to be done?</td>

   <td width="262"> </td>

  </tr>

  <tr>

   <td colspan="3" width="628">A: You should filter using content type. Please have a peek into Crawler 4j code located at <a href="https://github.com/yasserg/crawler4j/tree/master/crawler4j/src/main/java/edu/uci/ics/crawler4j/crawler">https://github.com/yasserg/crawler4j/tree/master/crawler4j/src/main/java/edu/uci/ics/crawler4j/cr </a><a href="https://github.com/yasserg/crawler4j/tree/master/crawler4j/src/main/java/edu/uci/ics/crawler4j/crawler">awler</a>You will get a hint on how to know the content type of the page, even if the extension is not explicitly mentioned in url</td>

  </tr>

 </tbody>

</table>




Q: Eclipse keeps crashing after a few minutes of running my code. But when I reduce the no of pages to fetch, it works fine.

A: Increase heap size for eclipse using this.

<a href="https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F"> </a><a href="https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F">https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F</a>




Q: What if a URL has an unknown extension?

A: Please check the content type of the page as it has an unknown extension




Q: Why do some links return True in shouldVisit() but cannot be visited by Visit()?

A: shouldVisit() function is used to calculate whether the page should be visited or not. It may or may not be a visitable page.




For example – If you are crawling the site http://viterbi.usc.edu/, the page http://viterbi.usc.edu/mySamplePage.html should be visited. but this page may return a 404 Not Found Error or it may be redirected to some other site like http://mysamplesite.com. In this case, shouldVisit() function would return true because the page should be visited but visit() will not be called because the page cannot be visited.

<strong>Comment:</strong>




<a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler</a>

<a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">4j</a><a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">–</a><a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">examples/crawler4j</a><a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">–</a><a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">examples</a><a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">–</a>

<a href="https://github.com/yasserg/crawler4j/blob/13afe9460c1e72ffebe1b14c260ae0fd2eaa5f5e/crawler4j-examples/crawler4j-examples-base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java">base/src/test/java/edu/uci/ics/crawler4j/examples/multiple/BasicCrawler.java</a>




has details on regular expressions that you need to take care.




<strong>Comment:</strong> Since many newspaper websites dump images and other types of media on CDN,  your crawl may only encounter html files. That is fine.




<strong>Comment</strong>: File types css,js,json and others should <strong>not</strong> be visited.




<strong>Comment</strong>: Some sites may have less than the 20,000 pages, but as long as the formula matches. i,e

# fetches attempted = # fetches succeeded + # fetches aborted + # fetches failed your homework is ok. However, the variation should not be more than 10% away from the limit as it is an indication that something is wrong.

<strong>Scenario: </strong>

My visit.csv file has about 15 urls lesser than the number of urls with status code 200. It is fine if the difference is less than 10%.




<strong>Comment</strong>: the homework description states that you only need to consider HTML, doc, pdf  and different image format URLs . But you should also consider URL’s with no extension as they may return a file of one of the above types.




<strong>Comment</strong>: The distinction between failed and aborted web pages. <em>failed</em>: Can be due to content not found, HTTP errors or other network related errors




<em>aborted</em>:  the client (the crawler) decided to stop the fetching. (ex: Taking too much time to fetch).

You may sum up both the values and provide the combined result in the write up.




<strong>Q:</strong> In the visit_NewsSite.csv, do we also need to chop “charset=utf-8” from content-type?  Or just chop “charset=urf-8” in the report?

A: You can chop Encoding part(charset=urf-8) in all places.







<strong>Q: REGARDING STATISTICS </strong>

<strong>A: </strong>#unique URLs extracted = #unique URLs within + #unique URLs outside       #total urls extracted is the sum of #outgoing links.

<strong>     </strong>#total urls extracted is the sum of all values in column 3 of visit.csv




<strong>Q: How to handle pages with NO Extension </strong>

A: Use <sub>getContentType()</sub> and don’t rely just on extension.

<strong><u>Note #1:</u></strong> Extracted urls do not have to be added to visit queue. Some of them which satisfy a requirement (e.g : content type, domain, not duplicate) will be added to visit queue. But others will be dumped by crawler.

However, as long as the grading guideline is satisfied, we will not deduct points.




<strong><u>Note#2:</u></strong> : 303 could be considered aborted. 404 could be considered failed.

To summarize: we consider a request to be aborted if the crawler decides to terminate that request. Client side timeout is an example.  Requests can fail due to reasons like content not found, server errors, etc.




<strong><u>Note#3:</u></strong> Fetch statistics:

<em># fetches attempted</em>: The total number of URLs that the crawler attempted to fetch. This is usually equal to the MAXPAGES setting if the crawler reached that limit; less if the website is smaller than that.

<em># fetches succeeded</em>: The number of URLs that were successfully downloaded in their entirety, i.e. returning a HTTP status code of 2XX.

<em># fetches failed or aborted</em>: The number of fetches that failed for whatever reason, including, but not limited to: HTTP redirections (3XX), client errors (4XX), server errors (5XX) and other network-related errors.

<strong><u>Note#4: </u></strong> Consider fetches failed and aborted as same similar to as mentioned in Note#3




<h2>Note#5:Hint on crawling pages other than html</h2>

Look for how to turn ON the Binary Content in Crawling in crawler4j. Make sure you are not just crawling the html parsed data and not the binary data which includes file types other than html.

Search on the internet on how to crawl binary data and I am sure you will get something on how to parse pages other than html types.

There will be pages other than html in almost every news site so please make sure you crawl them properly.




<strong>Q</strong>: Regarding the content type in visit_NewsSite.csv, should we display “text/html;charset=UTF8” or chop out the encoding and write “text/html” in the Excel sheet ?  A: ONLY TEXT/HTML, ignore rest.




<strong>Q:</strong> Should we limit the URLs that the crawler attempted to fetch within the news domain? e.g. if we encounter <u>www.facebook.com,</u> we should skip fetching by adding constraints in “shouldVisit()”? But do we need to include it in urls_NewsSite.csv?

A: Yes, you need to include every encountered url in urls_NewsSite.csv.




<strong>Q</strong>: All 3xx,4xx, 5xx should be considered as aborted?

A: YES




<strong>Q</strong>: ”cookie” domains are considered as original newsite domain ? A: NO




<ol>

 <li><strong>Q</strong>. More about statistics</li>

</ol>

A: visit.csv will contain the urls which are succeeded i.e. 200 status code with known/ allowed content types. Fetch.csv will include all the urls which are been attempted to fetch i.e. with all the status codes. fetch.csv entries will be = visit.csv entries (with 2xx status codes) + entries with status codes other than 2XX visit.csv =  entries with 2XX status codes.




“unknown” content types shouldn’t be included in fetch or visit.csv because only images, pdf, html content types are allowed.




(<strong>Note</strong>:-&gt; fetch.csv should have urls from news site domain only)