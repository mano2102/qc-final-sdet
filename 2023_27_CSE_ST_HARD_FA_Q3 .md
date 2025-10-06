  2023_27_CSE_ST_HARD_FA_Q3 
  <img width="1919" height="950" alt="image" src="https://github.com/user-attachments/assets/f77ebef4-32c1-4b0b-814d-5a3e8818b282" />
package runner;

import java.net.MalformedURLException;
import java.net.URL;
import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
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
	public void beforeMethod() throws MalformedURLException, Exception {
		// Opening the browser
		openBrowser();
		Screenshot.getScreenShot(driver, "sample");
		ExtentReports reports = Reporter.generateExtentReport("Sample");
		reports.flush();
		LoggerHandler.logInfo("Handled log info");

	}

	@Test
	public void test() {
		// Write your scripts hear
		// Scrolling to the footer
		JavascriptExecutor js = (JavascriptExecutor) driver;
		js.executeScript("window.scrollTo(0, document.body.scrollHeight)");
		WebElement input = driver
				.findElement(By.xpath("//*[@id=\"newsletter_email\"]"));
		input.sendKeys("demo123@gmail.com");
		WebElement submitBtn = driver.findElement(By.xpath("//*[@id=\"block-37881\"]/div/div/input"));
		submitBtn.click();
		WebElement newArrivals = driver
				.findElement(By.xpath("//*[@id=\"block-37882\"]/ul/li[3]/a"));
		newArrivals.click();
		WebElement filter = driver.findElement(
				By.xpath("//*[@id=\"products_list\"]/div[1]/div/div[1]/button"));
		filter.click();

		WebElement availabilty = driver.findElement(
				By.xpath("//*[@id=\"slideover-filters\"]/form/nav/div[1]/div[1]/a"));
		availabilty.click();

		WebElement stock = driver.findElement(
				By.xpath("//*[@id=\"slideover-filters\"]/form/nav/div[1]/div[1]/div/ul/li[1]/label"));
		stock.click();
		WebElement applyNow = driver.findElement(
				By.xpath("//*[@id=\"slideover-filters\"]/form/nav/div[2]/button"));
		applyNow.click();

	}

	@AfterMethod
	public void tearDown() {
		// Quitting the browser

		if (driver != null) {
			driver.quit();

		}
	}
}
