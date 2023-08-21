# Spidergram Example

This Spidergram example crawl is pre-configured with some common defaults
and a useful report template. It's designed to install and go without too
much hassle.

*Too* much.

## Installation

You'll need Docker, Docker Compose, Node.JS, and Spidergram installed. If you're
using a Mac without any of that stuff installed, the easiest way is to install
[Homebrew](https://brew.sh), then follow these instructions:

1. `brew install node`
2. `brew install docker-compose`
3. `npm install -g spidergram`
4. `docker-compose up --detach`

Congratulations. Things are installed.

## Running Spidergram

The default configuration file is set up to crawl `www.example.com`, which isn't terribly
helpful. You'll probably want to modify the `config/spidergram.config.yml` file, paying
attention to the `spider.seed` property (a list of URLs to use as starting points), and
the `urls.crawl` property (one or more [glob](https://lironzluf.github.io/minimatch-playground/) or regex patterns to use when matching urls
to crawl).

Once that's done, just type: `spidergram go`, and you should see something like:

```
Crawling URLs
 ███░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 7% | ETA: 80s | 9/115
```

That's it. The included configuration file already includes a starting-point URL,
rules for URL matching, and some basic data extraction settings. The `spidergram go`
command tells it to crawl the site, analyze the found pages, and then run a report.

## Manual Steps

If the crawl dies, or you have to cancel it before it's complete, `spidergram crawl --resume`
will pick up where it left off.

`spidergram analyze` will tell it to perform basic page processing and analysis;
there are a number of flags to turn specific analysis options on and off. On extremely
large sites (dozens of thousands of pages) this can take a while.

`spidergram report --list` will print out a list of the available reports, and
`spidergram report [name]` will run a specific report against the crawled data.

`spidergram url tree` can spit out a formatted tree view of the site's URLs; a
number of custom flags are available to control how it's output. For example,
`spidergram url tree --preset=collapse` will only show "branches" of the URL tree,
summarizing how many "leaf" pages exist in each branch.