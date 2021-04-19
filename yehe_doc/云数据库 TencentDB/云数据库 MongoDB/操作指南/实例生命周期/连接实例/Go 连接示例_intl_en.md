## Notes
TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support the MONGODB-CR and SCRAM-SHA-1 authentication methods, respectively. The connecting URIs for the two authentication methods are formed differently. For more information, please see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).

Download [mgo driver](https://gopkg.in/mgo.v2) and [MongoDB Go driver](https://github.com/mongodb/mongo-go-driver/).

## Sample Code for mgo 
```
func GetMgoURL(ip, user, password string, port int) string {
	urlString := ""
	if user == "" && password == "" {
		urlString = fmt.Sprintf("mongodb://%s:%d/admin", ip, port)
	}else {
		urlString = fmt.Sprintf("mongodb://%s:%s@%s:%d/admin", url.QueryEscape(user), url.QueryEscape(password), ip, port)
	}

	return urlString
}


url := service.GetMgoURL(reqPara.Ip, reqPara.User, reqPara.Password, reqPara.Port)
	session, err := mgo.Dial(url)
```

## Sample Code for MongoDB Go
Please see [MongoDB’s official document](https://www.mongodb.com/blog/post/quick-start-golang--mongodb--starting-and-setup).
