# CST8921 Lab 5: Serverless Computing
## Elizabeth Kaganovsky (040956095)

### Steps 1-3. Environment Setup, Portal Configuration
Screenshots omitted for brevity.

### Step 4. Create Storage Account
Simple creation of a storage account. For ease of cleanup, soft-delete and similar security features were disabled.
![](/Lab6/Screenshots/Step_4.png)

### Step 5. Enable Static Website Hosting
Azure offers multiple ways to host static websites, Azure Static Web Apps and Azure Blob Storage Static Websites. The former is a better choice for larger websites (which is to say, those larger than a couple pages) which may require global distribution and automatic CI/CD. The latter is a better choice for quick, easy, free testing due to the limited service but very fast deployment.
![](/Lab6/Screenshots/Step_5.png)

### Step 6-8. Create Website Folder with index.html/404.html Pages
![](/Lab6/Screenshots/Step_7_8.png)

### Step 9. Deploy to Static Website
The web page is deployed via VSC using the Azure Storage extension's `Deploy to Static Website via Azure Storage...` option.

### Step 10. Validate Deployment
Pages are accessible at the endpoint provided in step 5. Attempting to access the nonexistant `/w` directory brings up the 404 page correctly.
![](/Lab6/Screenshots/Step_10_1.png)
![](/Lab6/Screenshots/Step_10_2.png)

### Step 11. Cleanup
Cleaning up resources to save on costs.
![](/Lab6/Screenshots/Step_11.png)