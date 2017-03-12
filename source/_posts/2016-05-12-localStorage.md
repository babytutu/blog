---
title: localStorage
date: 2016-05-12 00:43:31
tags:
categories: [code]
---

## safair localStorage 踩坑

#### ios上safari开启隐身模式时，localStorage无法写入新的内容，并且会抛出异常导致js无法正常执行，最终页面无法正常加载。
[解决方案](https://github.com/nbubna/store)

<!--more-->

##### 常用方法
```js
store(key, data);                 // sets stringified data under key
store(key);                       // gets and parses data stored under key
store({key: data, key2: data2});  // sets all key/data pairs in the object
store();                          // gets all stored key/data pairs as an object
store(false);                     // clears all items from storage
```

##### 更多技巧
```js
store.set(key, data[, overwrite]); // === store(key, data);
store.setAll(data[, overwrite]);   // === store({key: data, key2: data});
store.get(key[, alt]);             // === store(key);
store.getAll();                    // === store();
store.clear();                     // === store(false);
store.has(key);                    // returns true or false
store.remove(key);                 // removes key and its data
store.each(callback);              // called with key and data args, return false to exit early
store.keys();                      // returns array of keys
store.size();                      // number of keys, not length of data
store.clearAll();                  // clears *ALL* areas (but still namespace sensitive)
```