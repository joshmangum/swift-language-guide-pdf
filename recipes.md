## Making the pdf from Swift.org documentation

### Retrieve html source

Let's make a copy of the whole documentation site. 

We'll make a directory named `source` and download the swift documentation site in it.

`<revision date>` is the date the documentation was revised, it's in the [revision history](https://docs.swift.org/swift-book/RevisionHistory/RevisionHistory.html) on the swift.org documentation site. It's in the form `2018-09-17`

```
> mkdir -p <revision date>/source
> cd <revision date>/source
> wget --recursive --no-clobber --page-requisites --convert-links --domains swift.org  --no-parent  https://docs.swift.org/swift-book/
```

### Make a copy to work on

Now let's create a copy of the html to modify, copy `source/` to `final/`. We'll keep the `source/` directory unchanged.

```
> cp -r source final
```
### View locally

To view the swift book documentation from your local repo:

```
> cd <revision date>/final/docs.swift.org
> python3 -m http.server 8080
```
Then open  `http://localhost:8080` in your browser. 

### Transform html

The script `assemble_html.py` takes each of the sections of the Language Guide and appends them into a single composite html page.

From the top level repo directory run:


```
> python3 assemble_html.py --revision <revision date>
```

The script will create a new html page named `WholeBook.html`, the new combined page is in 

`<revision date>/final/docs.swift.org/swift-book/LanguageGuide/WholeBook.html`

### View locally again 

If the python server from above isn't still running:

```
> cd <revision date>/final/docs.swift.org
> python3 -m http.server 8080
```

Now open `http://localhost:8080/LanguageGuide/WholeBook.html` in your browser. All the sections under "Language Guide" will be together in one html page ready for reference or to print. 

### Copy edited css to overwrite existing css file

```
> cp application.css <revision date>/final/docs.swift.org/swift-book/_static/stylesheets/
```

Apple provides a good print style sheet. This makes minor changes: removing page padding, adding contrast to some washed out text colors, and removing some extraneous navigation elements.

You can diff `./application.css` against `<revision date>/source/docs.swift.org/swift-book/_static/stylesheets/application.css` to see the changes. About 10 lines in all.

```
diff ./application.css <revision date>/source/docs.swift.org/swift-book/_static/stylesheets/application.css
```
This is great place to make any style changes to the document before converting to pdf. Just edit the css and reload your browser.

In the application.css file the edits are inside the print media query, look for:
```css

@media only print{
    /* all changes in here */
}

```

### Convert to pdf

Use Chrome for printing for the pdf. Just open `http://localhost:8080/LanguageGuide/WholeBook.html` and hit print. 

The generated pdfs are in `<revision date>/final/pdfs/`

For generating booklets of the pdf http://thekeptpromise.com/CreateBooklet/ was terrific and highly recommended ($19.99). This orders the pages so that you can print double sided with 2 pages per side, then fold it in half and staple it to make a very book-like document.

#### Gory printing details

On a mac:

Letter: Chrome (not system) print, Letter size, 100% scale, all defaults, then Save

A4: Chrome (not system) print, A4 size, 100% scale, all defaults, then Save

Booklet: This was a lot of eyeballing and guessing using CreateBooklet but the result is pretty good.

First using Chrome's default dialog, under more settings, Paper Size: Legal, scale: 112%, Margins: None. Then save as pdf.

Second, open the Legal sized pdf in CreateBooklet. Choose "Create Basic Booklet", Output format: choose Letter, add page numbers (Gill Sans Light, size 8, at X:-85%, Y:90%), Scale:55%, choose Split Into: 4 Booklets. 3 booklets works too but I had to poke the staples through by hand.







