# ZAP Scanning Report


## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 0 |
| Medium | 4 |
| Low | 5 |
| Informational | 2 |




## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| Absence of Anti-CSRF Tokens | Medium | 2 |
| Content Security Policy (CSP) Header Not Set | Medium | 4 |
| Missing Anti-clickjacking Header | Medium | 1 |
| Sub Resource Integrity Attribute Missing | Medium | 1 |
| In Page Banner Information Leak | Low | 3 |
| Permissions Policy Header Not Set | Low | 5 |
| Server Leaks Version Information via "Server" HTTP Response Header Field | Low | 9 |
| Timestamp Disclosure - Unix | Low | 1 |
| X-Content-Type-Options Header Missing | Low | 6 |
| Base64 Disclosure | Informational | 1 |
| Storable and Cacheable Content | Informational | 9 |




## Alert Detail



### [ Absence of Anti-CSRF Tokens ](https://www.zaproxy.org/docs/alerts/10202/)



##### Medium (Low)

### Description

No Anti-CSRF tokens were found in a HTML submission form.
A cross-site request forgery is an attack that involves forcing a victim to send an HTTP request to a target destination without their knowledge or intent in order to perform an action as the victim. The underlying cause is application functionality using predictable URL/form actions in a repeatable way. The nature of the attack is that CSRF exploits the trust that a web site has for a user. By contrast, cross-site scripting (XSS) exploits the trust that a user has for a web site. Like XSS, CSRF attacks are not necessarily cross-site, but they can be. Cross-site request forgery is also known as CSRF, XSRF, one-click attack, session riding, confused deputy, and sea surf.

CSRF attacks are effective in a number of situations, including:
    * The victim has an active session on the target site.
    * The victim is authenticated via HTTP auth on the target site.
    * The victim is on the same local network as the target site.

CSRF has primarily been used to perform an action against a target site using the victim's privileges, but recent techniques have been discovered to disclose information by gaining access to the response. The risk of information disclosure is dramatically increased when the target site is vulnerable to XSS, because XSS can be used as a platform for CSRF, allowing the attack to operate within the bounds of the same-origin policy.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<form id="sb-search" action="/search/">`
* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<form id="footer-search" action="/search/">`

Instances: 2

### Solution

Phase: Architecture and Design
Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.
For example, use anti-CSRF packages such as the OWASP CSRFGuard.

Phase: Implementation
Ensure that your application is free of cross-site scripting issues, because most CSRF defenses can be bypassed using attacker-controlled script.

Phase: Architecture and Design
Generate a unique nonce for each form, place the nonce into the form, and verify the nonce upon receipt of the form. Be sure that the nonce is not predictable (CWE-330).
Note that this can be bypassed using XSS.

Identify especially dangerous operations. When the user performs a dangerous operation, send a separate confirmation request to ensure that the user intended to perform that operation.
Note that this can be bypassed using XSS.

Use the ESAPI Session Management control.
This control includes a component for CSRF.

Do not use the GET method for any request that triggers a state change.

Phase: Implementation
Check the HTTP Referer header to see if the request originated from an expected page. This could break legitimate functionality, because users or proxies may have disabled sending the Referer for privacy reasons.

### Reference


* [ http://projects.webappsec.org/Cross-Site-Request-Forgery ](http://projects.webappsec.org/Cross-Site-Request-Forgery)
* [ http://cwe.mitre.org/data/definitions/352.html ](http://cwe.mitre.org/data/definitions/352.html)


#### CWE Id: [ 352 ](https://cwe.mitre.org/data/definitions/352.html)


#### WASC Id: 9

#### Source ID: 3

### [ Content Security Policy (CSP) Header Not Set ](https://www.zaproxy.org/docs/alerts/10038/)



##### Medium (High)

### Description

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware. CSP provides a set of standard HTTP headers that allow website owners to declare approved sources of content that browsers should be allowed to load on that page — covered types are JavaScript, CSS, HTML frames, fonts, images and embeddable objects such as Java applets, ActiveX, audio and video files.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/search/%3Fq=ZAP
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 4

### Solution

Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header, to achieve optimal browser support: "Content-Security-Policy" for Chrome 25+, Firefox 23+ and Safari 7+, "X-Content-Security-Policy" for Firefox 4.0+ and Internet Explorer 10+, and "X-WebKit-CSP" for Chrome 14+ and Safari 6+.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/Security/CSP/Introducing_Content_Security_Policy ](https://developer.mozilla.org/en-US/docs/Web/Security/CSP/Introducing_Content_Security_Policy)
* [ https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html ](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)
* [ http://www.w3.org/TR/CSP/ ](http://www.w3.org/TR/CSP/)
* [ http://w3c.github.io/webappsec/specs/content-security-policy/csp-specification.dev.html ](http://w3c.github.io/webappsec/specs/content-security-policy/csp-specification.dev.html)
* [ http://www.html5rocks.com/en/tutorials/security/content-security-policy/ ](http://www.html5rocks.com/en/tutorials/security/content-security-policy/)
* [ http://caniuse.com/#feat=contentsecuritypolicy ](http://caniuse.com/#feat=contentsecuritypolicy)
* [ http://content-security-policy.com/ ](http://content-security-policy.com/)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Missing Anti-clickjacking Header ](https://www.zaproxy.org/docs/alerts/10020/)



##### Medium (Medium)

### Description

The response does not include either Content-Security-Policy with 'frame-ancestors' directive or X-Frame-Options to protect against 'ClickJacking' attacks.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: `X-Frame-Options`
  * Attack: ``
  * Evidence: ``

Instances: 1

### Solution

Modern Web browsers support the Content-Security-Policy and X-Frame-Options HTTP headers. Ensure one of them is set on all web pages returned by your site/app.
If you expect the page to be framed only by pages on your server (e.g. it's part of a FRAMESET) then you'll want to use SAMEORIGIN, otherwise if you never expect the page to be framed, you should use DENY. Alternatively consider implementing Content Security Policy's "frame-ancestors" directive.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)


#### CWE Id: [ 1021 ](https://cwe.mitre.org/data/definitions/1021.html)


#### WASC Id: 15

#### Source ID: 3

### [ Sub Resource Integrity Attribute Missing ](https://www.zaproxy.org/docs/alerts/90003/)



##### Medium (High)

### Description

The integrity attribute is missing on a script or link tag served by an external server. The integrity tag prevents an attacker who have gained access to this server from injecting a malicious content. 

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<link rel="preload" href="https://www.google-analytics.com/analytics.js" as="script">`

