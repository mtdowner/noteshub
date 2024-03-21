# `animation`


The sub-properties of the [`animation`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation) property are:

[`animation-composition`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-composition)

Specifies the [composite operation](https://developer.mozilla.org/en-US/docs/Glossary/Composite_operation) to use when multiple animations affect the same property simultaneously. This property is not part of the `animation` shorthand property.

[`animation-delay`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-delay)

Specifies the delay between an element loading and the start of an animation sequence and whether the animation should start immediately from its beginning or partway through the animation.

[`animation-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-direction)

Specifies whether an animation's first iteration should be forward or backward and whether subsequent iterations should alternate direction on each run through the sequence or reset to the start point and repeat.

[`animation-duration`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-duration)

Specifies the length of time in which an animation completes one cycle.

[`animation-fill-mode`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode)

Specifies how an animation applies styles to its target before and after it runs.

[`animation-iteration-count`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-iteration-count)

Specifies the number of times an animation should repeat.

[`animation-name`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-name)

Specifies the name of the [`@keyframes`](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes) at-rule describing an animation's keyframes.

[`animation-play-state`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-play-state)

Specifies whether to pause or play an animation sequence.

[`animation-timeline`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline) Experimental

Specifies the timeline that is used to control the progress of a CSS animation.

[`animation-timing-function`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)

Specifies how an animation transitions through keyframes by establishing acceleration curves.

`animation` CSS property is shorthand for:
- [`animation-name`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-name)
- [`animation-duration`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-duration)
- [`animation-timing-function`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)
- [`animation-delay`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-delay)
- [`animation-iteration-count`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-iteration-count)
- [`animation-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-direction)
- [`animation-fill-mode`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode)
- [`animation-play-state`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-play-state)
- [`animation-timeline`](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline)

```css
animation: name-of-animation

@keyframes name-of-animation {
  50% {
    width: 100px;
  }
  100% {
    width: 500px;
  }
}
```

```css
animation-name: name-of-animation;
```

```css
animation-duration: 2s;
animation-duration: 400ms;
```

```css
animation-timing-function:
```

```css
animation-delay: 5s;
animation-delay: 100ms;
```

```css
animation-iteration-count
```

```css
animation-direction
```

```css
animation-fill-mode
```

```css
animation-play-state
```

```css
animation-timeline
```
