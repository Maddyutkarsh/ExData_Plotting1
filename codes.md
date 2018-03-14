### Plot 1

fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
library(dplyr)
subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]
p<-as.character(subSet$Global_active_power)
p<-as.numeric(p)
hist(p,main = "Global Active Power",xlab="Global Active Power(Kilowatts)",col="red")
dev.copy(png,file="plot1.png",height=480,width=480)
dev.off()




### Plot 2

fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
library(dplyr)
subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]

dateTime <- strptime(paste(subSet$Date, subSet$Time, sep=" "), "%d/%m/%Y %H:%M:%S")
q<-as.numeric(as.character(subSet$Global_active_power))
plot(dateTime,q,type="l",ylab="Global Active Power",xlab = "")
dev.copy(png,file="plot2.png",width=480,height=480)
dev.off() 



### Plot 3
fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
library(dplyr)
subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]

dateTime <- strptime(paste(subSet$Date, subSet$Time, sep=" "), "%d/%m/%Y %H:%M:%S")
plot(dateTime,as.numeric(as.character(subSet$Sub_metering1)),ylab="Energy sub metering",xlab="",type="l",col="black")
lines(dateTime,as.numeric(as.character(subSet$Sub_metering2)),type="l",col="red")
lines(dateTime,as.numeric(as.character(subSet$Sub_metering3)),col="blue",type="l")
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty=1, lwd=2.5, col=c("black", "red", "blue"),cex = 0.6)
png("plot3.png",width=480,height = 480)
dev.off()




### Plot 4

fd<-read.table("household_power_consumption.txt",sep=";",skip = 1)
colnames(fd)<-c("Date","Time","Global_active_power","Global_reactive_power","Voltage","Global_intensity","Sub_metering1","Sub_metering2","Sub_metering3")
library(dplyr)
subSet <- fd[fd$Date %in% c("1/2/2007","2/2/2007") ,]

dateTime <- strptime(paste(subSet$Date, subSet$Time, sep=" "), "%d/%m/%Y %H:%M:%S")
par(mfrow=c(2,2))
q<-as.numeric(as.character(subSet$Global_active_power))
plot(dateTime,q,type="l",ylab="Global Active Power",xlab = "")
plot(dateTime,as.numeric(as.character(subSet$Voltage)),ylab="Voltage",xlab = "datetime",type = "l")
plot(dateTime,as.numeric(as.character(subSet$Sub_metering1)),ylab="Energy sub metering",xlab="",type="l",col="black")
lines(dateTime,as.numeric(as.character(subSet$Sub_metering2)),type="l",col="red")
lines(dateTime,as.numeric(as.character(subSet$Sub_metering3)),col="blue",type="l")
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty=1, lwd=2.5, col=c("black", "red", "blue"),cex = 0.2)
plot(dateTime,as.numeric(as.character(subSet$Global_reactive_power)),xlab = "datetime",ylab = "Global_reactive_power",type = "l")
png("plot4.png",height=480,width=480)
dev.off()

