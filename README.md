A DIY RSVP page hosted on Ghost Blog using n8n & Google Sheets.

Situation: I am hosting my wedding website using Ghost Blog. I really like the idea of a custom domain, "newsletter" capability, the ease of the Ghost Editor, and the general Ghost feature set covers most of my bases. However, despite my searching and Ghost's support for many integrations, I can't find a way to provide an RSVP functionality that checks an existing list of guests and then allows one of those approved guests answer questions about their attendance and needs. I looked at FormSpree, FormBricks, SurveyMonkey, GoogleForms, Typeform, JotForm, Formstack and none (at quick glance) allowed for response validation in a manner that was cheap, easy, and actually did what I wanted. Of course, this leads to trying to make it yourself and spending way too much time on it. I am sharing it to maybe help someone who's trying to accomplish a similar effort. I don't plan to accomodate specific requests or build this out to be a more dynamic / scalable solution, hopefully you can make wanted changes by plugging this into ChatGPT or other to assist you with specific functionality.

Task / Ask: Provide a form for a guest to type their name. Their name is checked against an existing list of invitee's - if user does not exist, return Guest Not Found, if user does exist, continue to survey. Survey should support multiple questions such as, Can you make it to the Wedding? Will you need a seat on the bus? Can you make it to the Welcome Party? Do you have any dietary restrictions? - and save these responses inline to the guest on the initial validation spreadsheet.

Additional Functionality:

Dynamically Populate Spouses / +1's / and children so that one guest can respond for their whole family.
Pre-populate the form for users that are already logged in using the ghost {{member.name}} and {{member.email}} tags.
Don't ask certain follow up questions if the precursor question was a no - i.e. : Can you make it to the wedding? No - Then don't ask if they need a seat on the bus to the wedding they aren't going to.
Email confirmation of successful RSVP Submission.
Requirements: Note: I am self-hosting the following applications, I do not know for certain if this affects feature availability but it definitely adds a certain level of complexity that you need to be capable of addressing...

Ghost Blog - Not a requirement, you could put this on most webhosting platforms that support embedded code snippets, it is just what I happen to prefer at this time. - (https://ghost.org/docs/install/)
N8N - (https://docs.n8n.io/hosting/)
Google Sheets & Google OAUTH Setup
You will also need to ensure that your services are publicly accessible to the internet and that you can setup the Google OAuth procedure for N8N to connect to Google Sheets if you plan on using it like that.

Implementation: There are two ways to put this in Ghost, and it really depends on your use of the {{member.name}} or {{member.email}} tags. If you DON'T care about this, you can just embed this code on your editor page. If you DO care about this, you will need to create an .hbs file in your ghost appdata directory for RSVP-custom.hbs If you are using the custom-RSVP.hbs , you will also need to create a page for your site such as "{{@site.url}}/signin/" (which I use in my file) to show a log-in prompt if the user is not logged into ghost. We cannot populate the form with their name and email without it. If you don't care about this functionality, I'd recommend using the embed code or removing the snippit with the {{@site.url}}/signin/ from the top of the file.

Below is how my n8n flows look. The JSON is available to import these but be sure to update your fields for the webhook, googlesheet, and questionID's.

![image](https://github.com/ChuckBuilds/GhostRSVP/assets/33324927/13e5a216-40be-4194-8f80-85869f9ac640)


Please Ensure that your names are an EXACT match between Google Sheets and N8N form logic. It currently only cleans spaces and mis-capitalization that is input to the form, it will not clean the results in the Google Sheet that it compares against.


The Below Link opens up the Google Sheets form that is populating the names and storing the responses. https://docs.google.com/spreadsheets/d/1JPzBO8it9WDq33uG6QVUb3BSvW0mssAdZgaRSael314

Demo Available here: Use First Name: Test Last Name: Demo or any of the names in the Google Sheet above

https://www.chuck-builds.com/ghost-rsvp/


Example Form on my Wedding Website using my site's existing CSS themes. Example RSVP Form
![Example RSVP Form](https://github.com/ChuckBuilds/GhostRSVP/assets/33324927/17ab64ce-cd1f-4a27-a25c-b288df6ad814)

Basic Confirmation Email of submission. Email Confirmation Screenshot
![Email Confirmation Screenshot](https://github.com/ChuckBuilds/GhostRSVP/assets/33324927/9869d544-6396-4108-ac41-bb0dc6adc814)
