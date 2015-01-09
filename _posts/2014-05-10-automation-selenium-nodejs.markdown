---
layout: post
title:  "Automation - Selenium - NodeJS"
date:   2014-05-10 
categories: jekyll update
---


### **Selenium** *NodeJS*

1. Download and Install NodeJS and NPM.
2. Setup browser driver.
	- Download ChromeDriver: [https://code.google.com/p/selenium/wiki/ChromeDriver]
	- Put chromedriver to ***PATH***.
3. Created a new **.js** file. Add below code and save. (eg. **.js** named *fortest.js* and save to ***uiauto*** folder)

	```
	var webdriver = require('selenium-webdriver');
 	var driver = new webdriver.Builder().
 	   withCapabilities(webdriver.Capabilities.chrome()).
 	   build();
 	
 	driver.get('http://www.baidu.com');
 	driver.sleep(2000);
 	driver.findElement(webdriver.By.id('kw1')).sendKeys('webdriver');
 	driver.sleep(1000);
 	driver.findElement(webdriver.By.id('su1')).click();
 	driver.wait(function() {
 	 return driver.getTitle().then(function(title) {
 	   return title === 'webdriver_百度搜索';
 	 });
 	},
 	1000);
 	
 	//driver.
 	quit();
 	```

4. Install *selenium-webdriver* with npm.

    *** 1) Open command line and go to uiauto folder. ***
    
    ```npm install selenium-webdriver```

    *** 2) Run by node: ***
    
    ```node fortest.js```
