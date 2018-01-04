---
layout: post
title: Tuples All the Way Down
---
I am making progress on my astro chart python program. It turns out, my whole
issue in my last blog post, involving the line breaks, is completely moot! Here
is what my solution looks like now:  

```python
    chart = soup.find_all(string=re.compile("Degree"))
    chartlist = []
    for line in chart:
        planet = line.split(None, 1)[0]
        sign = line.rsplit(None, 1)[-1]
        chartlist.append((planet, sign))
    print chartlist
```
A wee bit of regex got involved-- but it turns out, I didn't even need to worry
about the linebreaks! Using the `find_all` function in BeautifulSoup and compiling
my query into a RegEx object allowed me to filter out any line that did not have
the word "degree" in it-- i.e., any line that was not one with a planet and a sign.
It then takes the first word in the line (the planet) and the last word in the
line (the sign), and stores them.

I am storing planets and signs in a list of tuples. I noticed something interesting
while building this list, though.  

If I declare a tuple and store the planet and sign in it, I can add it to the list
like so:  
```python
tup = (planet, sign)
chartlist += tup
```  
However, if I try to add a tuple to the list using `+=` without first declaring
a separate tuple variable (`chartlist += (planet, sign)`),
it doesn't work. It adds the planet and sign separately to the list, not as a
tuple. BUT! If I use the `append` function of lists instead, writing
`chartlist.append((planet, sign))`, it DOES successfully add the tuple to the
list.
