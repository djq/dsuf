### Overview of class

#### Part 1: R
* Basics: loading data, installing packages, 
* Exploring data, multiple dimensions
* Loading data from spatial sources

#### Part 2: QGIS
* Basics: loading data, installing plugins
* Simple calculations, spatial analysis
* Basic "WalkScore" type calculation

#### Part 3: If there is time...
* `sp` and `maptools`: plot quick maps
* `googleVis` 

### Data
The datasets we will use are available on Stellar [here](http://stellar.mit.edu/S/course/4/sp12/4.474/materials.html). Make a folder for this class and unzip them into that folder.

* Millenium Cities Data
* Cambridge MA Data from [OpenstreetMap](http://www.openstreetmap.org/)
* New York Building + Energy Data

(For the first example (Millenium Cities Data) you can access the data from the website; for the other examples you need to download the data.)

### Introduction to R

This is a comment:

	# this line is ignored
	
First, we are going to check that you all could install a package:

	install.packages('ggplot2')	

Loading data into a dataframe:

	# a dataframe is similar to an excel-spreadsheet
	# 'dataSample' is a variable; you can use any name here
	dataSample <- read.csv('pathToFile/file.csv')  # this assumes a csv file with headers
	
Load in the Millenium Cities Data:

	# read in data
	mil_city <- read.csv('http://stellar.mit.edu/S/course/4/sp12/4.474/courseMaterial/topics/topic5/resource/mil_city_small/mil_city_small.csv')
	# here we are reading the data directly from a URL!
	
To see the top part of your data use the `head` command:

	head(mil_city)
	
To see a summary of your data:
	
	summary(mil_city)
	
To access a column use the $ notation:

	mil_city$Urban_density		


### ggplot2

[ggplot2](http://had.co.nz/ggplot2/) is a visualization and analysis package for R. We are going to focus on using some of the plotting functions, and illustrate facet-plotting. First load the library into your workspace:

	library(ggplot2)	
	
On the ggplot2 website you can see many different types of plots. The most basic is the `qplot()` function; the more complicated plotting function is `ggplot()`. First try using `qplot` to examine some of the `mil_city` data.

	# first we will plot urban density against road length
	qplot(data=mil_city, x=Urban_density, y=Length_of_road_per_1000_people

	
You can make the same plot using `ggplot`. There are more ways of customizing things using `ggplot`

	ggplot(data = mil_city, aes(x = Urban_density, y = Length_of_road_per_1000_people)) + geom_point() 	
	
Now add a third dimension. We will group the data by color (colour!):

	ggplot(data = mil_city, aes(x = Urban_density, y = Length_of_road_per_1000_people)) + geom_point(aes(colour= Group))
	

Adding a 4th dimension, we can make the point size proportional to the average car trip:

	ggplot(data = mil_city, aes(x = Urban_density, y = Length_of_road_per_1000_people)) + geom_point(aes(colour= Group, size=Average_time_of_a_car_trip))
	
Here we used `geom_point()` but there are other types of plots such as lines (`geom_line()), area, etc.

	
#### Grouping data using ggplot2

Let's break up the data into 'facets'. This is a powerful method for examining data in subsets

	ggplot(data = mil_city, aes(x = Urban_density, y = Length_of_road_per_1000_people)) + geom_point() + facet_wrap(~Group)


* Try extending these plots by adding the previous dimensions, ilustrated by size or color.
*

### ggplot2 logistics

Labeling your Axes:

	# axes titles: xlab, ylab
	ggplot(data = mil_city, aes(x = Urban_density, y = Length_of_road_per_1000_people)) + geom_point() + xlab('Pop. Dens (People/Hectare)')
	# try adding ylab()
	
	# max/min - use + xlim(0,1000) + ylim(0,1000) (for example)
	
Saving your plot:
	plot1 <- ggplot(data = mil_city, aes(x = Urban_density, y = 	Length_of_road_per_1000_people)) + geom_point() + xlab('Pop. Dens (People/	Hectare)')
	
	ggsave() # puts in your working directory (see below, for exaplanation of working directory)
  
	ggsave(plot1, file="millenium_cities.pdf", width=4, height=4)
	
	
#### R is a language for statistical analysis:
You can perform all types of standard analysis:
* Try calculating the mean and standard deviation of all columns
* Calculate the max value in `Urban_density`
	

### Reading information from a shapefile

We are going to focus on exploring non-spatial patterns from spatial data.

First, set your working directory:
	
	# A shortcut of referring to the folder you are working in. e.g.
	setwd('/Users/djq/Dropbox/4.474/')

To read in a `dbf` file you can use the following command:
	
	library(foreign) 		# load a library that is installed by default in R
	setwd('/Users/djq/Dropbox/dusp_viz')		# set your working directory
	attributeTable <- read.dbf('pathToShapefile/shapefileName.dbf') # note this is to the '.dbf' part of the shapefile. We are ignoring the spatial information

The first shapefile we are using here is a sample of tax-assessors parcels from New York. Open it in QGIS to examine it, then read in the attribute table:

	mn <- read.dbf('data/manhattan/mn_small.dbf')
	
Trying plotting some values from this table (If you would like more examples using this specific dataset you can follow instrauctions from an IAP class.)
	

###	Joining more data to a dataframe

Load a dataframe of zipfiles for New York:

	elec <- read.csv('data/NY_Zip_energy.csv')

Now let's join this to tax-data, joining by zipcode keyword. I have aggregated the values from an NYC dataset, available [here](http://nycopendata.socrata.com/Environmental-Sustainability/Electric-Consumption-by-ZIP-Code-2010/74cu-ncm4). (Note: Spatial joins are possible in `R` but are not covering them in this workshop.)
		
Examine `elec` dataframe. Merge using `ZipCode` (note that spelling is identical in both dataframes):

	ny_data <- merge(mn, elec, 'ZipCode')
	
Try making a facet-plot by zipcode illustrating energy use.	
	
## sp

`sp` is another package in R that can be used for many spatial analyses. Here we are just using it to plot a shapefile.

	library(sp)
	
We are not focusing on beautiful cartography with this package. We just want to make quick plots of the data that are understandable. You can find some useful spplot references [here](http://r-spatial.sourceforge.net/gallery/)

Load in the NY zipcode shapefile and the following libraries:
	
	library(sp)
	library(maptools) 
	
Now, load the spatial piece of `NY_Zip_Energy` (the `.shp`):
	
	demo <- readShapePoly('data/ny_zip/NY_Zip_Energy.shp') 
	
And also load the attribute table for easy perusal:

	att <- read.dbf('data/ny_zip/NY_Zip_Energy.dbf') 
	
You can make a plot using the following commands:
	  
	spplot(demo, "kWh_res") # residential
	spplot(demo, "kWh_com") # commercial
	spplot(demo, "kWh_res", scales=list(draw = F), colorkey=F) # remove scales and key/legend
	
To save the plot (as a pdf, for example):

	ny_res_energy <- spplot(demo, "kWh_res") # store the plot	
	  
	pdf('ny_res_energy.pdf',height=5,width=5) # set up pdf
	print(ny_res_energy)    # print
	dev.off()               # close the PDF file
	
Fine tuning:
	
	spplot(demo, c("kWh_res","kWh_com")) # colour scale is a bit hard to read as one map has much larger values than the other
	
	spplot(demo, c("kWh_res","kWh_com"), names.attr = c("Residential","Commercial")) # change names
	
	spplot(demo, c("kWh_res","kWh_com"), col.regions = rainbow(100, start = 4/6, end = 1)) # tweaking colours

Scale-bars and further refinement are not very easy to include. My preference is to use another program for organizing these  details using another program. However, there are a few approaches you can use for adjusting the colors:

	library(classInt)
	library(RColorBrewer)
	pal = brewer.pal(7,"Greens")
	
	# demo = readOGR("data/ny_zip/", "NY_Zip_Energy") # alternative method of reading in data
	
	brks.qt = classIntervals(demo$kWh_res, n = 7, style = "quantile")
	brks.jk = classIntervals(demo$kWh_res, n = 7, style = "jenks")
	brks.eq = classIntervals(demo$kWh_res, n = 7, style = "equal")
	
	# Example of one of the map plots
	spplot(demo, "kWh_res", at=brks.eq$brks, col.regions=pal, col="transparent", main = list(label="Equal breaks"))

This example slighlty modified from [here](http://gis.stackexchange.com/questions/3310/what-is-the-most-useful-spatial-r-trick)

#### Try:

* Changing interval type of breaks
* Plotting the tax lots for one ZipCode, by one dimension
* Making a grid of plots, using several measurements

	




	









