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

## Ngnix Configuraiton
Configuring your Ngnix web server to block AI bots requires you to work on two different bits:

- a **map directive** to read http header for know AI bots
- an **if condition** that will implement a specific action if one of the AI bot declared in the map directive is found

### Map directive
This should be placed into the <code>http block</code> so it applies to all server blocks, this mean it will apply to all domains you may have (provided in each of their conf you add the if condition with the server block).

Depending on your configuration, but most likely than not you should have a <code>nginx.conf</code> file in <code>/etc/nginx/</code> om your server.
So, <code>/etc/nginx/nginx.conf/</code> is the file you should edit to add the map directive.

You can find an example in the *mad directive* file of this repository, where you'll have the same list of AI bots also declared in the robots.txt. Please note, there's no need for the two lists to be the same (robots.txt and Ngnix do not really talk to each other), but I guess the whole point is to cover as mamy known AI bots as possible.

A couple of considerations for the map directive.

**First**, in the following snippet from the code, the <code>$block_ai_bot</code> variable name can be (almost) anything, so you can name it $naughty_agents if you wish. The only thing is you obviously make sure to call that same variable name in the <code>if</code> conditiond

**Second**, spaces in bots names should be escaped -- either with <code>\s</code> (as in the map directive example provided) or by enclosing them in <code>"</code> quotes.

<code>
map $http_user_agent $block_ai_bot {
	default 0;
</code>

<code>
(...)
~*SemrushBot-SWA 1;
~*Sidetrade\sindexer\sbot 1;
(...)
</code>

Bots names are matched no matter the case, this is what <code>~*</code> is doing. Should you want for a name to be case sensitive, change it to <code>~BotName</code>.

