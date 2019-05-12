<h1>Java Selenium Cheat Sheet</h1>
<h2>Drivers</h2>
<p><strong>Chrome:</strong><br />System.setProperty(&ldquo;webdriver.chrome.driver&rdquo;, &ldquo;Chromedriver filepath&rdquo;);</p>
<p><strong>Firefox:</strong><br />System.setProperty(&ldquo;webdriver.gecko.driver&rdquo;, &ldquo;Geckodriver filepath&rdquo;);<br /><br /><strong>Internet Explorer:</strong><br />System.setProperty(&ldquo;webdriver.ie.driver&rdquo;, &ldquo;IE filepath&rdquo;);</p>
<p>//Class object reference to the Webdriver Interface<br />WebDriver driver = new ChromeDriver();</p>
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
<li>ID - driver.findElement(By.id("menu"));</li>
<li>Name - driver.findElement(By.name("home"));</li>
<li>Linktext - driver.findElement(By.Linktext("Read on Wikipedia"));</li>
<li>Partial Linktext - driver.findElement(By.PartialLinkText("Wikipedia"));</li>
<li>Tag Name - driver.findElement(By.TagName("a"));</li>
<li>Class Name - driver.findElement(By.ClassName("contaner-top"));</li>
<li>CSS - driver.findElement(By.CssSelector(".top-menu&gt;li"));</li>
<li>Xpath - driver.findElement(By.XPath("//*[@id='top-menu']/li"));</li>
</ol>
<h2>Waits</h2>
<p><strong>Implict</strong><br /><br />driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS); //wait x amount of time before throwing no such element exception, applies to all elements<br /><br /><strong>Explicit</strong></p>
<p>WebDriverWait wait=new WebDriverWait(driver, 20); //wait for certains conditions or maxmium amount of time exceeded, specific elements<br />WebElement element;<br />element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("#")));</p>
<p><strong>Fluent</strong> // type of explicit wait with maximum amount of time to wait condition but also frequency to check the condition<br /><br /> // Waiting 30 seconds for an element to be present on the page, checking<br /> // for its presence once every 5 seconds.<br /> Wait&lt;WebDriver&gt; wait = new FluentWait&lt;WebDriver&gt;(driver)<br /> .withTimeout(30, SECONDS)<br /> .pollingEvery(5, SECONDS)<br /> .ignoring(NoSuchElementException.class);</p>
<p>WebElement foo = wait.until(new Function&lt;WebDriver, WebElement&gt;() {<br /> public WebElement apply(WebDriver driver) {<br /> return driver.findElement(By.id("foo"));<br /> }<br /> });</p>
<p><strong>Sleep Thread</strong><br /><br />Thread.sleep(5000);&nbsp;</p>
<h2>Misc.</h2>
<ul>
<li>Retrieve attribute values (Button text)</li>
</ul>
<p>driver.findElement(By.XPath("//input[@name='submit']")).getAttribute("value");</p>
<ul>
<li>Control + Click (Click on element opens new tab)</li>
</ul>
<p>Actions action = new Actions(driver);<br />action.keyDown(Keys.CONTROL).build().perform();<br />driver.findElement(By.className("#")).click();<br />action.keyUp(Keys.CONTROL).build().perform();</p>
<ul>
<li>Kill chromedriver.exe instances in Task Manager with batch file</li>
</ul>
<p>Create a .bat file with input "taskkill /F /IM ChromeDriver.exe" and open when you want to close multiple chromedriver instances</p>