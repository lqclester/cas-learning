# cas登录/认证过程

## 名词
- TGT
- TGC
- ST (Service Ticket)

	ST是CAS为用户签发的访问某一service的票据。用户访问service时，service发现用户没有ST，则要求用户去CAS获取ST。用户向CAS发出获取ST的请求，如果用户的请求中包含cookie，则CAS会以此cookie值为key查询缓存中有无TGT，如果存在TGT，则用此TGT签发一个ST，返回给用户。用户凭借ST去访问service，service拿ST去CAS验证，验证通过后，允许用户访问资源。

- assertion
	
	存在着cas的登录后的用户信息，放在session里。
`

final Assertion assertion = request.getSession() != null ? (Assertion)request.getSession().getAttribute(AbstractCasFilter.CONST_CAS_ASSERTION) : null;
` 

## 认证过程  
- 当用户(*broswer*)访问cas client(*locoalhost:8080/app*)
 
	**CAS Validation Filter**检查**client**是否带有st或者session是否存在assertion，不存在则跳到cas登录页面

	```java
	response.sendRedirect(urlToRedirectTo);
	```
