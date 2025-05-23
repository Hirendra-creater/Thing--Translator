# Thing-Translator
📷 🗣 Point your camera at things to hear how to say them in a different language
https://github.com/Hirendra-creater/Thing-Translator.git

https://github.com/hirendra-creater/thing-translator?tab=readme-ov-file#an-ai-experiment

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta
      name="description"
      content="Point your camera at things to hear how to say them in a different language"

require('array.prototype.find').shim()
require('array.prototype.findindex').shim()

import choo from 'choo'
import requestCamera from './effects/request-camera'
import requestFullscreen from './effects/request-fullscreen'
import snap from './effects/snap'
import translate from './effects/translate'
import baseView from './views/base-view'
import {langList} from './config'

const app = choo()

app.model({
  state: {
    activeView: 'main',
    cameraReady: false,
    cameraError: false,
    stream: null,
    video: null,
    ctx: null,
    canvas: null,
    isSnapping: false,
    firstTime: true,
    fullscreen: false,
    label: '',
    translation: '',
    activeLang: langList[0],
    targetLang: 'english',
    guesses: '',
    rotateTerms: true
  },
  subscriptions: [
    (send, done) =>
      window.document.addEventListener('DOMContentLoaded', () =>
        send('requestCamera', done)
      )
  ],
  reducers: {
    showList: () => ({activeView: 'list'}),
    showMain: () => ({activeView: 'main'}),
    cameraError: () => ({cameraError: true}),
    startSnap: () => ({isSnapping: true, firstTime: false}),
    endSnap: () => ({isSnapping: false}),
    setFullscreen: () => ({fullscreen: true}),
    setLabelPair: (_, labels) => labels,
    changeLang: (_, lang) => ({
      activeView: 'main',
      activeLang: lang,
      label: '',
      translation: ''
    }),
    setStream: (_, {stream, video, ctx, canvas}) => ({
      cameraReady: true,
      stream,
      video,
      ctx,
      canvas
    })
  },
  effects: {
    requestCamera,
    snap,
    translate,
    requestFullscreen

    @import 'nib'

$yellow = #ffc234

*
  box-sizing border-box
  margin 0
  padding 0

html
  font-family 'Montserrat', 'Helvetica Neue', Helvetica, sans-serif

body
  background-color #000
  color #fff
  margin 0
  height 100vh
  overflow hidden


@keyframes flash
  0%
    background-color rgba(255, 255, 255, 1)

  100%
    background-color rgba(255, 255, 255, 0)

#target
  position absolute
  pointer-events none
  top 0
  bottom 0
  left 0
  right 0

  &.flashing
    animation flash .3s ease-out


.button
  text-transform uppercase
  font-size 7vw
  border 0.5vw solid #fff
  padding 3vw
  cursor pointer


#intro
  text-align center
  padding 4vw
  h1
    font-size 15vw
    font-weight normal

  h2
    font-weight normal
    font-size 5vw
    line-height 1.7
    padding 4vw

#video
  position fixed
  top 50%
  left 50%
  min-width 100%
  min-height 100%
  width auto
  height auto
  z-index -100
  transform translateX(-50%) translateY(-50%)
  pointer-events none

#lang-list
  ul
    position absolute
    top 50%
    left 0
    right 0
    list-style none
    text-align center
    transform translateY(-50%)

  li
    font-size 4.4vh
    text-transform uppercase
    line-height 2.2
    cursor pointer

    &.active
      color $yellow

    &:hover
      opacity .6

  .x
    position fixed
    z-index 2
    font-size 20vmin
    right 3vmin
    top -2.4vmin
    cursor pointer

    &:hover
      opacity .6


#main-view
  text-align center
  position absolute
  top 7vh
  bottom 45vmin
  left 0
  right 0
  width 100vw
  height 60vh
  transition opacity .2s ease-out

  &.faded
    pointer-events none
    opacity 0

  .row
    width 100%
    height 50%
    margin 0 auto

    h2, h4
      font-weight normal
      position relative
      top 50%
      transform translateY(-50%)
      width 100%

    h2
      font-size 12vmin
      white-space nowrap
      overflow hidden
      text-overflow ellipsis


    h4
      text-transform uppercase
      font-size 4vmin

    &:first-child
      h4
        text-decoration underline
        color $yellow
        &:hover
          cursor pointer
          opacity .6



#main-view.spell-view
  div:first-child
    border-bottom none

    h2
      font-size 45vw
      top 40vh


#canvas
  display none


#shroud
  background-color rgba(0, 0, 0, .2)
  position fixed
  top 0
  bottom 0
  left 0
  right 0


#shutter-button
  position fixed
  width 19vmin !important
  height 19vmin !important
  border-radius 50%
  background-color #fff
  border 1px solid #fff
  padding 1.5vmin
  background-clip content-box
  bottom 15vmin
  left 50% !important
  opacity .8
  transform translateX(-50%)
  cursor pointer
  transition opacity .2s
  -webkit-tap-highlight-color rgba(0,0,0,0)
  -webkit-tap-highlight-color transparent
  outline 0

  &:active
    opacity 1

  &:hover
    opacity .6

  &.busy
    opacity .3
    cursor wait


.debug
  user-select none
  bottom 2.5vmin
  position fixed
  width 90%
  left 50%
  transform translateX(-50%)
  font-family monospace
  font-size 3vmin
  line-height 1.5


@media (min-width 800px)
  #target
    left 50%
    top 40%
    border 2px dashed rgba(255, 255, 255, .5)
    transform translate3d(-50%, -50%, 0)
    display block
    height 70vmin
    width 70vmin

  #main-view
    .row

      h2
        font-size 60px
      h4
        font-size 20px
        bottom 70px

  #spinner
    top 40% !important


  #shutter-button
    width 100px !important
    height 100px !important
    padding 10px !important
    width 10vmin !important
    height 10vmin !important
    bottom 10vmin !important

  .x
    font-size 110px

  .debug
    font-size 1.6rem


#first-time
  position fixed
  width 100%
  font-size 2vh
  font-weight normal
  position fixed
  top 45%
  width 100%
  font-size 4.5vmin
  font-weight normal
  transform translateY(-50%)


@media (max-height 600px)
  #target
    display none


#cam-error
  width 50%
  text-align center
  font-size 3.2vmin
  line-height 1.5
  position absolute
  top 50%
  left 50%
  transform translate3d(-50%, -50%, 0)


#spinner
  animation rotator 1.4s linear infinite
  position fixed
  top 50%
  left 50%
  transform translate3d(-50%, -50%, 0)
  transition opacity .3s ease-out
  opacity 0

  &.active
    opacity 1

  circle
    fill none
    stroke-width 6
    stroke-linecap round
    cx 33
    cy 33
    r 30
    stroke-dasharray 187
    stroke-dashoffset 0
    stroke #fff
    transform-origin center
    animation dash 1.4s ease-in-out infinite


@keyframes rotator
  0%
    transform translate3d(-50%, -50%, 0) rotate(0deg)

  100%
    transform translate3d(-50%, -50%, 0) rotate(270deg)


@keyframes dash
  0%
    stroke-dashoffset 187

  50%
    stroke-dashoffset 46.75
    transform rotate(135deg)

  100%
    stroke-dashoffset 187
    transform rotate(450deg)


@media (max-height 450px)
  #main-view
    top 0 !important

  #shutter-button
    bottom 12vmin !important


*::-webkit-media-controls-panel
  display none !important
  -webkit-appearance none

*::--webkit-media-controls-play-button
  display none !important
  -webkit-appearance none

*::-webkit-media-controls-start-playback-button
  display none !important
  -webkit-appearance none
  }
})

app.router({default: '/'}, [['/', baseView]])
window.document.body.appendChild(app.start())
