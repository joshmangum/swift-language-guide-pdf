## Making the pdf from Swift.org documentation

### Retreive html source

To make a copy of the whole documentation site, we'll download the html into the `source` directory.

`<revision date>` is the date the documentation was revised, it's in the [revision history](https://docs.swift.org/swift-book/RevisionHistory/RevisionHistory.html) on the swift.org documentation site.

```
> mkdir <revision date>/source
> cd <revision date>/source
> wget --recursive --no-clobber --page-requisites --convert-links --domains swift.org  --no-parent  https://docs.swift.org/swift-book/
```

### Make a copy to work on

To create a copy of the html to modify, copy `source/` to `final/`. We'll keep `source/` unchanged.

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

The script `assemble_html.py` takes each of the sections of the Language Guide and makes a single composite html page.

From the top level repo directory run:


```
> python3 assemble_html.py 
```

(If you're doing a new revision date you'll need to change it in the python code).

The script will put the new combined page in `<revision date>/final/docs.swift.org/swift-book/LanguageGuide/WholeBook.html`

Now open `http://localhost:8080/LanguageGuide/WholeBook.html` in your browser. All the sections under "Language Guide" will be there together in one html page. 

### Copy edited css to overwrite existing css file

```
> cp application.css <revision date>/final/docs.swift.org/swift-book/_static/stylesheets/
```

Apple provides a nice print style sheet. This makes minor changes: removes page padding, adds contrast to some washed out text colors, and removes some navigation elements.

All the changes are inside the print media query. You can diff `./application.css` against `<revision date>/source/docs.swift.org/swift-book/_static/stylesheets/application.css` to see the them. About 10 lines in all.

This is great place to make any style changes to the document before converting to pdf.

In the application.css file look for:
```css
...
@media only print{
/* all changes here */
...
}

```

### Convert to pdf

Use Chrome for printing for the pdf. Just open `http://localhost:8080/LanguageGuide/WholeBook.html` and hit print. 

For generating booklets of the pdf http://thekeptpromise.com/CreateBooklet/ was terrific and highly recommended ($19.99). This lets you print out the booklet, fold it and staple it.



