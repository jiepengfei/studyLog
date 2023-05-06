省流: 使用[Element.animate()](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/animate) API或者JS操作[CSSKeyframesRule](https://developer.mozilla.org/en-US/docs/Web/API/CSSKeyframesRule)

涉及到滚动的功能需求时,需要给元素添加动画,如果要求是无缝滚动的话,需要使用元素宽高作为变量

但是我不知道怎么在css文件中使用js文件中需要的变量

最初我试图在JSX元素行内样式中添加动画,但是失败了:

以下这段话[出自](https://segmentfault.com/q/1010000040308956)

React Style 对应的是 HTML 中的的内联样式（inline style），内联样式处理的是单个 DOM 元素的样式。但是 `@keyframe` 是全局的动画关键帧序列，它并不是特定的样式属性，不属于某个 DOM 元素，自然也就不能通过内联样式定义。

如果一定要用 React Style 来实现，有两种情况：

1. 如果 `@keyframe` 是静态的，可以在 css 文件中定义。`style` 中通过 `animation-name` 使用。
2. 如果 `@keyframe` 要有动态性，styled-components 的实现思路应该是解析代码然后在 HTML 头部的 `<style>` 标签中定义 `@keyframe`。可以试着参照这个思路使用 [react-helmet](https://link.segmentfault.com/?enc=dB%2Bnj6QFanzSM%2FO8QZqVdQ%3D%3D.gmsMUgHiXQKknfVrDPULYrxONbt0QlmDeB3SsDEfZypwzzi1BPn%2B3plMA7wfI8Yo) 动态加入 `@keyframe`。还有一种可尝试的方法是通过 JS 操作 [CSSKeyframesRule](https://link.segmentfault.com/?enc=9tsSuCzNO7QMtQMYTjSQFg%3D%3D.HJXgkNrdHkzkVW0o%2Fop6mYX9R7LfclvdiCRlt3350GquMIdw9G9kAEkgLAp8iDiEyIyIrf5%2F2huw5wnujz97oJL7OjKiKWAnQ1RHa%2FKesv8%3D)

所以我只能在JS文件中添加动画,使用到了[Element.animate()](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/animate)这个api

```jsx
useEffect(() => {
if(textContainer && scrollBox) {
  const scrollBoxHeight = window.getComputedStyle(scrollBox).height;
  const textContainerHeight = window.getComputedStyle(textContainer).height;
  if (parseFloat(scrollBoxHeight) < parseFloat(textContainerHeight)) {
    scrollBox?.animate(
      [
        {transform:'translateY(100%)'},
        {transform:`translateY(-${textContainerHeight})`},
      ],
      {
        duration: 20000,  //  动画时长(单位毫秒)
        iterations: Infinity,
        fill: 'forwards',
        delay: 0,
        easing: 'linear',
      },
     );
     // hover暂停动画
     (scrollBox as any).onmouseover = () => {
      scrollBox.getAnimations().forEach(el=> el.pause())
    }
    (scrollBox as any).onmouseout = () => {
      scrollBox.getAnimations().forEach(el=> el.play())
    }
  }
}
}, [scrollBox, textContainer]);
```

