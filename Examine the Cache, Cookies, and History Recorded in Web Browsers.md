
# Windows Forensic Investigation (5-Examine the Cache, Cookies, and History Recorded in Web Browsers) :desktop_computer:

![Windows Forensics Methodology](https://miro.medium.com/v2/resize:fit:700/1*0O6nu1EvgXNUmJVzRTJsXQ.png)

The Windows forensics methodology passes with 8 phases, we have discussed the first four before. If you are interested in reading about them you can use the following links:

> _1- Gathering Volatile Information:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/1-%20Gathering%20Volatile%20Information.md)_
> 
> _2- Collecting Non-volatile Information:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/2-%20Collecting%20Non-volatile%20Information.md
)_
> 
> _3- Memory Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/3-%20Memory%20Analysis.md)_
> 
> _4- Registry Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/4-%20Registry%20Analysis.md)_

## Definition

_By examining the cache, cookie, and history recorded in web browsers, investigators can gain valuable insights into a user’s internet activity, which can be used to build a comprehensive picture of their behavior and activities online. This information can be critical in forensic investigations, particularly in cases where internet activity may have played a role in a crime or incident._

***Cache:***

_Firstly, the web browser cache contains temporary files that are created when a user visits websites. These files can include images, videos, and other media that the user has viewed, and can provide valuable information about the user’s internet activity, such as the websites they have visited, the files they have downloaded, and the searches they have conducted._

***Cookies:***

_Secondly, cookies are small text files that are created by websites and stored on the user’s computer. They can be used to track a user’s activity across different websites and sessions, and can provide information such as login credentials, preferences, and browsing habits._

***History:***

_Finally, the browser history provides a record of the user’s browsing activity, including the websites they have visited and the time and date of their visits. This can be particularly useful for investigators looking to trace a user’s online activities and build a timeline of their behavior._

> Today’s blog is a straight forward guide on how you can extract cache, cookies, and history from the any browser using  [nirsoft freeware](https://www.nirsoft.net/utils/)

_Directly navigate to the targeted task and download the necessary tools based on the browser you are facing._

## Cache

_The below listed tools read the cache folder of web browser, and displays the list of all files currently stored in the cache._

For each cache file, the following information is displayed: URL, Content type, File size, Last modified time, Last fetched time, Expiration time, Fetch count, Server name, and more.

> [***Internet Explorer Cache Viewer***](https://www.nirsoft.net/utils/ie_cache_viewer.html)
> 
> [***Mozilla Firefox Cache Viewer***](https://www.nirsoft.net/utils/mozilla_cache_viewer.html)
> 
> [***Google Chrome Cache Viewer***](https://www.nirsoft.net/utils/chrome_cache_view.html)
> 
> [***Safari Cache Viewer***](https://www.nirsoft.net/utils/safari_cache_view.html)
> 
> [***Opera Cache Viewer***](https://www.nirsoft.net/utils/opera_cache_view.html)

# **Cookies**

_This utility displays the details of all cookies that Internet Explorer stores on your computer. In addition, it allows you to change the content of the cookies, delete unwanted cookies files, save the cookies into a readable text file, find cookies by specifying the domain name, view the cookies of other users and in other computers, etc._

> [***Internet Explorer Cookies Viewer***](https://www.nirsoft.net/utils/iecookies.html)
> 
> [***Edge Cookies Viewer***](https://www.nirsoft.net/utils/edge_cookies_view.html)
> 
> [***Mozilla Firefox Cookies Viewer***](https://www.nirsoft.net/utils/mzcv.html)
> 
> [***Google Chrome Cookies Viewer***](https://www.nirsoft.net/utils/chrome_cookies_view.html)
> 
> [***Flash Cookies Viewer***](http://flashcookiesview%20v1.15/)

# **History**

_This utility reads all information from the history file on your computer, and displays the list of all URLs that you have visited with browsers in the last few days. It also allows you to select one or more URL addresses, and then remove them from the history file or save them into text, HTML or XML file. In addition, you are allowed to view the visited URL list of other user profiles on your computer, and even access the visited URL list on a remote computer, as long as you have permission to access the history folder._

> [***Internet Explorer History Viewer***](https://www.nirsoft.net/utils/iehv.html)
> 
> [***Mozilla Firefox History Viewer***](https://www.nirsoft.net/utils/mozilla_history_view.html)
> 
> [***Google Chrome History Viewer***](https://www.nirsoft.net/utils/chrome_history_view.html)
> 
> [***Safari History Viewer***](https://www.nirsoft.net/utils/safari_history_view.html)
> 
> [***The Four-mentioned-at-once***](https://www.nirsoft.net/utils/browsing_history_view.html)

# Extra ([**WebBrowserPassView**](https://www.nirsoft.net/utils/web_browser_password.html))

_[nirsoft](http://nirsoft.net/) has also a password recovery tool that reveals the passwords stored by the following Web browsers: Internet Explorer, Mozilla Firefox, Google Chrome, and Opera._

>_This tool can be used to recover your lost/forgotten password of any Website, including popular Web sites, like Facebook, Yahoo, Google, and Gmail, as long as the password is stored by your Web Browser. After retrieving your lost passwords, you can save them into text/html/csv/xml file._
