# challenge_non_pom
challenge without pom - just crude method in few mins

import java.io.File;
import java.util.List;
import java.util.concurrent.TimeUnit;

import org.junit.Assert;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class ValtechAmar {

	//@SuppressWarnings("deprecation")
	public static void main(String[] args) throws InterruptedException {

		File file = new File("C:\\Driver\\chromedriver.exe");
		System.setProperty("webdriver.chrome.driver", file.getAbsolutePath());

		ChromeDriver fd = new ChromeDriver();


		//Step 1: Get Valtech website
		fd.get("https://www.valtech.com");
		fd.manage().timeouts().implicitlyWait(3000, TimeUnit.SECONDS);
		
		//Check for latest news 
		String s = fd.findElementByClassName("news-post__listing-header").getText();
		String cmp = "LATEST NEWS";
		System.out.println(cmp + " Displayed as " + s);
		Assert.assertEquals("LATEST NEWS", s);
		
		//Click the Submenu
		fd.findElementByXPath("//*[@id='navigation-toggle-button']/div/div/div[1]/i").click();
		Thread.sleep(3000);
		
		//Click Cases
		fd.findElementByXPath("//*[@id='navigationMenuWrapper']/div/div[1]/ul/li[1]/a").click();
		cmp = "Cases";
		s = fd.findElementByTagName("h1").getText();
		System.out.println(cmp + " H1 tag displaying " + s);
		Assert.assertEquals("Cases", s);
		fd.navigate().back();
		
		//Click Services
		fd.findElementByXPath("//*[@id='navigationMenuWrapper']/div/div[1]/ul/li[3]/a").click();
		cmp = "Services";
		s = fd.findElementByTagName("h1").getText();
		System.out.println(cmp + " H1 tag displaying " + s);
		Assert.assertEquals("Services", s);
		fd.navigate().back();
		
		//Click Jobs
		fd.findElementByXPath("//*[@id='navigationMenuWrapper']/div/div[2]/ul/li[1]/a").click();
		cmp = "Jobs";
		s = fd.findElementByTagName("h1").getText();
		System.out.println(cmp + " H1 tag displaying " + s);
		Assert.assertEquals("Jobs", s);
		fd.navigate().back();
		
		//Click World map icon
		fd.findElementByXPath("//*[@id='contacticon']/div/div/div[1]/i").click();
		
		//Find number of offices
		List<WebElement> linkList = fd.findElements(By.className("contactcountry"));
		int totalOffices = 0;
		for (int i = 0; i < linkList.size(); i++) 
		{
			List<WebElement> linkInnerList = linkList.get(i).findElements(By.cssSelector("li"));
			totalOffices = linkInnerList.size() + totalOffices;
		}
		
		System.out.println("Total number of offices all over the world :: " + totalOffices);
		fd.quit();
	}


}
