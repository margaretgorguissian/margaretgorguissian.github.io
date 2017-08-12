---
layout: post
title: Breaking Bad
---

I am in the process of making a little python program that can be used to create an astrological birth chart.
It does not actually create the birth chart-- my friend built an Android app for making birth charts, and he
said the geometry sucked. My end goal for this is to write an Alexa skill that allows a user to say "Alexa,
what's my rising sign?" and Alexa says, "Jimmy, you are a rising Libra. May God help you." for Amazon's little
university free Echo promo thing-- so I don't really feel like dealing with geometry right now. I want something a
little quicker. 
  
Instead, I am using an existing birth chart maker, an accessing the information on the page after the user has
provided their birthplace, date, and time. Alabe.com has a free birth chart maker, and it is perfect for my use 
because unlike many other birt chart makers:
  
*  They don't e-mail you the birth chart  
*  They don't use latitude and longitude, just place names
*  They don't require you to choose a location from a list of locations
  
The birth chart urls are formatted like so:
  
`generic url blah blah/MONTH=integer & DAY=integer & YEAR=integer & HOUR=integer & MINUTE=integer
 & AMPM=string & TOWN=string & COUNTRY=string & STATE=string/some more url blah blah`
  
which lends itself very nicely for me writing a little program to insert whatever I want into the url and then 
accessing the birth chart. I have successfully done that in my program. However, it gets a little messy when I 
want to filter out JUST the birthchart information. I'm currently using Beautiful Soup to parse the page.
Here's what the meat of the page looks like, for my birth chart:
  
`<h4 style="text-align:center">`  
`    Here is the Astro Chart you requested:`  
`   </h4>`  
`  </div>`  
`  <div id="printReady">`  
`   <div class="chart" style="text-align:center">`  
`    <img alt="Free Birth Chart" src="pics/2457977570642.gif"/>`  
`   </div>`  
`   <br/>`  
`   <p>`  
`    <strong>`  
`with your Report!close attention to what is said about it. Now, onyou`  
`     <br/>`  
`     <br/>`  
`     Name: Astrolabe Customer`  
`     <br/>`  
`     December 24 1996`  
`     <br/>`  
`     4:20 PM  Time Zone is EST`  
`     <br/>`  
`     Washington, DC`  
`     <br/>`  
`     <br/>`  
`     Rising Sign	is in	27 Degrees	Gemini`  
`     <br/>`  
`and absorb things at a deeper level.uperficially -- try to dig in ay and`  
`     <br/>`  
     <br/>
     Sun         	is in	03 Degrees	Capricorn.
     <br/>
tireless in reaching your goals.g totally persistent, tenacious andt
     <br/>
     <br/>
     Moon        	is in	03 Degrees	Cancer.
     <br/>
you go out of your way to be accommodating to them.to contact, and. You
     <br/>
     <br/>
     Mercury     	is in	19 Degrees	Capricorn.
     <br/>
humor tends toward being earthy and slapstick crude.c. Your sense ofare
     <br/>
     <br/>
     Venus       	is in	09 Degrees	Sagittarius.
     <br/>
outspoken manner.ssive of you. You are known for your friendly,htlynlity
     <br/>
     <br/>
     Mars        	is in	26 Degrees	Virgo.
     <br/>
their right to choose their own lifestyles.tolerant of others andes.. You
     <br/>
     <br/>
     Jupiter     	is in	23 Degrees	Capricorn.
     <br/>
tend to be cool and detached.ous. You are very efficient but youThisthe
     <br/>
     <br/>
     Saturn      	is in	01 Degrees	Aries.
     <br/>
therefore are respected and admired.r your circumspection andfullyt to
     <br/>
     <br/>
     Uranus      	is in	02 Degrees	Aquarius.
     <br/>
interpersonal one-on-one relationships.n or neglect in your owngroupt.
     <br/>
     <br/>
     Neptune     	is in	26 Degrees	Capricorn.
     <br/>
