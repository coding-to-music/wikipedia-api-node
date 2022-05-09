# wikipedia-api-node

# 🚀 Javascript full-stack 🚀

https://github.com/coding-to-music/wikipedia-api-node

https://wikipedia-api-node.vercel.app

by Mustapha Mekhatria / smartvikisogn https://mustaphamekhatria.medium.com/

https://github.com/smartvikisogn

https://mustaphamekhatria.medium.com/get-wikipedia-pages-views-data-with-nodejs-54a265e0a78c

https://github.com/smartvikisogn/WikipediaAPINodeJS

## Environment Values

```java
none
```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/wikipedia-api-node.git
git push -u origin main
vercel --prod --confirm
```

# How to use Wikipedia API with Nodejs

Wikipedia has an enormous data set such as page view statistics, tables, etc. And in this article, I will show you how to access the statistics data or the page view statistics using Wikipedia API and NodeJS.

Remark

You can find the final project in this GitHub link. https://github.com/smartvikisogn/WikipediaAPINodeJS

I will use Wikipedia API to get the dates and the users views. You can read more about Wikipedia API here. The data that I am interested in are the pages view statistics for Africa, from 4/27/2017–5/17/2018. The request to fetch the data is as follow: https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/en.wikipedia/all-access/user/Africa/daily/2017042700/2018051700

## Remark

Notice how to use the API by introducing the words (in bold) pageviews, Africa and the date in the request.

Let’s get started :)

Go to Wikipedia.com, search for Africa, then click on the View history tab, then on Page view statistics (see pictures below).

The picture above displays the views statistics of Africa from 4/27/2018 to 5/17/2018, but I would like to get the data from 4/27/2017. So, go to the dates field on the left side of the chart, then write the right dates:

Now, it is time to write some code to get the data in a nice table.

## Code time

As I mentioned above, I will use NodeJS to extract the data. I will also use the request-promise package as it simplifies HTTP request, or in other words, it helps me easily access and fetch any web page.

The first thing to do is to create a folder to save all the code. Next, open the terminal, browse to the folder created earlier, and create a package.json file by running this command line:

```java
npm init
```

Install also the request-promise package:

```java
npm install --save request
npm install --save request-promise
```

Now, let’s create a file such as `readPagesViews.js`, and copy/paste the code below:

```java
var rp= require('request-promise');
var options={

    method: 'GET',    uri:'https://wikimedia.org/api/rest_v1/metrics/pageviews/per-article/en.wikipedia/all-access/user/Africa/daily/2017042700/2018051700',
    json:true

};
rp(options)
.then(function(parseBody){
var data=[];
for(i=0 ;i<parseBody.items.length;i++){
data.push([parseBody.items[i].timestamp,parseBody.items[i].views]);
}

    console.log(data);
    })
    .catch(function (err){

});
```

## Explanations

The first line requires the package request-promise and passes it to the variable rp. The options object gathers the Get method parameters such as the link to the Wikipedia API, and the way to receive the data in JSON (json:true)

The options object is then passed as a parameter to rp; once the Get is executed, the result (data from Wikipedia) is saved into the object parseBody.
Basically, parseBody is a set of data received from Wikipedia:

```java
...
{ project: 'en.wikipedia',
article: 'Africa',
granularity: 'daily',
timestamp: '2018051100',
access: 'all-access',
agent: 'user',
views: 6727 },
{ project: 'en.wikipedia',
article: 'Africa',
granularity: 'daily',
timestamp: '2018051200',
access: 'all-access',
agent: 'user',
views: 5450 },
...
```

But don’t forget, that the goal is to get the dates and the users views. To get those two variables from the parseBody object, I use the following loop to save the timestamp (dates) and the views (users views) in the object data:

```java
    var data=[];
    for(i=0 ;i<parseBody.items.length;i++){
        data.push([parseBody.items[i].timestamp,parseBody.items[i].views]);
    }
```

Go back to the terminal and execute the code:

```java
node readPagesViews.js
```

And voila! The data from the African Pageviews Analysis is stored in the object data:

```java
...
  [ '2017090300', 5433 ],
  [ '2017090400', 5767 ],
  [ '2017090500', 6016 ],
  [ '2017090600', 6025 ],
  [ '2017090700', 6164 ],
  [ '2017090800', 5468 ],
  [ '2017090900', 4710 ],
  [ '2017091000', 5314 ],
...
```

Feel free to share your experience with this code, or if you have a better way to get the data :)
