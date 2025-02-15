# Block AI bots crawlers
Prevent ai bots to crawl a website (NGNIX web server).

If you are looking for a solution to prevent AI bots to crawl your website, this approach is combining a robots.txt file and a web server directive.

Please **note the following**:

- while robots.txt files are a standard way of communicating to web crawler their's being welcome or not, not all crawlers are behaving accordingly; reports are some crawlers are not.
- the web server directive you find here is for the NGINX web server, if the web site you are working with is running on Apache this solution is not for you.
- new AI bots are showing up every day, they may change their name, or indeed implement way to by pass both robots.txt and the web server directive: what works today may not work tomorrow
- while uploading a robots.txt file should be fairly straightforward, tinkering with a web server is a different matter: you are on your own, if you are not comfortable messing with a web server doon't do it.

## Robots.txt
The robotx.txt file you find here should be placed in the root directory of the website you are working with.
Use a ftp/sftp tool or command according to your local and server setup.

More info on robots.txt could be found on **Google Search Central**: https://developers.google.com/search/docs/crawling-indexing/robots/intro

