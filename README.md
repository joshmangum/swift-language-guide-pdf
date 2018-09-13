## Swift Book PDF

This project offers

* PDF versions of the [Swift Language Guide](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html) book. 
* A script for downloading and transforming the html from Swift's site into one big html file. Which is then printable to a PDF using your browser.
* Swift Language Guide on one html file (great for easy searching).

### Grab and go 

##### Full page PDFs

[Letter size PDF](./2018-06-04/pdfs/Letter_The_Swift_Programming_Language_Guide_4.2.pdf) 

[A4 size PDF](./2018-06-04/pdfs/A4_The_Swift_Programming_Language_Guide_4.2.pdf)

##### Booklet PDFs

Booklet PDFs can be folded in half and stapled along the fold to make booklets. The whole book can be printed as three booklets.

Printed, they look like this:

![Booklets](./IMG_8592.JPG)


  - [Booklet 1 PDF](./2018-06-04/pdfs/Booklet1_The_Swift_Programming_Language_Guide_4.2.pdf)
  - [Booklet 2 PDF](./2018-06-04/pdfs/Booklet2_The_Swift_Programming_Language_Guide_4.2.pdf)
  - [Booklet 3 PDF](./2018-06-04/pdfs/Booklet3_The_Swift_Programming_Language_Guide_4.2.pdf)


#### View as one html page
To view the whole book in one html page download the repo. Then in the repo directory type

```
> cd 2018-06-04/final/docs.swift.org/swift-book/
> python -m http.server 8080
```

Then open http://localhost:8080/LanguageGuide/WholeBook.html in your browser


### How to

Want something slightly different?

[Recipes](recipes.md) explains how to go from scraping the Swift site to generating the PDFs.

Happy to accept pull requests.

### Credits

Orginal by Apple under [Creative Commons Attribution 4.0 International (CC BY 4.0) License](https://creativecommons.org/licenses/by/4.0/).

Offered under the same license.
