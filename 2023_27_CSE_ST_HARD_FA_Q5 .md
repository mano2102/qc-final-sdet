  2023_27_CSE_ST_HARD_FA_Q5 
  <img width="1913" height="944" alt="image" src="https://github.com/user-attachments/assets/8e092187-e4c9-405c-93a3-92707669ed52" />
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
	public void test() throws InterruptedException {
		WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

		// 1️⃣ Click on Contact safely
		By contactLocator = By.xpath("/html/body/div[3]/main/header/div/div[3]/ul/li/a/span[1]/span[2]");
		WebElement contact = wait.until(ExpectedConditions.elementToBeClickable(contactLocator));
		contact.click();
		Thread.sleep(3000);
		// 2️⃣ Wait until firstname field appears
		By firstNameLocator = By.xpath("//input[@name='firstname']");
		WebElement firstName = wait.until(ExpectedConditions.visibilityOfElementLocated(firstNameLocator));
		firstName.click();
		firstName.sendKeys("demo");

		// 3️⃣ Fill in last name
		By lastNameLocator = By.xpath("//input[@name='lastname']");
		WebElement lastName = wait.until(ExpectedConditions.visibilityOfElementLocated(lastNameLocator));
		lastName.sendKeys("user");

		// 4️⃣ Email field
		By emailLocator = By.xpath("//input[@name='email']");
		WebElement email = wait.until(ExpectedConditions.visibilityOfElementLocated(emailLocator));
		email.sendKeys("demouser@gmail.com");

		// 5️⃣ Select dropdown
		By selectLocator = By.xpath("//select[@name='monthly_paas_spend___budget']");
		WebElement sel = wait.until(ExpectedConditions.elementToBeClickable(selectLocator));
		Select select = new Select(sel);
		select.selectByIndex(2);

		// 6️⃣ Submit button
		By submitBtnLocator = By.xpath("//*[@id=\"hsForm_b663c71d-4483-4e2d-b7c7-9cca5762c0a3\"]/div[9]/div[2]/input");
		WebElement submitBtn = wait.until(ExpectedConditions.elementToBeClickable(submitBtnLocator));
		submitBtn.click();
	}

	@AfterMethod
	public void tearDown() {
		// Quitting the browser

		if (driver != null) {
			driver.quit();

		}
	}
}
