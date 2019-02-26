---
layout: post
title: "Crime in Llandaff North and Gabalfa"
date: 2019-01-02
---

Since I moved and bought my first house in Cardiff I have subscribed to my local Facebook group, <a href="https://www.facebook.com/groups/954644197903602/?ref=bookmarks">Llandaff North & Whitchurch Daily Life Cardiff</a>, in order to keep up-to-date with the current affairs in my area. What is apparent on the group is that people often post about crime in Llandaff North and Gabalfa, and it is often suggested that the areas are getting 'worse'.

The types of crimes posted about typically involve vehicles, or theft from households and businesses. Me and my wife have been victims of vehicle crime twice in the past two years, first the back windscreen of our old Renault Clio was smashed (nothing taken), then a few weeks ago the passenger window of our VW Up! was smashed (a small dehumidifier pad stolen, but recovered in the lane next to our house).

Just before the latest incident I browsing the <a href="https://data.police.uk/docs/">UK police stats website</a> out of curiosity. However, the latest incident sparked me to do something with this data. Is it possible to use this data to firstly answer whether the areas are getting worse, but also to analyse the data for crime hotspots and patterns. The aim is then to present the information gained at the local PACT meeting in January.

<h2>Methodology</h2>

As mentioned above, the first action was to source the crime stats for Llandaff North and Gabalfa. To do this I used API calls to <a href="https://data.police.uk/docs/">https://data.police.uk/docs/</a>. The API requires a signal point of call, or a polygon search. As I am analysing an area, I need to use the polygon approach:

<code>
https://data.police.uk/api/crimes-street/all-crime?poly=<i>polygon</i>&date=<i>date</i>
</code>

Where <code><i>polygon</i></code> is a list of latitudes and longitudes in the format <code><i>lat1</i>,<i>lon1</i>:<i>lat2</i>,<i>lon2</i>:<i>lat3</i>,<i>lon3</i></code>.

Area polygons were sourced from MapIt <a href="https://mapit.mysociety.org/area/12047.html">Gabalfa</a> and <a href="https://mapit.mysociety.org/area/12046.html">Llandaff North</a>. These were then simplified because the API doesn't handle complex polygons. For this work, the polygon is therefore defined as:

<code>
polygon = '51.5087,-3.2419:51.5112,-3.2396:51.5047,-3.2129:51.5047,-3.1835:51.4986,-3.1842:51.4948,-3.1930:51.4981,-3.2225:51.5009,-3.2298:51.5087,-3.2419'
</code>

Furthermore, an a limiting factor for this work is that the earliest data we can get crime stats for from the API is January 2016.

Nonetheless, we call the API for every month between 01-2016 and the current month (01-2019). This will return the crime stats per month to to the last complete month, November 2018 in this case as the crime stats for December 2018 have yet to be released.

Once we have the URL request working, we convert to JSON, and then append to a DataFrame to store the crime stats for the entire time period. In this instance, this returns 5,430 crimes.

<h2>Is Crime Getting Worse?</h2>

To answer this question I will firstly analyse the total number of crimes committed in the areas over the entire time series. To do this I group the DataFrame by month.

The results are shown below as a graph, then summarised.

INSERT GRAPH HERE.

<ul>
<li>Between 01-2016 and 12-2018 there have been 5,430 crimes committed in Llandaff North and Gabalfa.</li>
<li>Since 01-2016 the number of crimes in Llandaff North and Gabalfa has been on average 165 per month (median 163).</li>
<li>The month with the fewest number of crimes was 02-2018 (117) and the month with the greatest, 05-2016 (207).</li>
<li>In 2018, the month with the greatest number was 10-2018 (197). The month with the fewest was 02-2018 (117).</li>
<li>2018 so far has the fewest number of crimes (1,559), even using the average for December in 2016 and 2017 (1,559 + 156 = 1,715), this is still fewer than 2016 (1,827) and 2017 (1,876).</li>
<li>The first half (01-06) of 2018 has fewer crimes (686) than 2016 (775) and 2017 (862).</li>
<li>The second half of 2018 (currently 873 crimes) looks set to surpass 2016 (892) and 2017 (871); with the December average (156), this is set to be 1,029 crimes.</li>
</ul>
