#  Page Object Model in Selenium

## :black_nib: What is Page Object Model?

 POM is a design pattern in Selenium that creates an **Object Repository** for storing all web elements. In Page Object Model, consider each web page of an application as a class. Each class file will contain only corresponding web page elements.
 
 <br>

 ## :black_nib: Advantages of Page POM?
    
   :heavy_check_mark: **Easy Maintenance**: Ss every page is separate in POM, if there is any change in any webpage that can be easily detected. 

   :heavy_check_mark: **Reducing Code Duplication**: We can use a single object repository for different uses. we can integrate POM in Selenium with TestNG/JUnit for functional Testing and at the same time with JBehave/Cucumber for acceptance testing. 
   
   :heavy_check_mark: **Readability and Reliability**: We can easily identify actions that will be performed on a particular webpage by navigating through the java file.

<br>

:warning: Page objects themselves should never make ***verifications*** or ***assertions***  :warning: 

<br>


## :black_nib: What is PageFactory is Selenium?
Page Factory is a **class** provided by Selenium WebDriver to support Page Object Design patterns but it is very optimized.  It is used to initialize the elements of the Page Object or instantiate the Page Objects itself.

<br>

:one: **`@FindBy`**: An annotation used in Page Factory to locate and declare web elements. The @FindBy annotation supports :`id, name, className, css, tagName, linkText, partialLinkText, xpath`. Below is an example of declaring an element using @FindBy-

```
@FindBy(id="elementId")
WebElement element;
```

<br>

:two: **`initElements()`**: A `static` method in Page Factory class, it instantiate an instance of the given class. Also used to initialize all the web elements located by @FindBy annotation. 
```
public LoginPage(WebDriver driver) {           
         this.driver = driver; 
         PageFactory.initElements(driver, this);
}
```

<br>

:three: **Lazy Initialization**: `AjaxElementLocatorFactory` is a lazy load concept in Page Factory – page object design pattern to identify WebElements only when they are used in any operation.
```
AjaxElementLocatorFactory factory = new AjaxElementLocatorFactory(driver, 30);
PageFactory.initElements(driver, this);
```

<br>

## :black_nib: Differences between POM and PageFactory:

|Page Object Model|PageFactory|
|-----------------|-----------|
|Page Object Model is a design pattern|Page Factory expands on Page Object model<br> functionality by introducing more advanced<br> features|
|In POM, one needs to initialize every page<br>object individually|In PageFactory, all page objects are initialized<br> by using the initElements() method|
|Finding web elements using By|Finding web elements using @FindBy|
|does not provide lazy initialization|provides lazy initialization|

<br>

---

## :black_nib: *@CacheLookUp* annotation:
CacheLookUp annotation is used to keep a cache of a WebElement instead of searching for the WebElement every time from the WebPage. <br>

Whenever we use a WebElement from Page Object to perform some action, a FindElement is triggered to lookup for the latest version of WebElement from the WebPage. This lookup is basically a FindElement **REST Request** to Browser's Web driver. This lookup is one of the most time-consuming section.

<br>

## :black_nib: When not to use *@CacheLookUp*

 It is not suitable for elements that are dynamic. For **AJAX** based applications, it may not work where the **DOM** changes based on user action on the page.

<br>

## :memo: Sources:

1. <https://www.browserstack.com/guide/page-object-model-in-selenium>
2. <https://www.toptal.com/selenium/test-automation-in-selenium-using-page-object-model-and-page-factory>
3. <https://www.toolsqa.com/selenium-webdriver/cachelookup-in-pageobjectmodel>
4. <https://www.guru99.com/page-object-model-pom-page-factory-in-selenium-ultimate-guide.html>