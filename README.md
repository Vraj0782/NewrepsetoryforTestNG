# NewrepsetoryforTestNG

package TestNGCertification;

import org.testng.annotations.Test;
import org.testng.asserts.SoftAssert;



import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.Platform;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.AfterClass;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;
import java.net.MalformedURLException;
import java.net.URL;
public class TestNGTodo{
	public String username = "vraj40009";
	public String accesskey = "eU5Y5GBMp7vRN8nRlk7tDSTPyz8wvTGFALmSMIq63LpCMoliWL";
	public static RemoteWebDriver driver = null;
	public String gridURL = "@hub.lambdatest.com/wd/hub";
	boolean status = false;
	public static SoftAssert sft;
	@Parameters("browser")
	@BeforeClass
	public void setUp(String browser) throws Exception {
		DesiredCapabilities capabilities = new DesiredCapabilities();
		capabilities.setCapability("browserName", browser);
		capabilities.setCapability("version", "70.0");
		capabilities.setCapability("platform", "win10"); // If this cap isn't specified, it will just get the any available one
		capabilities.setCapability("build", "My_LambdaTestSampleApp");
		capabilities.setCapability("name", "My_LambdaTestJavaSample");
		try {
			driver = new RemoteWebDriver(new URL("https://" + username + ":" + accesskey + gridURL), capabilities);
			driver.get("https://www.lambdatest.com/selenium-playground/.");
		} catch (MalformedURLException e) {
			System.out.println("Invalid grid URL");
		} catch (Exception e) {
			System.out.println(e.getMessage());
		}
	}
	@Test
	public void testScenario_01() throws Exception {
		try {//Change it to production page
			
			@SuppressWarnings("deprecation")
			WebDriverWait wait=new WebDriverWait(driver, 10);
			WebElement LastElement = driver.findElement(By.xpath("//a[@href=\"https://www.facebook.com/lambdatest/\"]"));
			Thread.sleep(2000);
			wait.until(ExpectedConditions.visibilityOf(LastElement));
			String PageTitle = driver.getTitle();
			sft=new SoftAssert();
			sft.assertEquals(PageTitle, "Selenium Grid");

		} 
		catch (Exception e) {
			System.out.println(e.getMessage());
		}

	}
	@Test
	public void testScenario_02() throws InterruptedException
	{
		//driver.get("https://www.lambdatest.com/selenium-playground/.");
		Thread.sleep(2000);
		driver.findElement(By.xpath("//a[@href=\"https://www.lambdatest.com/selenium-playground/checkbox-demo\"]")).click();
		WebElement checkBox = driver.findElement(By.xpath("//input[@type=\"checkbox\"and @id=\"isAgeSelected\"]"));
		checkBox.click();
		Thread.sleep(2000);
		boolean selected = checkBox.isSelected();
		if (selected)
		{
			System.out.println("Single check box Demo is selected  for 1st Time ");
		}
		else
		{
			System.out.println("Single check box Demo is  not selected  for 1st Time");
		}
		Thread.sleep(2000);
		checkBox.click();
		boolean deSelected = checkBox.isSelected();
		if (deSelected)
		{
			System.out.println("Single check box Demo is selected  for 2nd Time ");
		}
		else
		{
			System.out.println("Single check box Demo is  not selected  for 2nd Time ");
		}

	}
	@Test
	public void testScenario_03() throws InterruptedException

	{	Thread.sleep(2000);
		driver.get("https://www.lambdatest.com/selenium-playground/");
		Thread.sleep(2000);
		driver.findElement(By.xpath("//a[@href=\"https://www.lambdatest.com/selenium-playground/javascript-alert-box-demo\"]")).click();
		Thread.sleep(2000);
		driver.findElement(By.xpath("//button[@type=\"button\"and @class=\"btn btn-dark my-30 mx-10 hover:bg-lambda-900 hover:border-lambda-900\"]")).click();
		Thread.sleep(3000);
		Alert alert = driver.switchTo().alert();
		String text = alert.getText();
		Thread.sleep(3000);
		alert.accept();
		
		if(text.equalsIgnoreCase("I am an alert box!"))
		{
			System.out.println("text Scenario_03 is Pass ");
		}
		else {
			System.out.println("text Scenario_03 is fail ");
		}
	}



	@AfterClass
	public void tearDown() throws Exception {
		if (driver != null) {
			((JavascriptExecutor) driver).executeScript("lambda-status=" + status);
			driver.quit();
			sft.assertAll();
		}
	}
}

