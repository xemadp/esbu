# esbu

Simple utility for creating and managing static blog-style pages, all in one bash script.

## What does it do?
* Markdown entries from src/ get converted to html files in dst/entries/.
* Capable of maintaining drafts.
* Creates a summary page with the five most recent blog entries.
* Creates a page with the rolling view of the blog.
* Creates an rss feed.

## Requirements
requires the markdown tool for converting .md files to .html files.

## Usage
esbu OPTION arg1 [arg2]

OPTIONS:

* new - create new blog post
* list - list all blog entries
* remove - remove a given entry name
* draft - edit drafts
* summary - make index.html ( contains a summary of entries )
* finalize - finalize blog - ready to deploy

EXAMPLES:

* esbu new newpost  => creates a new entry as newpost.md
* esbu remove newpost => removes newpost
* esbu list =>  lists all entries


### Make sure you edit the SITE variable in esbu to whatever website you'd want to deploy to!

for example usage of esbu check out [this link](https://asciinema.org/a/502910)

\*\*\* *NOTE*  that esbu will create needed folders if they don't exist upon execution in the directory you run it in, so make sure you already have templates folder when you run it, otherwise an empty template folder will be created which will break things.

you can use `esbu new newentry` to start editing newentry.md after editing it you can either add it to entry queue or make it a draft.
You can do `esbu finalize` to finalize every .md file in src(except for drafts).
finalizing basically means all .md files in src will be turned to .html files, rss, summary and blog pages will be also be generated.
when finalizing, previous entries that have been finalized before will also be ignored,
for example if you had entry1.md and finalized it yesterday, that means that if you create entry2.md today and finalize both entry1.md and entry2.md, entry1.md will not be finalized again. 

## Templates
You need to have all the files that are in the templates folder, Make sure you edit templates to suit your own blog, You can practically change everything in templates *EXCEPT* from strings that are in this %FORMAT%, they are used in esbu in order to generate pages so don't delete/change them.

### quirks
You can put `<!---height=X H-->` where X is pixels, after a photo in a markdown file and esbu will maintain the mentioned size in the html file as well.
example:

``` md
![](image.jpg) <!---height=350 H--->
```

will be :

 
`<p><img src="image.jpg" alt="" style="width:100%;height:auto';max-width:350px" ></p>`

and thus maintaining the size mentioned.
You can deactiate this by uncommenting the second markdown line in finalize function.


## TODO

- [] Add custom sync script support;
- [] Add dates to markdown entries
