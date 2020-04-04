# vue-text-slide

Vue component `TextSlide` to animate text changes with default or custom styles. Whenever your data property changes, the component will animate leaving / entering values. 

[Demo](https://codesandbox.io/s/vue-text-slide-demo-zlq32)

```
<TextSlide :txt="msg" />
```

Default styles can be overriden like:

```
<TextSlide
  :txt="count"
  :styles="{background:'red', height:'2em', width:'2em', borderRadius:'1em'}"
  :styles-inner="{color:'white', alignItems:'center', justifyContent:'center'}"
  distance-x="50%"
  data-key="give-me-unique-key"
/>
```

## optional props

- `styles`, an object to style the component's outer box
- `styles-inner`, an object to style the component's inner box
- `distance-x`, to override the default translateX amount `5%`
- `data-key`, optional to make each component unique for application that uses multiple components