expectations on all fronts.als unless you have lowered yourd itllality
     <br/>
     <br/>
     Pluto       	is in	04 Degrees	Sagittarius.
     <br/>
pursue their own course in life will be reasserted. individuals tolyems
     <br/>
     <br/>
     N. Node     	is in	03 Degrees	Libra.
     <br/>
personal private needs that should not be neglected.hers -- you have
     <br/>
     <br/>
     <br/>
1-800-THE-NOVA for prices and information.s at offerings at re under your
     <br/>
     <br/>
    </strong>
   </p>
`   <p>`  
`   </p>`  
`  </div>`  
  
Notice anything?
  
The stuff I want-- namely, the planets and their signs, aren't between any tags besides the broader `<p>` tags.
I don't know if this is just nasty formatting, or if it's purposeful to discourage people like me from scraping
the webpage.
  
This reminds me of a problem I encountered in my Digital Humanities class in Fall 2016. I wanted to run some
analysis on Greek texts, but for one of the texts I was using, all the lines were not between `<p>` tags, they were
just separated by `<br>` tags. At the time, I was using the data analytics software KNIME, not writing code in python,
and didn't know how to fix the issue, so I just chose a better formatted text to analyze (in my defense, I was short
on time). 
  
Not doing that this time! On Stack Overflow, I found [a user who was in the same situation I was-- and with them,
an answer!](https://stackoverflow.com/questions/5275359/using-beautifulsoup-to-extract-text-between-line-breaks-e-g-br-tags)
I copied an pasted the answer into my code, changing nothing, and my output looked like this:
  
`Name: Astrolabe Customer
December 24 1996
4:20 PM  Time Zone is EST
Washington, DC
Rising Sign	is in	27 Degrees	Gemini
and absorb things at a deeper level.uperficially -- try to dig in ay
Sun         	is in	03 Degrees	Capricorn.
tireless in reaching your goals.g totally persistent, tenacious andt
Moon        	is in	03 Degrees	Cancer.
you go out of your way to be accommodating to them.to contact, and.
Mercury     	is in	19 Degrees	Capricorn.
humor tends toward being earthy and slapstick crude.c. Your sense of
Venus       	is in	09 Degrees	Sagittarius.
outspoken manner.ssive of you. You are known for your friendly,htlyn
Mars        	is in	26 Degrees	Virgo.
their right to choose their own lifestyles.tolerant of others andes.
Jupiter     	is in	23 Degrees	Capricorn.
tend to be cool and detached.ous. You are very efficient but youThis
Saturn      	is in	01 Degrees	Aries.
therefore are respected and admired.r your circumspection andfullyt
Uranus      	is in	02 Degrees	Aquarius.
interpersonal one-on-one relationships.n or neglect in your owngroup
Neptune     	is in	26 Degrees	Capricorn.
expectations on all fronts.als unless you have lowered yourd itll
Pluto       	is in	04 Degrees	Sagittarius.
pursue their own course in life will be reasserted. individuals toly
N. Node     	is in	03 Degrees	Libra.
personal private needs that should not be neglected.hers -- you have
1-800-THE-NOVA for prices and information.s at offerings at re under`
  
Here is the code I copied:
  
`for br in soup.findAll('br'):  
    next_s = br.nextSibling  
    if not (next_s and isinstance(next_s,NavigableString)):  
        continue  
    next2_s = next_s.nextSibling  
    if next2_s and isinstance(next2_s,Tag) and next2_s.name == 'br':  
        text = str(next_s).strip()  
        if text:  
            print "Found:", next_s  
`
What does this say?
  *  For every br (line break) in the soup:
  *  Find the "next sibling" of the linebreak (because this code is so poorly formatted, it is the next line)
  *  If the next line (line A) doesn't exist, or if it's not a navigable string, go to the next br
  *  Otherwise check to see if the line after next is a br
  *  If it is, strip line A of any tags and print line A
  
For now, I have achieved my goal: discard the line breaks, and access what is in between them. Now, on the the next one: 
getting just what I care about from the lines: the planet and the sign.
