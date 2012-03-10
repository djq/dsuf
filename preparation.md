
# Programs to install

We will be using the following software programs during class. The programs are all open-source and cross platform (win/mac/linux).

* R: [http://www.r-project.org/](http://www.r-project.org/)
* Rstudio: [http://rstudio.org/](http://rstudio.org/)
* QGIS: [http://www.qgis.org/](http://www.qgis.org/)

Install `R` first, then install `RStudio`. After you install `R` try downloading and installing a package by pasting the following line into the command line editor:

	install.packages('ggplot2')	

You will be asked where you want to download the package from. You can type `74` (for example) and it will use that location to download packages in the future. Install `sp` and `maptools` also using the same command. For example:

	install.packages('sp')	
	# do the same for 'maptools'
	
Please check that you can open `QGIS` also. When installing, there is no need to choose the sample datasets provided. As the class time is short, we will start on Tuesday assuming that you have downloaded these programs and installed these packages.

### ggplot2

[ggplot2](http://had.co.nz/ggplot2/) is a visualization and analysis package for R. We are going to use it to illustrate how multiple dimensions of measurement can be shown on a plot, and to illustrate how data can be grouped. Both of these features are very useful for identifying patterns when examining data from cities.

### sp / Maptools

These packages enable plotting of spatial data directly in `R`. Depending on how much time we have in class we may not use them but I will include instructions about their use at the end of the notes.


### Useful references:

* [QGIS Manual](http://qgis.org/en/documentation/manuals.html)
* [Quick-R](http://www.statmethods.net/ ) 
* [StackOverflow](http://stackoverflow.com/questions/tagged/r)
