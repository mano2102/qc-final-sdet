
  2023_27_CSE_ST_HARD_FA_Q2 
<img width="1919" height="934" alt="image" src="https://github.com/user-attachments/assets/4a37d36e-62c2-45e7-8ad7-e0cc7bf19a4b" />

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
		WebElement span = driver
				.findElement(By.xpath("/html/body/div[3]/main/header/div/div[1]/nav/ul/li[3]/a/span[1]/span[2]"));
		span.click();
		WebElement search = driver.findElement(By.xpath("//*[@id=\"search\"]"));
		search.sendKeys("render");
		WebElement filters = driver
				.findElement(By.xpath("/html/body/div[3]/main/div[2]/section/div[2]/div/div[2]/button/span"));
		filters.click();
		WebElement engineering = driver.findElement(
				By.xpath("/html/body/div[3]/main/div[2]/section/div[2]/div/div[2]/div/div[2]/div[2]/label"));
		engineering.click();
		search.clear();
		search.sendKeys("AI");

		WebElement product = driver.findElement(
				By.xpath("/html/body/div[3]/main/div[2]/section/div[2]/div/div[2]/div/div[2]/div[3]/label"));
		product.click();

	}

	@AfterMethod
	public void tearDown() {
		// Quitting the browser

		if (driver != null) {
			driver.quit();

		}
	}
}

