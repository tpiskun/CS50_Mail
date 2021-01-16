# Project 3

Project3 Submission for Harvard's CS50: Web Programming with Python and JavaScript Course.

## Motivation
To further master the JavaScript, Python, CSS, and HTML skills needed for front-end development, this project is an example of a modern tech stack. This project is similar to the "Mail" Application and uses custom written API's to allow a user to register an account, login, receive an email, send an email, reply to an email, and toggle between archiviving an email.

## Build Status
[![Build Status](https://travis-ci.com/username/projectname.svg?branch=master)](https://travis-ci.com/username/projectname)

## Features
This project is client-side and therefore allows the to do the following:
* Send Mail: When a user submits the email composition form, the JavaScript will call the appropriate API to send the email.
  * values for recipients, subject, and body are required
* Mailbox: When a user visits their Inbox, Sent mailbox, or Archive, the appropriate mailbox is loaded
  * When a mailbox is visited, the application will query the API for the latest emails in that mailbox.
  * When a mailbox is visited, the name of the mailbox will appear at the top of the page.
* Emails: Each email will display who the email is from, what the subject line is, and the timestamp of the email.
  * If the email is unread, it will appear with a white background
  * If the email has been read, it will appear with a gray background.
* Archive: Allow users to archive and unarchive emails that they have received.
  * Once an email has been archived or unarchived, the user's indbox will be loaded
* Reply: Allows user to reply to an email 
  * The composition form will be Pre-filled with the recipient field set to whoever sent the original email.
  * The subject line will be prefilled and a 'Re:' will be added to the original subject line

## Installation
This project requires Django.

## API Reference
To get, send, and update emails this application’s uses its own APIs.

Querying through emails:

`Get/emails/<str:mailbox>`

Sending a `GET` request to `/emails/<mailbox>` where `<mailbox>` is either `inbox`, `sent`, or `archive` will return back to you (in JSON form) a list of all emails in that mailbox, in reverse chronological order. For example, if you send a `GET` request to `/emails/inbox`, you might get a JSON response like the below (representing two emails):

```
[
    {
        "id": 100,
        "sender": "foo@example.com",
        "recipients": ["bar@example.com"],
        "subject": "Hello!",
        "body": "Hello, world!",
        "timestamp": "Jan 2 2020, 12:00 AM",
        "read": false,
        "archived": false
    },
    {
        "id": 95,
        "sender": "baz@example.com",
        "recipients": ["bar@example.com"],
        "subject": "Meeting Tomorrow",
        "body": "What time are we meeting?",
        "timestamp": "Jan 1 2020, 12:00 AM",
        "read": true,
        "archived": false
    }
]
```

Each Get will return a unique email ID as well as the sender, recipients, subject, body, timestamp, read, and archived values for each respective email. 

`GET /emails/<int:email_id>`

Sending a `GET` request to `/emails/email_id` where `email_id` is an integer id for an email will return a JSON representation of the email, like the below:

```
{
        "id": 100,
        "sender": "foo@example.com",
        "recipients": ["bar@example.com"],
        "subject": "Hello!",
        "body": "Hello, world!",
        "timestamp": "Jan 2 2020, 12:00 AM",
        "read": false,
        "archived": false
}
```
Note that if the email doesn’t exist, or if the user does not have access to the email, the route instead return a 404 Not Found error with a JSON response of `{"error": "Email not found."}`.

`POST/emails`
To send an email, you can send a POST request to the `/emails route`. The route requires three pieces of data to be submitted: a recipients value (a comma-separated string of all users to send an email to), a subject string, and a body string.

The recipient must have a valid email. If an email does not exist you’ll get a JSON response of `{"error": "User with email baz@example.com does not exist."}`

`PUT /emails/<int:email_id>`
To mark an email as read/unread or as archived/unarchived use PUT request to `/emails/<email_id>` where `email_id` is the id of the email you’re trying to modify

## How to Use?
This is to be run using Django and to make any neccessary migrations  

To run the application: 
```
$ python manage.py runserver
```
For migrations:
```
$ python manage.py makemigrations mail
```
```
$ python manage.py migrate
```

## Credits
Source Code provided by Harvard's CS50 curriculum and professor Brian Yu.
