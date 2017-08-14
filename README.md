# Linking Playlist Radio to Facebook Instant Articles

These code examples serve to show how to connect Playlist Radio playlists to Facebook Instant Articles through an RSS feed.

## Connecting Website

You need to insert this meta tag into the Playlist Radio head tag

```html
<meta property="fb:pages" content="109592009722217" />
```

## Facebook Instant Articles HTML Markup

For Facebook Instant Articles, you need to update an RSS feed with specific HTML for the article.
I have created the exact HTML code you need to insert data into and then push along to the RSS feed. You will find it in the article.html file in this repo. The code is commented to show what data needs to be added and where, but I will also lay it out below.

**Data to be added in each HTML snippet before sending off**
1. URL to Playlist on Playlist Radio --> Add into href attribute of <link> inside the <head>
2. URL to Playlist Cover Image --> Add into src attribute of <img>
3. Text Name of Playlist --> Add into <h1>
4. URL for each 3rd Party Playlist --> Add into respective href of <a> with corresponding name (i.e. iTunes, Spotify, etc.)
5. Text of Song List --> Add a new <li> for each song name / artist inside the <ol>

## Creating RSS Feed

I have created an example of this using the [Feed](https://www.npmjs.com/package/feed) package in Node.js
You can check it out [here](https://github.com/mwhitcom/rss-facebook-test).

There is also an example of how the RSS xml file should look when outputed. Basically you put the entire HTML snippet once data has been added into <content:encoded>.

**Essentially this is the flow:**
1. HTML snippet in article.html is stored in a varible on server side
2. Playlist is created on front end and data is dynamically added into HTML snippet
3. HTML snippet is then sent into function that creates and updates RSS feed
4. rss.xml file is created or updated (stored in public/rss/rss.xml)
5. Facebook then reads RSS feed (i.e. http://www.playlistradio.com/rss/rss.xml) and pulls in new playlist

I called the feed creation / update function inside of the server side function that stored the new playlist data in the database.

