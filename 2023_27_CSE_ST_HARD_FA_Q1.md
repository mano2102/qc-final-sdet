  2023_27_CSE_ST_HARD_FA_Q1 
  <img width="1919" height="948" alt="image" src="https://github.com/user-attachments/assets/007d8903-dd5c-458c-b8c4-2f932105c43b" />
package runner;

import java.net.MalformedURLException;
import java.net.URL;
import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.openqa.selenium.support.events.EventFiringDecorator;
import org.openqa.selenium.support.events.WebDriverListener;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

import com.aventstack.extentreports.ExtentReports;

import utils.EventHandler;
import utils.LoggerHandler;
import utils.Reporter;
import utils.Screenshot;
import utils.Base;

public class TestRunner extends Base {
	
	@BeforeMethod
	public void beforeMethod() throws MalformedURLException ,Exception{
		// Opening the browser
		openBrowser();
		Screenshot.getScreenShot(driver,"sample");
		ExtentReports reports=Reporter.generateExtentReport("Sample");
		reports.flush();
		LoggerHandler.logInfo("Handled log info");

	}

	@Test
	public void test() {
		// Write your scripts hear
		WebElement search = driver.findElement(By.xpath("//*[@id=\"small-searchterms\"]"));
		search.sendKeys("laptop");
		WebElement searchBtn = driver.findElement(By.xpath("//*[@id=\"small-search-box-form\"]/button"));
		searchBtn.click();
		WebElement searchBtnAdv = driver.findElement(By.xpath("//*[@id=\"main\"]/div/div[2]/div/div[2]/div[1]/form/div[1]/div/div[1]/div[2]/label"));
		searchBtnAdv.click();
        WebElement selectabe =driver.findElement(By.xpath("//*[@id=\"cid\"]"));

		Select sel = new Select(selectabe);
		sel.selectByIndex(3);

		WebElement searchOn= driver.findElement(By.xpath("//*[@id=\"main\"]/div/div[2]/div/div[2]/div[1]/form/div[2]/button"));
		searchOn.click();

		WebElement asusLaptop=driver.findElement(By.xpath("//*[@id=\"main\"]/div/div[2]/div/div[2]/div[3]/div/div[2]/div/div/div[1]/div"));
		asusLaptop.click();
		WebElement addToCart =driver.findElement(By.xpath("//*[@id=\"add-to-cart-button-5\"]"));
		addToCart.click();
	}

	@AfterMethod
	public void tearDown() {
		// Quitting the browser

		if (driver != null) {
			driver.quit();
		
		}
	}

}
