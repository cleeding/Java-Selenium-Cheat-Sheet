<h1>Java Selenium Cheat Sheet</h1>
<h2>Drivers</h2>
<p><strong>Chrome:</strong><br>System.setProperty("webdriver.chrome.driver", "Chromedriver filepath");</p>
<p><strong>Firefox:</strong><br>System.setProperty("webdriver.gecko.driver", "Geckodriver filepath");</p>
<p><strong>Internet Explorer:</strong><br>System.setProperty("webdriver.ie.driver", "IE filepath");</p>
<p>//Class object reference to the Webdriver Interface<br>WebDriver driver = new ChromeDriver();</p>
<h2>Basic Methods</h2>
<ul>
<li>driver.get("https://www.google.com");</li>
<li>driver.getTitle();</li>
<li>driver.getCurrentUrl();</li>
<li>driver.getPageSource();</li>
<li>driver.navigate().to();</li>
<li>driver.navigate().back();</li>
<li>driver.findElement(By.id("#")).sendKeys("#");</li>
<li>driver.findElement(By.id("#")).click();</li>
<li>driver.close(); //Closes current Window</li>
<li>driver.quit(); //Closes entire browser</li>
<li>driver.manage().window().maximize() ;</li>
</ul>
<h2>Locator Hierarchy</h2>
<ol>
<li>ID - driver.findElement(By.id("menu")); //Alpha numeric ID may change on refresh so check</li>
<li>Name - driver.findElement(By.name("home"));</li>
<li>Linktext - driver.findElement(By.Linktext("Read on Wikipedia"));</li>
<li>Partial Linktext - driver.findElement(By.PartialLinkText("Wikipedia"));</li>
<li>Tag Name - driver.findElement(By.TagName("a"));</li>
<li>Class Name - driver.findElement(By.ClassName("contaner-top")); //Classes should not have spaces - use CSS/Xpath for compound classes</li>
<li>CSS - driver.findElement(By.CssSelector(".top-menu&gt;li"));</li>
<li>CSS standard // tagName[attribute='value'] or [attribute='value']  for id can also do tagName#id_value or #id_value and also tagName.className_value //to check CSS in browser $("")</li>
<li>CSS regular expression - tagName[Attribute*='value']
</li><li>Xpath - driver.findElement(By.XPath("//*[@id='top-menu']/li")); //Ignore Xpath if starts from HTML - not available</li>
<li>Xpath standard // //tagName[@attribute='value'] or //*[@attribute='value'] and to check in browser $x("//tagName[@attribute='value']")</li>
<li>Xpath regular expression - //tagName[contains(@attribute, 'value')]</li>
</ol>For multiple values such as class name, Selenium identifies first one scanning top left first<br>
<h2>Static dropdown</h2>
<p>Select s = new Select(driver.findElement(By.Id("#"));<br>
s.selectByVisibleText("Apple"); and s.deselectByVisibleText("Apple");<br>
s.selectByValue("4"); and s.deselectByValue("4");<br>
s.selectByIndex(2); and s.deselectByIndex(2);
</p>
<h2>JavaScript pop-ups</h2>
<p>System.out.println(driver.switchTo().alert().getText());<br>
//driver.switchTo().alert().sendKeys("dog");<br>
driver.switchTo().alert().accept(); //Accept = ok done yes<br>
//driver.switchTo().alert().dismiss();
</p>
<h2>Waits</h2>
<p><strong>Implict</strong><br><br>driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS); //wait x amount of time before throwing no such element exception, applies to all elements<br><br><strong>Explicit</strong></p>
<p>WebDriverWait wait=new WebDriverWait(driver, 20); //wait for certains conditions or maxmium amount of time exceeded, specific elements<br>WebElement element;<br>element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("#")));</p>
<p><strong>Fluent</strong> // type of explicit wait with maximum amount of time to wait condition but also frequency to check the condition<br><br> // Waiting 30 seconds for an element to be present on the page, checking<br> // for its presence once every 5 seconds.<br> Wait&lt;WebDriver&gt; wait = new FluentWait&lt;WebDriver&gt;(driver)<br> .withTimeout(30, SECONDS)<br> .pollingEvery(5, SECONDS)<br> .ignoring(NoSuchElementException.class);</p>
<p>WebElement foo = wait.until(new Function&lt;WebDriver, WebElement&gt;() {<br> public WebElement apply(WebDriver driver) {<br> return driver.findElement(By.id("foo"));<br> }<br> });</p>
<p><strong>Sleep Thread</strong><br><br>Thread.sleep(5000);&nbsp;</p>
<h2>Misc.</h2>
<h3>Retrieve attribute values (Button text)</h3><ul>

</ul>
<p>driver.findElement(By.XPath("//input[@name='submit']")).getAttribute("value");</p>
<h3>Control + Click (Click on element opens new tab)</h3><ul>

</ul>
<p>Actions action = new Actions(driver);<br>action.keyDown(Keys.CONTROL).build().perform();<br>driver.findElement(By.className("#")).click();<br>action.keyUp(Keys.CONTROL).build().perform();</p>
<h3>Kill chromedriver.exe instances in Task Manager with batch file</h3><ul>

</ul>
<p>Create a .bat file with input "taskkill /F /IM ChromeDriver.exe" and open when you want to close multiple chromedriver instances</p>