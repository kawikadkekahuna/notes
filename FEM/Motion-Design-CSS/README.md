ntroduction

### Transitions
-- --
#### Overview
  Can be thought of as: _"How do we change this property if it is changed by CSS"_

 A transition describes how a property should display change when given a different value.

### Shorthand
```bash
.foo {
  transition: <property> <duration> <timing-function> <delay>
}
```
### Verbose
```bash
.foo {
  transition-property // property you want to transition
  transition-duration // seconds or milliseconds
  transition-timing-function "cushioning" for the transition.  Defaults to `ease` [OPTIONAL]
  transition-delay: // the number of milli/seconds to delay the transition before firing. [OPTIONAL]
}
```
### Multiple Properties:
```bash
.foo {
  transition-property: height color // property you want to transition
  transition-duration: 500ms 100s // seconds or milliseconds
  transition-delay: 1000s 500s // the number of milli/seconds to delay the transition before firing.  // optional
}
```
- Note: Downside of writing transitions in this format is that you need to assure that property values match up.  ie: the first property given should be correlated with the first delay and duration given.

So, with that given, here is a better example using css statements:

```bash
.foo {
  transition:
    color 2s,
    transform 300ms 1s;
}
  ```

Only **SOME** properties are transitionable
  - Full list of transition-properties can be found [here] (https://www.w3.org/TR/css3-transitions/#animatable-properties-)
#### Key points
---
 - For production, better to measure time in `ms`.  Better compatability with JS / avoid unit conversions.
 - Better than littering CSS with decimal points
 - Avoid using `transition: all`, as it may cause unwanted animations / transitions. Also heavy resource cost because it's watching all possible properties.
 - Replace "ease" with "slow" ie: ease-in == slow-in, fast out (inferred).
   - `ease-in` can be thought of as acceleration
   - `ease-out` can be through of deceleration
   - easings.net for preset bezier curve values
 - User initiated events should probably be `ease-out`, to enhance the client's interactiveness with your application
 - Unasked events, such as a modal asking for a user's email, should be `ease-in`, ultimately to lessen the chances that your audience would be surprised and provides a less disruptful experience.

#### Pros of Transitions
-- --

 - **Single fire**: If you only want something to happen once.
 - **Granularity**: If you would only animate one or two properties in a given state
 - **Bulletproof**: If transitions aren't supported the change happens anyway.

#### Durations
-- --

 - 100ms will feel instantaneous to the user.
 - 1 second will still feel connected.
 - < 10s, should be a movie or explicit "play" button
 - 250~300ms sweet spot for many animations
 - Gross medium for vast majority of humans will notice change
 - faster != better
   - Animations may be necessary to improve user experience.  The cost we pay with performing these animations is time.



### Animations
-- --
  Can be thought of as _"I told you to change the property, now do it"_

  ### Shorthand
```bash
.foo {
  animation: <keyframe> <duration> <timing-function> <delay> <iterate>
}

@keyframes <keyframe> {
  0% { background: #000; }
  100% { background: #fff; }
}
```
### Verbose
```bash
.foo {
  animation-name // The name of the keyframe block
  animation-duration // How long it takes from animations to go from 0 - 100%
  animation-iteration-count // The number of times you want to go from 0 - 100%.  Default: 1
  animation-timing-function // Like transition-timing-function
  animation-delay: // Like transition-delay
  animation-fill-mode: // <backwards, forwards, both, none>
  animation-play-state: // Can be running or paused
  animation-direction: // Can determine order of keyframes
}
```
### Multiple Properties:
Same as transitions:
```bash
.foo {
  animation: {
    <keyframe1> 1s linear 1,
    <keyframe2> 2s ease-out infinite 2s;
  }
}
```

### Steps timing function:

 - steps(x, <start, end>) is a timing function
 - ...splits a block of keyframes into x equal steps, then hops between them.
 - Second argument determiens what frame should be "eaten".

### Takeways
- Fill Modes:
    - **backwards**: Retains properties before it plays.
    - **forwards**: Retains properties before it plays.
    - **none**: Retains properties before it plays.
    - **both**: Retains properties before it plays.
- Play State:
    - Defaulted to **running**
    - Can be **paused**
- Direction:
  - Defaulted to **normal**
  - **alternate**: will run 0% - 100%, and then 100% - 0%, and then 0% - 100%, repeat.
  - **reverse**: will run from 100% to 0%.
  - **alternate-reverse**: will run from 100% to 0%, then 0% to 100%, then 100% to 0%, repeat.
- **Looping** is only done through css animations.
- **Self starting**: Doesn't require trigger like **transition**
- **Repeating**: You can set how many times it repeats
- **Alternating**: Can alternate between the end state and start state
- **Grouping**: Each animation can change a number of properties.

