# Hosting our Website on Google Cloud Run
**9/25/2023 • Ashton Curry**

I was able to complete the google cloud integration with continuous deployment of our github. To do this I had to accomplish two things:
1. Make a dockerfile that created a container for our code (you need to download docker here: https://www.docker.com/).

    I created a dockerfile using the following code from this github: 
    https://github.com/vercel/next.js/blob/canary/examples/with-docker/Dockerfile
    The only part of the file i edited was commenting out **Run yarn** and uncommenting **npm run build**. 

    This youtube tutorial gives a nice description on what's happening and how to complete this process:
    https://www.youtube.com/watch?v=Pd2tVxhFnO4

2. Merge our github onto Google run:
    I did this after completing our dockerfile. I just followed the google cloud guide:
    https://cloud.google.com/run/docs/continuous-deployment-with-cloud-build?authuser=2#new-service

    I also added a the quayside.app domain to the cloud run service by copying the given DNS addresses which are retrieveable from the custom domains page in the cloud run interface. They were placed into the quayside domain DNS section under custom domains.
