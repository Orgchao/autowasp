# Autowasp #
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

![picture](./images/Autowasp1.png)

Welcome to Autowasp, a Burp Suite extension that integrates Burp issues logging with OWASP Web Security Testing Guide (WSTG) to provide a streamlined web security testing flow for the modern-day penetration tester! This tool will guide new penetration testers to understand the best practices of web application security and automate OWASP WSTG checks. This README will provide an introduction of Autowasp and its key features, the steps to download it, how to use the tool and end off by sharing how security researchers and developers can make this tool better! 

# Existing features #

Currently, Autowasp supports the following functionalities:

 **1. Testing Checklist - Be guided by OWASP!**

 With the ability to fetch OWASP WSTG checklist, Autowasp aims to aid new penetration testers in conducting penetration testing or web application.
* Summary of OWASP WSTG test cases
* How to test – black/white box testing
* Relevant testing tools to aid your test
* Relevant testing tools to aid your test

![picture](./images/OWASP%20WSTG.PNG)
	 
 **2. Logger Tool - Log down the Vulns!**
 
Autowasp Logger tab provides penetration testers with the ability to extract and consolidate Burp Scanner issues. This extender tool will automate and flag vulnerable network traffic issues, allowing users to send vulnerable proxy items from Burp’s `proxy`, `intruder` and `repeater` tab to the extender. These vulnerable issues can then be mapped to WSTG IDs and be used to generate an Excel report upon engaging a penetration test.
	 ![picture](./images/Logger%20Tool.PNG)
	 ![trafficLogging](./images/trafficLogging.gif)

# Prerequisites #

 - Burp Suite (either Community or Professional)

# Dependencies #

- Apache commons collections 4.3
- Apache commons compress 1.18
- GSON 2.8.5
- Jsoup 1.12.1
- Apache POI 4.1.0
- XMLBeans 3.1.0

# Installation #
## Building the jar 
***Using IntelliJ IDE***

1. Clone the repository to a location of your choice
```
git clone https://github.com/imthomas93/Autowasp.git
```
2. Open IntelliJ, you can either import Project or Open Project  (***File > Open..***)
3. Head to ***File>Project Structure...*** (***Ctrl+Alt+Shift+S***)
4. Under ***Project Settings**, select ***Artifacts***, click the ***+***, add ***JAR*** and select ***Empty***
5. Replace ***unnamed*** with any name of your choice
6. Under Available Elements, Right-click and extract the following Maven libraries into Output Root
        1. commons-codec:1.12
        2. commons-collections:4.4.4
        3. commons-compress:1.18
        4. commons-math3:3.6.1
        5. curvesapi-1.06
        6. gson-2.8.5
        7. jsoup-1.12.1
        8. poi-4.1.0
        9. poi-ooxml-4.1.0
        10. poi-ooxml-schemas-4.1.0
        11. xmlbeans-3.1.0
