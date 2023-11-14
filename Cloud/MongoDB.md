# Next.js integration with MongoDB
**11/14/2023 • Mya Schroder**

### Structuring
MongoDB is a non-relational database that we chose to use because it grants us data flexibility, which is important in the future as we add additional functionality to our app. MongoDB data is formatted into Collections (similar to a table in a relational DB). For next.js we have a Project, Task, Team, and User Collection. Each entry in a Collection is called a Document (similar to a row in a relational DB). Currently, we have the same attributes (similar to columns in a relational DB) in each Collection, enforced on next.js side. Something we should eventually look into is enforcing this structure and verify data on the MongoDB side of things.

### Connecting
To host our MongoDB database, we are using Atlas, backed by Google Cloud because it is simple to use, makes it easy to visualize data, and best of all, free for development (with the M0 Sandbox Shared ter). Because of we are using the free tier, to connect our DB to our website hosted in Google Cloud Run, we had to set the IP Network Access List to accept incoming requests from all IP addresses. Although any connections still need proper database credentials, this is still not the most secure. However, it is okay for development when we are not handling any confidential user data. In the future, we need to set up Peering or a Private Endpoint between our website on Google Cloud Run and MongoDB, and restrict access from all other IP addresses.

### Reading/Writing Data
In next.js to read/write data, we are using the Mongoose library to make our lives easier. This allows us to make queries and write to the database. With Mongoose, you can create Schemas, which represent your data structure. For each Schema, you initialize a model, which you can use to read/write from MongoDB. For example:
```js

// Initialize schema for User Collection
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  email: { type: String, unique: true },
  username: String,
  teamIDs: [ObjectId]
})

// Initialize model for userSchema
export const User = mongoose.model('User', userSchema, 'User');

 // Connect to database
await mongoose.connect(/*<INSERT URI HERE>*/) 

// Get one user from the User Collection where their ID is 1234
const users = await User.findOne({ _id: 1234 })     
```


We created an API for our MongoDB logic using next.js routes in src/app/api/mongoDB (see [Next.js/API](Next.js/API.md) for more details). That way, our client side can fetch from using GET/POST requests like createProject, getProjects, getTasks, and getUsers. For example, a fetching a user would look like:
```js
// Fetch the document for the  User with ID 1234
useEffect(() => {
    fetch(`/api/mongoDB/getUsers?id=${1234}`, {
    method: 'GET',
    headers: {}
    }).then(async (response) => {
    const body = await response.json()
    if (!response.ok) {
        console.error(body.message);  // If error, log it in the console
    } else {
        console.error(body.users);  // Log the response in the console
    }
    }).catch(error => {
    console.error(error);  // If error, log it in the console
    })
})
```

We can verify the request or the database data coming from MongoDB in the API before it's sent to the user.

