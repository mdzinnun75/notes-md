#  Page Object Model in Selenium

## :black_nib: What is Page Object Model?

 POM is a design pattern in Selenium that creates an **Object Repository** to store web elements. In POM, we follow the principle of separation of Object Repository and Test Classes. Each object repository only contains the elements of the respective webpage.

 
 <br>

## :black_nib: What are the advantages of POM:
    
   :heavy_check_mark: **Easy Maintenance**: As every page is separate in POM, if there is any change in any webpage that is easy to identify and change. Changes in the object repository don't impact the code elsewhere.

   :heavy_check_mark: **Reusability**: A single object repository can be used for different TestCases. Also, we can integrate the same POM in Selenium with different types of tests like functional testing and acceptance testing at the same time. 
   
   :heavy_check_mark: **Readability**: Testers can easily identify actions that will be performed on a particular webpage.

<br>


:warning: Page objects themselves should never make ***verifications*** or ***assertions***  :warning: 

<br>


## :black_nib: What is PageFactory in Selenium?
PageFactory is a very optimized way of implementing POM. It is a class provided by Selenium WebDriver which expands the functionality of plain POM.

<br>

:one: **`@FindBy`**: An annotation used in Page Factory to declare web elements. The @FindBy annotation supports :``id, name, className, css, tagName, linkText, partialLinkText, xpath``. Below is an example of declaring an webelement using @FindBy-

```
@FindBy(class="elementClass")
WebElement element;
```

<br>

:two: **`initElements()`**: A ``static`` method in Page Factory class, it instantiate an instance of the given class. Also used to initialize all the web elements defined by @FindBy annotation.
 
```
public RegistrationPage(WebDriver driver) {           
         this.driver = driver; 
         PageFactory.initElements(driver, this);
}
```

<br>

:three: **AjaxElementLocatorFactory**: `AjaxElementLocatorFactory` is **Lazy Loading** concept in PageFactory. It is used to deal with dynamic elements that change during runtime based on user actions, especially on Ajax-heavy applications. Timeout is also possible to set for a webelement using AjaxElementLocatorFactory.

```
AjaxElementLocatorFactory ajaxFactory = new AjaxElementLocatorFactory(driver, 30);
PageFactory.initElements(ajaxFactory, this);
```

<br>

## :black_nib: Default behavior of PageFactory:

- Webelements declared using `@FindBy` are initialized at once and yet not searched in the browser DOM
- WebDriver searches a particular webelement each and every time it is called or any action happened to it.
- For static elements, it provides ``@CacheLookup`` annotation to cache web elements for future uses.

<br>

## :black_nib: Differences between POM and PageFactory:

|Page Object Model|PageFactory|
|-----------------|-----------|
|Page Object Model is a design pattern.|PageFactory is a ``class`` that provides an implementation of POM .|
|In POM, individual initialization of every page<br> object is needed.|In PageFactory, all the page objects are initialized<br> at once by using the initElements() method.|
|Define web elements using `By`|Define web elements using `@FindBy` annotation.|
|POM is **not optimal** as it doesn't support lazy initialization.|Supports lazy initialization and it is **optimal**.|
|POM is not capable of handling `StaleElementReferenceException`.|It effeciently handles `StaleElementReferenceException` by <br>searching everytime when  any stale element is called.| 

<br>

---

## :black_nib: *@CacheLookUp* annotation:
``@CacheLookUp`` annotation is used to keep a cache of WebElement on its first arrival on the webpage instead of searching over and over again, usually used for elements that never change.

A findElement() **REST Request** is sent to the WebDriver every time a WebElement is called from page object repository. This satisfies one of the important Pagefactory benefits of looking for the newest version of webelements after page loading. But, it makes the process slow and time-consuming(a lot obviously!). Here, ``@CacheLookUp`` comes to solve the problem.


<br>


## :black_nib: When not to use *@CacheLookUp*?

It is not suitable for elements that are dynamic in nature. For **AJAX** based applications, it may not work where the **DOM** frequently changes based on user interaction. Upon using @CacheLookUp annotation, WebDriver may throw **StaleElementExceptions**.

<br>

### :memo: Sources:

- <https://www.browserstack.com/guide/page-object-model-in-selenium>
- <https://www.toptal.com/selenium/test-automation-in-selenium-using-page-object-model-and-page-factory>
- <https://www.toolsqa.com/selenium-WebDriver/cachelookup-in-pageobjectmodel>
- <https://www.guru99.com/page-object-model-pom-page-factory-in-selenium-ultimate-guide.html>
- <https://www.softwaretestinghelp.com/page-object-model-pom-with-pagefactory/>