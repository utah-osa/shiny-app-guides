# My app is Slow - Help!
Hello, you are here because your app is slow. Bummer! This will walk you through a heuristic process on how to find the bottle necks and resolve them. 

Ready?

## Q1: What type of "slowness"?
What do you mean by "slow"? 
- I dont know!
- The app takes a long time to start. 
- The app's features such as plots, tables, and calculations lead to a slow user experience

### I don't know! 
Try profiling your app using profvis, or by using smartly placing "Sys.time" calls. You can also try commenting out all your Outputs and adding them back in one at a time until you find the slow Output(s). This will help you narrow down where the bottleneck is at. You can also do a simple check to see how long any associated data takes to load. For example, if you app takes 30 seconds to load, and you try loading the CSV file outside the app and the CSV read takes 25 seconds, then it is easy to see that the CSV reading is where the bottle neck is occuring. 

### My app takes a long time to start
This is usually due to the dataset(s) you are using taking a long time to load and get transformed before you serve the app. 

Recommendations: 
1. Using a new R script, see if you can load your data and apply any transformations before the app starts and then save that table/dataframe as an RDS. In the app.R you will read the RDS instead of the csv/txt file that contains the data.
2. Use data.table or vroom for reading large files. 
3. Use C++ wrapper functions where possible. Many tidyverse functions have nice syntax, but are slower than the packages they are built from. For example, instead of doing regex manipulation and detection with "stringr" use "stringi" instead. 
4. Check if you can remove unused columns from your dataframe.
5. Change packages if you are using a package/framework that requires full app rendering instead of lazy-loading. For example, Flexdashboard has to render the entire document which is wasteful for multi page apps. 

### The app's features such as plots, tables, and calculations lead to a slow user experience 
1. Try switching to faster packages/functions. If you are using tidyverse stuff, try "dtplyr" which is a wrapper for data.table. Switch to data.table entirely if you can. Use C++ wrapper functions where possible. Many tidyverse functions have nice syntax, but are slower than the packages they are built from. For example, instead of doing regex manipulation and detection with "stringr" use "stringi" instead. Finally, look for spots where you can apply "vectorized" functions using the "purrr" package or base apply functions. R's for loops are much faster than they were 5 years ago, but the functional programming tools are still a bit faster and have the benefit of improved readability. 
2. Add "reactive" datasets in the server for shared/similar filters and transformations. [https://shiny.posit.co/r/getstarted/shiny-basics/lesson6/](https://shiny.posit.co/r/getstarted/shiny-basics/lesson6/). This is especially helpful when the same "filter" options are applied to a common dataset.
3. 

## Q2: Is the slowness related to the machine specs? 
If an app is pretty fast on your local development environment, but possible in production it is likely due to the machine ram and gpu difference. If you suspect this is the issue increase the cloud run or compute engine ram and gpu and redeploy. 

## Q3: Is the slowness is due to a long database query?
If you have identified the bottleneck being slow due to query retreival, this is a challenging issue to resolve. First, see if you can expand the WHERE clause to reduce the number of rows or modify the number of columns selected to only contain essential fields. Next, if using BigQuery see if any easy partitions work. For example, a unique entity id or fiscal year are often great partitions that can quickly shrink the queries domain.  

