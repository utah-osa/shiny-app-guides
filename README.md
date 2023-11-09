# Checklist
Hello and Congratulations! You are here because you are developing a cool R shiny app. This repository was built to help guide you along the process and get your app deployed as quickly as possible. 

### Local Development Checklist
This is the stage where you are developing the app or perhaps you and another analyst are working together on it. You have not yet shown the app to managers/stakeholders. 

-[ ] The app has an Github repo
-[ ] The repo has a README.md explaining what the app does 
-[ ] The app has a folder called "app" in the root directory of the repo.
-[ ] The app folder has an app.R file
-[ ] Any images, css, or js are in a www folder. 
-[ ] Any required data and helper scripts exist in the app folder. 
-[ ] All charts and widget colors in the app follow the OSA style guide.
-[ ] The R files follow the [Tidyverse style guide](https://style.tidyverse.org/index.html).Variable and function names follow accepted conventions, R scripts have acceptable names, etc. See [lintr](https://github.com/r-lib/lintr)

### Alpha Checklist (for showing the work-in-progress app to John, David, or Stakeholders)
After receiving feedback from Auditor Dougall, David Stringfellow, and other key stakeholders for the office - here are common requirements that your app should follow:

-[ ] Any numeric value that is a currency should display a numeric format of $x,xxx.xx or $x,xxx. This includes all tables, charts, and user input fields. 
-[ ] Any numeric value that is a percentage should display a numeric format of x,xxx.xx% or $x,xxx%. This includes all tables, charts, and user input fields. 
-[ ] Any numeric value that is a year does not have a comma format 
-[ ] Any other numeric field should have a standard comma format of x,xxx. 
-[ ] The app is free of grammar errors and typos
-[ ] If you are sharing via a public url then the app must serve in under 5 seconds. Otherwise, just be smart and make sure the app can run on your local machine before you show it to stakeholders. 
-[ ] All charts/plots and tables have a title

### Beta / First Cloud Deployment Checklist
This is a list of requirements that have to happen to get your app converted into a Dockerized app that can be deployed from one of our various cloud services. Sometimes this will happen before we show Auditor Dougall the app, but usually this is the stage where we publish the app online and allow users to Beta test the app. Most of the time the testing is done internally, but oftentimes we will send this to entity officials or researchers. 

-[ ] The app has an Github repo (hopefully it has already had one)
-[ ] The repo has a Dockerfile
-[ ] The repo has a cloudbuild.yaml
-[ ] The repo has a Rprofile.site
-[ ] The repo has a GCP cloud build trigger set up for pushes from main or dev branch.

### Production Checklist (Final checks before publishing)
These are the final checks before publishing the "production" or "stable" version of the app. It incorporates all the prior checks in addition to the following:

-[ ] The app does not reference any files on the LAN, or cloud. All local files are in the app folder. Any other data is queried via an ODBC or DBI connection.
-[ ] All service accounts related to the app have least privilege access. 
-[ ] The app, if applicable, contains both State of Utah and OSA branding. This includes the header bars, footers, etc. The only reason and time this can be omited is when the app is being embedded in another site that has the branding.
-[ ] The app is served in under 5 seconds, unless there is an accepted reason for taking longer. 
-[ ] If applicable, Subdomain is registered and networking record requests are completed.