7. Click Build Project (***Build > Build Project***)
8. The autowasp.jar file will be built in /repository location/out/artifacts/chosen_jar_name/chosen_jar_name.jar
***Alternatively, you can use the precompiled jar [here](https://github.com/imthomas93/Autowasp/releases)***

## Installing the jar
 1. Open Burp Suite
	 - Community version: 
		 - Temporary project with default/preferred settings
	 - Professional version: 
		 - Either temporary project or new/existing project
		 - Default/preferred settings
 2. Click on **Extender** located on the top row of tabs
 3. Under the **Extensions** tab on the second row, click **Add**
 4. Under **Extension Details**, click **Select file** and select the Autowasp JAR file, then click **Next**
 5. You should see no output or errors and a new tab labeled Autowasp on the top row.

# Usage

***A general testing workflow using Autowasp would include the following steps:***

  1. Display the OWASP checklist in Autowasp for reference.
  2. Add the target URL to scope and perform scanning.
  3. Map the scan issues to specific test cases in the checklist OR
  4. Manually explore the website's pages, then click “Enable Burp Scanner Logging” to display the scanner issues under the **Logger** tab
  5. Map findings to the checklist
  6. Insert security observations and evidence associated with the logs.
  7. Generate a report containing the checklist, logs, evidence, and comments. (**NOTE**: This feature only works for BurpSuite `v2020.9.1` and before only. We are currently working with PortSwigger for a fix)


## **1. Displaying the Testing checklist** ##

### First time: ###
1. Click the **Fetch WSTG Checklist** button to fetch the checklist from the forked [WSTG documentation](https://github.com/GovTech-CSG/www-project-web-security-testing-guide/blob/master/v42/4-Web_Application_Security_Testing/README.md) (Note: this may take a few minutes due to the number of pages)  
2. To avoid downloading the WSTG checklist every time, you may click **Save a Local WSTG Checklist** and save the checklist to your local machine. 
	![fetchChecklist](./images/fetchChecklist.gif)
	
### Subsequent times: ###
1. Choose **Load local checklist** to start your penetration testing work.
2. This should load the checklist almost instantly.
	![uploadChecklist](./images/uploadChecklist.gif)
	
### Excluding Checklist item(s): ###
* Find any of the testing item not applicable to your application testing, you can exclude these items by selecting the checkbox on the right. 

## **2. Adding to scope and scanning** ##
1. Add the target URL to scope and perform scan.
 ![addTargetScope](./images/addTargetScope.gif)
 
2. Manually explore the website's pages, then click **Enable Burp Scanner Logging** to display the scanner issues under the **Logger** tab.
 ![scannerLogic](./images/scannerLogic.gif)
 
3. Note that items from **Proxy -> HTTP History**, **Intruder** & **Repeater** tabs can be sent to Autowasp by right clicking on them, followed by clicking **Send to Autowasp**. 
 ![SendfromProxy](./images/SendfromProxy.gif)

## **3. Mapping findings to the checklist** ##

- Click on a specific log in the **Logger** table
- Click on the empty **Mapped to OWASP WSTG** field on the right side of the table entry.
- Choose a specific test to map the log to using the drop-down list
* Note that his will only work if you have the checklist already displayed
 ![mapToCheckList](./images/mapToCheckList.gif)

## **4. Inserting tester comments and evidence** ##
1. Click on a specific log in the **Logger** table
2. On the lowest row of tabs, click on either **Pen Tester Comments** or **Evidence**
3. Enter what you wish to note down, then click **Save Comments** or **Save Evidence**
 ![writeComments](./images/writeComments.gif)

## **5. Report Generation** ##

1. Click on **Generate Excel File** and choose a location to save the file to
2. Open the excel file and check that the observation, comments, and evidence, have been saved beside the associated test case
3. You can also find the URL pointing to the full article hosted on OWASP's GitHub repository for every test case in the checklist
 ![generateReport](./images/generateReport.gif)

# Contributing #

[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/govtech-csg/Autowasp/issues)

Do you have  ideas to make Autowasp even more useful? WWe welcome contributions from developers like yourself to improve the Autowasp tool and highlight any potential problems. Here are some important resources to get you started:

   * [Burp Extender APIs](https://portswigger.net/burp/extender/api/burp/package-summary.html)
   * [Singapore Government Developer Portal](https://www.developer.tech.gov.sg/) - leverage on our latest technological solutions, execute your digital projects, and join our community of developers.
   * If you find bugs, log us an [issue ticket](https://github.com/govtech-csg/Autowasp/issues) to report them. Do ensure the bug has not already been reported by searching on GitHub under Issues.
   * Have a question but unsure who to contact, drop us an email to Thomas_LIM@tech.gov.sg

## Submitting changes
Please send a [GitHub Pull Request to us](https://github.com/govtech-csg/Autowasp/pull/new/master) with a clear list of what you've done (read more about [pull requests](http://help.github.com/pull-requests/)). 

Always write a clear log message for your commits. We accept one-liners for small changes, but bigger changes should include changes and impact:
    $ git commit -m "A brief summary of the commit
    > 
    > A paragraph describing what changed and its impact."

## Coding conventions

Start reading our code and you'll get the hang of it. The code serves as an extention module to BurpSuite to extend functionality of web security testing. Autowasp uses the following coding conventions:

  * We use Java for this extender.
  * Some of the Burp extender' APIs have been overwritten in order for us to have better control of the extender’s behaviour. Refer to overwritten classes  [here](https://github.com/govtech-csg/Autowasp/tree/master/src/main/java/autowasp/http).
  * Please do not add additional table listener as it affects the user experience of the extender. That said, we welcome changes to make Autowasp better!
  * Add a comment whenever you include a new function so that we can understand your contribution better.

Autowasp is an open-source software so bear in mind that the open-source community can read your code. Do adhere to our coding conventions detailed in GitHub Readme and keep your codes understandable and easy to follow. Think of it like driving a car: you may love performing donuts, but you have to consider the well-being of your passengers and make the ride as smooth as possible. That is of course, <em>unless your passengers love the thrill as well.</em>

# Authors #

👤 **Thomas Lim**

 - Email: Thomas_LIM@tech.gov.sg
 - GitHub: [@imthomas93](https://github.com/imthomas93)

👤 **Yin Yi De**

- Email: YIN_Yide@tech.gov.sg
- GitHub: [@retaric](https://github.com/retaric)

👤 **Quek Kai Yu**

- Email: Kai_Yu_QUEK_from.tp@tech.gov.sg
- GitHub: [@kaiyu92](https://github.com/kaiyu92)

👤 **Aloysius Wang**

- Email: Aloysius_WANG@tech.gov.sg
- GitHub: [@aloy-wee-sious](https://github.com/aloy-wee-sious)

👤 **Matthew Ng**

- Email: Matthew_NG_from.TP@tech.gov.sg
- GitHub: [@matthewng1996](https://github.com/matthewng1996)



