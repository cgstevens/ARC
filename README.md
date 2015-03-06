# ARC
Advanced RedGate Compare

###Overview
Out of the box RedGate traditionally only compares one data source to one another data source.  
These data sources can be either a database or a file repository.   

Who just has 1 single database?  Everywhere I have worked we have 5 minimal to track.  
What if you have 5 core but just want to easily monitor 30 or more.   

There are a few ways to track your changes when modifying your scripts.  Common way is to add what you did at the top of the script change.  Now you know what that person did on this date. If you want to see the change then you can compare.  What if you want to see what to see what was change back 3 revisions ago? 
Seeing the comment 3 revisions back doesn't reveal what was really changed.  To do this we need some sort of version history stored in a repository.  Having a couple of options; I have used SVN previously but using GIT is the norm here so let's stick with that.  The other factor is we don't develop in a sequential order amongst our dev teams. Who knows what is going to QA from what team and do we want those changes in our dev environment? We may not be ready for those since we are not on the same release cycle as the other teams.  

Now having access to RedGate SDK, Git and the love to make my job and others easier I came up with Advanced RedGate Comparer, ARC for short. ARC was design to make existing tasks easier.    I decided to do this in WPF using the MVVM pattern.  
I'll be honest I didn't separate it fully like I wanted to. Each section could be refactor to be its own View and ViewModels.

On start the app will check to see if have a SQL Toolkit license. I think just having the SDK is valid as well.  Review your license if you run into issues.


###Configuration Menu Option
  Open Config Folder
  
    ServerList.xml - Configure the database server/credentials and file repositories.
    DatabaseList.xml - Configure the list of databases to connect to.
    FilterList.xml - Allows you to configure different filters per environment. (coming soon)
    CompareList.xml - Allows you to configure different compare options per environment.
    
    
    
    
###DataSource Compare
    You can compare 2 types of data sources; Microsoft SQL Database or SQL Scripts in a source control repository.
    Git Integration: The first step to integrated Git int ARC was to display what branch the user is working on. To accomplish this I used LibGit2Sharp. Now that I have that working we could build on that to wire up with Sync to Source action. This would allow the ability to commit to the repository when syncing.
    Executing the Compare will cycle through the databases.  Using the IAsyncResult you have the limit of 64 request. I haven't reached this limit in this application but in case you have the need to do so it will queue the requests.
