# Database less OTP- A concept
Hello, firstly I am not an expert, so please teach me if anything goes wrong in this post and please don't judge my english.

Let's talk about the topic...

## How a otp system works (as per my knowledge)

### First way
First a user come to the authentication page, then he sees a form where he has to enter his email or phone number and request a otp to verify that email/phone and he recives a otp. Then he copies that otp and paste it in the box and now that email/phone is verified.
### Second way
In this way he recives a link in his mail, and when he clicks on it the email gets verified.

### What happens in backend

When a user requests for otp by sending his email to backend, The backend creates a random string and store it in redis cache with a expiry life time along with its email. And when the user sends that otp, in backend that otp gets matched with the stored one.

## The concept

### Thought
 every time I have created this system for authentication I had a thought do I really need a database and a redish instance costs 1500 INR for a month and I think it's a pricy for a toy project as we don't really want OTP for any-other purpose. So I thought using a hashing kind of thing to eliminate the database completely.
### Approach
Lets divide the OTP into 2 parts
1. The raw OTP string
2. Hashed OTP string
The raw OTP string will be sent to the email/phone
The hashed OTP will be shared with the requested user (Browser)

And in the next request user will provide the OTP from email and stored hash OTP. And, in backend we can compare them and if it matches.

But a user can change the hash and send it. So here comes the JSON web token we can add the hash and email to a JWT so that user can't change the hash and we can also add a JWT expiry time for the OTP.

Normally a OTP is 6 digit number. So a person can create a rainbow table of all 6 digits hash and and match it to know the OTP. To over come this we can use hmac who takes a starting key so brute force is not possible.

``` JS
export function hashedOTP(otp: string) {
  return crypto.createHmac('sha256', process.env.CRYPTO_SECRET).update(otp).digest('hex');
}
```

## Demo

For this I have created a working Demo - [https://db-less-otp.netlify.app/](https://db-less-otp.netlify.app/)

Backend Github Repo - [https://github.com/SBRakeshRath/DB-less-OTP-Backend](https://github.com/SBRakeshRath/DB-less-OTP-Backend)
Frontend Github Repo - [https://github.com/SBRakeshRath/DB-less-OTP-Frontend](https://github.com/SBRakeshRath/DB-less-OTP-Frontend)

** I am Using a gmail account so I don't want you to spam this as you can send only 500 emails

Please point-out the vulnerabilities and how to fix them. 