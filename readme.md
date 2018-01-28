# making the recurse center space programmable

We would love a catchier name for this research, please help in [this thread](https://github.com/jedahan/research/issues/1), or zulip, or in person...

### philosophy

Please share your ideas, experience, and feelings about these!

* describe the current state of things
* examples are friendlier than documentation
* human readable over machine readable
* working code over correct code
* as little code as possible
* support implementations, then transports, then protocols, then languages, then platforms
  * for example, javascript in memory in the browser -> javascript over http in the browser -> rest over http
* when implementing protocol/platform support, native is better than consistent
  * for example, use osc channels: `/assert 'today is a beautiful day'` is bettter than `/room { assert: { facts: [ 'today is  beautiful day' ] } }`


### examples

```javascript in the browser
import Room from "room.js"
const room = new Room()

const canvas = document.createElement('canvas')
document.body.appendChild(canvas)
const context = canvas.getContext('2d')

room
  .ask('$name is a $thing at ($x, $y)')
  .then({name, x, y} => context.fillText(name, x, y))
```

### targets

**Bold** means we have implemented support, otherwise its what we want to support

* languages: **[javascript](https://github.com/jedahan/roomjs)**, c
* protocols: **[http](https://github.com/jedahan/room-http)**, stdin/stdout, websockets, osc
* platforms: **[browser](https://github.com/modernserf/rumor-visualizer)**, **[node.js](https://github.com/jedahan/roomjs)**, arduino, openFrameworks, Cinder

### protocols

We will try and describe implementations of protocols/transports here so people can implement their own experiments, though this is very likely to be out-of-date

#### HTTP

The id is just a client id, we might hide it

    POST /assert { fact: 'some string here' } -> { _id: Number }

    POST /retract { fact: 'some string here' } -> { _id: Number}

    POST /select { facts: [ '$what string here' ] } -> { solutions: [ { what: 'some' } ] }

## inspirations

- realtalk
- roomdb
- datalog
