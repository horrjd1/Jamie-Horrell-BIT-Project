---
layout: post
title:  "Site Restructure"
date:   2020-03-12 18:17:51 +1300
categories: jekyll update
---

### Site Restructure
For this sprint I was assigned with restructuring the file system of the site into what we had decided during our scrum meeting on monday. Doing this furthered my understanding of the infrastructure of the site and what each part is doing. In order to achieve this I also had to change the routes for a lot of files as well as update the snapshots. I had Trent and Liams assistance for this since most of it was completely new to me.

### Cors
Cross-Origin Resource Sharing. My team last semester had set up the resources to use CORS on the site but weren't using it, so I was tasked with making the new express backend use it. I started by doing some research into what CORS is and how it works in my own time.Once I understood what I had to complete I added the following into the back-ends app.js file.
```
var app = express()
```
and
```
app.use(cors())
```
 The rest was set up by Trent and Liam previously but I still had to review to understand what it was doing.