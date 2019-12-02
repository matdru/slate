# Adding Event Handlers

**Previous:**  
[Installing Slate](installing-slate.md)   


## Adding Event Handlers

Okay, so you've got Slate installed and rendered on the page, and when you type in it, you can see the changes reflected. But you want to do more than just type a plaintext string.

What makes Slate great is how easy it is to customize. Just like other React components you're used to, Slate allows you to pass in handlers that are triggered on certain events. You've already seen how the `onChange` handler can be used to store the changed editor value, but let's try adding more...

Let's use the `onKeyDown` handler to change the editor's content when we press a key.

Here's our app from earlier:

```javascript
class App extends React.Component {
  state = {
    value: initialValue,
  }

  onChange = ({ value }) => {
    this.setState({ value })
  }

  render() {
    return <Editor value={this.state.value} onChange={this.onChange} />
  }
}
```

Now we add an `onKeyDown` handler:

```javascript
class App extends React.Component {
  state = {
    value: initialValue,
  }

  onChange = ({ value }) => {
    this.setState({ value })
  }

  // Define a new handler which prints the key that was pressed.
  onKeyDown = (event, editor, next) => {
    console.log(event.key)
    return next()
  }

  render() {
    return (
      <Editor
        value={this.state.value}
        onChange={this.onChange}
        onKeyDown={this.onKeyDown}
      />
    )
  }
}
```

Cool, now when a key is pressed in the editor, its corresponding keycode is logged in the console.

Now we want to make it actually change the content. For the purposes of our example, let's implement turning all ampersand, `&`, keystrokes into the word `and` upon being typed.

Our `onKeyDown` handler might look like this:

```javascript
class App extends React.Component {
  state = {
    value: initialValue,
  }

  onChange = ({ value }) => {
    this.setState({ value })
  }

  onKeyDown = (event, editor, next) => {
    // Return with no changes if the keypress is not '&'
    if (event.key !== '&') return next()

    // Prevent the ampersand character from being inserted.
    event.preventDefault()

    // Change the value by inserting 'and' at the cursor's position.
    editor.insertText('and')
  }

  render() {
    return (
      <Editor
        value={this.state.value}
        onChange={this.onChange}
        onKeyDown={this.onKeyDown}
      />
    )
  }
}
```

With that added, try typing `&`, and you should see it suddenly become `and` instead!

This offers a sense of what can be done with Slate's event handlers. Each one will be called with the `event` object, and the `editor` that lets you perform commands. Simple!

**Next:**  
[Defining Custom Block Nodes](defining-custom-block-nodes.md)   


