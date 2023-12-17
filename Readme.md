cmd-lets
--Get-Service
--Verb-Noun

## Getting help from online

-> get-help get-service -online
-> get-verb

get-help get-service -showwindow

# Objects Properties

to get the properties and methods for a particaular command
->gm get-member

->$pshome
->is the path of the powershell home

-Get-Process -name notepad | gm

->$fruits = @("mango","banana","stawberry")
 $fruits | where {$\_ -eq "Mango"}

##create the file with date
$firstName = "Gopi";
$lastName = "Katari";

# $shortDate = Get-Date -Format "dd_mmm_yyyy_HH_mm_s";

$shortDate = Get-Date -Format "dd_mmm_yyyy";
$longDate = Get-Date -Format "F";
$test = "**\*\***\***\*\***some test mesage changes asd fsdafasdfdasd";

$content = "FirstName  =  $firstName
LastName   = $lastName + '_'
Date = $longDate
"+$test

Set-Content -Path "D:\$shortDate$firstName$lastName.txt" -Value $content

##----------------------
Write-Output 'FOR LOOP';

for($i=0;$i -lt 10; $i++){
 Write-Output "Looping times" ($i+1)
}
##----------------------

$cars = @('vw','honda','hyundai','maruti');

$choice = "HYUNDAI"

switch ($choice.ToLower()) {
"vw" {
echo("you have selected"+ $choice)
}
"hyundai" {
echo("you have selected hyundai"+ $choice)
}
"Ford" {
echo("you have selected Ford"+ $choice)
}
Default {
echo("Executing the default")
}
}
##-------------Functions---------

Function MyFunctionName {
//function body
}

## function with parameters

Function TestFunction{
//accepting argument using $args
}

function testFunc {
param($one,$two)

echo ("one =>"+ $one);
echo ("two =>"+ $two);
}

testFunc -two "two" -one "first"

## ------------Functions end---------

ipconfig /displaydns
route print
netstat -ano

## get the installeed apps

Get-ItemProperty HKLM:\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName,DisplayVersion, Publisher, InstallDate | Format-Table

## Process Retriver

Get-Process | Where {$_.ProcessName -eq "chrome" -AND $_.CPU -gt 40 } | sort CPU -Descending

## stop Retriver

Stop-Process -id 1368 -PassThru

# list the trusted hosts

Get-Item WSMan:\localhost\Client\TrustedHosts -Force

# Starting the remote session challenge

$passwd = convertto-securestring -AsPlainText -Force -String <your password>

$cred = new-object -typename System.Management.Automation.PSCredential 
-argumentlist "Domain\User",$passwd

$session = new-pssession -computername <computer> -credential $cred
Enter-PSSession -ComputerName cname -Credential domain/user

# Copu files from and to from remote machine

$session = New-PSSession -ComputerName CNAME -Credential (Get-Credential);
//copy file from local computer to remot machine
Copy-Item -Path SOURCEPATH -Destination DESTINATIONPATH -ToSession $session

//copy file from remote computer to local machine
Copy-Item -Path SOURCEPATH -Destination DESTINATIONPATH -FromSession $session

Remove-PSSession $session

# who rebooted the server

$credential = Get-Credentaial
Get-WinEvent -ComputerName Gopi -Credential $credential -FilterHashtable @{logname = 'System'; id=1074} | Format-Table -wrap

Get-WinEvent -ComputerName Gopi -FilterHashtable @{logname = 'System'; id=1074} | Sort-Object TimeCreated | Select-Object -Last 1 | Format-Table -wrap

Get-Volume
Get-WmiObject -Class win32_LogicalDisk | select-object DeviceID,Size,FreeSpace
