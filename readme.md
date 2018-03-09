# living room, a programmable space @ recurse center

We are making Lovelace, a room inside Recurse Center, programmable. To get started playing around with the same ideas that exist there, checkout [living-room-js][]
For more context, check out our [research blog](https://livingroomresearch.tumblr.com/).

# table of contents
- [I have a sensor / some information, how do I share it?](#i-have-a-sensor---some-information--how-do-i-share-it-)
  * [Install and test the codebase](#install-and-test-the-codebase)
  * [Next, assert some new facts with the commandline client **](#next--assert-some-new-facts-with-the-commandline-client---)
- [I want to make a visualization for the room](#i-want-to-make-a-visualization-for-the-room)
- [interacting with the crosby room-database](#interacting-with-the-crosby-room-database)
- [helping out](#helping-out)
- [development philosophy](#development-philosophy)
- [implementations](#implementations)
- [inspirations](#inspirations)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# I have a sensor / some information, how do I share it?

Let's say you have a program that print to stdout, this section will show how to get that information into the room, and make sure its there.


## Install and test the codebase

```bash
git clone --recursive https://github.com/jedahan/living-room.git
cd living-room-js
yarn
yarn test
```

This should copy [http://localhost:5000][] to your clipboard. Navigate there, and if everything is working, **Timon**, **Pumba**, and **Simba** will just be chilling in your browser. If not, please [file an issue](https://github.com/jedahan/living-room-js/issues/new). To see other examples, do e.g. `http://localhost:5000/particles`.

## Next, assert some new facts with the commandline client **

```bash
yarn assert '#beepo is a friend at (0.3, 0.25)'
```

The visualization should now show a fourth label, beepo

** Now connect your sensor **

For example, if your sensor writes one fact per line, you can use `xargs` like so:

```bash
node examples/sensor.js | xargs -I {} yarn assert {}
```

This should start randomly adding some more animals to the canvas


# I want to make a visualization for the room

First, we'll want to see what the room has heard (this assumes `yarn test` is running locally):

```bash
curl http://localhost:3000/facts
```

You might see a bunch of strings like "#Simba is a cat at (0.5, 0.5)" and "#Elnora is a Xiphosura at (0.0676, 0.8081)".

Lets say we want a list of animal types, we can use pattern matching with the `$` symbol:

```bash
yarn select '#$name is a $animal at ($x, $y)'
```

This is neat, but we want to do something with the browser and maybe make it more performant. The client library has support for subscriptions! See the html in **[examples/]()** for more information, but the general gist is:

```javascript
room
  .subscribe(`$name is a $animal at ($x, $y)`)
  .on(response => {
    console.log(response.solutions)
  })
```

This will run whatever callback is passed to `on()` every time there are new solutions to the original subscription.

# interacting with the crosby room-database

If you look in the examples/index.html file, it is expecting that you are running the room-server locally (this is the relevant line in index.html: `<script src="http://localhost:3000/socket.io/socket.io.js" ></script>`). If you want to point to the room-server running on the crosby machine, change this to `<script src="http://crosby.cluster.recurse.com:3000/socket.io/socket.io.js" ></script>`. You will also need to change the room constructor to `const room = new window.room('http://crosby.cluster.recurse.com:3000')`.

# helping out

For helping out please see [our github issues](https://github.com/jedahan/living-room/issues). We have tagged issues with broad tracks of development:

**[persisting][]** - making the system run and deploy as painless as possible

**[involving][]** - providing a clear entry point for anyone who wants to play in this space

**[playing][]** - writing new sensors, toys, and tools within a space, and

**[exploring][]** - trying out projects, reading papers, watching talks, researching work that could help inform the future of the project.

# development philosophy

Writing the philosophy is to help provide context about decisions made, not to be a set of rules that must be followed. Everything about it can be changed, and we welcome feelings, opinions, and discussion.

**describe the current state of things**

> aspirations become out-of-date quickly, and can be captured in github issues, discussions, etc

**examples are friendlier than documentation**

> examples can be verified easily, and invite exploration

**human readable over machine readable**

> we are focused on exploration of concepts and inviting contributors over performance

**as little code as possible**

> the code that works the best does the least

**support implementations, then transports, then protocols, then languages, then platforms**

> this gets us to the meat of doing interesting things first, then supporting the widest range of sensors and platforms as possible. For example, javascript in memory in the browser, then javascript over http in the browser, then rest over http, then a javascript rest client.

**when implementing protocol/platform support, native is better than consistent**
> for example, using osc channels (`/assert 'today is a beautiful day'`) interoperates with osc libraries better than `/room {assert: {facts: ['today is a beautiful day']}}`, since they don't require json support.

# implementations

If an implementation has no link, it means we would like to support it but haven't written anything yet!

* languages: **[javascript client][living-room-js]**, c
* protocols: **[http, osc, and socketio server][living-room-server]**
* platforms: **[browser & node.js client][living-room-js]**, arduino, openFrameworks, clojure
* visualizers: **[subscription vis](https://github.com/modernserf/rumor-visualizer)**

# inspirations

- realtalk
- roomdb
- datalog
- linda

[living-room-server]: https://github.com/jedahan/living-room-server
[living-room-js]: https://github.com/jedahan/living-room-js
[involving]: https://github.com/jedahan/living-room/issues?q=is%3Aopen+is%3Aissue+label%3Ainvolving/
[persisting]: https://github.com/jedahan/living-room/issues?q=is%3Aopen+is%3Aissue+label%3Apersisting/
[playing]: https://github.com/jedahan/living-room/issues?q=is%3Aopen+is%3Aissue+label%3Aplaying/
[exploring]: https://github.com/jedahan/living-room/issues?q=is%3Aopen+is%3Aissue+label%3Aexploring/
