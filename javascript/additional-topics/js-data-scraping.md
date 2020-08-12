# Data Scraping

## Objectives

* Identify situations where data scraping would be beneficial
* Understand the methods and legality of data scraping
* Use modules such as Cheerio to scrape data from the web

## What is web scraping?

Scraping \(Screen Scraping, Web Data Extraction, Web Harvesting, etc\) refers to the process of requesting an HTML page and picking out relevant data from the document string. In other words, you can scrape content off of web pages by parsing the html.

#### Why scrape?

* no API available
* API is unreliable/unkept/etc.
* no fee or call limit \(unless a rate-limit is set up\)
* more anonymous than getting data through dev resources

#### Why not scrape?

* need to log into site in order to access desired data
* organization of data makes it hard/laborious to access
* web page structure frequently changes \(program that uses scraped data would need constant updates\)
* copywrite and other legal issues

**NOTE:** The legality of data scraping and using a site's data may depend on a site's terms of use. Scraping a site and using the data for profit may violate a site's terms of use, so be careful before scraping a site. This is not legal advice, and we are not lawyers, but we recommend that you contact a lawyer if you want to scrape data for a for-profit application.

## Getting Started: Scraping Seattle Neighborhoods

Let's try creating a program that will scrape neighborhood data from this site:

[https://visitseattle.org/partners/?frm=partners&ptype=visitors-guide&s=&neighborhood=Capitol+Hill](https://visitseattle.org/partners/?frm=partners&ptype=visitors-guide&s=&neighborhood=Capitol+Hill)

To get started, create a new folder, and initialize npm. We'll also want to install two modules:

* `request` - for accessing external resources via HTTP
* `cheerio` - essentially, this is server side jQuery. We will be using this to traverse the data we get back from our request.

### Step 1: Get the HTML document

There are multiple ways to get an HTML document, but we'll use the `request` module in this example. To scrape data from the site, we need to request the webpage. In a `gethoods.js` file, import the `request` and `cheerio` modules, then make a request to the Seattle Neigbhborhoods website.

```javascript
const request = require('request')
const URL = 'https://visitseattle.org/partners/?frm=partners&ptype=visitors-guide&s=&neighborhood=Capitol+Hill'

request(URL, (error, response, body) => {
    console.log(body);
});
```

Run the program and take a look at your output. What did the request return?

Look over the [Cheerio Documentation](https://github.com/cheeriojs/cheerio) - for more info about our next steps.

### Step 2: Parse the HTML

The request to the seattle neighborhoods url gave us the entire HTML document string - now we need to parse it in order to pick out the specific data we're looking for. This is where Cheerio comes in! Inside the callback function of request, we'll pass the html we got back into the `cheerio.load()` function. We store the result, which is a cheerio object, in the dollar sign variable because cheerio is designed to mimic jQuery selectors \(though technically, we could store it in any variable we'd like\).

```javascript
request(URL, (error, response, body) => {
  var $ = cheerio.load(body);
  console.log($);
});
```

Run the program and take a look at the `cheerio` object. How might we find the html again? Does the `cheerio` object contain a method for this?

### Step 3: Identify the content you want to scrape.

* First you have to identify what content you're looking to scrape and how to access it. Let's aim to scrape the names of all the busineses listed on this page of Capitol Hill businesses. Open the dev tools and inspect the page to see if you can pinpoint the elements that have the relvant information for each result.

Upon some inspection, we can see that the results live inside of a `search-results` `div`, which contains a `search-results-partner` `section` element. Inside *that* there is a `search-result-container` `div` that has a `search-result` `div` for each result.

Let's try to target the name of the first business. Inspect the first `search-result` `div` and identify exactly where the business name lives.

The business name can be found inside the `search-result-preview` `div` as both the `title` of the nested `a` tag, as well as the `h3` child of that anchor. 

First let's grab the first `search-result-preview` element. Cheerio uses [jQuery selectors](https://www.w3schools.com/jquery/jquery_ref_selectors.asp) to identify elements.

```javascript
request(URL, (error, response, body) => {
    let $ = cheerio.load(body);
    let result = $('.search-result-preview').html();
    console.log(result)
});
```

Now let's target the `title` attribute:

```javascript
request(URL, (error, response, body) => {
    let $ = cheerio.load(body);
    let result = $('.search-result-preview > a').attr('title');
    console.log(result)
});
```
Great! Now we know how to find the title of **one** business, but how do we get all of them?

# THE REST OF THIS IS TODO!!!

### Step 4: Traverse the DOM \(scrape!\)

* Cheerio has its own `.map()` function to parse through a cheerio object, but it still returns another cheerio object

```javascript
    var neighborhoods = $('.info-window-content').map(function(index, element) {
        // find() docs -> traversing -> find
        return {
            name: $(element).find('h4').text(),
            link: $(element).find('a').attr('href')
        };
    });
    console.log(neighborhoods);
```

This still gives us a lot of gobbledy-gook we didn't ask for. Use the `.get()` function after `.map()` to see an array of exactly what we asked for \(see docs -&gt; traversing -&gt; get\):

```javascript
    // add .get() to just get back what you asked for, instead of an entire cheerio object
    var neighborhoods = $('.info-window-content').map(function(index, element) {
        return {
            name: $(element).find('h4').text(),
            link: $(element).find('a').attr('href')
        };
    }).get();
    console.log(neighborhoods);
```

### Final Code

[cheerio-scraping-seattle-neighborhoods repo](https://github.com/WDI-SEA/cheerio-scraping-seattle-neighborhoods)

```javascript
var request = require('request');
var cheerio = require('cheerio');

request('http://www.visitseattle.org/things-to-do/neighborhoods/', function(error, response, data) {
    var $ = cheerio.load(data);

    var neighborhoods = $('.info-window-content').map(function(index, element) {
        return {
            name: $(element).find('h4').text(),
            link: $(element).find('a').attr('href')
        };
    }).get();

    console.log(neighborhoods);
});
```

## Exercise

Modify your code to scrape the photo and description of each neighboorhood too! Your `console.log` should print out and array of objects that each include a `name`, a `link`, a `photo` \(if there is one\), and a `description`.

## Scraping multiple sites

By scraping this site, we were able to return an array of neighborhoods, complete with their name and a link to more information. Now, if we want to get neighborhood descriptions, we would need to make many more requests to retrieve additional webpages. Look at the notes for [async](js-async.md) for how to accomplish this task.

## Some other resources on scraping

* [Scraping with Node](http://maxogden.com/scraping-with-node.html)
* [Web Scraping For Fun and Profit](https://blog.hartleybrody.com/web-scraping/)

