# ZAP Scanning Report


## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 0 |
| Medium | 5 |
| Low | 11 |
| Informational | 6 |




## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| Application Error Disclosure | Medium | 1 |
| Content Security Policy (CSP) Header Not Set | Medium | 2 |
| Missing Anti-clickjacking Header | Medium | 2 |
| Sub Resource Integrity Attribute Missing | Medium | 2 |
| Vulnerable JS Library | Medium | 1 |
| Cookie Without Secure Flag | Low | 2 |
| Cookie with SameSite Attribute None | Low | 2 |
| Cookie without SameSite Attribute | Low | 2 |
| Dangerous JS Functions | Low | 1 |
| Incomplete or No Cache-control Header Set | Low | 3 |
| Permissions Policy Header Not Set | Low | 3 |
| Private IP Disclosure | Low | 1 |
| Server Leaks Information via "X-Powered-By" HTTP Response Header Field(s) | Low | 3 |
| Strict-Transport-Security Header Not Set | Low | 11 |
| Timestamp Disclosure - Unix | Low | 28 |
| X-Content-Type-Options Header Missing | Low | 11 |
| Base64 Disclosure | Informational | 7 |
| Information Disclosure - Suspicious Comments | Informational | 13 |
| Modern Web Application | Informational | 2 |
| Non-Storable Content | Informational | 2 |
| Storable and Cacheable Content | Informational | 3 |
| Storable but Non-Cacheable Content | Informational | 6 |




## Alert Detail



### [ Application Error Disclosure ](https://www.zaproxy.org/docs/alerts/90022/)



##### Medium (Medium)

### Description

This page contains an error/warning message that may disclose sensitive information like the location of the file that produced the unhandled exception. This information can be used to launch further attacks against the web application. The alert could be a false positive if the error message is found inside a documentation page.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Internal Server Error`

Instances: 1

### Solution

Review the source code of this page. Implement custom error pages. Consider implementing a mechanism to provide a unique error reference/identifier to the client (browser) while logging the details on the server side and not exposing them to the user.

### Reference



#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Content Security Policy (CSP) Header Not Set ](https://www.zaproxy.org/docs/alerts/10038/)



##### Medium (High)

### Description

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware. CSP provides a set of standard HTTP headers that allow website owners to declare approved sources of content that browsers should be allowed to load on that page — covered types are JavaScript, CSS, HTML frames, fonts, images and embeddable objects such as Java applets, ActiveX, audio and video files.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 2

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

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: `X-Frame-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: `X-Frame-Options`
  * Attack: ``
  * Evidence: ``

