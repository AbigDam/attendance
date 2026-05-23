This is a simple attendance project meant to be used by school clubs or other small events that want to keep attendance by simply having someone click "Sign-In" next to their name/PfP on a single dedicated device.
Setting this up may seem tricky at first, but I've written this explanation with soemone who knows nothing about programming or google sheets in mind.

# **Hosting the site**
After downloading the code from here, find an online hosting service for your website.
The easiest to use is probably https://tiiny.host/
Which ever one you use, simply upload the code to the site as it is when you download it.
Get the URL or "link" to the website, once you knwo what that link is, move on to the next step. 
The website may look like its working but it WILL NOT WORK until everything else is done.

# **Setting Up API**

## Project Configuration
First visit this url [https://console.cloud.google.com/auth/overview/create](https://console.cloud.google.com/auth/overview/create)
Sign into google if you have not already

Add in your App Information (App Name and Email Adress)
Select "External" for Audience
Add a contact email
Agree to Googles Terms and Services

## Selecting Audience
Once your project is created you should see multiple tabs on the left hand side  
Click "Audience"  
Then underneath "Test users" you should see "+ Add users"  
Click that, and add the email addresses of the owner of the device which will have the attendance system on it.  
To clarify, if a teacher will keep the attendance on a computer in the front of class to be used by 300 students,   
only put the email adress of the teacher, not of the students.  

As of May 2026, You are limited to 100 email addresses which should be more than enough for an attendance application.  

## Creating Clients
Now that you've selected your audience, look at the tabs on the left hand side again  
click "Clients"  
Then at the top click "Create Client"
Now select "Web Application"
underneath "Authorized JavaScript origins" type the URL or "link" that you got earlier.
It should now tell you your client ID.  Copy this, and save it for later.

## API Key
First visit this url [https://console.cloud.google.com/apis/credentials?project=rosy-antler-470920-d0](https://console.cloud.google.com/auth/overview/create](https://console.cloud.google.com/apis/credentials?project=rosy-antler-470920-d0))
Click "Create Credentials"
Then "API Key"
Under the "Select API Restrictions" dropdown, select "Google Sheets API"
Leave the rest as default and click "Create"
It should now tell you your API Key. Copy this, and save it for later.


# **Setting up your google sheet**
Create a new google sheet using the same google account you used for the API.

## Tabs
At the bottom of the sheet, there will be a plus button allowing you to add new Tabs. When you add a tab by clicking the button it should prompt you for a name.
Create 1 tab name "Summary" and a second tab named "Students"
One the top row of the Students tab add the word "Names" in the first column, and "Images" in the second column.

## Share Access
Click "Share" in the top right hand corener, 
and then under "General Access" click "Anyone with the link" and then "Edit" on the right.
Now copy the share link and save it for the next step.

## Sheet ID
When looking at your share link, you'll see the sheet ID in the middle on the link. The link is formated as so:
https://docs.google.com/spreadsheets/d/SHEET_ID/edit?usp=sharing
The string of letters and numbers between "/d/" and "/edit" is the SHEET ID
Do not include the slashes as part of the SHEET ID
Now copy the SHEET id and save it for later

# **Finalizing the Site**

## Editing the Code
Redownload the code from this repository.
Open it using a text editor such as notepad
Line 33 includes `const CLIENT_ID = "";` add YOUR client ID into the quotation makrs
Line 34 includes`const API_KEY = ""; ` add YOUR API key the same way
Line 36 includes `const SHARE_LINK = "";` add YOUR share link into the quotation marks as before.
Line 35 includes `const SHEET_ID = "";` add YOUR sheet ID into the qutation makers here just as before
Now save this as a new file.

## Updating your website
Earlier you hosted our website using the code directly downloaded from the page.
Now, while keeping the URL the same, simply update the code to use your new file.
In https://tiiny.host/ simply click "update" and then upload your new code by dragging and dropping or by browsing your computers files and clicking on your new file.
Now you've done it! The site should be working and its time to use it for attendance!


# Using the Site

**Basics**
- Authorize google to start up the page; Select the email whch you chose when you were selecting audience to authorize google.
- Google required RE-AUTHORIZATION every ~ 1 hour, when this happens, simply click on the same account account, since the browser remembers the password.
- ALL CLICKS to Enter/Exit are instantly recorded in the spreadsheet tab labeled "Sheet1" as an entry or exit.
- The master sheet is under the tab "Summary", and is only updated when you click Update Sheet, which you can do at any time.

**Adding Students**
- Click "Open Summary Sheet" to open the spreadsheet.  The tab "Students" includes a list of all students.  Populate this with all students who may sign up for attendance.  Include images for each student so that they have a profile picture they can use to quickly find themselves.  
Images should be included as public links that end in .jpg, .png or another image ending and NOT .com, .org, .co, etc.  
The order you list students in on this tab does not effect anything

**Ordering Students**  
Admin, or whoever collects attendance may want the Master sheet to order students in a particular way.  To get this order, you'll need to make additions to Sheet1.  
Scroll to the top of the sheet, and add in each students name one by one in the left column.  In the middle column add "in" to indicate entering, and in the left column add a date before the school year started in the correct format ex:  
```2026-05-23T08:27:59.138Z```
Which means "May 23rd, 2026, TIME 8:27:59.138 TIMEZONE 'Z'  "  
This is because the masterspreadsheet orders students based on who entered first, and by adding students first in a particular order you force the master sheet to order them that way.

**Adding Hours**
You may need manually increase or decrease someone attendance for various reasons.  
The master spreadsheet is completely re-generated everytime you click update. So making changes there will be useless if you want to give someone extra hours.   
Similar to how we ordered students, we will use Sheet1 to insert or remove hours for a student.  

If we want to give student1 five more hours for example, we can simple go to the last time he signed in and move it back 5 hours.   
So if he signed in at ```2026-09-23T14:27:15.135Z``` then we will change it to ```2026-09-23T09:27:15.135ZZ```  
Notice we change "14" to "09" since we are giving them 5 hours.  

If we want to remove hours, we can do the same thing, but for when they signed out.  

**Common Errors**  
Rmember, google requires RE-AUTHORIZATION every ~ 1 hour, so make sure all students know to click back on the email adress when they are prompted for re-authorization and not to x out the prompt.    
If, for whatever reason, someone does not do this, their signing in/out will not be recorded until google is re-authorized.  This may result in that student getting 24 hours to 0 hours for the day.   
In my experience using this for 30 students everyday for 1 school year, I ran into this issue about 9 times.  When this happens, manually correct hours using the above described method.  

