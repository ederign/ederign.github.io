---
layout: post
title:  "What is new on Business Central, from Foundation Team perspective — March 2020"
permalink: /:year/:month/:day/:title:output_ext
date:   2020-03-20 00:00:00 -0500
---
Recently, we pushed a lot of cool new features on Business Central added by Foundation Team. Those features are available soon at 7.34 release.
This post will do a quick overview of those. I hope you guys enjoy it!

## Branch support on REST APIs

Users can leverage branch support on the REST API.

[![Branch Rest](/assets/2020/rest.png "Branch Rest")](/assets/2020/rest.png)

See more details on the [full blog post](https://medium.com/kie-foundation/new-rest-endpoints-on-business-central-45d3c39d1c43).

## Maven archetype support

Users can create projects based on templates.

[![Maven Archetypes](/assets/2020/archetyp.png "Maven Archetype")](/assets/2020/archetyp.png)

See more details on the [full blog post](https://medium.com/kie-foundation/maven-archetype-support-in-business-central-b5fdf5e98556).

## Create projects from empty repositories

Users can import an empty repository from a git provider service

[![Empty Repositories](/assets/2020/empty.png "Maven Archetype")](/assets/2020/empty.png)

See more details on the [full blog post](https://medium.com/kie-foundation/import-an-empty-repository-into-business-central-b3fb76bab103).

## Squash Commits on a Change request

Users can choose to squash commits when merging a change request.

[![Squash Commits](/assets/2020/squash.png "Maven Archetype")](/assets/2020/squash.png)

See more details on the [full blog post](https://medium.com/kie-foundation/squash-commits-when-merging-a-change-request-bb8bcdc992c5).



## Other bug fixes and improvements:

We also fixed several bugs and improved Business Central on some specific scenarios:

* [JBPM-8826](https://issues.jboss.org/browse/JBPM-8826) — Forms — 10 Listeners get added each time a form is rendered
* [AF-2232](https://issues.redhat.com/browse/AF-2232) IllegalStateException displayed briefly in the UI when logging out from business-central
* [AF-2397](https://issues.redhat.com/browse/AF-2397) — Deletion of group from Business Central UI does not remove group from the security-policy.properties file
* [AF-2396](https://issues.redhat.com/browse/AF-2396) — Rest request to list spaces fails when RHPAM is integrated with RHSSO using SAML protocol
* [JBPM-8851](https://issues.redhat.com/browse/JBPM-8851)— Rename an asset change the quantity of assets returned by a search
* [AF-2424](https://issues.redhat.com/browse/AF-2424) Issue with the group permissions for the “Pages”
* [AF-2341](https://issues.redhat.com/browse/AF-2341) — Not able to restore files if the file uses a tag
* [AF-2395](https://issues.redhat.com/browse/AF-2395) -Unexpected error on Project level while launching test on cloned via REST project
* [AF-1395](https://issues.redhat.com/browse/AF-1395) — The new Form modeler editor is not locked when it is edited
* [AF-574](https://issues.redhat.com/browse/AF-574) — [Layout editor] Components disappear after moving
* [AF-903](https://issues.redhat.com/browse/AF-903) — [Settings] Made changes are no longer displayed after saving
* [AF-2404](https://issues.redhat.com/browse/AF-2404) — Package dropdown button is not visible (slowly appears) when creating an asset

## Thank you to everyone involved!

I would like to thank everyone involved with this release, from the awesome Foundation Team Engineers, to the lifesavers QEs and all the UX people that help us make our work look awesome!
