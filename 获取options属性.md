## HTML

```html
<select name="choose-fruits" id="fruits" >
   <option value="Apple"  data-sku="fruits-1">Apple</option>
   <option value="Orange" data-sku="fruits-2">Orange</option>
   <option value="banana" data-sku="fruits-3">banana</option>
<select>
```

## JavaScript

```js
let fruitList = document.getElementById("fruits");
let index = fruitList.selectedIndex;
let fruitSku = fruitList.options[index].getAttribute("data-sku")
fruitList.onchange = () => {
    index = fruitList.selectedIndex;
    fruitSku = fruitList.options[index].getAttribute("data-sku")
    console.log(fruitSku);
}
```

## jQuery

```js
// 直接获取
console.log($('#fruits').find("option:selected").attr("data-sku"));
// onChange
$('#fruits').change(function () {
    console.log($(this).find("option:selected").data('sku'));
})
```

