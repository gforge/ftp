cat("\n ** Starting .Rprofile **")
options(rstudio.markdownToHTML = 
  function(inputFile, outputFile) {      
    require(markdown)
    htmlOptions <- markdownHTMLOptions(defaults=TRUE)
    # LibreOffice hangs when the png is included in the html file
    # I have therefore this option where you actively 
    # have to choose inline if you want the png to be inline
    if (getOption("base64_images", "No") != "inline")
      htmlOptions <- htmlOptions[htmlOptions != "base64_images"]
    
    # Now in this section we skip writing to the outputfile
    # and keep the markdown text in the md_txt variable
    md_txt <- markdownToHTML(inputFile, options = htmlOptions,
                   stylesheet=ifelse(file.exists('custom.css'), 
                                     'custom.css',
                                     getOption("markdown.HTML.stylesheet")))
    
    if (getOption("LibreOffice_adapt", "Yes") == "skip"){
      writeLines(md_txt, con=outputFile)
    }else{
      # Annoyingly it seems that Libre Office currently 
      # 'forgets' the margin properties of the headers,
      # we therefore substitute these with a element specific
      # style option that works. Perhaps not that pretty but
      # it works and can be tweaked for most things.
      writeLines(
        gsub("<h([0-9]+)>", 
             "<h\\1 style='margin: 10pt 0pt 0pt 0pt;'>", 
             gsub("<h1>",
                  "<h1 style='margin: 24pt 0pt 0pt 0pt;'>",
                  md_txt)), 
        con=outputFile)
    }
  }
)

# I’ve  added some automated comments just as a reminder, remove
# the cat() if you want the .Rprofile to be quiet (note, the output does
# not affect the knitr document)
cat("\n * If you want knitr markdown png-files to be inside the document",
    " then set the options(base64_images = 'inline') for it to work.")
cat("\n * If you don't want the Libre Office adaptations then set",
    " options(LibreOffice_adapt = 'skip')")
cat("\n * If you want knitr markdown to use a custom css then",
    " just input a 'custom.css' file in the Rmd file's directory.")
cat("\n ** End .RProfile **\n")