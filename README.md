# Cybersecurity

## week8-Cybersecurity
Dekuwin E. I. Kogda

# Project 7- Pentesting Live Targets

Time spent: **10** hours spent in total

> Objective: Identify which two vulnerabilities the blue target has, which two vulnerabilities the green target has, and which two vulnerabilities the red target has

# Pentesting Report

### Authenticated Stored Cross-Site Scripting (XSS)

#### Summary
- Vulnerability types: Cross-Site Scripting (XSS)
- Tested in version: 4.2.0
- Fixed in version: 4.2.3
  
  
  
#### GIF Walkthrough 
![](week7p3.gif?raw=true)


#### Steps to recreate: 
  - Login as the admin
  - Create a new post
  - In the body of the post, insert the following shortcode:

    ```<a href="[caption code=">]</a><a title=" onmouseover=alert('pwnd!')  ">link</a>```

- Commit the changes to the post and click on `view post` link 
- An alert window will pop up with the message `pwnd!`

#### Affected source code:
- [WPScan Vulnerability Database Vulnerability #8111](https://wpvulndb.com/vulnerabilities/8111)
- [WordPress Codex for v4.2.3](https://codex.wordpress.org/Version_4.2.3)


### Unauthenticated Stored Cross-Site Scripting (XSS)

#### Summary
- Vulnerability types: Cross-Site Scripting (XSS)
- Tested in version: 4.2.0
- Fixed in version: 4.2.1

#### GIF Walkthrough 
![](week7p2.gif?raw=true)

#### Steps to recreate
  - Create a comment as a regular user.
  - This comment is then accepted by the admin.
  - Using the same information as the first comment, add the following line of code in the `comment` form:
    
    `<a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a>`
- Since once the given credential has been accepted to give comment, the next comment does not need to be approved by the administrator any longer.
- When the admin logged themself into WP and click on the comment section of the post where the XSS script is located, the script will be executed. 
- An alert window will pop up with the message `hello world`

#### Affected source code
- [WPScan Vulnerability Database Vulnerability #7945](https://wpvulndb.com/vulnerabilities/7945)
- [Letter by Jouko Pynnönen Regarding the Discovery of the Vulnerability](https://packetstormsecurity.com/files/131644/)


### Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds

#### Summary
- Vulnerability types: Cross-Site Scripting (XSS)
- Tested in version: 4.2.0
- Fixed in version: 4.2.13

#### GIF Walkthrough 
![](week7P1.gif?raw=true)

#### Steps to recreate
  - Create a new post as an admin.
  - Inside the body of the new post, insert the following shortcode:

    `[embed src='https://youtube.com/embed/12345\x3csvg onload=alert("pwnd!")\x3e'][/embed]`
- Save the change and click on `view post` link
- An alert window will pop up with the message `pwn`

#### Affected source code
- [WPScan Vulnerability Database Vulnerability #8768](https://wpvulndb.com/vulnerabilities/8768)
- [GitHub Commit History on this Issue](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)


## Assets

There are no other scripts or file that were used to complete this assignment

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs are created with [LiceCap](http://www.cockos.com/licecap/)

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [2018] [Dekuwin E. I. Kogda]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
