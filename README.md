# The Slimcoin Project Website

The Slimcoin Project Website is a communication tool for the project participants and other interested community members. It contains basic information about the Slimcoin cryptocurrency as well as a basic help section, complemented by the [Wiki](https://github.com/slimcoin-project/Slimcoin/wiki).

The website uses [Jekyll](https://jekyllrb.com/), the default Github Pages page generator. New pages can by added by adding text files in the [Markdown format](https://en.wikipedia.org/wiki/Markdown). If you want write access, you can request it in the Bitcointalk thread. Or you can simply fork the repository and do pull requests.

We want the Website to stay an open project, so we would like all contributions being licensed by an open content license. The license to use is yet not decided, but it should allow content re-distribution and modification.

# Theme and multilingual approach

The theme used is a "mashup": The basic structure is a modification from the [Minima Jekyll theme](https://github.com/jekyll/minima) that allows multi-lingual sites. It is free software licensed under the MIT license. Since December 2017, the site heavily uses design elements from the old *slimcoin.club* website that unfortunately went offline (which was based on Semantic-UI framework).

For reference, the [readme file of the multlingual theme modification](Readme-multilingual.md) is conserved.

# Translations

For a new language being added, there are three different kinds of translations needed:

* the **index.html** file (home page) - in this one you must translate the text content of the HTML file. This file must be located in the base directory of the web site (the same one where this README file resides).
* **other pages** - are available as .md (Markdown) files and can be much easier translated. See the syntax [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). These files are located in subdirectories of the **content** folder, whose name is the **language code**. If you add a completely new language version, please add a new subdirectory.
* **metadata** like description, footer items, etc.. These are translated in the **\_config.yml** file. Simply add, to every item provided, the language code (see "lang" below) and your translation.

Each page (including index.html) contains a YAML header, the so-called **Front Matter**, with some metadata. **These items** can or must be translated:

* **title** - title shown as HTML title and h1 heading.
* **lang** - language; this is the code shown in the language menu. Please provide a commonly used two-letter code like en for English, es for Spanish, ru for Russian or pl for Polish.
* **menuitem** - the title shown in the main menu. It should be very short (at most, 3 words).
* **permalink** - the link target where you will find the page. **This one must be translated** because otherwise it will conflict with other language versions.

Do not translate the following items:

* **ref** - is a language independent identifier for each page (often a shortened english title).
* **layout** - is the layout of the page. Normally, it should be "page".
* **category** - the category determines the menu where the item will appear. It is language-independent and in English.
* **priority** - is the priority for a page to appear in the main menu. The lower the priority, the further left the menuitem title of the page appears. The index page should have the lowest priority "1", followed by the "About" page with "2".
* **codeType** - pages with code can use two syntax highlighting models ("analysis" and "guide")

# Why Jekyll?

The Jekyll structure may seem complicated, but using Jekyll the site is much easier to maintain than with static HTML files. Jekyll works almost like a CMS, only that it doesn't use any database or server-side scripts. It generates automatically header, footer and HTML head for each page with a simple command. And it's deeply integrated with Github Pages - Github executes the command automatically and builds the site every time something has changed.

**Examples**: 
* if you want to modify the menu bar, you only have to edit header-home.html and header-page.html. All sub-pages will update the menu bar automatically.
* if you want to add a new stylesheet, simply edit head.html and include it there. All sub-pages will include it.
* if you add a new page and edit the category in the front matter accordingly, it will appear automatically in the menu you specify ("technology" or "help")


# How to change the base HTML pages

Every page is built by Jekyll automatically when it's modified, the final site is stored in the **_site** folder. Jekyll uses, basically, four elements per page: head, header, content, and footer.

Three of them are HTML files that are stored in the **_includes** folder:

* **head.html** - this file contains the HTML head, with elements like links to stylesheets and JavaScript files.
* **header-home.html** - this file contains the header in the "big" variant used on the home pages. The header consists mainly of the menu bar and a masthead/banner.
* **header-page.html** - this file contains the header in a smaller variant, without the masthead.
* **footer.html** - this file contains the footer, with (currently) four columns.

Between the header and the footer, the **content** of the file is placed.

There are three template files, stored in the **_layouts** folder:

* **home-layout.html** - this file is used by the home pages and cointain head, the bigger header, content and footer.
* **page-layout.html** - this file is used by every other page and does only include head, the smaller header, content and footer.
* **page.html** - contains additional formatting for static content pages, like help texts.
* **post.html** - (currently not used) is similar to page.html but is for periodic posts and news items, like blog posts.

**Note:** Each sub-page of the site is stored in a sub-directory of the site, so if you want to link to it, you must link to that subdirectory, not to a link to a file. For example, the About page is located at http://slimco.in/about/. However, most of the links are generated automatically by Jekyll (e.g. if you add a new help page).

**Note 2:** If changing the design, DON'T touch the contents of the **_site** directory directly! This directory is generated automatically each time something is changed, so you will eventually lose all your changes.
