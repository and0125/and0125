# Tech Stack inforamtion

A tech stack is the set of technologies used to build a website.

Important components are:

- Front-end layer: includes the tool required to build a user interface.
    - on the web this is likely a javascript library
    - on mobile this could be iOS or android.
- Back-end layer: includes tools for server-side run-times like node.js or python, along with a database.
    - This technology portion may be purchased from a provided.
- API: the tools used as middleware to connect the front end to the backend. Usually its a REST API, and inclues essential 3rd party providers like:
    - stripe for payments
    - twilio for text message
    - sendgrid for emails

## Common tech stacks

- MEAN: mongoDB, express, angular, and node.
    - got popular becasue 
- MERN and MEVN are also available variations.

Stackshare.io is a site where you can see what stack companies are using.

## Questions to establish a tech stack

### Front end stack

- where are users primarily using the application?
    - if its laptops, use javascript with a library like typescript.
- Next you need a UI framework, likely react for me.
    - not the best or fastest, but react is most popular. 
    - can easily build a react native mobile app afterwarrds as well. 
    - can use Redux for state management.
- Stack can use tailwind css which gives prebuilt utility classes to style things quickly.
- can also use SASS to help write code more efficiently which is a css-preprocessor.
- can use a post-css tool to remove unused styles and prepare the css for production.
- Also need a module bundler that combines the files into a bundle to use in the browser. Webpack is the most popular option.

### backend stack

- picking the database is the biggest question.
    - could use NoSQL document-based tech like mongodb or firestore, but these can struggle to represent relationships.
    - SQL databases like PostgreSQL can handle relationships, but are not flexible to changing requirements, and generally more expensive to operate.
    - ALso there are some graph databases like neo4j. 
- You can add a Redis cache layer to store the data in memory as opposed to disk. But to do this you need a server side run time.
    - this is where python comes in with Django. 
    - Ruby, laravel, spring, node js.
    - one option is node js and nestjs, and you can use type orm to avoid writing raw sql queries.

This gives you the runtime for writing and executing code, and to make that available around the world, you'll need a web server like Apache or nginx. 

With a server framework, you need to figure out how to deploy that server. Before deploying, you'll need to make sure the code environment is standardized for deployment using docker containers to any cloud server.

Then you can orchestrate the containers using kubernetes, then we can host these on AWS.

You can then use terraform to programmatically update the environment.

Then you can host the source code in the cloud using github or gitlab. 

### API 

The next thing is to build an API to communicate between the front end and backend. 

You can use Apollo to build a graphQL API.

You also may not want to deal with some features like payments, user authentication, can use twilio to send messages, sendgrid for emails, etc.

use 3rd party APIs for thing sthat are too complicated to do on your own.

Know that the end users just want a good experience. 

### One Simple Stack

- petite vuew 
- use bootstrap to get to a decent looking UI for web, and ionic to wrap the application with a webview
- the Firebase could firestore handles user authentication, and can be included in the application through a script tag.
- You can use firebase to deploy python or node js code in a serverless way. 
- not going to work with ci/cd pipeline, because unless you're updating this daily, you don't need this.


