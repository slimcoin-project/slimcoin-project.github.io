# The Slimcoin Project Website

The Slimcoin Project Website is a communication tool for the project participants and other interested community members. It contains basic information about the Slimcoin cryptocurrency as well as a basic help section, complemented by the [Wiki](https://github.com/slimcoin-project/Slimcoin/wiki).

The website uses Jekyll, the default Github Pages generator. New pages can by added by adding text files in the Markdown format. If you want write access, you can request it in the Bitcointalk thread. Or you can simply fork the repository and do pull requests.

We want the Website to stay an open project, so we would like all contributions being licensed by an open content license. The license to use is yet not decided, but it should allow content re-distribution and modification.

# Theme and multilingual approach

The theme used is a modification from the [Minima Jekyll theme](https://github.com/jekyll/minima) that allows multi-lingual sites. It is free software licensed under the MIT license.

For reference, the [readme file of the multlingual theme modification](Readme-multilingual.md) is conserved.

# Translations

For a new language being added, there are three different kinds of translations needed:

* the **index.html** file (home page) - in this one you must translate the text content of the HTML file.
* **other pages** - are available as .md (Markdown) files and can be much easier translated. See the syntax [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).
* **metadata** like description, footer items, etc.. These are translated in the **\_config.yml** file. Simply add, to every item provided, the language code (see "lang" below) and your translation. 

Each page (including index.html) contains a **header** with some metadata. **These items** can or must be translated:

* **title** - title shown as HTML title and h1 heading.
* **lang** - language; this is the code shown in the language menu. Please provide a commonly used two-letter code like en, es or pl.
* **menuitem** - the title shown in the main menu. It should be very short (at most, 3-4 words).
* **permalink** - the link target where you will find the page. **This one must be translated** because otherwise it will conflict with other language versions.

Do not translate the following items:

* **ref** - is a language independent identifier for each page (often a shortened english title).
* **layout** - is the layout of the page. Normally, it should be "page".
* **priority** - is the priority for a page to appear in the main menu. The lower the priority, the further left the menuitem title of the page appears. The index page should have the lowest priority "1", followed by the "About" page with "2".
