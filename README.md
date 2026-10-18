## Install dependencies
mvn clean install

## Install Playwright browsers
mvn exec:java -Dexec.mainClass=com.microsoft.playwright.CLI -Dexec.args="install"

## Run tests
mvn test
