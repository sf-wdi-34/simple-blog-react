# React.js Blog App

---

![react-logo](./images/react-white-logo.png)

---

In this lab, you will be creating a simple blog app using what you learned in the React Intro lesson. 

## Initial Setup

First, let's set up our blog app:

```bash
$ npm i -g create-react-app
$ create-react-app blog-app
$ cd blog-app
$ npm run start
```
## 1. Create a blog post component

* Create a `post` object literal in `src/index.js` that has the below properties.
  1. `title`
  2. `author`
  3. `body`
  4. `comments` (array of strings)
* Render these properties using a Post component.
* The HTML (or more accurately, JSX) composition of your Post is up to you.

## 2. Add Nested components to blog

### Nested Components 

It would be a pain to have to explicitly define every comment inside of `<Post/>`, especially if each comment itself had multiple properties.
* This problem is a tell tale sign that our separation of concerns is being stretched, and its time to break things into a new component.

We can nest Comment components within a Post component.
* We create these comments the same way we did with posts: `extends Component` and `.render`
* Then we can reference a comment using `<Comment />` inside of Post's render method.

Let's create a new file for our Comment component, `src/Comment.js`...

```js
import React, {Component} from 'react'

class Comment extends Component {
  render () {
    return (
      <div>
        <p>{this.props.body}</p>
      </div>
    )
  }
}

export default Comment
```

Then in `src/App.js`, we need to load in our `Comment` component and render it inside of our `Post` component...

```js
import React, { Component } from 'react';
// Load in Comment component
import Comment from './Comment.js'
import './App.css';


class Post extends Component {
  render() {
    return (
      <div>
        <h1>{this.props.title}</h1>
        <p>By {this.props.author}</p>
        <div>
          <p>{this.props.body}</p>
        </div>
        <h3>Comments:</h3>
        // Render Comment component, passing in data
        <Comment body={this.props.comments[0]} />
      </div>
    );
  }
}

export default Post;
```

> **Note**: We could put all of our code in one file, but it's considered a good practice to break components outs into different files to help practice separation of concerns. The only downside is we have to be extra conscious of remembering to **export / import** each component to where its rendered.


## 3. Add nested comments to your blog

Using what you've just learned, amend your `Post`'s render method to include reference to a variable, `comments`, that is equal to the return value of generating multiple `<Comment />` elements. Make sure to pass in the `comment` body as an argument to each `Comment` component. Then render the `comments` some where inside the UI for a `Post`.

> **NOTE:** You can use `.map` in `Post`'s `render` method to avoid having to hard-code all your `Comment`'s. Read more about it [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) and [here](http://cryto.net/~joepie91/blog/2015/05/04/functional-programming-in-javascript-map-filter-reduce/).
>
> **HINT I:** You should only have to return one `<Comment />` inside of `.map`.
>
> **HINT II:** Remember that whenever you write vanilla Javascript inside of JSX, you need to surround it with single brackets (`{}`).

## 4. Implement State 

Implement `state` in our Blog by making `body` a mutable value.

1. Initialize a state using a `constructor()` method for our `Post` to set a initial state. It should create a state value called `body`. Set it to the `body` of your hard-coded `post`.
2. Modify `Post`'s `render` method so that `body` comes from `state`, not `props`.
3. Create a `handleClick` method inside `Post` that updates `body` based on a user input.
  * You should use `setState` somewhere in this method.
  * How can you get a user input? Keep it simple and start with `prompt`.
4. Add a button to `Post`'s `render` method that triggers `handleClick`.

## Bonus

Use a form to take in user input.
* The post body should be updated using a method that is triggered by `onSubmit`.
* One option is to keep track of what the new input is going to be by triggering a method using `onChange` on the `<input>`
* Another option is to pass an event object to the `onSubmit` method and traverse the DOM from `e.target` to find the `<input>` value.

> **NOTE:** You're starting to mock Angular's two-way data binding!

