---
layout: archive
title: "Web Scraper V2"
permalink: /feige_web_scraper/
author_profile: true
---
Hello! This page will be used to help set up the web scraper. 

## Overview

With the new website format, the main difficulty is in order to view if an item is in stock, various buttons need to clicked (something the previous scraper was unable to accomidate). 

Thankfully, every time we click one of the buttons the URL will change. This allows us to split the scraping up into two different steps: **INDEXING** -- or identifying the URLs that we are trying to scrap, and **SCRAPING** -- once we have the URLs, checking the URL, brand name, and sku. 

## Requirements

The following will outline different packages that need to be installed for the new scraper to work.

### 1. Python Packages

first, install the *Selenium* package by typing the following into your command line. (I believe we used powershell last time?)

```console
$ pip install selenium
```

### 2. Chrome Web Driver

Selenium works by using what is known as the *Chrome Web Driver*. 

First, make sure that you have downloaded [Google Chrome](https://www.google.com/chrome/dr/download/)

Next, check the version of Google Chrome that you have [following this](https://help.illinoisstate.edu/technology/support-topics/device-support/software/web-browsers/what-version-of-chrome-do-i-have).

Finally, download the correct version of the [Chrome Web Driver](https://chromedriver.chromium.org/downloads) depending on your version of Google Chrome. This should a file named chromedriver.exe. We want this file to be in the same folder as the scraper. Below is an image of what it looks like on my computer. 

<div markdown="0" width="50%">    
    <img src="../images/feige_files.png" alt="Girl in a jacket" width="50%">
</div>
<br/>

## Usage
There are two ways to use the scraper...

### 1. Find all of the URLs using selenium, then start scraping
```console
$ python new_scraper.py
```

This command will do the following things:
1. open a chrome driver and start finding all the useful URLs (typically takes ~2 minutes and only does this once)
2. Saves these useful URLs to a file that you can use in the future instead of repeating this process every time
3. Begins to scrape the URLS

### 2. Load all the URLs from a file, then start scraping
```console
$ python new_scraper.py --file links.json
```
This command will do the following things:
1. this will open the file named `links.json` and use these useful URLs (instead of using Selenium). This will save ~2 minutes when the script starts.
2. Begins to scrape the URLS

<br/>

## Variables you can modify
In the script, I tried to put enough comments to make it understandable if you want to know how everything works. Below, I'll outline a couple things that can be useful to change.


### 1. Add In *Manual* Links
At the top of the script...
```python
manual_links = ["https://www.brownells.com/reloading/components/primers/rifle-primers/?sku=749004526"]
```

You can use this array to add in links that the indexing component missed. Currently, the only known missed example is [this primer](https://www.brownells.com/reloading/components/primers/rifle-primers). The reason is because they have multiple stages of buttons. 

To add these manual links, make the selection of what you want to scrape (i.e. Standard -- Small Rifle) **THEN** copy the link and paste it into the `manual_links` array. 

### 2. Specify SKUs to ignore
```python
sku_nums_to_ignore = ["749004527"]
```
Simply enter the SKU numbers that you would like to ignore

### 3. Ignore entire brands
Visit the `should_exclude` function for an example of how to ignore an entire brand.

# Final Comments

Through a little testing, I've found their new website periodically takes a really long time to service requests. I haven't tested it for a prolonged time but we can see how it works