# How NextAuth implements OAuth
**11/8/2023 • Ashton Curry | Updated 11/14/2023 • Mya Schroder**

NextAuth.js is a open-source authentication tool that works with OAuth services such as google, github, facebook, and many more. It integrates the OAuth services for you and handles the process of call backs and more. NextAuth.js gives you a lot of customizeable options, such as locking specific pages or content in the webapp behind a session authorization. It's why we chose to use it with our application. 

The implementation process follows a few steps, all of which can be looked at with David Gray's tutorial on youtube: https://www.youtube.com/watch?v=w2h54xz6Ndw

In summary we needed to create routing and options page which enabled the providers such as google and github to appear as options to log into the website. Then, a middleware file acts as a guard for the client-side of the website. The file allows you to tell the website which pages or content can be accessed by someone not signed in and those who have signed in. Unfortunately, we could not find a way to use middleware to protect all the API routes. Instead NextAuth recommends using the getServerSession in each API route as shown [here](https://next-auth.js.org/getting-started/example).Finally, we had to add client IDs and secrets to our environmental variables for each provider as well as NextAuths secrets (for authentication JWT). 

Provider OAuth services have to be setup from their respective websites. You just need to input callback URLs and copy the client IDs and secrets that are generated after you create the OAuth service. The whole process is explained in depth by NextAuth's documentation here: https://next-auth.js.org/configuration/providers/oauth.

To link verified Oath user to our MongoDB database, we use the NextAuth signIn, session, and jwt [callbacks](https://next-auth.js.org/configuration/callbacks). After a user is verified with Oath, the SignIn callback is called, with info like user (which contains the name and email) passed to it. Using the email, we see if this user exists in our MongoDB User collection. If not, we create a new user. The jwt callback is called whenever a jwt web token is created (i.e. at sign in) or changed, passing token, user, and other info. Here we add our own MongoDB User ID to be stored in `token.sub` so it can be accessed in the session callback. The session callback is called whenever a session is checked, and passes the token, user, and other data. Here we assign session.`userId` to `token.sub` so we can access the User ID in the rest of the app via `useSession()`. For example:

```js
const { data: session } = useSession()
const userID = session.userId
```