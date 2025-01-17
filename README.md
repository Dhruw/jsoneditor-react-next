# jsoneditor-react-next

This is a forked version of the [json-editor-react](https://github.com/vankop/jsoneditor-react)
When using this as part of a NextJS application we run into the [CSS Import Dependency Issue](https://github.com/vercel/next.js/blob/master/errors/css-npm.md).
This is a workaround for that.

## Installation

```
npm install --save jsoneditor jsoneditor-react-next
```

## Usage

```javascript
import { JsonEditor as Editor } from 'jsoneditor-react-next';
import 'jsoneditor-react/es/editor.min.css';
```

later in render method:

```jsx
render() {
    return (
        <Editor
            value={yourJson}
            onChange={this.handleChange}
        />
    );
}
```

If you want use with [Ajv](https://github.com/epoberezkin/ajv):

```jsx
import Ajv from 'ajv';

const ajv = new Ajv({ allErrors: true, verbose: true });

...

render() {
    return (
        <Editor
            value={yourJson}
            onChange={this.handleChange}
            ajv={ajv}
            schema={yourSchema}
        />
    );
}
```

If you want use with [Ace Editor](https://github.com/thlorenz/brace):

```jsx
import ace from 'brace';
import 'brace/mode/json';
import 'brace/theme/github';

...

render() {
    return (
        <Editor
            value={yourJson}
            onChange={this.handleChange}
            ace={ace}
            theme="ace/theme/github"
            schema={yourSchema}
        />
    );
}
```

Or:

```jsx
import 'brace';
import 'brace/mode/json';
import 'brace/theme/github';

...

render() {
    return (
        <Editor
            value={yourJson}
            onChange={this.handleChange}
            theme="ace/theme/github"
            schema={yourSchema}
        />
    );
}
```

Or define your own ace theme

## Async component

If you using webpack and es6 dynamic imports you can load ```jsoneditor-react``` asynchronously.
You can use [react-imported-component](https://github.com/theKashey/react-imported-component) or your own implementation

```javascript
import importedComponent from 'react-imported-component';

const JsonEditor = importedComponent(() => import(/* webpackChunkName:'jsoneditor' */'jsoneditor-react'));
```

Or with [Ajv](https://github.com/epoberezkin/ajv) and [Ace Editor](https://github.com/thlorenz/brace):

```jsx
const JsonEditor = importedComponent(() => Promise.all([
    import(/* webpackChunkName:'jsoneditor' */'jsoneditor-react'),
    import(/* webpackChunkName:'jsoneditor' */'brace'),
    import(/* webpackChunkName:'jsoneditor' */'ajv'),
    import(/* webpackChunkName:'jsoneditor' */'brace/mode/json'),
    import(/* webpackChunkName:'jsoneditor' */'brace/theme/github')
]).then(([{ JsonEditor: Editor }, ace, Ajv ]) => {
    const ajv = new Ajv();
    return function EditorHoc(props) {
        return (
            <Editor
                ace={ace}
                ajv={ajv}
                theme="ace/theme/github"
                {...props}
            />
        );
    }
}));
```

## Playground

You can view usage of ```jsoneditor-react``` using our storybook.

#### Steps to run storybook

* fork or clone repository
* ```npm run dev```
* View ```http://localhost:9001```

Right now only one story exporting in storybook: ```/stories/Editor.jsx```, to add more use ```/.storybook/config.js```

## Api

Working on ```docs``` folder.
Right now you can use [props declaration](/src/Editor.jsx)

## Test

Will be soon!😁