Instances: 2

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

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/nocfbnnmjnndkbipkabodnheejiegccf" />`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/nocfbnnmjnndkbipkabodnheejiegccf" />`

Instances: 2

### Solution

Provide a valid integrity attribute to the tag.

### Reference


* [ https://developer.mozilla.org/en/docs/Web/Security/Subresource_Integrity ](https://developer.mozilla.org/en/docs/Web/Security/Subresource_Integrity)


#### CWE Id: [ 345 ](https://cwe.mitre.org/data/definitions/345.html)


#### WASC Id: 15

#### Source ID: 3

### [ Vulnerable JS Library ](https://www.zaproxy.org/docs/alerts/10003/)



##### Medium (Medium)

### Description

The identified library jquery, version 3.3.1 is vulnerable.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `{jquery:"3.3.1"`

Instances: 1

### Solution

Please upgrade to the latest version of jquery.

### Reference


* [ https://blog.jquery.com/2019/04/10/jquery-3-4-0-released/ ](https://blog.jquery.com/2019/04/10/jquery-3-4-0-released/)
* [ https://nvd.nist.gov/vuln/detail/CVE-2019-11358 ](https://nvd.nist.gov/vuln/detail/CVE-2019-11358)
* [ https://github.com/jquery/jquery/commit/753d591aea698e57d6db58c9f722cd0808619b1b ](https://github.com/jquery/jquery/commit/753d591aea698e57d6db58c9f722cd0808619b1b)
* [ https://blog.jquery.com/2020/04/10/jquery-3-5-0-released/ ](https://blog.jquery.com/2020/04/10/jquery-3-5-0-released/)


#### CWE Id: [ 829 ](https://cwe.mitre.org/data/definitions/829.html)


#### Source ID: 3

### [ Cookie Without Secure Flag ](https://www.zaproxy.org/docs/alerts/10011/)



##### Low (Medium)

### Description

A cookie has been set without the secure flag, which means that the cookie can be accessed via unencrypted connections.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: `connect.sid`
  * Attack: ``
  * Evidence: `set-cookie: connect.sid`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: `connect.sid`
  * Attack: ``
  * Evidence: `set-cookie: connect.sid`

Instances: 2

### Solution

Whenever a cookie contains sensitive information or is a session token, then it should always be passed using an encrypted channel. Ensure that the secure flag is set for cookies containing such sensitive information.

### Reference


* [ https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/06-Session_Management_Testing/02-Testing_for_Cookies_Attributes.html ](https://owasp.org/www-project-web-security-testing-guide/v41/4-Web_Application_Security_Testing/06-Session_Management_Testing/02-Testing_for_Cookies_Attributes.html)


#### CWE Id: [ 614 ](https://cwe.mitre.org/data/definitions/614.html)


#### WASC Id: 13

#### Source ID: 3

### [ Cookie with SameSite Attribute None ](https://www.zaproxy.org/docs/alerts/10054/)



##### Low (Medium)

### Description

A cookie has been set with its SameSite attribute set to "none", which means that the cookie can be sent as a result of a 'cross-site' request. The SameSite attribute is an effective counter measure to cross-site request forgery, cross-site script inclusion, and timing attacks.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 2

### Solution

Ensure that the SameSite attribute is set to either 'lax' or ideally 'strict' for all cookies.

### Reference


* [ https://tools.ietf.org/html/draft-ietf-httpbis-cookie-same-site ](https://tools.ietf.org/html/draft-ietf-httpbis-cookie-same-site)


#### CWE Id: [ 1275 ](https://cwe.mitre.org/data/definitions/1275.html)


#### WASC Id: 13

#### Source ID: 3

### [ Cookie without SameSite Attribute ](https://www.zaproxy.org/docs/alerts/10054/)



##### Low (Medium)

### Description

A cookie has been set without the SameSite attribute, which means that the cookie can be sent as a result of a 'cross-site' request. The SameSite attribute is an effective counter measure to cross-site request forgery, cross-site script inclusion, and timing attacks.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: `connect.sid`
  * Attack: ``
  * Evidence: `set-cookie: connect.sid`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: `connect.sid`
  * Attack: ``
  * Evidence: `set-cookie: connect.sid`

Instances: 2

### Solution

Ensure that the SameSite attribute is set to either 'lax' or ideally 'strict' for all cookies.

### Reference


* [ https://tools.ietf.org/html/draft-ietf-httpbis-cookie-same-site ](https://tools.ietf.org/html/draft-ietf-httpbis-cookie-same-site)


#### CWE Id: [ 1275 ](https://cwe.mitre.org/data/definitions/1275.html)


#### WASC Id: 13

#### Source ID: 3

### [ Dangerous JS Functions ](https://www.zaproxy.org/docs/alerts/10110/)



##### Low (Low)

### Description

A dangerous JS function seems to be in use that would leave the site vulnerable.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `eval`

Instances: 1

### Solution

See the references for security advice on the use of these functions.

### Reference


* [ https://angular.io/guide/security ](https://angular.io/guide/security)


#### CWE Id: [ 749 ](https://cwe.mitre.org/data/definitions/749.html)


#### Source ID: 3

### [ Incomplete or No Cache-control Header Set ](https://www.zaproxy.org/docs/alerts/10015/)



##### Low (Medium)

### Description

The cache-control header has not been set properly or is missing, allowing the browser and proxies to cache content.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: `Cache-Control`
  * Attack: ``
  * Evidence: `private`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/images/manifest.json
  * Method: `GET`
  * Parameter: `Cache-Control`
  * Attack: ``
  * Evidence: `public, max-age=0`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: `Cache-Control`
  * Attack: ``
  * Evidence: ``

Instances: 3

### Solution

Whenever possible ensure the cache-control HTTP header is set with no-cache, no-store, must-revalidate.

### Reference


* [ https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html#web-content-caching ](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html#web-content-caching)
* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)


#### CWE Id: [ 525 ](https://cwe.mitre.org/data/definitions/525.html)


#### WASC Id: 13

#### Source ID: 3

### [ Permissions Policy Header Not Set ](https://www.zaproxy.org/docs/alerts/10063/)



##### Low (Medium)

### Description

Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. This policy ensures the user privacy by limiting or specifying the features of the browsers can be used by the web resources. Permissions Policy provides a set of standard HTTP headers that allow website owners to limit which features of browsers can be used by the page such as camera, microphone, location, full screen etc.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 3

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

### [ Private IP Disclosure ](https://www.zaproxy.org/docs/alerts/2/)



##### Low (Medium)

### Description

A private IP (such as 10.x.x.x, 172.x.x.x, 192.168.x.x) or an Amazon EC2 private hostname (for example, ip-10-0-56-78) has been found in the HTTP response body. This information might be helpful for further attacks targeting internal systems.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `10.0.2.2`

Instances: 1

### Solution

Remove the private IP address from the HTTP response body.  For comments, use JSP/ASP/PHP comment instead of HTML/JavaScript comment which can be seen by client browsers.

### Reference


* [ https://tools.ietf.org/html/rfc1918 ](https://tools.ietf.org/html/rfc1918)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Server Leaks Information via "X-Powered-By" HTTP Response Header Field(s) ](https://www.zaproxy.org/docs/alerts/10037/)



##### Low (Medium)

### Description

The web/application server is leaking information via one or more "X-Powered-By" HTTP response headers. Access to such information may facilitate attackers identifying other frameworks/components your web application is reliant upon and the vulnerabilities such components may be subject to.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `X-Powered-By: Express`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `X-Powered-By: Express`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `X-Powered-By: Express`

Instances: 3

### Solution

Ensure that your web server, application server, load balancer, etc. is configured to suppress "X-Powered-By" headers.

### Reference


* [ http://blogs.msdn.com/b/varunm/archive/2013/04/23/remove-unwanted-http-response-headers.aspx ](http://blogs.msdn.com/b/varunm/archive/2013/04/23/remove-unwanted-http-response-headers.aspx)
* [ http://www.troyhunt.com/2012/02/shhh-dont-let-your-response-headers.html ](http://www.troyhunt.com/2012/02/shhh-dont-let-your-response-headers.html)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Strict-Transport-Security Header Not Set ](https://www.zaproxy.org/docs/alerts/10035/)



##### Low (High)

### Description

HTTP Strict Transport Security (HSTS) is a web security policy mechanism whereby a web server declares that complying user agents (such as a web browser) are to interact with it using only secure HTTPS connections (i.e. HTTP layered over TLS/SSL). HSTS is an IETF standards track protocol and is specified in RFC 6797.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/9b704c621adc8a1dcae59307e0023894dbfd2413.css%3Fmeteor_css_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon.svg
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon_16.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon_32.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/safari_pinned.svg
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/touchicon_180.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/images/manifest.json
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/theme.css%3F1807b422d007328786a00d34e6c63ee6022dd2b3
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 11

### Solution

Ensure that your web server, application server, load balancer, etc. is configured to enforce Strict-Transport-Security.

### Reference


* [ https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html ](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html)
* [ https://owasp.org/www-community/Security_Headers ](https://owasp.org/www-community/Security_Headers)
* [ http://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security ](http://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)
* [ http://caniuse.com/stricttransportsecurity ](http://caniuse.com/stricttransportsecurity)
* [ http://tools.ietf.org/html/rfc6797 ](http://tools.ietf.org/html/rfc6797)


#### CWE Id: [ 319 ](https://cwe.mitre.org/data/definitions/319.html)


#### WASC Id: 15

#### Source ID: 3

### [ Timestamp Disclosure - Unix ](https://www.zaproxy.org/docs/alerts/10096/)



##### Low (Low)

### Description

A timestamp was disclosed by the application/web server - Unix

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `02490772`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `06030829`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `07579219`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `08428051`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `0980054069`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `11094988`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `11555082`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `22245052`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `23600113`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `23904354`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `25127483`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `26554796`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `27864386`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `27963438`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `32790954`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `40441379`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `44735961`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `46190251`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `46355327`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `47817702`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `55731005`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `65283709`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `67973749`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `68509058`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `69174481`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `77042449`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `81559304`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `91155959`

Instances: 28

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

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/9b704c621adc8a1dcae59307e0023894dbfd2413.css%3Fmeteor_css_resource=true
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon.svg
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon_16.png
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon_32.png
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/safari_pinned.svg
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/touchicon_180.png
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/touchicon_180_pre.png
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/images/manifest.json
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/theme.css%3F1807b422d007328786a00d34e6c63ee6022dd2b3
  * Method: `GET`
  * Parameter: `X-Content-Type-Options`
  * Attack: ``
  * Evidence: ``

Instances: 11

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

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `3AHi7p8OJkBt7L72ubbPI9--K1haaEExIW`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `3AWDJZ9PFYpNdbu9mCx0gLHpir_NWw0ujf`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/9b704c621adc8a1dcae59307e0023894dbfd2413.css%3Fmeteor_css_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `PHN2ZyB2aWV3Qm94PSIwIDAgNDMwIDQzMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4NCjxnIGlkPSJzaWduLWluIiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgMCAwIDAuNSAwIDApIj4NCjxwYXRoIGZpbGw9IiNmZmZmZmYiIGQ9Ik02NjAuNjcyIDUwMC4wMzJxMCAxNC41MDggLTEwLjYwMiAyNS4xMWwtMzAzLjU1MiAzMDMuNTUycS0xMC42MDIgMTAuNjAyIC0yNS4xMSAxMC42MDJ0LTI1LjExIC0xMC42MDIgLTEwLjYwMiAtMjUuMTF2LTE2MC43MDRoLTI0OS45ODRxLTE0LjUwOCAwIC0yNS4xMSAtMTAuNjAydC0xMC42MDIgLTI1LjExdi0yMTQuMjcycTAgLTE0LjUwOCAxMC42MDIgLTI1LjExdDI1LjExIC0xMC42MDJoMjQ5Ljk4NHYtMTYwLjcwNHEwIC0xNC41MDggMTAuNjAyIC0yNS4xMXQyNS4xMSAtMTAuNjAyIDI1LjExIDEwLjYwMmwzMDMuNTUyIDMwMy41NTJxMTAuNjAyIDEwLjYwMiAxMC42MDIgMjUuMTF6bTE5Ni40MTYgLTE5Ni40MTZ2MzkyLjgzMnEwIDY2LjQwMiAtNDcuMTUxIDExMy41NTN0LTExMy41NTMgNDcuMTUxaC0xNzguNTZxLTcuMjU0IDAgLTEyLjU1NSAtNS4zMDF0LTUuMzAxIC0xMi41NTVxMCAtMi4yMzIgLS41NTggLTExLjE2dC0uMjc5IC0xNC43ODcgMS42NzQgLTEzLjExMyA1LjU4IC0xMC44ODEgMTEuNDM5IC0zLjYyN2gxNzguNTZxMzYuODI4IDAgNjMuMDU0IC0yNi4yMjZ0MjYuMjI2IC02My4wNTR2LTM5Mi44MzJxMCAtMzYuODI4IC0yNi4yMjYgLTYzLjA1NHQtNjMuMDU0IC0yNi4yMjZoLTE3NC4wOTZ0LTYuNDE3IC0uNTU4IC02LjQxNyAtMS42NzQgLTQuNDY0IC0zLjA2OSAtMy45MDYgLTUuMDIyIC0xLjExNiAtNy41MzNxMCAtMi4yMzIgLS41NTggLTExLjE2dC0uMjc5IC0xNC43ODcgMS42NzQgLTEzLjExMyA1LjU4IC0xMC44ODEgMTEuNDM5IC0zLjYyN2gxNzguNTZxNjYuNDAyIDAgMTEzLjU1MyA0Ny4xNTF0NDcuMTUxIDExMy41NTN6Ii8+DQo8L2c+DQo8L3N2Zz4=`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/safari_pinned.svg
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `org/TR/2001/REC-SVG-20010904/DTD/svg10`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `nnrrrmrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrmmmmmmmnNmmmmmmrrmmNmmmmrr1111111111`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `3ALhWX2FWTsxm0rbmalnEmy71XlO69qAJh`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `22autoupdateVersionRefreshable`

Instances: 7

### Solution

Manually confirm that the Base64 data does not leak sensitive information, and that the data cannot be aggregated/used to exploit other vulnerabilities.

### Reference


* [ http://projects.webappsec.org/w/page/13246936/Information%20Leakage ](http://projects.webappsec.org/w/page/13246936/Information%20Leakage)


#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Information Disclosure - Suspicious Comments ](https://www.zaproxy.org/docs/alerts/10027/)



##### Informational (Low)

### Description

The response appears to contain suspicious comments which may help an attacker. Note: Matches made within script blocks or files are against the entire content not only comments.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `from`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `admin`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `administrator`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `bug`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `db`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `from`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `query`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `select`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `TODO`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `user`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `username`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/c029a6b2088014967102f8efaaf260dc7e0d3df5.js%3Fmeteor_js_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Where`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `from`

Instances: 13

### Solution

Remove all comments that return information that may help an attacker and fix any underlying problems they refer to.

### Reference



#### CWE Id: [ 200 ](https://cwe.mitre.org/data/definitions/200.html)


#### WASC Id: 13

#### Source ID: 3

### [ Modern Web Application ](https://www.zaproxy.org/docs/alerts/10109/)



##### Informational (Medium)

### Description

The application appears to be a modern web application. If you need to explore it automatically then the Ajax Spider may well be more effective than the standard one.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script>/* eslint-disable */

'use strict';
(function() {
	var debounce = function debounce(func, wait, immediate) {
		var timeout = void 0;
		return function () {
			var _this = this;

			for (var _len = arguments.length, args = Array(_len), _key = 0; _key < _len; _key++) {
				args[_key] = arguments[_key];
			}

			var later = function later() {
				timeout = null;
				!immediate && func.apply(_this, args);
			};

			var callNow = immediate && !timeout;
			clearTimeout(timeout);
			timeout = setTimeout(later, wait);
			callNow && func.apply(this, args);
		};
	};

	var cssVarPoly = {
		test: function test() {
			return window.CSS && window.CSS.supports && window.CSS.supports('(--foo: red)');
		},
		init: function init() {
			if (this.test()) {
				return;
			}

			console.time('cssVarPoly');
			cssVarPoly.ratifiedVars = {};
			cssVarPoly.varsByBlock = [];
			cssVarPoly.oldCSS = [];
			cssVarPoly.findCSS();
			cssVarPoly.updateCSS();
			console.timeEnd('cssVarPoly');
		},
		findCSS: function findCSS() {
			var styleBlocks = Array.prototype.concat.apply([], document.querySelectorAll('#css-variables, link[type="text/css"].__meteor-css__'));
			var counter = 1;
			styleBlocks.map(function (block) {
				if (block.nodeName === 'STYLE') {
					var theCSS = block.innerHTML;
					cssVarPoly.findSetters(theCSS, counter);
					cssVarPoly.oldCSS[counter++] = theCSS;
				} else if (block.nodeName === 'LINK') {
					var url = block.getAttribute('href');
					cssVarPoly.oldCSS[counter] = '';
					cssVarPoly.getLink(url, counter, function (counter, request) {
						cssVarPoly.findSetters(request.responseText, counter);
						cssVarPoly.oldCSS[counter++] = request.responseText;
						cssVarPoly.updateCSS();
					});
				}
			});
		},
		findSetters: function findSetters(theCSS, counter) {
			cssVarPoly.varsByBlock[counter] = theCSS.match(/(--[^:; ]+:..*?;)/g);
		},


		updateCSS: debounce(function () {
			cssVarPoly.ratifySetters(cssVarPoly.varsByBlock);
			cssVarPoly.oldCSS.filter(function (e) {
				return e;
			}).forEach(function (css, id) {
				var newCSS = cssVarPoly.replaceGetters(css, cssVarPoly.ratifiedVars);
				var el = document.querySelector('#inserted' + id);

				if (el) {
					el.innerHTML = newCSS;
				} else {
					var style = document.createElement('style');
					style.type = 'text/css';
					style.innerHTML = newCSS;
					style.classList.add('inserted');
					style.id = 'inserted' + id;
					document.getElementsByTagName('head')[0].appendChild(style);
				}
			});
		}, 100),

		replaceGetters: function replaceGetters(oldCSS, varList) {
			return oldCSS.replace(/var\((--.*?)\)/gm, function (all, variable) {
				return varList[variable];
			});
		},
		ratifySetters: function ratifySetters(varList) {
			varList.filter(function (curVars) {
				return curVars;
			}).forEach(function (curVars) {
				curVars.forEach(function (theVar) {
					var matches = theVar.split(/:\s*/);
					cssVarPoly.ratifiedVars[matches[0]] = matches[1].replace(/;/, '');
				});
			});
			Object.keys(cssVarPoly.ratifiedVars).filter(function (key) {
				return cssVarPoly.ratifiedVars[key].indexOf('var') > -1;
			}).forEach(function (key) {
				cssVarPoly.ratifiedVars[key] = cssVarPoly.ratifiedVars[key].replace(/var\((--.*?)\)/gm, function (all, variable) {
					return cssVarPoly.ratifiedVars[variable];
				});
			});
		},
		getLink: function getLink(url, counter, success) {
			var request = new XMLHttpRequest();
			request.open('GET', url, true);
			request.overrideMimeType('text/css;');

			request.onload = function () {
				if (request.status >= 200 && request.status < 400) {
					if (typeof success === 'function') {
						success(counter, request);
					}
				} else {
					console.warn('an error was returned from:', url);
				}
			};

			request.onerror = function () {
				console.warn('we could not get anything from:', url);
			};

			request.send();
		}
	};
	var stateCheck = setInterval(function () {
		if (document.readyState === 'complete' && typeof Meteor !== 'undefined') {
			clearInterval(stateCheck);
			cssVarPoly.init();
		}
	}, 100);

	var DynamicCss = {};

	DynamicCss.test = function () {
		return window.CSS && window.CSS.supports && window.CSS.supports('(--foo: red)');
	};

	DynamicCss.run = debounce(function () {
		var replace = arguments.length > 0 && arguments[0] !== undefined ? arguments[0] : false;

		if (replace) {
			var colors = RocketChat.settings.collection.find({
				_id: /theme-color-rc/i
			}, {
				fields: {
					value: 1,
					editor: 1
				}
			}).fetch().filter(function (color) {
				return color && color.value;
			});

			if (!colors) {
				return;
			}

			var css = colors.map(function (_ref) {
				var _id = _ref._id,
						value = _ref.value,
						editor = _ref.editor;

				if (editor === 'expression') {
					return '--' + _id.replace('theme-color-', '') + ': var(--' + value + ');';
				}

				return '--' + _id.replace('theme-color-', '') + ': ' + value + ';';
			}).join('\n');
			document.querySelector('#css-variables').innerHTML = ':root {' + css + '}';
		}

		cssVarPoly.init();
	}, 1000);
})();
</script>`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script>/* eslint-disable */

'use strict';
(function() {
	var debounce = function debounce(func, wait, immediate) {
		var timeout = void 0;
		return function () {
			var _this = this;

			for (var _len = arguments.length, args = Array(_len), _key = 0; _key < _len; _key++) {
				args[_key] = arguments[_key];
			}

			var later = function later() {
				timeout = null;
				!immediate && func.apply(_this, args);
			};

			var callNow = immediate && !timeout;
			clearTimeout(timeout);
			timeout = setTimeout(later, wait);
			callNow && func.apply(this, args);
		};
	};

	var cssVarPoly = {
		test: function test() {
			return window.CSS && window.CSS.supports && window.CSS.supports('(--foo: red)');
		},
		init: function init() {
			if (this.test()) {
				return;
			}

			console.time('cssVarPoly');
			cssVarPoly.ratifiedVars = {};
			cssVarPoly.varsByBlock = [];
			cssVarPoly.oldCSS = [];
			cssVarPoly.findCSS();
			cssVarPoly.updateCSS();
			console.timeEnd('cssVarPoly');
		},
		findCSS: function findCSS() {
			var styleBlocks = Array.prototype.concat.apply([], document.querySelectorAll('#css-variables, link[type="text/css"].__meteor-css__'));
			var counter = 1;
			styleBlocks.map(function (block) {
				if (block.nodeName === 'STYLE') {
					var theCSS = block.innerHTML;
					cssVarPoly.findSetters(theCSS, counter);
					cssVarPoly.oldCSS[counter++] = theCSS;
				} else if (block.nodeName === 'LINK') {
					var url = block.getAttribute('href');
					cssVarPoly.oldCSS[counter] = '';
					cssVarPoly.getLink(url, counter, function (counter, request) {
						cssVarPoly.findSetters(request.responseText, counter);
						cssVarPoly.oldCSS[counter++] = request.responseText;
						cssVarPoly.updateCSS();
					});
				}
			});
		},
		findSetters: function findSetters(theCSS, counter) {
			cssVarPoly.varsByBlock[counter] = theCSS.match(/(--[^:; ]+:..*?;)/g);
		},


		updateCSS: debounce(function () {
			cssVarPoly.ratifySetters(cssVarPoly.varsByBlock);
			cssVarPoly.oldCSS.filter(function (e) {
				return e;
			}).forEach(function (css, id) {
				var newCSS = cssVarPoly.replaceGetters(css, cssVarPoly.ratifiedVars);
				var el = document.querySelector('#inserted' + id);

				if (el) {
					el.innerHTML = newCSS;
				} else {
					var style = document.createElement('style');
					style.type = 'text/css';
					style.innerHTML = newCSS;
					style.classList.add('inserted');
					style.id = 'inserted' + id;
					document.getElementsByTagName('head')[0].appendChild(style);
				}
			});
		}, 100),

		replaceGetters: function replaceGetters(oldCSS, varList) {
			return oldCSS.replace(/var\((--.*?)\)/gm, function (all, variable) {
				return varList[variable];
			});
		},
		ratifySetters: function ratifySetters(varList) {
			varList.filter(function (curVars) {
				return curVars;
			}).forEach(function (curVars) {
				curVars.forEach(function (theVar) {
					var matches = theVar.split(/:\s*/);
					cssVarPoly.ratifiedVars[matches[0]] = matches[1].replace(/;/, '');
				});
			});
			Object.keys(cssVarPoly.ratifiedVars).filter(function (key) {
				return cssVarPoly.ratifiedVars[key].indexOf('var') > -1;
			}).forEach(function (key) {
				cssVarPoly.ratifiedVars[key] = cssVarPoly.ratifiedVars[key].replace(/var\((--.*?)\)/gm, function (all, variable) {
					return cssVarPoly.ratifiedVars[variable];
				});
			});
		},
		getLink: function getLink(url, counter, success) {
			var request = new XMLHttpRequest();
			request.open('GET', url, true);
			request.overrideMimeType('text/css;');

			request.onload = function () {
				if (request.status >= 200 && request.status < 400) {
					if (typeof success === 'function') {
						success(counter, request);
					}
				} else {
					console.warn('an error was returned from:', url);
				}
			};

			request.onerror = function () {
				console.warn('we could not get anything from:', url);
			};

			request.send();
		}
	};
	var stateCheck = setInterval(function () {
		if (document.readyState === 'complete' && typeof Meteor !== 'undefined') {
			clearInterval(stateCheck);
			cssVarPoly.init();
		}
	}, 100);

	var DynamicCss = {};

	DynamicCss.test = function () {
		return window.CSS && window.CSS.supports && window.CSS.supports('(--foo: red)');
	};

	DynamicCss.run = debounce(function () {
		var replace = arguments.length > 0 && arguments[0] !== undefined ? arguments[0] : false;

		if (replace) {
			var colors = RocketChat.settings.collection.find({
				_id: /theme-color-rc/i
			}, {
				fields: {
					value: 1,
					editor: 1
				}
			}).fetch().filter(function (color) {
				return color && color.value;
			});

			if (!colors) {
				return;
			}

			var css = colors.map(function (_ref) {
				var _id = _ref._id,
						value = _ref.value,
						editor = _ref.editor;

				if (editor === 'expression') {
					return '--' + _id.replace('theme-color-', '') + ': var(--' + value + ');';
				}

				return '--' + _id.replace('theme-color-', '') + ': ' + value + ';';
			}).join('\n');
			document.querySelector('#css-variables').innerHTML = ':root {' + css + '}';
		}

		cssVarPoly.init();
	}, 1000);
})();
</script>`

Instances: 2

### Solution

This is an informational alert and so no changes are required.

### Reference




#### Source ID: 3

### [ Non-Storable Content ](https://www.zaproxy.org/docs/alerts/10049/)



##### Informational (Medium)

### Description

The response contents are not storable by caching components such as proxy servers. If the response does not contain sensitive, personal or user-specific information, it may benefit from being stored and cached, to improve performance.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `private`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/robots.txt
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `private`

Instances: 2

### Solution

The content may be marked as storable by ensuring that the following conditions are satisfied:
The request method must be understood by the cache and defined as being cacheable ("GET", "HEAD", and "POST" are currently defined as cacheable)
The response status code must be understood by the cache (one of the 1XX, 2XX, 3XX, 4XX, or 5XX response classes are generally understood)
The "no-store" cache directive must not appear in the request or response header fields
For caching by "shared" caches such as "proxy" caches, the "private" response directive must not appear in the response
For caching by "shared" caches such as "proxy" caches, the "Authorization" header field must not appear in the request, unless the response explicitly allows it (using one of the "must-revalidate", "public", or "s-maxage" Cache-Control response directives)
In addition to the conditions above, at least one of the following conditions must also be satisfied by the response:
It must contain an "Expires" header field
It must contain a "max-age" response directive
For "shared" caches such as "proxy" caches, it must contain a "s-maxage" response directive
It must contain a "Cache Control Extension" that allows it to be cached
It must have a status code that is defined as cacheable by default (200, 203, 204, 206, 300, 301, 404, 405, 410, 414, 501).   

### Reference


* [ https://tools.ietf.org/html/rfc7234 ](https://tools.ietf.org/html/rfc7234)
* [ https://tools.ietf.org/html/rfc7231 ](https://tools.ietf.org/html/rfc7231)
* [ http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html (obsoleted by rfc7234) ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html (obsoleted by rfc7234))


#### CWE Id: [ 524 ](https://cwe.mitre.org/data/definitions/524.html)


#### WASC Id: 13

#### Source ID: 3

### [ Storable and Cacheable Content ](https://www.zaproxy.org/docs/alerts/10049/)



##### Informational (Medium)

### Description

The response contents are storable by caching components such as proxy servers, and may be retrieved directly from the cache, rather than from the origin server by the caching servers, in response to similar requests from other users.  If the response data is sensitive, personal or user-specific, this may result in sensitive information being leaked. In some cases, this may even result in a user gaining complete control of the session of another user, depending on the configuration of the caching components in use in their environment. This is primarily an issue where "shared" caching servers such as "proxy" caches are configured on the local network. This configuration is typically found in corporate or educational environments, for instance.

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/9b704c621adc8a1dcae59307e0023894dbfd2413.css%3Fmeteor_css_resource=true
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=31536000`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/sitemap.xml
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/theme.css%3F1807b422d007328786a00d34e6c63ee6022dd2b3
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``

Instances: 3

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

### [ Storable but Non-Cacheable Content ](https://www.zaproxy.org/docs/alerts/10049/)



##### Informational (Medium)

### Description

The response contents are storable by caching components such as proxy servers, but will not be retrieved directly from the cache, without validating the request upstream, in response to similar requests from other users. 

* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon.svg
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=0`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon_16.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=0`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/favicon_32.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=0`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/safari_pinned.svg
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=0`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/assets/touchicon_180.png
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=0`
* URL: https://rocketchat-bruce-59e31e-dev.apps.klab.devops.gov.bc.ca/images/manifest.json
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `max-age=0`

Instances: 6

### Solution



### Reference


* [ https://tools.ietf.org/html/rfc7234 ](https://tools.ietf.org/html/rfc7234)
* [ https://tools.ietf.org/html/rfc7231 ](https://tools.ietf.org/html/rfc7231)
* [ http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html (obsoleted by rfc7234) ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html (obsoleted by rfc7234))


#### CWE Id: [ 524 ](https://cwe.mitre.org/data/definitions/524.html)


#### WASC Id: 13

#### Source ID: 3


