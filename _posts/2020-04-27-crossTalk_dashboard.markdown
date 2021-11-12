---
title:  "Serverless Dashboard with R using {Flexdashboard}"
date:   2021-05-28

categories: R Dashboard
header:
    teaser: "/pics/clee.jpg"

toc: false
toc_label: "overview"
excerpt: "Building a Serverless Dashboard with R"
---
Imagine as a marketing manager you need to discuss about the impact of COVID-19 alert levels on product sales with other departments. Would you go through a 25-slide deck to a 5-minute meeting? Would you project multiple Excel workbooks to convince your colleagues what you are showing is not boring at all. Or you will send them a dashboard by email before the meeting to get everyone onboard quicky and focus on the idea you are about to deliver. 
 
Indeed, dashboards are the perfect tool when you want to visualize a lot of complex data and to provide users at-a-glance views of key performance indicators relevant to a particular objective. It is easy to create a dashboard using R. 

![Overview](/pics/dashboard/overview1.JPG)  

This dashboard is a simple static html file created using R. [Demo](/pics/dashboard/data_explore.html) It contains simple graphs and filters without the need for a Shiny server. The shortcoming of that it requires to precompute most of the variables as not much computation is possible. However, it makes deployment much easier.  

{flexdashboard} is the framework allowing us to build a dashboard. Once data is loaded, use {htmlwidgets} to covert the data to a SharedData object. The interaction between sidebar filters and tables/graphs was made possible by using {crosstalk}. 

Steps:
-	Create an R markdown file 
![Step1](/pics/dashboard/s1.PNG
-	New markdown file is shown
![Step2](/pics/dashboard/s2.PNG
-	Click Knit and select knit flexdashboard to view the dashboard
![Step3](/pics/dashboard/s3.PNG

Try it with the code [here](https://github.com/clfee/Shiny-apps) .

```





---