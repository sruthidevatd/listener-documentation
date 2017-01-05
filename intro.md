# Teradata Listener Documentation

##### Version {{book.release}}

Teradata Listener enables you to easily start streaming data at scale to many systems, such as to Teradata, HDFS, Hbase, Aster, or to a custom app using [Broadcast Streams](user-guide/broadcast-streams.md).

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


---

##### Generated {{book.date}}

Copyright &copy; {{book.year}} by Teradata. All rights reserved.