Instances: 1

### Solution

Provide a valid integrity attribute to the tag.

### Reference


* [ https://developer.mozilla.org/en/docs/Web/Security/Subresource_Integrity ](https://developer.mozilla.org/en/docs/Web/Security/Subresource_Integrity)


#### CWE Id: [ 345 ](https://cwe.mitre.org/data/definitions/345.html)


#### WASC Id: 15

#### Source ID: 3

### [ In Page Banner Information Leak ](https://www.zaproxy.org/docs/alerts/10009/)



##### Low (High)

### Description

The server returned a version banner string in the response content. Such information leaks may allow attackers to further target specific issues impacting the product and version in use.

* URL: http://scanme.nmap.org/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7`
* URL: http://scanme.nmap.org/search/%3Fq=ZAP
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7`
* URL: http://scanme.nmap.org/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7`

Instances: 3

### Solution

Configure the server to prevent such information leaks. For example:
Under Tomcat this is done via the "server" directive and implementation of custom error pages.
Under Apache this is done via the "ServerSignature" and "ServerTokens" directives.

### Reference


* [ https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/08-Testing_for_Error_Handling/ ](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/08-Testing_for_Error_Handling/)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Permissions Policy Header Not Set ](https://www.zaproxy.org/docs/alerts/10063/)



##### Low (Medium)

### Description

Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. This policy ensures the user privacy by limiting or specifying the features of the browsers can be used by the web resources. Permissions Policy provides a set of standard HTTP headers that allow website owners to limit which features of browsers can be used by the page such as camera, microphone, location, full screen etc.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/search/%3Fq=ZAP
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/ga.js
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 5

### Solution

Ensure that your web server, application server, load balancer, etc. is configured to set the Permissions-Policy header.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Feature-Policy ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Feature-Policy)
* [ https://developers.google.com/web/updates/2018/06/feature-policy ](https://developers.google.com/web/updates/2018/06/feature-policy)
* [ https://scotthelme.co.uk/a-new-security-header-feature-policy/ ](https://scotthelme.co.uk/a-new-security-header-feature-policy/)
* [ https://w3c.github.io/webappsec-feature-policy/ ](https://w3c.github.io/webappsec-feature-policy/)
* [ https://www.smashingmagazine.com/2018/12/feature-policy/ ](https://www.smashingmagazine.com/2018/12/feature-policy/)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Server Leaks Version Information via "Server" HTTP Response Header Field ](https://www.zaproxy.org/docs/alerts/10036/)



##### Low (High)

### Description

The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/images/sitelogo.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/search/%3Fq=ZAP
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/shared/css/main.css
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/shared/ga.js
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/shared/images/tiny-eyeicon.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/site.css
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`
* URL: http://scanme.nmap.org/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Apache/2.4.7 (Ubuntu)`

Instances: 9

### Solution

Ensure that your web server, application server, load balancer, etc. is configured to suppress the "Server" header or provide generic details.

### Reference


* [ http://httpd.apache.org/docs/current/mod/core.html#servertokens ](http://httpd.apache.org/docs/current/mod/core.html#servertokens)
* [ http://msdn.microsoft.com/en-us/library/ff648552.aspx#ht_urlscan_007 ](http://msdn.microsoft.com/en-us/library/ff648552.aspx#ht_urlscan_007)
* [ http://blogs.msdn.com/b/varunm/archive/2013/04/23/remove-unwanted-http-response-headers.aspx ](http://blogs.msdn.com/b/varunm/archive/2013/04/23/remove-unwanted-http-response-headers.aspx)
* [ http://www.troyhunt.com/2012/02/shhh-dont-let-your-response-headers.html ](http://www.troyhunt.com/2012/02/shhh-dont-let-your-response-headers.html)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Timestamp Disclosure - Unix ](https://www.zaproxy.org/docs/alerts/10096/)



##### Low (Low)

### Description

A timestamp was disclosed by the application/web server - Unix

* URL: http://scanme.nmap.org/shared/ga.js
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `11009417`

Instances: 1

### Solution

Manually confirm that the timestamp data is not sensitive, and that the data cannot be aggregated to disclose exploitable patterns.

### Reference


* [ http://projects.webappsec.org/w/page/13246936/Information%20Leakage ](http://projects.webappsec.org/w/page/13246936/Information%20Leakage)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ X-Content-Type-Options Header Missing ](https://www.zaproxy.org/docs/alerts/10021/)



##### Low (Medium)

### Description

The Anti-MIME-Sniffing header X-Content-Type-Options was not set to 'nosniff'. This allows older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body, potentially causing the response body to be interpreted and displayed as a content type other than the declared content type. Current (early 2014) and legacy versions of Firefox will use the declared content type (if one is set), rather than performing MIME-sniffing.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/images/sitelogo.png
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/css/main.css
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/ga.js
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/images/tiny-eyeicon.png
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/site.css
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``

Instances: 6

### Solution

Ensure that the application/web server sets the Content-Type header appropriately, and that it sets the X-Content-Type-Options header to 'nosniff' for all web pages.
If possible, ensure that the end user uses a standards-compliant and modern web browser that does not perform MIME-sniffing at all, or that can be directed by the web application/web server to not perform MIME-sniffing.

### Reference


* [ http://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx ](http://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx)
* [ https://owasp.org/www-community/Security_Headers ](https://owasp.org/www-community/Security_Headers)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Base64 Disclosure ](https://www.zaproxy.org/docs/alerts/10094/)



##### Informational (Medium)

### Description

Base64 encoded data was disclosed by the application/web server. Note: in the interests of performance not all base64 strings in the response were analyzed individually, the entire response should be looked at by the analyst/security team/developer(s).

* URL: http://scanme.nmap.org/shared/css/main.css
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `PHN2ZyB2ZXJzaW9uPSIxLjEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDEgMSI+PHBhdGggZD0iTTEsMEExLDEgMCwwLDAgMCwxTDAsMFoiIGZpbGw9IiMyYTBkNDUiLz48L3N2Zz4K`

Instances: 1

### Solution

Manually confirm that the Base64 data does not leak sensitive information, and that the data cannot be aggregated/used to exploit other vulnerabilities.

### Reference


* [ http://projects.webappsec.org/w/page/13246936/Information%20Leakage ](http://projects.webappsec.org/w/page/13246936/Information%20Leakage)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Storable and Cacheable Content ](https://www.zaproxy.org/docs/alerts/10049/)



##### Informational (Medium)

### Description

The response contents are storable by caching components such as proxy servers, and may be retrieved directly from the cache, rather than from the origin server by the caching servers, in response to similar requests from other users.  If the response data is sensitive, personal or user-specific, this may result in sensitive information being leaked. In some cases, this may even result in a user gaining complete control of the session of another user, depending on the configuration of the caching components in use in their environment. This is primarily an issue where "shared" caching servers such as "proxy" caches are configured on the local network. This configuration is typically found in corporate or educational environments, for instance.

* URL: http://scanme.nmap.org/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/images/sitelogo.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/search/%3Fq=ZAP
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/css/main.css
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/ga.js
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/shared/images/tiny-eyeicon.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/site.css
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: http://scanme.nmap.org/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 9

### Solution

Validate that the response does not contain sensitive, personal or user-specific information.  If it does, consider the use of the following HTTP response headers, to limit, or prevent the content being stored and retrieved from the cache by another user:
Cache-Control: no-cache, no-store, must-revalidate, private
Pragma: no-cache
Expires: 0
This configuration directs both HTTP 1.0 and HTTP 1.1 compliant caching servers to not store the response, and to not retrieve the response (without validation) from the cache, in response to a similar request. 

### Reference


* [ https://tools.ietf.org/html/rfc7234 ](https://tools.ietf.org/html/rfc7234)
* [ https://tools.ietf.org/html/rfc7231 ](https://tools.ietf.org/html/rfc7231)
* [ http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html (obsoleted by rfc7234) ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html (obsoleted by rfc7234))


#### CWE Id: [ 524 ](https://cwe.mitre.org/data/definitions/524.html)


#### WASC Id: 13

#### Source ID: 3


