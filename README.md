# cloud-event-management-system

Event showcase + registration site I put together for an iSchool cloud class
project. Plain HTML/CSS, hosted as a static site on S3 behind CloudFront.

Live: https://d2djseb7f73sd3.cloudfront.net

## Pages

- `index.html` - landing page
- `events.html` - upcoming events
- `registration.html` - sign-up form, the only page that talks to a backend
- `contact.html` - contact info (the form here is just for show)

## How registration works

The form on `registration.html` POSTs JSON (`name`, `email`, `role`,
`selectedEvent`, `notes`) to an API Gateway endpoint. Behind that is a Lambda that
saves the registration to DynamoDB and sends a confirmation email through SES.

That backend was set up in the AWS console, so its code isn't in this repo, only the
frontend is. If you fork this you'll need your own endpoint and to swap the URL in
`registration.html`.

## Running it

No build step. Open `frontend/index.html` in a browser, or upload the `frontend/`
folder to an S3 bucket with static hosting (I put CloudFront in front of it for HTTPS).

## Things I'd fix

- event list and the stats on the home page are hardcoded
- the filter chips on the events page don't do anything yet
- the form doesn't check `response.ok`, so a failed request can still look like success
