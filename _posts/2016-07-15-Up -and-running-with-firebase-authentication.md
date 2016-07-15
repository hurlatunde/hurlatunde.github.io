---
layout: post
title: Up and running with Firebase Authentication
excerpt: "Firebase Authentication makes authentication easy for end users and developers. It allows you to focus on your users, and not the sign-in infrastructure to support them."
categories: [Firebase, Authentication, Google, Login, Login Authentication]
comments: true
image:
  feature: https://firebase.google.com/docs/auth/images/auth-providers.png
  credit: Google Firebase
  creditlink: https://firebase.google.com/docs/auth/?utm_campaign=Firebase_announcement_education_general_en_05-18-16_&utm_source=Firebase&utm_medium=yt-desc
---

## How does it work?

![Google Firebase](https://firebase.google.com/docs/auth/images/auth-providers.png)
{: .pull-right}

To sign a user into your app, you first get authentication credentials from the user. These credentials can be the user's email address and password, or an OAuth token from a federated identity provider. Then, you pass these credentials to the Firebase Authentication SDK. Our backend services will then verify those credentials and return a response to the client.

After a successful sign in, you can access the user's basic profile information, and you can control the user's access to data stored in other Firebase products. You can also use the provided authentication token to verify the identity of users in your own backend services.

<iframe width="100%" height="520" src="https://www.youtube.com/embed/8sGY55yxicA" frameborder="0" allowfullscreen></iframe>

Firebase Authentication provides backend services, easy-to-use SDKs, and ready-made UI libraries to authenticate users to your app. It supports authentication using passwords, popular federated identity providers like Google, Facebook and Twitter, and more.

##### Firebase Authentication integrates tightly with other Firebase services, and it leverages industry standards like OAuth 2.0 and OpenID Connect, so it can be easily integrated with your custom backend.


Read more -- [Firebase Google](https://firebase.google.com/docs/auth/?utm_campaign=Firebase_announcement_education_general_en_05-18-16_&utm_source=Firebase&utm_medium=yt-desc)