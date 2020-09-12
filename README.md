# my-own-react

Based on the repo by [Rodrigo Pombo](https://github.com/pomber/didact). The goal is to understand the code behind the React library.

The direct article usedto involve `Hooks` is from:
https://pomb.us/build-your-own-react/

## Steps Invovled

---

- `Step I`: The createElement Function
- `Step II`: The render Function
- `Step III`: Concurrent Mode
- `Step IV`: Fibers
- `Step V`: Render and Commit Phases
- `Step VI`: Reconciliation
- `Step VII`: Function Components
- `Step VIII`: Hooks

**However, but first...**

## Step Zero: Review

---

    const element = <h1 title="foo">Hello</h1>
    const container = document.getElementById("root")
    ReactDOM.rennder(element, container)

Line one defines a React Element.

The Next one gets a node from the DOM.

The last one renders the React element into the container.

**This example will remove React specific code with vanilla JavaScript.**

### **Replace `Line One`**

---

`Line One` is JSX defined so we need valid JS. JSX is transformed to JS by build tools like Babel. The tranform process:

- Replace the code inside the tags with a call to createElement, passing the tag name, the props, and the children as parameters.

React.createElement creates an object from it's arguments. Replace the function call with it's output:

    const element = React.createElement(
        "h1",
        { title: "foo"},
        "Hello"
    )
    const container = document.getElementById("root")
    ReactDOM.render(element, container)

An `element` is an object with two properties: type and props (it has more but `these two` are important for the project).

`Type` is a string that specifies the type of DOM node to create which is the tagName you pass to document.createElement when you create an HTML element.

`Props` is another object having the keys and values from the JSX attributes. It has a special property of `children`.

`Children` in this case is a string, but it’s usually an array with more elements. That’s why elements are also trees:

    const element = {
        type: "h1",
        props: {
            title: "foo",
            children: "Hello",
        },
    }

    const container = document.getElementById("root")
    ReactDOM.render(element, container)

### **Replace `Line 3`**

---

Note `Render` is where React changes the DOM on `Line 3`.

Create a `node` element of type for `h1`, and assign
all the element props to that node.

Plus create the nodes for the children. This is for `children` in the element object.

    const element = {
        type: "h1:,
        props: {
            title: "foo",
            children: "Hello",
        },
    }

    const container = document.getElementById("root")

    const node = document.createElement(element.type)
    node["title"] = element.props.title

    const text = document.createTextNode("")
    text["nodeValue"] = element.props.chidren

The final part is to append the `textNode` to the `h1` and the `h1` to the `container`:

    node.appendChild(text)
    container.appendChild(node)

**NOW** The app is the same as before but without using React:

    const element = {
        type: "h1",
        props: {
            title: "foo",
            children: "Hello",
        }
    }

    const container = document.createElementById("root")

    const node = document.createElement(element.type)
    node["title"] = element.props.title

    const text = document.createTextNode("")
    text["nodeValue] = element.props.chidren

    node.appendChild(text)
    container.appendChild(node)
