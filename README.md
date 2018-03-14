## Introduction

This assignment uses data from
the <a href="http://archive.ics.uci.edu/ml/">UC Irvine Machine
Learning Repository</a>, a popular repository for machine learning
datasets. In particular, we will be using the "Individual household
electric power consumption Data Set" which I have made available on
the course web site:


* <b>Dataset</b>: <a href="https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip">Electric power consumption</a> [20Mb]

* <b>Description</b>: Measurements of electric power consumption in
one household with a one-minute sampling rate over a period of almost
4 years. Different electrical quantities and some sub-metering values
are available.


The following descriptions of the 9 variables in the dataset are taken
from
the <a href="https://archive.ics.uci.edu/ml/datasets/Individual+household+electric+power+consumption">UCI
web site</a>:

<ol>
<li><b>Date</b>: Date in format dd/mm/yyyy </li>
<li><b>Time</b>: time in format hh:mm:ss </li>
<li><b>Global_active_power</b>: household global minute-averaged active power (in kilowatt) </li>
<li><b>Global_reactive_power</b>: household global minute-averaged reactive power (in kilowatt) </li>
<li><b>Voltage</b>: minute-averaged voltage (in volt) </li>
<li><b>Global_intensity</b>: household global minute-averaged current intensity (in ampere) </li>
<li><b>Sub_metering_1</b>: energy sub-metering No. 1 (in watt-hour of active energy). It corresponds to the kitchen, containing mainly a dishwasher, an oven and a microwave (hot plates are not electric but gas powered). </li>
<li><b>Sub_metering_2</b>: energy sub-metering No. 2 (in watt-hour of active energy). It corresponds to the laundry room, containing a washing-machine, a tumble-drier, a refrigerator and a light. </li>
<li><b>Sub_metering_3</b>: energy sub-metering No. 3 (in watt-hour of active energy). It corresponds to an electric water-heater and an air-conditioner.</li>
</ol>

## Loading the data





When loading the dataset into R, please consider the following:

* The dataset has 2,075,259 rows and 9 columns. First
calculate a rough estimate of how much memory the dataset will require
in memory before reading into R. Make sure your computer has enough
memory (most modern computers should be fine).

* We will only be using data from the dates 2007-02-01 and
2007-02-02. One alternative is to read the data from just those dates
rather than reading in the entire dataset and subsetting to those
dates.

* You may find it useful to convert the Date and Time variables to
Date/Time classes in R using the `strptime()` and `as.Date()`
functions.

* Note that in this dataset missing values are coded as `?`.




## Making Plots

Our overall goal here is simply to examine how household energy usage
varies over a 2-day period in February, 2007. Your task is to
reconstruct the following plots below, all of which were constructed
using the base plotting system.

First you will need to fork and clone the following GitHub repository:
[https://github.com/rdpeng/ExData_Plotting1](https://github.com/rdpeng/ExData_Plotting1)


For each plot you should

* Construct the plot and save it to a PNG file with a width of 480
pixels and a height of 480 pixels.

* Name each of the plot files as `plot1.png`, `plot2.png`, etc.

* Create a separate R code file (`plot1.R`, `plot2.R`, etc.) that
constructs the corresponding plot, i.e. code in `plot1.R` constructs
the `plot1.png` plot. Your code file **should include code for reading
the data** so that the plot can be fully reproduced. You should also
include the code that creates the PNG file.

* Add the PNG file and R code file to your git repository

When you are finished with the assignment, push your git repository to
GitHub so that the GitHub version of your repository is up to
date. There should be four PNG files and four R code files.


The four plots that you will need to construct are shown below. 


### Plot 1

> fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
> colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
>library(dplyr)
>subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]
>p<-as.character(subSet$Global_active_power)
> p<-as.numeric(p)
> hist(p,main = "Global Active Power",xlab="Global Active Power(Kilowatts)")
>dev.copy(png,file="plot1.png",height=480,width=480)
> dev.off()


![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 


### Plot 2

> fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
> colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
>library(dplyr)
>subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]

>subSet$date <- as.Date(subSet$date, format="%d %m %Y")
>subSet$time <- strptime(subSet$time, format="%H:%M:%S")
>subSet[1:1440,"time"] <- format(subSet[1:1440,"time"],"2007-02-01 %H:%M:%S")
>subSet[1441:2880,"time"] <- format(subSet[1441:2880,"time"],"2007-02-02 %H:%M:%S")

>#Use Basic plot function
>plot(subSet$time,as.numeric(as.character(subSet$global_active_power)),xlab="",ylab="Global Active Power",type="l")

>#Step.3:Saving the plot in a PNG File

>dev.copy(png,file="plot1.png",width=480,height=480)
>dev.off() 

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


### Plot 3
> fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
> colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
>library(dplyr)
>subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]

>dateTime <- strptime(paste(subSet$Date, subSet$Time, sep=" "), "%d/%m/%Y %H:%M:%S")
>plot(dateTime,as.numeric(as.character(subSet$Sub_metering1)),ylab="Energy sub metering",xlab="",type="l",col="black")
>lines(dateTime,as.numeric(as.character(subSet$Sub_metering2)),type="l",col="red")
>lines(dateTime,as.numeric(as.character(subSet$Sub_metering3)),col="blue",type="l")
>legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty=1, lwd=2.5, col=c("black", "red", "blue"))
>png("plot3.png",width=480,height = 480)
>dev.off()


![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 


### Plot 4

> fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
> colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
>library(dplyr)
>subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]

>dateTime <- strptime(paste(subSet$Date, subSet$Time, sep=" "), "%d/%m/%Y %H:%M:%S")
par(mfrow=c(2,2))
>q<-as.numeric(as.character(subSet$Global_active_power))
> plot(dateTime,q,type="l",ylab="Global Active Power",xlab = "")
>q<-as.numeric(as.character(subSet$Global_active_power))
>plot(dateTime,q,type="l",ylab="Global Active Power",xlab = "")
>plot(dateTime,as.numeric(as.character(subSet$Voltage)),ylab="Voltage",xlab = "datetime",type = "l")
>plot(dateTime,as.numeric(as.character(subSet$Sub_metering1)),ylab="Energy sub metering",xlab="",type="l",col="black")
>lines(dateTime,as.numeric(as.character(subSet$Sub_metering2)),type="l",col="red")
>lines(dateTime,as.numeric(as.character(subSet$Sub_metering3)),col="blue",type="l")
>legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty=1, lwd=2.5, col=c("black", "red", "blue"))
>plot(dateTime,as.numeric(as.character(subSet$Global_reactive_power)),xlab = "datetime",ylab = "Global_reactive_power",type = "l")
>png("plot4.png",width=480,height = 480)
>dev.off()




![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 

