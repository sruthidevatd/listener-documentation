# Teradata Listener Documentation

Teradata Listener enables you to easily start streaming data at scale to many systems, such as to Teradata, HDFS, Hbase, and Aster.

<div class="row">
 <div class="grid-4">
 <a href="user-guide/index.md" class="btn btn-raised btn-block"><i class="fa fa-desktop"></i> User Guide</a>
 </div>
 <div class="grid-4">
 <a href="ingest/index.md" class="btn btn-raised btn-block"><i class="fa fa-code"></i> Ingest API</a>
 </div>
 <div class="grid-4">
 <a href="api/index.md" class="btn btn-raised btn-block"><i class="fa fa-code"></i> Application API</a>
 </div>
</div>
<div class="row">
 <div class="grid-4">
 <a href="installation/prerequisites.md" class="btn btn-raised btn-block"><i class="fa fa-download"></i> Installation</a>
 </div>
 <div class="grid-4">
 <a href="troubleshooting/intro.md" class="btn btn-raised btn-block"><i class="fa fa-question-circle"></i> Troubleshooting</a>
 </div>
 <div class="grid-4">
 <a href="GLOSSARY.md" class="btn btn-raised btn-block"><i class="fa fa-book"></i> Glossary</a>
 </div>
</div>

## Common Tasks

**I've installed Listener. Now what?**

1. Set up LDAP in [Settings](user-guide/settings.md) for one or more groups so users can log in.
2. Promote users to admin in [Manage Users](user-guide/manage-users.md).
3. Admins add systems for your users in [Manage Systems](user-guide/manage-systems.md).

**I want to start streaming data.**

1. Create a data source and get a key.
2. Post data via Ingest.

**I want to persist (store) data that I'm streaming.**

1. Admin adds a system (Teradata, HDFS, Hbase, or Aster).
2. Verify data is being ingested to your data source.
3. Create a target for that source.

## Contributing to Listener Documentation

All you need is a GitHub ID, and you can propose changes to the Listener documentation by doing the following:

1. Complete the [Dedication to Public Domain Agreement (DPDA)](/contributing/contributing-documentation.md). It takes just a minute or two to complete the DPDA, and you complete it only once.
2. At the top of any documentation page, click **EDIT IN GITHUB**. 
3. Click **Fork this repository and propose changes**.
4. Make the desired changes and submit a pull request.

A Teradata team member will review any pull requests, confirm we received the DPDA from you, and merge all or parts of your suggested changes as soon as possible.  

### GitHub Writing and Formatting Resources

For help writing and formatting your comments, the following GitHub resources may be helpful:

- [Basic Writing and Formatting Syntax](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
- [Printable Markdown Cheatsheet](https://services.github.com/kit/downloads/github-git-cheat-sheet.pdf)


---

Copyright &copy; 2016 by Teradata. All rights reserved.
