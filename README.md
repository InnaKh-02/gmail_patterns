# Gmail Patterns
## Description
This is a test automation framework for the **Hardcore** task from the WebDriver course. It supports multiple browsers, logging, and flexible configurations for different environments.

## Configuration File Template for Gmail Automation Testing
Here’s an example template for your configuration file (qa.properties) to configure Gmail automation settings:
```properties
email=
password=
recipient=
subject=
body=
```
## List of corrections
| Class | Problem | Solution |
| ----------- | ----------- | ----------- |
| GmailFacade(GmailService)      | (Single Responsibility Principle) GmailService is responsible for login, drafts, and sent emails simultaneously, holding too much knowledge of the system.      | The responsibilities were separated into individual service classes: AuthService, DraftService, and SentService. Each class encapsulates its own logic. The GmailFacade now delegates to these classes and serves solely as a coordinator.      |
| DriverFactory     | (Open/Closed Principle) DriverFactory was hardcoded to support only Chrome and Firefox, requiring modification to add new browsers. | The BrowserDriverStrategy interface with a createDriver() method was introduced. Concrete classes such as ChromeDriverStrategy and FirefoxDriverStrategy were implemented. DriverFactory now uses a strategy map, allowing easy extension.  |
| BasePage      | (Liskov Substitution Principle) Methods like waitForVisibility(...) and waitWithJsExecutor(...) were called by subclasses but not defined or enforced in BasePage, breaking substitutability.      | Replaced static usage with an instance of WaitUtils, injected and used consistently through composition. BasePage now clearly defines and delegates wait behavior, ensuring subclass substitutability.      |

## Design Patterns Used
- **Singleton**: In the DriverSingleton class to manage a single instance of WebDriver.
- **Factory Method**: In the DriverFactory class to create instances of WebDriver based on browser type.
- **Facade**: In the GmailFacade class to provide a simplified interface for interacting with various services (login, drafts, sent emails).

## Run Tests

Run all tests:
```sh
mvn clean test
```
Run with a specific browser:
```sh
mvn -Dbrowser=firefox clean test
```
Run for a specific environment:
```sh
mvn -Denv=qa clean test
```
