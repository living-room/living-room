### **New to the living room? check out [the introduction](https://github.com/jedahan/living-room/wiki)**

---

# living room, a programmable space @ recurse center

We are making Lovelace, a room inside Recurse Center, programmable. 

To get started playing around with the same ideas that exist there, checkout [living-room-js][]
For more context, check out our [research blog](https://livingroomresearch.tumblr.com/).

Itching to get started?

![Diagram of submodules in living-room](/docs/images/living-room.png)

# interacting with lovelace

The official room-server to be used @ RC is running on crosby, a cluster computer that is currently in lovelace. We will now point our commandline and web clients to that computer so you can start interacting with all the cool sensors and visualizers.

If you look in the [examples/index.html](examples/index.html) file, it is expecting that you are running the room-server locally (this is the relevant line in index.html: `<script src="http://localhost:3000/socket.io/socket.io.js" ></script>`). If you want to point to the room-server running on the crosby machine, change this to `<script src="http://crosby.cluster.recurse.com:3000/socket.io/socket.io.js" ></script>`. You will also need to change the room constructor to `const room = new window.room('http://crosby.cluster.recurse.com:3000')`.

To use the commandline you will need to `export LIVING_ROOM_HOST=http://crosby.cluster.recurse.com:3000`.

# next steps

* Try getting a friend together, and making a game!
* ...more to come

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
