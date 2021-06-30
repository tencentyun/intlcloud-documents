




    
        
            
                
            </div>
            
        </div>
        
            
                
            </div>
        </div>
    </div>
</div>

#### 요청

#### 요청 예시

### 예시 1

```plaintext




```

### 예시 2

```plaintext




```

> ?



#### 파라미터 요청











#### 응답

#### 응답



#### 응답



```plaintext

	<Owner>
		| id   | String | 초대 ID |
		
	</Owner>
	
		
			
			
			
		
		
			
			
			
		
	

```




| ---------------------- | ------ | ------------------------------- | --------- |





| ------------------ | ---------------------- | ---------------- | --------- |






| ------------------ | ---------------------------- | ------------------------------------------------------------ | ------ |
| - - ID           | 버킷 소유자의 완전한 ID로, 포맷은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다.<br>예시: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String |





| ------------------ | ------------------------------ | ---------- | --------- |





| ------------------ | ------------------------------------- | ------------------------------------------------------------ | ------ |




#### 오류코드

스트림 푸시 및 중단 에러 코드와 해당 오류 원인에 대한 자세한 내용은 [스트림 중단 에러 코드](https://intl.cloud.tencent.com/document/product/267/31083)를 참조하십시오.

## 실제 사례



#### 요청

```plaintext


Date: Fri, 21 Jun 2019 09:24:28 GMT

Connection: close
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 805
Connection: close
Date: Fri, 21 Jun 2019 09:24:28 GMT
Server: tencent-cos



	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		
	</Owner>
	
		
			
			
			
		
		
			
			
			
		
		
			
			
			
		
		
			
			
			
		
	

```



#### 요청

```plaintext

Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:28 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
Connection: close
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 495
Connection: close
Date: Fri, 21 Jun 2019 09:24:28 GMT
Server: tencent-cos



	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		
	</Owner>
	
		
			
			
			
		
		
			
			
			
		
	

```
