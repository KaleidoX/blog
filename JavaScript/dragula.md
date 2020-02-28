dragula.js 使用方式

```javascript
dragula(Array.from(document.querySelectorAll(".part")), {
  isContainer: function(el) {
    console.log(1)
    return false; // only elements in drake.containers will be taken into account
  },
  moves: function(el, source, handle, sibling) {
    console.log(2)
    return true; // elements are always draggable by default
  },
  accepts: function(el, target, source, sibling) {
    console.log('elements change end', { el, target, source, sibling })
    // 元素换地方后触发
    return true; // elements can be dropped in any of the `containers` by default
  },
  invalid: function(el, handle) {
    console.log(4)
    return false; // don't prevent any drags from initiating by default
  },
  direction: "vertical", // Y axis is considered when determining where an element would be dropped
  copy: false, // elements are moved by default, not copied
  copySortSource: false, // elements in copy-source containers can be reordered
  revertOnSpill: false, // spilling will put the element back where it was dragged from, if this is true
  removeOnSpill: false, // spilling will `.remove` the element, if this is true
  mirrorContainer: document.body, // set the element that gets mirror elements appended
  ignoreInputTextSelection: true // allows users to select input text, see details below
});
```



