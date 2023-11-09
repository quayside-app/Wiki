# How NextAuth implements OAuth
**11/8/2023 • Ashton Curry**

NextAuth.js is a open-source authentication tool that works with OAuth services such as google, github, facebook, and many more. It integrates the OAuth services for you and handles the process of call backs and more. NextAuth.js gives you a lot of customizeable options, such as locking specific pages or content in the webapp behind a session authorization. It's why we chose to use it with our application. 

The implementation process follows a few steps, all of which can be looked at with David Gray's tutorial on youtube: https://www.youtube.com/watch?v=w2h54xz6Ndw

In summary we needed to create routing and options page which enabled the providers such as google and github to appear as options to log into the website. Then, a middleware file acts as a gaurd for the website. The file allows you to tell the website which pages or content can be accessed by someone not signed in and those who have signed in. Finally, we had to add client IDs and secrets to our enviromental variables for each provider as well as NextAuths secrets (for authentication JWT). 

Provider OAuth services have to be setup from their respective websites. You just need to input callback URLs and copy the client IDs and secrets that are generated after you create the OAuth service. The whole process is explained in depth by NextAuth's documentation here: https://next-auth.js.org/configuration/providers/oauth