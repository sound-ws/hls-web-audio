> This repo is a subtree split of our monorepo which will be made public in due course. We cannot process any pull-requests to this repo. Please contact us for help.

# hls-web-audio

A package allowing for playing audio through the [HLS protocol](https://en.wikipedia.org/wiki/HTTP_Live_Streaming) using the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API).

The benefit is that one can have a very precise multi-track player.

## Usage

```JS
import { Controller, HLS } from '@soundws/hls';

// Create a controller to control playback
const controller = new Controller();

// register the HLS tracks with the controller
const drums = new HLS({ controller });
const piano = new HLS({ controller });
const vocal = new HLS({ controller });

// Load all the tracks
Promise.all([
  drums.load('http://my-server.com/drums.m3u8').promise,
  piano.load('http://my-server.com/piano.m3u8').promise,
  vocal.load('http://my-server.com/vocal.m3u8').promise
]).then(() => {
  controller.play()
}).catch((err) => {
  console.error(err)
})

// seek
controller.currentTime = 30 // seconds
controller.pct = 50 // percent

// events
controller.on('start', () => { /*..*/ }) // when playback starts
controller.on('pause', () => { /*..*/ }) // when playback pauses
controller.on('pause-start', () => { /*..*/ }) // when pausing (due to buffering) starts
controller.on('pause-end', () => { /*..*/ }) // when pausing (due to buffering) ends
controller.on('timeupdate', ({ t, pct }) => { /*..*/ }) // progress events, emitted ongoing
controller.on('seek', ({ t, pct }) => { /*..*/ }) // seek event, when currentTime is changed via setting either controller.currentTime or controller.pct
```

# License

Copyright (C) 2019-2023 First Coders LTD

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <https://www.gnu.org/licenses/>.
