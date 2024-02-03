# Next.js APIs
**11/14/2023 • Mya Schroder**

Next.js lets you create APIs as route.js files in folders within the `src/app/api` directory. We have separated our MongoDB, chatGPT, and Oath logic into APIs to make a distinction between the user-logic and the business-logic. This also allows our components to be more modular from each other so we can swap out logic if needed.