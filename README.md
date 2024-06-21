# Health Care Plan Quotes

This project is a web application designed to help users find and enroll in health insurance plans. It includes features such as plan filtering, enrollment form validation, and integration with multiple APIs for phone validation and sending SMS messages.

## Table of Contents
- [Features](#features)
- [APIs Utilized](#apis-utilized)
  - [Marketplace API](#marketplace-api)
  - [ClickSend API](#clicksend-api)
  - [Abstract API](#abstract-api)
  - [Chase Data Corp API](#chase-data-corp-api)
- [External Libraries](#external-libraries)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)

## Features
- **Plan Search**: Users can search for health insurance plans by providing their ZIP code, annual income, age, and gender.
- **Plan Filtering**: Users can filter plans by issuer, type, and sort them by premium or deductible.
- **Enrollment Form**: Users can fill out an enrollment form with personal details and submit it.
- **Phone Validation**: The phone number entered in the enrollment form is validated using the Abstract API.
- **SMS Notification**: An SMS notification is sent to users upon successful form submission using the ClickSend API.
- **Form Validation**: The application validates the user's age and state participation in the federal marketplace.

## APIs Utilized

### Marketplace API
- **Endpoint**: `https://marketplace.api.healthcare.gov/api/v1/plans/search`
- **Purpose**: Fetches available health insurance plans based on user input.
- **API Key**: `kRw5hB8ZreXQeO0258wgCB6x9543otMW`
- **Example Request**:
  ```javascript
  const endpointUrl = `https://marketplace.api.healthcare.gov/api/v1/plans/search?apikey=kRw5hB8ZreXQeO0258wgCB6x9543otMW&limit=10`;
  fetch(endpointUrl, {
      method: "POST",
      headers: {
          "Content-Type": "application/json",
          "Accept": "application/json",
      },
      body: JSON.stringify(data)
  });

  
### ClickSend API
Endpoint: https://rest.clicksend.com/v3/sms/send
Purpose: Sends SMS notifications to users upon successful form submission.
API Key: B55B3754-6BA0-A1AC-2FF9-6C518C93C8AF

- **Example Request**:
const message = {
    messages: [
        {
            from: '+18332369491',
            to: phoneNumber,
            body: 'Hi, Health Care Plan Quotes here! We received your application for health insurance. An agent will be reaching out shortly to finalize your application. Or, call us at (855) 968-5736.',
            source: 'web'
        }
    ]
};

fetch('https://rest.clicksend.com/v3/sms/send', {
    method: 'POST',
    headers: {
        'Authorization': 'Basic ' + btoa(username + ':' + apiKey),
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(message)
});

###Chase Data Corp API
Endpoint: https://api.chasedatacorp.com/HttpImport/InjectLead.php
Purpose: Submits user enrollment data to the CRM.

- **Example Request**:
const endpoint = 'https://api.chasedatacorp.com/HttpImport/InjectLead.php';
const params = new URLSearchParams({
    token: '9b8ad439-3450-4ce9-8f4a-62ba090de965',
    accid: 'fchc',
    Campaign: 'ACA',
    Subcampaign: 'Healthcareplanquotes.com',
    FirstName: document.getElementById('enrollmentForm').querySelector('[name="firstName"]').value,
    LastName: document.getElementById('enrollmentForm').querySelector('[name="lastName"]').value,
    PrimaryPhone: document.getElementById('enrollmentForm').querySelector('[name="phone"]').value,
    Notes: document.getElementById('planNameInput').value,
    adv_Gender: document.getElementById('genderInput').value,
    adv_Additional__Notes: document.getElementById('enrollincome').value,
    adv_Policy__ID: document.getElementById('planIdInput').value,
    ZipCode: document.getElementById('enrollzipcode').value,
    State: document.getElementById('state').value,
    adv_Date__of__Birth: document.getElementById('dobInput').value 
});

fetch(`${endpoint}?${params.toString()}`, {
    method: 'POST',
    mode: 'no-cors'
})
.then(() => {
    console.log("Enrollment submitted successfully!");
    window.location.href = "https://healthcareplanquotes.com/thank-you";
})
.catch(error => {
    console.error('Error submitting enrollment:', error);
    alert("Failed to submit enrollment, check console for details.");
});

###
Certainly! Here is a comprehensive README file that outlines the APIs and tools utilized in your application:

markdown
Copy code
# Health Care Plan Quotes

This project is a web application designed to help users find and enroll in health insurance plans. It includes features such as plan filtering, enrollment form validation, and integration with multiple APIs for phone validation and sending SMS messages.

## Table of Contents
- [Features](#features)
- [APIs Utilized](#apis-utilized)
  - [Marketplace API](#marketplace-api)
  - [ClickSend API](#clicksend-api)
  - [Abstract API](#abstract-api)
  - [Chase Data Corp API](#chase-data-corp-api)
- [External Libraries](#external-libraries)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)

## Features
- **Plan Search**: Users can search for health insurance plans by providing their ZIP code, annual income, age, and gender.
- **Plan Filtering**: Users can filter plans by issuer, type, and sort them by premium or deductible.
- **Enrollment Form**: Users can fill out an enrollment form with personal details and submit it.
- **Phone Validation**: The phone number entered in the enrollment form is validated using the Abstract API.
- **SMS Notification**: An SMS notification is sent to users upon successful form submission using the ClickSend API.
- **Form Validation**: The application validates the user's age and state participation in the federal marketplace.

## APIs Utilized

### Marketplace API
- **Endpoint**: `https://marketplace.api.healthcare.gov/api/v1/plans/search`
- **Purpose**: Fetches available health insurance plans based on user input.
- **API Key**: `kRw5hB8ZreXQeO0258wgCB6x9543otMW`
- **Example Request**:
  ```javascript
  const endpointUrl = `https://marketplace.api.healthcare.gov/api/v1/plans/search?apikey=kRw5hB8ZreXQeO0258wgCB6x9543otMW&limit=10`;
  fetch(endpointUrl, {
      method: "POST",
      headers: {
          "Content-Type": "application/json",
          "Accept": "application/json",
      },
      body: JSON.stringify(data)
  });
ClickSend API
Endpoint: https://rest.clicksend.com/v3/sms/send
Purpose: Sends SMS notifications to users upon successful form submission.
API Key: B55B3754-6BA0-A1AC-2FF9-6C518C93C8AF
Example Request:
javascript
Copy code
const message = {
    messages: [
        {
            from: '+18332369491',
            to: phoneNumber,
            body: 'Hi, Health Care Plan Quotes here! We received your application for health insurance. An agent will be reaching out shortly to finalize your application. Or, call us at (855) 968-5736.',
            source: 'web'
        }
    ]
};

fetch('https://rest.clicksend.com/v3/sms/send', {
    method: 'POST',
    headers: {
        'Authorization': 'Basic ' + btoa(username + ':' + apiKey),
        'Content-Type': 'application/json'
    },
    body: JSON.stringify(message)
});
Abstract API
Endpoint: https://phonevalidation.abstractapi.com/v1
Purpose: Validates the phone number entered by the user in the enrollment form.
API Key: 6df860a9461c41ccbe151f0aa0e7e343
Example Request:
javascript
Copy code
const phone = document.getElementById('phone').value;
const url = `https://phonevalidation.abstractapi.com/v1/?api_key=6df860a9461c41ccbe151f0aa0e7e343&phone=${phone}`;

fetch(url)
    .then(response => response.json())
    .then(data => {
        if (data.valid) {
            // Proceed with form submission
        } else {
            // Show validation error
        }
    })
    .catch(error => console.error('Error:', error));
Chase Data Corp API
Endpoint: https://api.chasedatacorp.com/HttpImport/InjectLead.php
Purpose: Submits user enrollment data to the CRM.
Example Request:
javascript
Copy code
const endpoint = 'https://api.chasedatacorp.com/HttpImport/InjectLead.php';
const params = new URLSearchParams({
    token: '9b8ad439-3450-4ce9-8f4a-62ba090de965',
    accid: 'fchc',
    Campaign: 'ACA',
    Subcampaign: 'Healthcareplanquotes.com',
    FirstName: document.getElementById('enrollmentForm').querySelector('[name="firstName"]').value,
    LastName: document.getElementById('enrollmentForm').querySelector('[name="lastName"]').value,
    PrimaryPhone: document.getElementById('enrollmentForm').querySelector('[name="phone"]').value,
    Notes: document.getElementById('planNameInput').value,
    adv_Gender: document.getElementById('genderInput').value,
    adv_Additional__Notes: document.getElementById('enrollincome').value,
    adv_Policy__ID: document.getElementById('planIdInput').value,
    ZipCode: document.getElementById('enrollzipcode').value,
    State: document.getElementById('state').value,
    adv_Date__of__Birth: document.getElementById('dobInput').value 
});

fetch(`${endpoint}?${params.toString()}`, {
    method: 'POST',
    mode: 'no-cors'
})
.then(() => {
    console.log("Enrollment submitted successfully!");
    window.location.href = "https://healthcareplanquotes.com/thank-you";
})
.catch(error => {
    console.error('Error submitting enrollment:', error);
    alert("Failed to submit enrollment, check console for details.");
});


###External Libraries

jQuery: Used for various DOM manipulations.
Lottie: Used for displaying loading animations.
FontAwesome: Used for displaying icons in the UI.
Google Tag Manager: Used for managing tags and tracking user interactions.
Google Analytics: Used for tracking and analyzing web traffic.

Usage
Enter ZIP Code: Start by entering your ZIP code in the first step.
Provide Income: Enter your annual income in the second step.
Enter Age and Gender: Provide your age and gender in the third step. If you are 65 years or older, you will be prompted to visit your state's Medicare website.
Select Plan Year: Choose the plan year in the final step and click "Search Marketplace" to view available plans.
Filter and Sort Plans: Use the filter options to narrow down the plans by issuer, type, and sort them by premium or deductible.
Enroll in a Plan: Click the "Enroll" button next to the plan you want to enroll in, fill out the enrollment form, and submit it. Your phone number will be validated, and you will receive an SMS notification upon successful submission.
