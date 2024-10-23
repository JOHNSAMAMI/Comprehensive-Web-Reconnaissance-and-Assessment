# Comprehensive-Web-Reconnaissance-and-Assessment
 Project Overview
This project involves a comprehensive security assessment of the Damn Vulnerable Web Application (DVWA), specifically the XVWA site hosted on a local server. The assessment aims to identify security vulnerabilities using various penetration testing tools, culminating in a high-level report that details the findings, vulnerabilities, and recommended mitigation strategies.
Business Understanding
In today's digital landscape, ensuring the security of web applications is paramount for protecting sensitive data and maintaining user trust. The company recognizes the importance of identifying potential vulnerabilities in their web applications to safeguard against cyber threats. By conducting this security assessment, the organization seeks to enhance its security posture, comply with best practices, and protect its assets from unauthorized access and exploitation.
Tools and Frameworks
•	OWASP ZAP: An open-source web application security scanner used to discover vulnerabilities through spidering and active scanning.
•	DIRB: A command-line tool designed to discover directories and files on a web server by using a wordlist.
•	Prober: A penetration testing tool included in Kali Linux that helps identify server software and potential vulnerabilities based on versioning.
Project Description
The assessment began with a thorough evaluation of the XVWA site hosted at http://192.168.1.11/xvwa/. The initial phase involved utilizing the OWASP ZAP Spider tool to map the web application's structure. 
Steps taken in this assessment:
1. OWASP ZAP Spider Assessment
•	Preparation:
o	Launched the OWASP ZAP tool on the testing environment.
o	Configured ZAP with the target URL: http://192.168.1.11/xvwa/.
•	Spidering Process:
o	Initiated the spider scan to crawl the XVWA site.
o	Allowed the spider to automatically discover and map all reachable resources (files and directories) on the site.
Screenshots 1a-1c
After the scan completed, reviewed the generated site map and captured a screenshot of the site map, showing the expanded view of the XVWA domain tree. The spider revealed a total of N files and directories, showcasing the publicly accessible components of the application.
Following the initial assessment, a deeper analysis was conducted using DIRB to uncover hidden directories that may not be visible to traditional scanning methods. 
 DIRB Directory Scanning
•	Preparation:
o	Opened a terminal in Kali Linux where DIRB is installed.
o	Specified the target URL: http://192.168.1.11/xvwa/.
•	Running the Scan:
o	Executed the DIRB command to start a directory brute-forcing scan.
o	Used a standard wordlist to probe for hidden directories and files on the web server.
•	Review of Results:
o	Analyzed the output for discovered directories and files.
o	Noted status codes for each found resource (e.g., 200 OK).
o	Captured a screenshot of the scan results for inclusion in the report.
Screenshots 2a & 2b
Key Findings from DIRB:
The scan revealed the following directories, all returning a status code of 200:
•	/git/HEAD - Potentially sensitive version control information.
•	/css/ - Contains style sheets; identified as listable.
•	/js/ - Contains JavaScript files; identified as listable.
•	/php.ini - Configuration file that could expose sensitive information.
•	/setup/ - Likely contains setup files that should not be publicly accessible.
Additional observations noted that several directories (/css/, /js/, /fonts/, /img/) were listable. This directory listing feature could allow unauthorized users to browse through these directories, leading to potential exploitation.
Next, Prober was employed to determine the server environment running on port 443. 
Prober Assessment
•	Preparation:
o	Launched the Prober tool on Kali Linux.
o	Specified the target for probing: http://192.168.1.11/xvwa/ on port 443.
•	Probing the Server:
o	Initiated the probing process to identify server software and versioning.
o	Allowed Prober to analyse the server's response and gather information about the underlying technologies.
•	Review of Results:
o	Compiled the findings on server software versions (OpenSSL, Apache Tomcat, and Windows XP IIS).
o	Captured a screenshot of the Prober results showing the identified server information.
Screenshots 3a-3c
Findings from Prober:
To further evaluate the server environment, Prober was utilized to probe the XVWA site on port 443. The analysis yielded the following results:
•	OpenSSL versions: Ranging from 0.9.8 to 1.0.2g. These versions are outdated and known to contain multiple vulnerabilities.
•	Apache Tomcat version: 7.0.55. This version has several known vulnerabilities that could be exploited if not patched.
•	Operating System: Identified as Windows XP Microsoft IIS 5.1, which is a deprecated platform with a known history of security issues.
Vulnerabilities Identified:
1.	Outdated OpenSSL: Known vulnerabilities exist in the older OpenSSL versions that could allow for exploits such as Heartbleed, leading to sensitive data leaks.
2.	Apache Tomcat Vulnerabilities: The version in use (7.0.55) has multiple CVEs associated with it, including remote code execution vulnerabilities.
3.	Windows XP and IIS 5.1 Risks:
o	Outdated OS: Windows XP is no longer supported, making it susceptible to numerous unpatched vulnerabilities.
o	IIS 5.1 Vulnerabilities: This web server version has a history of issues, including buffer overflows and directory traversal attacks, that could allow for unauthorized access.

Conclusion
The assessment of the XVWA site revealed several security vulnerabilities and weaknesses due to outdated software and configuration issues. Immediate action is recommended, including upgrading to a modern operating system and web server, applying available patches, and implementing strict access controls to mitigate potential risks. By addressing these vulnerabilities, the organization can significantly enhance its security posture and better protect its web applications from potential threats.


