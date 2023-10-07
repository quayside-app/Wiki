# How calls to ChatGPT's API work
**10/3/2023 • Eleonora Stadtmüller Caballero**

Integrating ChatGPT into our React.js web application meant that a few things had to be accomplished:
1. Set up the routing to make HTTP requests to the ChatGPT API endpoint (I will look into using a library like axios for this to make our lives easier)
	* We are currently using the chat completions API: https://platform.openai.com/docs/guides/gpt/chat-completions-api 
2. In our user input form, the user "prompt" needs to be passed to the API call as user content
3. In our user input form, the user "API key" needs to be passed to the API call as API key (temporary way to handle the API key until we can store it in Google Cloud  
Secrets)
4. Get the API response back and pass it to the Graph.js component to handle
	* This meant passing data (response.json() from NewProjectModal.js to Graph.js), which I accomplished by making a React.js Data Context that wraps the code in layout.js (where NewProjectModal is called)
	* TODO: Figure out how to make the response display the tasks and subtasks in a consistent manner