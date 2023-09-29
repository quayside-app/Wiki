# How Next.js Impacts Routing
**9/27/2023 • Mya Schroder**

Next.js makes url routing easier. There are 2 options for routing with Next.js: Page Routing and App Routing. We decided to go with App Routing because that's what Next recommends and let's you use Next's latest features. [App Routing](https://nextjs.org/docs/app/building-your-application/routing) helps automatically handles routing so each folder you add with a `page.js` file  in the `app` directory is added to the URL path. For example if this is your file structure, the app routes will be as followed:
```
# Assumes url is quayside.com
app/
    page.js # This is "home" page so url is quayside.com
    teams/
        page.js  # url that shows this page is quayside.com/teams
        softfeet/
            page.js  # url that shows this page is quayside.com/teams/softfeet
    
    settings/
        page.js  # url that shows this page is quayside.com/settings

```

Next.js has a couple file names that it automatically recognizes and handles specially. The main ones that we have used so far are:
* `page.js` - Show up as the page the user looks at like mentioned above.
* `layout.js` - If this in a folder, `page.js` in this folder or it's children folders will inherit the the html styling layout specified.



**Our Folder Structure**
For the POC layout, we took a highly component-oriented approach so we can reuse components when we add to the site later on.
 
The file structure we implemented to do this is based off of common Next.js/web-dev practices we looked up. The 2 main folders we have are:
1. `src` Folder - Contains all "code"
     - `app` Folder - Contains all the pages for the website. So far we just have the home page.
          - `global.css` - The CSS styles used by the whole website. Good for light/dark themes if we implement them.
          - `layout.js` - This contains components that we want to show up on every page. Right now, we have the navbar and left-sidebar here.
          - `page.js` - This is our home page.

     - `components` Folder - Contains all the components that are used in the pages. A lot of these like `Dropdown.js` are reused multiple times within a page. Others, like `NewProjectModal.js` may only be used once but make pages more readable if they are separated into their own component. Components also can use other components. **Note**: it may helpful in the future to separate components further into folders for organization.

2. `public` Folder - Contains any static files like pictures and svgs. &#x21B3;`svg` Folder - Contains svg files for icons (like plus, dropdown, etc icons). The reason we're using svgs for icons instead of images because you can change the color/shape/etc. more easily.

