![](RackMultipart20200907-4-12s3sf2_html_b73384b8cad90393.jpg)

# **Technical Academy Workshop**
![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png) 

# **HANA Cloud Services – Data Loading**

- **Release Date: September 06, 2020**

# Table of Contents

**[1.](#_Toc50328717)****DATA Loading INTRODUCTION 3**

**[2.](#_Toc50328718)****APPENDIX 13**

1.
# DATA Loading INTRODUCTION

At the conclusion of this exercise, you will be introduced to:

• Data Loading in SAP HANA Cloud Relational Data Lake

_ **Hands-on Lab – Data Loading** _

The purpose of the hands on exercises is to give you an opportunity to load data in relational data lake in SAP HANA Cloud. The exercises will guide you on loading data from Azure blob storage into the relational data lake and then create a virtual table to access the data in HANA Cloud

**Loading data with Relational Data Lake**

Expected time – 10 minutes

| **Steps**
 | **Screen shots**
 |
| --- | --- |
|
| |
|
- Your Instructor will provide connection and environment information. Our labs are being run on HAHA Cloud.
 | ![](RackMultipart20200907-4-12s3sf2_html_898bb32e71c0ef35.png) |
| --- | --- |
|
| |
|
- Launch Google Chrome browser
- Navigate to the URL provided by the instructor and use the informed credentials to login on SAP HANA Database Explorer

 | ![](RackMultipart20200907-4-12s3sf2_html_dbffd825beee74b.png) |
|
| |
|
- Once the SAP HANA Database Explorer starts, you can add your database by clicking + sign
 | ![](RackMultipart20200907-4-12s3sf2_html_e20a85892d4faeb9.png) |
|
| |
|
- Provide database details

Database Type: SAP HANA Database
Host: d1c353c3-ea74-4e9a-bda5-897d70fd7376.hana.prod-us10.hanacloud.ondemand.com
Port Number: 443
User: will be providedPassword: Welcome01
Check: Save PasswordCheck: Connect tot he database using SSLUncheck: Verify certificate
Name to Show in Display: Optional | ![](RackMultipart20200907-4-12s3sf2_html_b60b732a3099df2e.png) |
|
| |
|
- We have a csv file WEATHER\_SENSOR\_DATA\_DAILY.csv loacated in AZURE blob storage as shown in the screenshot.
- You do not need to log into the AZURE portal, as you will be provided with the path and credentials to load this file into your relational data lake.
 | ![](RackMultipart20200907-4-12s3sf2_html_9e52e31b4eddc19f.gif) |
|
| |
|
- Click on ![](RackMultipart20200907-4-12s3sf2_html_9bd597b7b808c44e.gif)icon **(1)** to open a **SQL console** window
- Use the below sql to create a table in the relational data lake

**CALL SYSRDL#CG.REMOTE\_EXECUTE(&#39;****BEGIN ****CREATE TABLE**  **\&lt;yourInumber\&gt;**** \_WEATHER\_SENSOR\_DATA\_DAILY****(STATION\_ID VARCHAR(100) ,** **PRECIPITATION DECIMAL(5,2) ,** **SOLAR\_RADIATION DECIMAL(7,2) ,** **VAPOR\_PRESSURE DECIMAL(7,2) ,** **AIR\_TEMPERATURE DECIMAL(5,2) ,** **RELATIVE\_HUMIDITY DECIMAL(5,2) ,** **DEW\_POINT DECIMAL(5,2) ,** **WIND\_SPEED DECIMAL(5,2) ,** **SOIL\_TEMPERATURE DECIMAL(5,2) ,** **DATETIME\_DATE DATE)****END&#39;);**
Note: Replace the phrase **\&lt;yourInumber\&gt;** with your actual I number in the above command | ![](RackMultipart20200907-4-12s3sf2_html_8a3f0858128c05ac.gif) |
|
| |
|
- Expand the **Catalog (1)**
- Navigate to **Remote Sources (2)**
- Choose **SYSRDL#CG\_SOURCE (3)** to access the relational data lake remote source
- Select the SYSRDL#CG from the **Schema (4)** drop down
- Type the name of the table in the **Object (5)** field that you created in the previous step.
- Click on **Search (6)** to search for the table.
- Once the table is displayed, select the **checkbox (7)**
- Click on **Create Virtual**** Table (8)**
 | ![](RackMultipart20200907-4-12s3sf2_html_b8f084ff715c105a.gif) |
|
| |
|
- Provide the name of the virtual table and select your schema
- Then click on create to create the virtual table.
 | ![](RackMultipart20200907-4-12s3sf2_html_90a0e2eb13ca1434.png) |
|
| |
|
- Click on **Tables**
- The virtual **table** will be visible in the bottom pane.

 | ![](RackMultipart20200907-4-12s3sf2_html_a166f4ea7c203971.gif) |
|
| |
|
- Go back to SQL console and use the below SQL to load the data lake table from the csv file loacated in AZURE blob storage

**CALL SYSRDL#CG.REMOTE\_EXECUTE(&#39;****BEGIN ****LOAD TABLE**  **\&lt;YourInumber\&gt;\_**** WEATHER\_SENSOR\_DATA\_DAILY ( **** STATION\_ID, **** PRECIPITATION, **** SOLAR\_RADIATION, **** VAPOR\_PRESSURE, **** AIR\_TEMPERATURE, **** RELATIVE\_HUMIDITY, **** DEW\_POINT, **** WIND\_SPEED, **** SOIL\_TEMPERATURE, **** DATETIME\_DATE) ****USING FILE &#39;&#39;BB://hscsgcontainter/WEATHER\_SENSOR\_DATA\_DAILY.csv&#39;&#39;**** delimited by &#39;&#39;,&#39;&#39; ****Row Delimited by &#39;&#39;##&#39;&#39;**** FORMAT CSV ****ESCAPES OFF**** CONNECTION\_STRING &#39;&#39;DefaultEndpointsProtocol=https;AccountName=hscsgstorage;AccountKey=+qapVjkWrv4gR5CYGHlBR1EKgIgXh8OKec1CFPQtvGQeFa/7fVKtfg3oS9SpItnPFMzkjxONKUWVblZraRMzGA==;EndpointSuffix=core.windows.net&#39;&#39; ****QUOTES ON;**** END&#39;);**
Note1: Replace the phrase **\&lt;yourInumber\&gt;** with your actual I number in the above command Note2: The above command **two single quotes enclosing** File name, row and column delimiter and connection\_string. |

 ![](RackMultipart20200907-4-12s3sf2_html_56df0f676bdab0e8.png) |
|
| |
|
- Navigate to the virtual table ,right click and choose Open Data

 | ![](RackMultipart20200907-4-12s3sf2_html_80451284b465d42b.gif) |
|
| |
|
- The data can now be previewed.
 | ![](RackMultipart20200907-4-12s3sf2_html_bc31ca0a21ca1b72.png) |
|
| |
|
- Switch to Analysis
- Add Datetime\_date to Axis
- Add AIR\_TEMPERATURE to Value
- Add Station\_ID = 253 to filter
- Switch to Line Chart
 | ![](RackMultipart20200907-4-12s3sf2_html_b7ee4509d72b9204.png) |
|
| |
|
- Click Schemas
- Click Choose Schema
 | ![](RackMultipart20200907-4-12s3sf2_html_c2a522168315f147.gif) |
|
| |
|
- Select SOURCEDATA schema
 | ![](RackMultipart20200907-4-12s3sf2_html_336e65ad69964fb1.gif) |
|
| |
|
- Click Tables
- The tables in SOURCEDATA schema should appear
 | ![](RackMultipart20200907-4-12s3sf2_html_991f77457d3bd2ca.png) |

1.
# APPENDIX

SQL statements used in the exercise :

CALL SYSRDL#CG.REMOTE\_EXECUTE(&#39;

BEGIN

  CREATE  TABLE \&lt;yourInumber\&gt;\_WEATHER\_SENSOR\_DATA\_DAILY

        (STATION\_ID VARCHAR(100) ,

PRECIPITATION DECIMAL(5,2) ,

SOLAR\_RADIATION DECIMAL(7,2) ,

VAPOR\_PRESSURE DECIMAL(7,2) ,

AIR\_TEMPERATURE DECIMAL(5,2) ,

RELATIVE\_HUMIDITY DECIMAL(5,2) ,

DEW\_POINT DECIMAL(5,2) ,

WIND\_SPEED DECIMAL(5,2) ,

SOIL\_TEMPERATURE DECIMAL(5,2) ,

DATETIME\_DATE DATE)

        END&#39;);

CALL SYSRDL#CG.REMOTE\_EXECUTE(&#39;

BEGIN

LOAD TABLE \&lt;yourInumber\&gt;\_WEATHER\_SENSOR\_DATA\_DAILY (

STATION\_ID,

PRECIPITATION,

SOLAR\_RADIATION,

VAPOR\_PRESSURE,

AIR\_TEMPERATURE,

RELATIVE\_HUMIDITY,

DEW\_POINT,

WIND\_SPEED,

SOIL\_TEMPERATURE,

DATETIME\_DATE)

USING FILE &#39;&#39;BB://hscsgcontainter/WEATHER\_SENSOR\_DATA\_DAILY.csv&#39;&#39;

delimited by &#39;&#39;,&#39;&#39;

Row Delimited by &#39;&#39;##&#39;&#39;

FORMAT CSV

ESCAPES OFF

CONNECTION\_STRING &#39;&#39;DefaultEndpointsProtocol=https;AccountName=hscsgstorage;AccountKey=+qapVjkWrv4gR5CYGHlBR1EKgIgXh8OKec1CFPQtvGQeFa/7fVKtfg3oS9SpItnPFMzkjxONKUWVblZraRMzGA==;EndpointSuffix=core.windows.net&#39;&#39;

QUOTES ON;

END&#39;);

![](RackMultipart20200907-4-12s3sf2_html_1345245233c98274.png)

![](RackMultipart20200907-4-12s3sf2_html_ceeaca08e3813045.png)
