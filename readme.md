# living room, or making the recurse center space programmable

We are making Lovelace, a room inside Recurse Center, programmable. To get started playing around with the same ideas that exist there, checkout [room-client](https://github.com/jedahan/room-client).

For helping out please see [our github issues](https://github.com/jedahan/research/issues). We have tagged issues with broad tracks of development: **persistence** - making the system run and deploy as painless as possible

**onramping** - providing a clear entry point for anyone who wants to play in this space

**playing** - writing new sensors, toys, and tools within a space, and

**exploring** - trying out projects, reading papers, watching talks, researching work that could help inform the future of the project.

## development philosophy

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

## implementations

If an implementation has no link, it means we would like to support it but haven't written anything yet!

* languages: **[javascript](https://github.com/jedahan/roomjs)**, c
* protocols: **[http](https://github.com/jedahan/room-http)**, stdin/stdout, websockets, osc
* platforms: **[browser](https://github.com/modernserf/rumor-visualizer)**, **[node.js](https://github.com/jedahan/roomjs)**, arduino, openFrameworks, Cinder


## inspirations

- realtalk
- roomdb
- datalog
