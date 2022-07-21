# esbu

Simple utility for creating and managing static blog-style pages, all in one bash script.

## What does it do?
* Markdown entries from src/ get converted to html files in dst/entries/.
* Capable of maintaining drafts.
* Creates a page with the rolling view of the blog.
* Creates an rss feed.
* Creates an index.html page with a blog summary.

## Installing 

``` bash
git clone "https://github.com/xemadp/esbu"
cd esbu
chmod +x esbu
```
open esbu and edit the SITE variable in esbu to whatever website you'd want to deploy to!
you can copy esbu to your $PATH directory, but make sure you have the proper templates when you run
it in a different directory!

## Requirements
requires the markdown tool for converting .md files to .html files.

## Usage
esbu OPTION arg1 [arg2]
OPTIONS:

* n, new - create new blog post
* e, edit - edit already existing blog posts
* l, list - list all blog entries
* rm, remove - remove a given entry 
* r, rename - rename a given entry 
* d, draft - edit drafts
* fd, finishdraft - move draft to src folder - ready to build
* b, build - build blog - ready to deploy

EXAMPLES:

* esbu new newpost  => creates a new entry as newpost.md
* esbu remove newpost => removes src/newpost.md and dst/entries/newpost.html (if it exists)
* esbu r newpost post => renames src/newpost.md to src/post.md
* esbu d newdraft => creates src/drafts/newdraft.md and opens it in editor
* esbu fd newdraft => moves src/drafts/newdraft.md to src/newdraft.md
* esbu list =>  lists all entries
* esbu f =>  builds all entries


\*\*\* *NOTE*  that esbu will create needed folders if they don't exist in the directory you run it in, so make sure you already have proper templates when you run it, otherwise an empty template folder will be created which will break things.

you can use `esbu new newentry` to start editing newentry.md after editing it you can either add it to entry queue or make it a draft.
You can do `esbu build` to build every .md file in src(except for drafts).
finalizing basically means all .md files in src will be turned to .html files, rss, summary and blog pages will be also be generated.
when building, previous entries that have been built before will also be ignored,
for example if you had entry1.md and built it yesterday, that means that if you create entry2.md today and build both entry1.md and entry2.md, entry1.md will not be built again. 

## Templates
You need to have all the files that are in the templates folder, Make sure you edit templates to suit your own blog, You can practically change everything in templates *EXCEPT* from strings that are in this %FORMAT%, they are used by esbu in order to generate pages so don't delete/change them.

### Features
You can put `<!---height=Xpx-->` where X is the amount of pixels, after a photo in a markdown file and esbu will maintain the mentioned size in the html file as well.
example:

``` md
![](image.jpg) <!---height=350px--->
```

will be :

 
`<p><img src="image.jpg" alt="" style="width:100%;height:auto';max-width:350px" ></p>`

and thus maintaining the size mentioned.
You can deactiate this by uncommenting the sed command after the markdown command in build function.


## TODO

- [ ] Add custom sync script support;
- [x] Add dates to markdown entries
