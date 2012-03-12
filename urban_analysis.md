
# Programs to install

We will be using the following software programs during class. The programs are all open-source and cross platform (win/mac/linux).

* R: [http://www.r-project.org/](http://www.r-project.org/)
	* mac: [mac pkg](http://cran.mtu.edu/bin/macosx/R-2.14.2.pkg)
	* windows: [windows exe](http://cran.mtu.edu/bin/windows/base/R-2.14.2-win.exe) 
	* linux: [instructions](http://cran.mtu.edu/)
* RStudio: [http://rstudio.org/](http://rstudio.org/)
	* mac: [mac dmg](http://download1.rstudio.org/RStudio-0.95.262.dmg)
	* windows: [windows exe](http://download1.rstudio.org/RStudio-0.95.262.exe) 
	* linux: [packages](http://rstudio.org/download/desktop) 
* QGIS: [http://www.qgis.org/](http://www.qgis.org/)
	* 	mac: [gdal](http://www.kyngchaos.com/files/software/frameworks/GDAL_Complete-1.9.dmg) + [qgis dmg](http://www.kyngchaos.com/files/software/qgis/Qgis-1.7.4-4.dmg) 
	* 	windows: [qgis exe](http://www.qgis.org/downloads/QGIS-OSGeo4W-1.7.4-d211b16-Setup.exe)
	* 	linux: [instructions](http://hub.qgis.org/projects/quantum-gis/wiki/Download#Linux)

Install `R` first, then install `RStudio`. After you install `R` try downloading and installing a package by pasting the following line into the command line editor:

	install.packages('ggplot2')	

You will be asked where you want to download the package from. You can type `74` (for example) and it will use that location to download packages in the future. Install `sp`, `maptools` and `googleVis` using the same command. For example:

	install.packages('sp')	
	# do the same for 'maptools'
	
Please check that you can open `QGIS` also. When installing `QGIS`, there is no need to choose the sample datasets provided. If you are using a Mac, you need to install GDAL first, and then QGIS. 

As the class time is short, we will start on Tuesday assuming that you have downloaded and installed these packages and programs.

### ggplot2

[ggplot2](http://had.co.nz/ggplot2/) is a visualization and analysis package for R. We are going to use it to illustrate how multiple dimensions of measurement can be shown on a plot, and to illustrate how data can be grouped. Both of these features are very useful for identifying patterns when examining data from cities.

### sp / maptools / googleVis

These packages enable plotting of spatial data directly in `R`. Depending on how much time we have in class we may not discuss them in class but I will include instructions about their use in the notes.


### Useful references:

* [QGIS Manual](http://qgis.org/en/documentation/manuals.html)
* [Quick-R](http://www.statmethods.net/ ) 
* [StackOverflow](http://stackoverflow.com/questions/tagged/r)


	









