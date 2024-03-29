---
title: "How to take comments in json"
date: 2023-09-13
---


## comments in json

the first problem was how to comment in a json file

Here has a quite simply solution for it.

I had ever heard about minify-json library which can use a function call to remove all the comments in the files.

## highlight problem

But the second problem was raising. How to support the highlight function when we use comments in json feature.

All I can think about was that we should use the javascript file highlight function for our json file.

It compare to the json file is just one different point which we should add “export default” in the keyword phrase in the beginning of the file.

## How to make a compatible for existed data

And there is an old data compatible issue.  The existed data all using the json format store in database already.

But if we want to using the feature, it’s a force update bounce to effect our existed data. 

There is the quick shoot for that problem. When we edit the existed data. We can detect whether the beginning start with “export default”, if not, we should add to.

So, when they publish the new version of it. It’ll have the data correct process automatically.

## How to detect the data format correct or nor

It’s simple when we’re using the json format to validate user’s input correct or nor. It’s just using JSON.parse() to try to parse the string. If there is an error happened. It’s obviously not the valid JSON.

But when it comes to the we need to detect it correct or nor in javascript. It’s quite different.

However, when we’re writing json in javascript file, it’s more freedom than writing in json file. For example the key we name in javascript we can not wrap in “” quotes, and the value also. 

If we use the json data in javascript call with JSON.parse() function. you’ll get format error 100 %!

How to solve it?

There is a thought but no way to implement yet.

before we use the function prettier

![prettierBefore](https://raw.githubusercontent.com/cjfff/blog/f18d31857705aa2e6a7c381179290ced5649480b/assets/how-to-take-commonts-in-json/image1.png)

then after

![prettierAfter](https://raw.githubusercontent.com/cjfff/blog/f18d31857705aa2e6a7c381179290ced5649480b/assets/how-to-take-commonts-in-json/image2.png)

As you can see, we get the ideally json format.

![format](https://raw.githubusercontent.com/cjfff/blog/f18d31857705aa2e6a7c381179290ced5649480b/assets/how-to-take-commonts-in-json/image3.png)

For that ideally output, I found the shot for that, though you maybe thinking it’s a little bit hack.  But what I wanted was that let the function run first.

Ok, Let’s take a look on it how I solve the problem.

The first, we have two functions defined. and when we called the jsonminify and get the result of it, then we can pass out result onto the function getObject which create a eval function inside and return the object out. 

```tsx
import jsonminify from 'jsonminify'

export const createFN = (obj: string) => {
  return `(() => (${obj}))()`;
};

export const getObject = (str: string) => {
  return eval(createFN(str));
};

getObject(jsonminify(strin))
```

We can take a look on the result.

![result](https://raw.githubusercontent.com/cjfff/blog/f18d31857705aa2e6a7c381179290ced5649480b/assets/how-to-take-commonts-in-json/image4.png)

Sum up, maybe we can detect the json correct or nor, but we can get the right format json from javascript file, it’s well for us to be continue done the function.

## backend solution

Base on the solution we mentioned above. It’s a simply deal when we tackle to the data.

We just need to handle one place. The Get method. We purpose on not any effects on the original usage. 

So, base on the existed function, we add a query key “raw” to the get-config api. When we need the raw data(it means the comments no to be remove), we need to add the raw=1 in the query of url.

For example like that:  `/api/v1/config/jsonComment?raw=1` 

Then we get the data don’t get through the comments remove process.

![remove](https://raw.githubusercontent.com/cjfff/blog/f18d31857705aa2e6a7c381179290ced5649480b/assets/how-to-take-commonts-in-json/image5.png)

And if you don’t pass the query to it, it’ll return the json to you as usually as it does. 

## Summary

Through the start to the end. 

We target on how to handle the first question “How to comments in JSON”. Unfortunately, It’s impossible to comments in JSON though.

The technique society recommends us to use the key “_comments” to add some notes on the json.

But that solution is not our wanted. In the end, I found the javascript-library `jsonminify`. but we lack of the editor supported the highlight of coding syntax. If we’re still using the JSON file extension for it. When we add some comments on json. We’ll get errors immediately. So, In the end, I’ve consider to using the javascript file extension to achieve the new feature. But base on the solution. I encountered others issues. I need to found a way to format the data when it needs to be json.

However, it works so well in the end. 

In the end, thanks for your time for read this.
