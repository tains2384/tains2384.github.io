---
layout: post
title: Phone number authentication với NuxtJS + Firebase
tags: [firebase, authentication]
comments: true
---

<!-- Content here -->
## Setup Firebase
1. Access Firebase, create project, add app (web)
2. Copy Firebase config để cài đặt Nuxt Firebase

## Setup Nuxt Firebase

Làm theo hướng dẫn của <a href="https://firebase.nuxtjs.org/guide/getting-started/" target="_blank">NuxtJS Firebase</a>

> **Chú ý:** Kích hoạt service <a href="https://firebase.nuxtjs.org/guide/options/#auth" target="_blank">auth</a> để có thể gửi tin nhắn tới điện thoại


## Setup code để gửi tin nhắn đến điện thoại

> **Chú ý:**
> `firebase.auth` tương đương với `this.$fireAuthObj`<br />
> Firebase dùng `reCAPTCHA verifier` để confirm callback xác nhận OTP người dùng nhập vào là đúng

* Setup khi `mounted`

```javascript
// Thiết lập ngôn ngữ hoặc lấy ngôn ngữ của browser
this.$fireAuthObj().languageCode = 'vi'
this.$fireAuthObj().useDeviceLanguage()

// sign-in-button => là id của button nhấn send OTP
// size: invisible => captcha ko cần người dùng interact
// Gán function recaptchaVerifier vào window để dùng lại ở button send OTP
window.recaptchaVerifier = new this.$fireAuthObj.RecaptchaVerifier('sign-in-button', {
  'size': 'invisible',
  'callback': (response) => {
    // reCAPTCHA solved, allow signInWithPhoneNumber.
    console.log("response", response)
  }
});
```
* Khi click button send OTP

```javascript
const phoneNumber = +84987654321 // Phải có mã vùng phía trước (eg. +84)
const appVerifier = window.recaptchaVerifier;
this.$fireAuthObj().signInWithPhoneNumber(phoneNumber, appVerifier)
  .then((confirmationResult) => {
    // SMS sent. Prompt user to type the code from the message, then sign the
    // user in with confirmationResult.confirm(code).
    window.confirmationResult = confirmationResult;
  }).catch((error) => {
    // Error; SMS not sent
    // ...
  });
```

* Khi nhập mã OTP để xác thực

```javascript
const otp = 123456
window.confirmationResult.confirm(otp).then((result) => {
  // User signed in successfully.
  const user = result.user;
  // ...
}).catch((error) => {
  // User couldn't sign in (bad verification code?)
  // ...
});
```
