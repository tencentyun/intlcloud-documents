## Release 4
Release time: 15:15:08, June 28, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateVulsReport](https://cloud.tencent.com/document/api/692/18089)
* [DescribeVulsNumber](https://cloud.tencent.com/document/api/692/18088)
* [DescribeVulsNumberTimeline](https://cloud.tencent.com/document/api/692/18087)

New data structures:

* [VulsTimeline](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#VulsTimeline)

## Release 3

Release time: 12:15:42, June 14, 2018

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateSites](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16748)
	* New input parameters: UserAgent
* [DescribeConfig](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16757)
	* New output parameters: Appid
* [DescribeSitesVerification](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16753)
	* **Modified output parameters:** SitesVerification
* [ModifySiteAttribute](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16754)
	* New input parameters: NeedLogin, LoginCookie, LoginCheckUrl, LoginCheckKw, ScanDisallow

Modified data structure:

* [Site](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Site)
	* New members: NeedLogin, LoginCookie, LoginCookieValid, LoginCheckUrl, LoginCheckKw, ScanDisallow, UserAgent
	* **Deleted members:** LastScanExtsCount
* [SitesVerification](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#SitesVerification)
	* New members: VerifyUrl, VerifyFileUrl
* [Vul](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Vul)
	* New members: Appid, Uin

## Release 2

Release time: 17:08:50, May 24, 2018

This release contains:

Improvement to existing documentation.

Modified data structure:

* [Monitor](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Monitor)
	* New members: Id, Appid
	* **Deleted members:** ID
* [Site](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Site)
	* New members: LastScanExtsCount, Appid, Uin
* [SitesVerification](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#SitesVerification)
	* New members: Id, Appid

## Release 1

Release time: April 24, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateMonitors](https://cloud.tencent.com/document/api/692/16743)
* [CreateSites](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16748)
* [CreateSitesScans](https://cloud.tencent.com/document/api/692/16749)
* [CreateVulsMisinformation](https://cloud.tencent.com/document/api/692/16740)
* [DeleteMonitors](https://cloud.tencent.com/document/api/692/16744)
* [DeleteSites](https://cloud.tencent.com/document/api/692/16750)
* [DescribeConfig](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16757)
* [DescribeMonitors](https://cloud.tencent.com/document/api/692/16745)
* [DescribeSiteQuota](https://cloud.tencent.com/document/api/692/16751)
* [DescribeSites](https://cloud.tencent.com/document/api/692/16752)
* [DescribeSitesVerification](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16753)
* [DescribeVuls](https://cloud.tencent.com/document/api/692/16741)
* [ModifyConfigAttribute](https://cloud.tencent.com/document/api/692/16758)
* [ModifyMonitorAttribute](https://cloud.tencent.com/document/api/692/16746)
* [ModifySiteAttribute](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16754)
* [VerifySites](https://cloud.tencent.com/document/api/692/16755)

New data structures:

* [Filter](https://cloud.tencent.com/document/api/692/16759#Filter)
* [Monitor](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Monitor)
* [MonitorMiniSite](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#MonitorMiniSite)
* [MonitorsDetail](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#MonitorsDetail)
* [Site](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Site)
* [SitesVerification](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#SitesVerification)
* [Vul](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/692/16759#Vul)


