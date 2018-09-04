## Suggested loaders

* [sass-resources-loader](https://vue-loader.vuejs.org/en/configurations/pre-processors.html): it will helps if you want to import some global variables.

## Be careful

* [Vue's Compatibility issues in IE9](https://blog.suzper.com/2017/03/16/IE9%E5%9C%A8vue%E4%B8%8B%E7%9A%84%E4%B8%80%E4%BA%9B%E5%85%BC%E5%AE%B9/)
* Since the [change detection caveats](https://vuejs.org/v2/guide/reactivity.html#Change-Detection-Caveats) in Vue will not trigger change while you change an object in array, you may need to use `$set`。like:
```
  this.$set(this.dataList, indexOfItem, item);
```
to force tigger the update of view pages.
