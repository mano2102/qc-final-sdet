  2023_27_CSE_ST_HARD_FA_Q4 
  <img width="1919" height="952" alt="image" src="https://github.com/user-attachments/assets/62748a8c-5b9d-46f5-a83e-70590ab39eff" />

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

		WebElement electronics = driver
				.findElement(By.xpath("/html/body/div[6]/div[2]/ul[1]/li[2]/a"));
		electronics.click();

		WebElement cameraPhoto = driver
				.findElement(By.xpath("//*[@id=\"main\"]/div/div[3]/div/div[2]/div[1]/div/div[1]/div/h2/a"));
		cameraPhoto.click();
		WebElement icam = driver
				.findElement(By
						.xpath("//*[@id=\"main\"]/div/div[3]/div/div[2]/div[2]/div[2]/div/div/div[2]/div/div[2]/h2/a"));
		icam.click();
		WebElement addToCart = driver.findElement(
				By.xpath("//*[@id=\"add-to-cart-button-17\"]"));
		addToCart.click();

		WebElement shoppingCart = driver.findElement(
				By.xpath("//*[@id=\"bar-notification\"]/div/p/a"));
		shoppingCart.click();

		WebElement couponCodeBox = driver.findElement(
				By.xpath("//*[@id=\"discountcouponcode\"]"));
		couponCodeBox.sendKeys("EX500");

		WebElement applyCoupon = driver.findElement(
				By.xpath("//*[@id=\"applydiscountcouponcode\"]"));
		applyCoupon.click();

	}

	@AfterMethod
	public void tearDown() {
		// Quitting the browser

		if (driver != null) {
			driver.quit();

		}
	}
}
