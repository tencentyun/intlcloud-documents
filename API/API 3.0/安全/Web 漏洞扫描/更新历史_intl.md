## Release 4
Release time: 15:15:08, June 28, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateVulsReport](/document/api/692/18089)
* [DescribeVulsNumber](/document/api/692/18088)
* [DescribeVulsNumberTimeline](/document/api/692/18087)

New data structures:

* [VulsTimeline](/document/api/692/16759#VulsTimeline)

## Release 3

Release time: 12:15:42, June 14, 2018

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateSites](/document/api/692/16748)
	* New input parameters: UserAgent
* [DescribeConfig](/document/api/692/16757)
	* New output parameters: Appid
* [DescribeSitesVerification](/document/api/692/16753)
	* **Modified output parameters:** SitesVerification
* [ModifySiteAttribute](/document/api/692/16754)
	* New input parameters: NeedLogin, LoginCookie, LoginCheckUrl, LoginCheckKw, ScanDisallow

Modified data structure:

* [Site](/document/api/692/16759#Site)
	* New members: NeedLogin, LoginCookie, LoginCookieValid, LoginCheckUrl, LoginCheckKw, ScanDisallow, UserAgent
	* **Deleted members:** LastScanExtsCount
* [SitesVerification](/document/api/692/16759#SitesVerification)
	* New members: VerifyUrl, VerifyFileUrl
* [Vul](/document/api/692/16759#Vul)
	* New members: Appid, Uin

## Release 2

Release time: 17:08:50, May 24, 2018

This release contains:

Improvement to existing documentation.

Modified data structure:

* [Monitor](/document/api/692/16759#Monitor)
	* New members: Id, Appid
	* **Deleted members:** ID
* [Site](/document/api/692/16759#Site)
	* New members: LastScanExtsCount, Appid, Uin
* [SitesVerification](/document/api/692/16759#SitesVerification)
	* New members: Id, Appid

## Release 1

Release time: April 24, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateMonitors](/document/api/692/16743)
* [CreateSites](/document/api/692/16748)
* [CreateSitesScans](/document/api/692/16749)
* [CreateVulsMisinformation](/document/api/692/16740)
* [DeleteMonitors](/document/api/692/16744)
* [DeleteSites](/document/api/692/16750)
* [DescribeConfig](/document/api/692/16757)
* [DescribeMonitors](/document/api/692/16745)
* [DescribeSiteQuota](/document/api/692/16751)
* [DescribeSites](/document/api/692/16752)
* [DescribeSitesVerification](/document/api/692/16753)
* [DescribeVuls](/document/api/692/16741)
* [ModifyConfigAttribute](/document/api/692/16758)
* [ModifyMonitorAttribute](/document/api/692/16746)
* [ModifySiteAttribute](/document/api/692/16754)
* [VerifySites](/document/api/692/16755)

New data structures:

* [Filter](/document/api/692/16759#Filter)
* [Monitor](/document/api/692/16759#Monitor)
* [MonitorMiniSite](/document/api/692/16759#MonitorMiniSite)
* [MonitorsDetail](/document/api/692/16759#MonitorsDetail)
* [Site](/document/api/692/16759#Site)
* [SitesVerification](/document/api/692/16759#SitesVerification)
* [Vul](/document/api/692/16759#Vul)


