# Rendering

Slate will render custom nodes for [`Block`](../slate-core/block.md) and [`Inline`](../slate-core/inline.md) models, based on what you pass in as your schema. This allows you to completely customize the rendering behavior of your Slate editor.

## Props

```javascript
{
  attributes: Object,
  children: Object,
  editor: Editor,
  isSelected: Boolean,
  isFocused: Boolean,
  node: Node,
  parent: Node,
  readOnly: Boolean,
}
```

### `attributes`

`Object`

A dictionary of DOM attributes that you must attach to the main DOM element of the node you render. For example:

```javascript
return <p {...props.attributes}>{props.children}</p>
```

```javascript
return (
  <figure {...props.attributes}>
    <img src={...} />
  </figure>
)
```

### `children`

`Object`

A set of React children elements that are composed of internal Slate components that handle all of the editing logic of the editor for you. You must render these as the children of your non-void nodes. For example:

```javascript
return <p {...props.attributes}>{props.children}</p>
```

### `editor`

`Editor`

A reference to the Slate [`<Editor>`](editor.md) instance. This allows you to retrieve the current `value` of the editor, or perform a `change` on the value. For example:

```javascript
const value = editor.value
```

```javascript
editor.moveToRangeOfDocument().delete()
```

### `isSelected`

`Boolean`

A boolean representing whether the node you are rendering is currently selected. You can use this to render a visual representation of the selection.

This boolean is true when the node is selected and the editor is blurred.

### `isFocused`

`Boolean`

A boolean representing whether the node you are rendering is currently focused. You can use this to render a visual representation of the focused selection.

### `node`

`Node`

A reference to the [`Node`](../slate-core/node.md) being rendered.

### `parent`

`Node`

A reference to the parent of the current [`Node`](../slate-core/node.md) being rendered.

### `readOnly`

`Boolean`

Whether the editor is in "read-only" mode, where all of the rendering is the same, but the user is prevented from editing the editor's content.

