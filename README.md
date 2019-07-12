# Weekly Nerd @cmda-minor-web · 2018-2019

## Frontend United
School gave us the very nice opportunity to go to the Frontend United conference in the Jaarbeurs in Utrecht.

### How to design a award winning website?
The first college I attended was the one gave by Peter van Grieken and Luc Princen.

Peter van Grieken is an inclusive design consultant and the founder of design studio [Frozen Rockets](https://frozenrockets.nl/). He helps organisations to reach as many people as possible by helping them design accessible products and services. In a previous life he ran a showbizz website, but you can still ask him about the latest Hollywood gossip.

Luc Princen is an independent developer and designer from The Netherlands specializing in WordPress and frontend development. He loves open source, elegant code, fast load times, Dungeons & Dragons and playing the occasional (grand) strategy game.

Last year they had won the prize for [Best Site](https://www.kit.nl/) at the Automatic Design Awards. They talk about the decisions they have made during the making process. They also discus how they have used WordPress’ Gutenberg editor throughout the website while they also had to take care of the usability and accessibility.

At first Luc talked about the CMS system WordPress. He said that WordPress is already 16 years old and actually is pretty ancient nowadays. It will take a developer approximately 15 years to renew WordPress to todays standards he said. He also spoke about the usage of the Gutenberg plugin in their award winning website. Gutenberg is an content editor in WordPress and allows you to easily create an website.

Then Peter took it over. He said that the idea of modular design is that it needs to be re-usable and that it is important to keep accessibility in mind during the process. To test your application you need to throw your mouse out and try to use your app with your keyboard he claimed. "Designing focus states is not hard" and that is why Peter says that there is no excuse not to design for accessibility.

#### Conclusion
The award winning website they made wasn't one of the most beautifull website i had ever seen, but designing an award winning website isn't all about the design. It is also how you can interact with it. I liked the way they talked about accessibility and that it sometimes isn't even in the clients budget, and the said that it always needs to be in the budget because you never know who is going to use your website. Small, big, old, young, with or without an disability to design an award winning website your website must be ready for everyone.


### Get your screen together. Design skills for frontend people.
The second college i attended was one gave by Silvia Otto Sequeira

Working as UX/UI Practice Lead at [OutSystems](https://www.outsystems.com/), Sílvia leads a global team of designers creating applications for all sorts of companies operating regionally or worldwide. Her mission is to always work as user advocate by designing better products, and help others doing the same. And then writing and talking about it.

In the talk she guides us through the process of delivering applications on a short period of time. She says: sometimes it feels like we are delivering the babies but don't take care of the babies so we need to rely on who comes next. Why should a frontend developer learn about design? Because design is everyone's job.

She talks about specific moments that happen throughout the cycle of development.

| Cycle |
|------|------|
| Non-Realistic, Non-Perfomant | _ You've got to know what works and what doesn't _ |
| Winging it moments | _ The features that come after design _ |
| Near enough complex | _ Near enough is okay for most stakeholders _ |
| Backend mindset | _ Does it work? Then it's done _ |


She says that everytime you face something like this, you are forced to make design decisions. But she also claims that understanding and discussing what designers are doing doesn't make you a designer.

She walked us through the 10 heuristic rules of how to put a screen together.

|heuristics |
|------|------|
| 1. | Visibility of system status | _Let users know what is going on. If you have more info about a state, privide the user_  |
| 2. | Match between system and real world | _ Lets use examples from the real world, use our conventions wisely _ |
| 3. | User control and freedom | _ Give users a sense of control, give them opportunities to get out, cancel or undo _ |
| 4. | Consistency and standards | _ For example the hamburger menu, a user know that there is something behind _ |
| 5. | Error prevention | _ User needs to be in control _ |
| 6. | Recognize rather than recall | _ User doesn' remember things, make something that is understood after the first look _ |
| 7. | Flexibillity and efficiency of use | _ Give the user what they want, give them faster ways to complete goals _ |
| 8. | Aesthetic and minimalist design | _ Make it easier for the user _ |
| 9. | Help users recognize, diagnose and recover from errors | _ Give users the opportunity to redo an action after an error _ |
| 10. | Help and documentation | _ Give users help when they need it, when they need it _ |

#### Conclusion
A lot of the things in the college where very familiar to me because of the courses i followed on university. It was very nice to see how they are implemented in a big process. Although i think she sometimes was a little vague and i didn't really got her point.

## Socket.io
## What is socket.io?
Socket.io is a JavaScript library for realtime web apps. It provides realtime, bi-directional communication between web clients and servers. It has two parts: a client-side library that runs in the browser, and a server-side library for Node.js. Both components have a nearly identical API.

Communication on the web is usually asynchronous. The client requests and the server responds. Back in the days when the web introduced itself, this was fine. But nowadays we need something faster and immediate. In this picture, for example, the server can't decide for itself to send something to the client. The client has to reload the page to see changes.
![](HTTP image)

Socket.io that creates some sort of pipe communication that remains open between client and the server. The browser and the server stay connected to each other and can exchange messages, in one direction and the other, through this pipe. The server can decide for itself to send a message to the client.
![](Socket image)

Socket.io allows us to use websockets very easily. For example, if the browser doesn’t support WebSocket but Flash is installed, socket.io will go through Flash to do the communication in real time. If not, it can use other techniques such as AJAX Long Polling or "Forever Iframe" which is based on an invisible iframe that loads progressively to retrieve updates from the server.
The good news is that you don’t need to know the details about how these techniques work. However, I think it’s good to at least know their name and that they exist.

## Why do we use Socket.io?
For example: you can build an chat application with Socket.io. But i hear you think: Why don't just use HTTP or HTTPS calls to communicate with the server? Wel let's say that you are building an chat application. When person 1 is typing then person 2 should know that person 1 is typing. If you use HTTP calls, Person 2 will never know that person 1 is typing because of the delay. Socket.io sends this "typing" information realtime. That is why we use socket.io.

## How do we use Socket.io

#### Setting up the base
At first you need to set up a base server(app.js) and install Socket.io
`npm install socket.io`

Then there is the server or in most of the times `app.js` or `index.js`
```js
const express = require('express'); // NodeJS framework
const ejs = require('ejs'); // Embedded JavaScript templating
const app = express() // App set up
const socket = require('socket.io'); // requiring socket.io

// base server settings
app.set('view engine', 'ejs');
app.use(express.static('public'));

app.get("/", function(req, res){
  res.render("index")
});

// on which port the can server can be found
let server = app.listen(1000);
console.log('Port 1000');

// Loading socket.io
let io = socket(server)

// When a client connects, we see a message in the console
  socket.on('connection', function(socket){
    console.log('User connected', socket.id);
  })
```

After that there is the client, or `index.ejs`(for a better overview i write a script within the `index.ejs` file)

```html
<h1>Base communication with Socket.io</h1>

<script src="/socket.io/socket.io.js"></script>
<script>
let socket = io('http://localhost:1000')

socket.on('connect', function() {
  console.log("connection made id", socket.id);
})
</script>
```
And here the result! You can see that there is a log in the server console and in the client console.
![](result socket)

#### For what do we use socket.io
  - [Chat applications]()
  - [Gathering realtime data](https://final-assignment-zarjxmiosj.now.sh/login)

#### Which sites use socket.io?
  - [Trello](https://trello.com/nl) _Planning app_
  - [Heroku](https://id.heroku.com/login) _app to deploy server-side projects_
  - [DuckDuckGo](https://duckduckgo.com/) _Search engine_
  - [imgur](https://imgur.com/) _Funny GIF's, images and videos_

#### Conclusion
In My opinion Socket.io is a very easy and friendly in use framework which makes it possible to do almost anything if it comes to realtime stuff.

## NodeJS
## Azat Mardan: You don't know NodeJS
This talk is given by Azat Mardan. Azat Mardan has over 14 years of experience in web, mobile, and software development. With a Bachelor’s degree in Informatics and a Master of Science degree in Information Systems Technology, Azat possesses deep academic knowledge as well as extensive practical experience. Azat is an experienced software engineer, author and educator. He published 11 books and counting.


Mardan says that our lives are becoming more and more digital, so by building better software, we can improve lives of other people. After that he started with the basics of NodeJS and why we should use it. He says that there are two types of systems, the first one is `input` and `output` bound, and the other one is CPU bound. When we are building webapplications, we usually work with the `input` and `output` bound system. So, what is `input` and `output`? It can be an writing tool, database, making a request to a server or something else which takes a lot of time for the process to be finished. NodeJS has a thing that is called a non-blocking i/o, or non blocking `input` and `output`. When we are building an app with NodeJS, we have some clients making a request. Under the hood of NodeJS we have an event loop which was borrowed from the google chrome V8 engine. The event loop is always looking for things to execute, and then it delegates the actual processes to other systems, for example file systems or databases. When the delegation passes, it also gives an callback and when the system is done that callback is executed and usually that code has the data to send back to the client.

#### Comparison with Java
After that he compares NodeJS with Java. He shows an example where he executes 3 `system.out.printIn()` functions with one `Thread.sleep()` function between the second and third `system.out.printIn()` function. He said that nothing happens with the code until the `Thread.sleep()` function has passed.
```Java
system.out.printIn("Step: 1")
system.out.printIn("Step: 2")
Thread.sleep(1000)
system.out.printIn("Step: 3")
```

Then he grabs an example of the same sort of functions in NodeJS. And as NodeJS uses JavaScript on the server, he can do the same as in Java, but then with simple `console.logs` and one `setTimeout` function. Instead of waiting until the `setTimeout` function is executed, this code doesn't stop and keeps on running.
```js
console.log('Step: 1')
setTimeout(function() {
  console.log('Step: 3')
}, 1000)
console.log('Step: 2')
```
So when this code runs, it will first log `Step: 1` after that the code continues and it will log `Step: 2` then after the 1000 miliseconds it wil log `Step: 3`. So in comparison to Java the code is nog sleeping, but it is scheduled to execute in the future. He claims that this is the most important feature in his presentation: Nodejs allows you to write faster applications.

#### blocking or non-blocking webservers
Then he talks about blocking Web servers. He names Python, Ruby and Java as examples of blocking web servers. Each subsequent request will be blocked by the previous request. So you create a cue. He names a coffeebar as an example. People order their drink at the cashier and the cashier turns around and starts making the drink. He creates an cue because he can not be a cashier and a barista at once. Then he talks about non-blocking web servers(NodeJS). He says that there is an event loop again and that event loop delegates the tasks to other underlying systems. The event loop is almost never blocked and it is also single threaded. Then he goes back to his coffeebar example. He says you can compare this to the way Starbucks works. You order your drink, they write your name on the cup, and you go to your table an continue what you where doing. And after a while they call you and you can fetch your drink. So in general, you can execute other functions while waiting for an other function to execute. Although you can write blocking code in NodeJS Mardan claims, but even so. NodeJS is typically much faster than other platforms.

His favorite benefit of NodeJS is that you can use JavaScript everywhere. He says that you have one language to rule the whole stack. This has the benefit that you can think faster, Re-use code and you can learn quicker because of the use of JavaScript. When you know JavaScript it is very easy to start with NodeJS he says.


#### Events
Then he talks about events. Events are part of the core of NodeJS and supported by the most of the core modules of while more advanced patterns such as promises, async/await are not. Events is a Node observer pattern, they are everywhere in the node core modules. So if you know how to work with events, you basically know how to work with NodeJS. Then he shows an example how to use these event listeners:
```js
  let events = require('events')
  let emitter = new events.eventEmmitter()

  emitter.on('knock', function(){
    console.log('Who is there?');
  })

  emitter.on('knock', function(){
    console.log('Go away!');
  })

  emitter.emit('knock')
```
So to explain this. `knock` is a single event but within that event you can have many functionalities executed.
The order in which it will be executed is the same as it is defined. Then Mardan shows a list of possible listeners.
```js
  emitter.listeners(eventName)
  emitter.on(eventName, listener)
  emitter.once(eventName, listener)
  emitter.removeListener(eventName, listener)
```

#### Handling large data
He introduces streams. They allow us to use large data and we don't need to wait until the whole piece of data has loaded. He names the four types of streams:
  - Readable
  - Writable
  - Duplex
  - Transform

Stream inherit from Event Emitter and streams are practically everywhere. HTTP requests are streams, Standard input/output are streams and file reads and file writes are some examples of streams.  

#### Conclusion
Azat Mardan really knows what he is talking about and he shows the benefits of working with NodeJS. Altough i'm not yet there, i can see the power of NodeJS. And since i have worked with it pretty often, i can go and implement these benefits within my code!
