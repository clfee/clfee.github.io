---
title:  "Serverless Dashboard with R and {crosstalk}"
date:   2021-05-28

categories: R Dashboard
header:
    teaser: "/pics/clee.jpg"

toc: false
toc_label: "overview"
excerpt: "Building a Serverless Dashboard with R"
---
Email is the most accessible form of online communication; it helps to capture and retain audience attention. In fact, email marketing outperforms other online marketing strategies, including SEO (organic search), PPC (paid search), and content marketing.  Several strategies have been developed for better marketing campaigns, such as personalize email messages, target audience by segmentation (ex: past purchase/browse histories, area …, etc.) 

Trackig the performance of the emails will help to build deeper understanding of audience behavior and find new ways to grow revenue. Traditional analytics—list size, opens and clicks—provide a high level snapshot, but they do not provide insights on the underlying drivers behind those metrics. A dashboard shares your analysis not only makes easy to communicate results but also provide opportunites to identify new metrics.

![Overview](/pics/dashboard/overview1.JPG)  

This dashboard is a simple static html file created using R. [Demo](/pics/dashboard/data_explore.html) It contains simple graphs and filters without the need for a Shiny server. The shortcoming of that it requires to precompute most of the variables as not much computation is possible. However, it makes deployment much easier.  

{flexdashboard} is the framework allowing us to build a dashboard. Once data is loaded, use {htmlwidgets} to covert the data to a SharedData object. The interaction between sidebar filters and tables/graphs was made possible by using {crosstalk}. 

```yml
library(flexdashboard) 
library(crosstalk)
llibrary(plotly)
library(leaflet)
library(htmltools)

# Convert dataframe to ShareData Object
df <- read_csv("data.csv")
sd1 <- SharedData$new(df)

# Create interactive plot 
ggplotly(sd1 %>% 
           ggplot(aes(Purchase_history), fill = click)) + 
           geom_bar(bins=8, position = "dodge")+ 
           xlab("Past Purchase") +
           theme_minimal())
```





---