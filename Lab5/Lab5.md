# CST8921 Lab 5: Serverless Computing
## Elizabeth Kaganovsky (040956095)

### 1. Step A1 - Create Storage Account 
![](/Lab5/Screenshots/Step_A1.png)

### Step A2 - Create Blob Container 
![](/Lab5/Screenshots/Step_A2.png)

### Step B1 - Create Function App 
![](/Lab5/Screenshots/Step_B1.png)

### Step B2 - Create Function 
![](/Lab5/Screenshots/Step_B2.png)

### Step C1 - Create Event Subscription 
I encountered a restriction on my student account preventing the creation of an event grid system topic. To accomodate this, I switched to the CloudLabs.ai Azure subscription and followed the same steps up to this point.
![](/Lab5/Screenshots/Step_C1_1.png)
![](/Lab5/Screenshots/Step_C1_2.png)

### Step D1 - Update Function Code 
![](/Lab5/Screenshots/Step_D1.png)
![](/Lab5/Screenshots/Step_D2_1.png)

### Step D2 - Verify Function Settings 
![](/Lab5/Screenshots/Step_D2_2.png)

### Step E2 - Upload File 
![](/Lab5/Screenshots/Step_E1.png)

### Step F1 - Confirm Function Invocation 
![](/Lab5/Screenshots/Step_F_1.png)
Unfortunately due to an unknown issue, I struggled with a persistent error that prevented me from being able to properly use the functions I created. The ProcessBlobUpload function rapidly disappeared from the function app overiew page, as did other functions. The creation of the initial ProcessBlobUpload function created dummy code which I replaced with that used in the lab, but this code would be unable to be saved. Subsequent function creations suffered from the same issue. I attempted this on both my Algonquin account and CloudLabs.ai account and followed typical troubleshooting steps but could not resolve the issue.

### Step F2 - View Logs (Blob Content) 

### Part G - Cleanup (Mandatory) 