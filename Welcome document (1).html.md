# Welcome to StackEdit!

----------

----------

Hello, I am your first Markdown document within **StackEdit**[1](#fn:stackedit "See footnote"). Don’t delete me, I can be helpful. I can be recovered anyway in the `Utils` tab of the `Settings` dialog.

----------

## Documents

**StackEdit** stores your documents in your browser, which means all your documents are automatically saved locally and are accessible **offline!**

> **Note:**
> 
> -   StackEdit is accessible offline after the application has been loaded for the first time.
> -   Your local documents are not shared between different browsers or computers.
> -   Clearing your browser’s data may **delete all your local documents!** Make sure your documents are backed up using **Google Drive** or **Dropbox** synchronization (see [Synchronization](#synchronization) section).

#### Create a document

The document panel is accessible using button in the navigation bar. You can create a new document by clicking the `New document` sub-menu in the document panel.

#### Switch to another document

All your local documents are listed in the document panel. You can switch from one to another by clicking a document in the document panel or you can also use Ctrl+\[ and Ctrl+\] to toggle documents by most recently used.

#### Rename a document

You can rename the current document by clicking the document title in the navigation bar.

#### Delete a document

You can delete the current document by clicking the `Delete document` sub-menu in the document panel.

#### Export a document

You can save the current document to a file using the `Export to disk` sub-menu from the menu panel.

> **Tip:** See [Publish a document](#publish-a-document) section for a description of the different output formats.

----------

## Synchronization

**StackEdit** can be combined with **Google Drive** and **Dropbox** to have your documents centralized in the _Cloud_. The synchronization mechanism will take care of uploading your modifications or downloading the latest version of your documents.

> **Note:**
> 
> -   Full access to **Google Drive** or **Dropbox** is required to be able to import any document in StackEdit. Permission restrictions can be configured in the settings.
> -   Imported documents are downloaded in your browser and are not transmitted to a server.
> -   If you experience problems saving your documents on Google Drive, check and optionally disable browser extensions, such as Disconnect.

#### Open a document

You can open a document from **Google Drive** or the **Dropbox** by opening the `Synchronize` sub-menu and by clicking `Open from...`. Once opened, any modification in your document will be automatically synchronized with the **Google Drive** / **Dropbox** file.

#### Save a document

You can save any document by opening the `Synchronize` sub-menu and by clicking `Save on...`. Even if your document is already synchronized with **Google Drive** or **Dropbox**, you can export it to a another location. **StackEdit** can synchronize one document with multiple locations.

#### Synchronize a document

Once your document is linked to a **Google Drive** or a **Dropbox** file, **StackEdit** will periodically (every 3 minutes) synchronize it by downloading/uploading any modification. Any conflict will be detected, and a local copy of your document will be created as a backup if necessary.

If you just have modified your document and you want to force the synchronization, click the button in the navigation bar.

> **Note:** The button is disabled when you have no document to synchronize.

#### Manage document synchronization

Since one document can be synchronized with multiple locations, you can list and manage synchronized locations by clicking `Manage synchronization` in the `Synchronize` sub-menu. This will let you remove synchronization locations that are associated to your document.

> **Note:** If you delete the file from **Google Drive** or from **Dropbox**, the document will no longer be synchronized with that location.

----------

## Publication

Once you are happy with your document, you can publish it on different websites directly from **StackEdit**. As for now, **StackEdit** can publish on **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **Tumblr**, **WordPress** and on any SSH server.

#### Publish a document

You can publish your document by opening the `Publish` sub-menu and by choosing a website. In the dialog box, you can choose the publication format:

-   Markdown, to publish the Markdown text on a website that can interpret it (**GitHub** for example),
-   HTML, to publish the document converted into HTML (on a blog for example),
-   Template, to have a full control of the output.

> **Note:** The default template is a simple webpage wrapping your document in HTML format. You can customize it in the `Advanced` tab of the `Settings` dialog.

#### Update a publication

After publishing, **StackEdit** will keep your document linked to that publication which makes it easy for you to update it. Once you have modified your document and you want to update your publication, click on the button in the navigation bar.

> **Note:** The button is disabled when your document has not been published yet.

#### Manage document publication

Since one document can be published on multiple locations, you can list and manage publish locations by clicking `Manage publication` in the menu. This will let you remove publication locations that are associated to your document.

> **Note:** In some cases, if the file has been removed from the website or the blog, the document will no longer be published on that location.

----------

## Markdown Extra

**StackEdit** supports **Markdown Extra**, which extends **Markdown** syntax with some nice features.

> **Tip:** You can disable any **Markdown Extra** feature in the `Extensions` tab of the `Settings` dialog.
> 
> **Note:** You can find more information about **Markdown** syntax [here](http://daringfireball.net/projects/markdown/syntax "Markdown") and **Markdown Extra** extension [here](https://github.com/jmcmanus/pagedown-extra "Pagedown Extra").

### Tables

**Markdown Extra** has a special syntax for tables:

Item

Value

Computer

$1600

Phone

$12

Pipe

$1

You can specify column alignment with one or two colons:

Item

Value

Qty

Computer

$1600

5

Phone

$12

12

Pipe

$1

234

### Definition Lists

**Markdown Extra** has a special syntax for definition lists too:

Term 1

Term 2

Definition A

Definition B

Term 3

Definition C

Definition D

> part of definition D

### Fenced code blocks

GitHub’s fenced code blocks[2](#fn:gfm "See footnote") are also supported with **Prettify** syntax highlighting:

```
// Foo
var bar = 0;
```

> **Tip:** To use **Highlight.js** instead of **Prettify**, just configure the `Markdown Extra` extension in the `Settings` dialog.
> 
> **Note:** You can find more information:
> 
> -   about **Prettify** syntax highlighting [here](https://code.google.com/p/google-code-prettify/),
> -   about **Highlight.js** syntax highlighting [here](http://highlightjs.org/).

### Footnotes

You can create footnotes like this[3](#fn:footnote "See footnote").

### SmartyPants

SmartyPants converts ASCII punctuation characters into “smart” typographic punctuation HTML entities. For example:

ASCII

HTML

Single backticks

`'Isn't this fun?'`

‘Isn’t this fun?’

Quotes

`"Isn't this fun?"`

“Isn’t this fun?”

Dashes

`-- is en-dash, --- is em-dash`

– is en-dash, — is em-dash

### Table of contents

You can insert a table of contents using the marker `[TOC]`:

-   [Welcome to StackEdit!](#welcome)
    -   [Documents](#documents)
        -   -   [Create a document](#create-a-document)
            -   [Switch to another document](#switch-to-another-document)
            -   [Rename a document](#rename-a-document)
            -   [Delete a document](#delete-a-document)
            -   [Export a document](#export-a-document)
    -   [Synchronization](#synchronization)
        -   -   [Open a document](#open-a-document)
            -   [Save a document](#save-a-document)
            -   [Synchronize a document](#synchronize-a-document)
            -   [Manage document synchronization](#manage-document-synchronization)
    -   [Publication](#publication)
        -   -   [Publish a document](#publish-a-document)
            -   [Update a publication](#update-a-publication)
            -   [Manage document publication](#manage-document-publication)
    -   [Markdown Extra](#markdown-extra)
        -   [Tables](#tables)
        -   [Definition Lists](#definition-lists)
        -   [Fenced code blocks](#fenced-code-blocks)
        -   [Footnotes](#footnotes)
        -   [SmartyPants](#smartypants)
        -   [Table of contents](#table-of-contents)
        -   [MathJax](#mathjax)
        -   [UML diagrams](#uml-diagrams)

### MathJax

You can render _LaTeX_ mathematical expressions using **MathJax**, as on [math.stackexchange.com](http://math.stackexchange.com/):

The _Gamma function_ satisfying Γ(n)=(n−1)!∀n∈N

> **Tip:** Make sure you include **MathJax** into your publications to render mathematical expression properly. Your page/template should include something like this:

```
<script type="text/javascript" src="https://stackedit.io/libs/MathJax/MathJax.js?config=TeX-AMS_HTML"></script>
```

> **Note:** You can find more information about **LaTeX** mathematical expressions [here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).

### UML diagrams

You can also render sequence diagrams like this:

Created with Raphaël 2.1.0AliceAliceBobBobHello Bob, how are you?Bob thinksI am good thanks!

And flow charts like this:

Created with Raphaël 2.1.0StartMy OperationYes or No?Endyesno

> **Note:** You can find more information:
> 
> -   about **Sequence diagrams** syntax [here](http://bramp.github.io/js-sequence-diagrams/),
> -   about **Flow charts** syntax [here](http://adrai.github.io/flowchart.js/).

----------

1.  [StackEdit](https://stackedit.io/) is a full-featured, open-source Markdown editor based on PageDown, the Markdown library used by Stack Overflow and the other Stack Exchange sites. [↩](#fnref:stackedit "Return to article")
2.  **GitHub Flavored Markdown** (GFM) is supported by StackEdit. [↩](#fnref:gfm "Return to article")
3.  Here is the _text_ of the **footnote**. [↩](#fnref:footnote "Return to article")
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA2MjY0MDYxNl19
-->