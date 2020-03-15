---
layout: post
title:  "Site Restructure"
date:   2020-03-12 18:17:51 +1300
categories: jekyll update
---

### Site Restructure
For this sprint I was assigned with restructuring the file system of the site into what we had decided during our scrum meeting on monday. Doing this furthered my understanding of the infrastructure of the site and what each part is doing. In order to achieve this I also had to change the routes for a lot of files as well as update the snapshots.

### Cors
Cross-Origin Resource Sharing. My team last semester had set up the resources to use CORS on the site but weren't using it, so I was tasked with making the new express backend use it. I did this by adding:
```
var app = express()
```
and
```
app.use(cors())
```
into the back-ends app.js file. I also did some research into what CORS is and how it works in my own time.