import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.time.Duration;
import java.time.LocalDate;

public class Main {
    public static void main(String[] args) {

        System.setProperty("webdriver.chrome.driver", "C:\\Users\\SUGUNA\\Downloads\\chromedriver-win64\\chromedriver-win64\\chromedriver.exe");


        ChromeOptions chromeOptions = new ChromeOptions();
        WebDriver browser = new ChromeDriver(chromeOptions);

        browser.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));


        browser.get("https://www.expedia.com/");


        WebElement languageSelectButton = browser.findElement(By.xpath("//button[@aria-label='Select Language']"));
        languageSelectButton.click();
        WebElement englishLanguageOption = browser.findElement(By.xpath("//button[@data-language='en']"));
        englishLanguageOption.click();

        WebElement regionSelectButton = browser.findElement(By.xpath("//button[@aria-label='Select Region']"));
        regionSelectButton.click();
        WebElement indiaRegionOption = browser.findElement(By.xpath("//button[text()='India']"));
        indiaRegionOption.click();


        WebElement flightsTabButton = browser.findElement(By.xpath("//span[text()='Flights']"));
        flightsTabButton.click();


        WebElement departureCityField = browser.findElement(By.id("location-field-leg1-origin"));
        departureCityField.sendKeys("Kolkata");


        WebElement arrivalCityField = browser.findElement(By.id("location-field-leg1-destination"));
        arrivalCityField.sendKeys("Hyderabad");


        WebElement departureDateSelector = browser.findElement(By.id("d1-btn"));
        departureDateSelector.click();

        LocalDate departureDate = LocalDate.now().plusDays(30);
        String departureDay = String.valueOf(departureDate.getDayOfMonth());
        WebElement departureDayButton = browser.findElement(By.xpath("//button[@data-day='" + departureDay + "']"));
        departureDayButton.click();


        WebElement travelersSelector = browser.findElement(By.xpath("//button[@aria-label='Travellers']"));
        travelersSelector.click();
        WebElement increaseAdultCountButton = browser.findElement(By.xpath("//button[@data-test='adult-stepper-increment']"));
        increaseAdultCountButton.click(); // Increment to 2 adults
        WebElement confirmTravelersButton = browser.findElement(By.xpath("//button[text()='Done']"));
        confirmTravelersButton.click();


        WebElement searchFlightsButton = browser.findElement(By.xpath("//button[@data-test='submit-button']"));
        searchFlightsButton.click();


        WebDriverWait wait = new WebDriverWait(browser, Duration.ofSeconds(10));
        WebElement firstAvailableFlight = wait.until(ExpectedConditions.elementToBeClickable(By.xpath("//button[contains(text(),'Select')]")));
        firstAvailableFlight.click();


        try {
            Thread.sleep(5000); // Pause for 5 seconds
        } catch (InterruptedException e) {
            e.printStackTrace();
        }


        browser.quit();
    }
}
