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
- **Example Request**:
  ```javascript
  const endpointUrl = `https://marketplace.api.healthcare.gov/api/v1/plans/search?apikey=`;
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
- **Example Request**:
```javascript
const message = {
    messages: [
        {
            from: '',
            to: phoneNumber,
            body: 'Hi, Health Care Plan Quotes here! ',
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
```

### Abstract API
Endpoint: https://phonevalidation.abstractapi.com/v1
Purpose: Validates the phone number entered by the user in the enrollment form.
- **Example Request**:
```javascript
const phone = document.getElementById('phone').value;
const url = `https://phonevalidation.abstractapi.com/v1/?api_key=&phone=${phone}`;

fetch(url)
    .then(response => response.json())
    .then(data => {
        if (data.valid) {
            // Proceed with form submission
        } else {
            // Show validation error
            document.getElementById('validation-message').textContent = 'Invalid phone number. Please enter a valid phone number.';
            document.getElementById('validation-message').style.color = 'red';
        }
    })
    .catch(error => console.error('Error:', error));
```
    
### Chase Data Corp API
Endpoint: https://api.chasedatacorp.com
Purpose: Submits user enrollment data to the CRM.
- **Example Request**:
```javascript
const endpoint = 'https://api.chasedatacorp.com/HttpImport/InjectLead.php';
const params = new URLSearchParams({
    token: '',
    accid: '',
    Campaign: '',
    Subcampaign: '',
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
```
### External Libraries
jQuery: Used for various DOM manipulations.
Lottie: Used for displaying loading animations.
FontAwesome: Used for displaying icons in the UI.
Google Tag Manager: Used for managing tags and tracking user interactions.
Google Analytics: Used for tracking and analyzing web traffic.
