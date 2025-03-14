# mockschema

[![npm package](https://img.shields.io/badge/npm-v0.0.4-blue.svg)](https://www.npmjs.com/package/mockschema)

> The best way to generate fake data to work with your components.

---

### Why you need use?
 * Tiny size: ~1kb
 * Save time
 * Increase productivity


### How it works?
When you work with Components, sometimes you don't have API yet, but you need to put some data, like an Array with Objects for your component show, simulating your API data. With Mock Schema, you don't need
create a lot of objects, variables... You just use the ```mock``` function, and the schema will be returned.


#### Install

Npm: `npm install mockschema` </br>
CDN: `https://unpkg.com/mockschema@0.0.4`

#### Real life example:

```javascript
import {h, Component, render} from 'preact';

import Appbar from 'preact-mui/lib/appbar';
import Button from 'preact-mui/lib/button';
import Container from 'preact-mui/lib/container';

import { mock, createSchema } from 'mockschema';

createSchema({
  person: {
    id:0, 
    name:'Jhon Dow', 
    age: 25
  }
})

class Example extends Component {
  render() {
    return (
      <div>
        <Appbar></Appbar>
        <Container fluid={true}>
        {/** 
          * mock will return an Array with 10 object
          * the id will auto incremented by mock
          */}
          {mock('person', 10).map( person => (
            <div>{person.id} {person.name}</div>
          ))}
          <Button color="primary">button</Button>
        </Container>
      </div>
    );
  }
}

render(<Example />, document.getElementById('example'));
```

---

### API

 Create a Schema
 * Create a Schema that will be used in your application
```javascript
/**
 * @name createSchema
 * @description Create an Schema of your fake data
 * @param {Object} schema The schema
 */
 
// store/index.js
import {createSchema} from 'mockschema';

createSchema({
  posts: {
    id: '1',
    title: 'Foo Bar',
    author: 'Jhon Doe'
  },
  animals: {
    id: 1,
    list: ['Cat', 'Dog', 'Bird']
  }
});
```

Generate your Schema
 * Always return an array with the quantity of objects passed in the function. The ```id``` attribute will be incremented automaticaly by mockschema.

```javascript
/**
  * @name mock
  * @description Generate a schema
  * @param {String | Object} schema The Object Schema
  * @param {Intenger} How many objects you want to render
  * @return {Array} An array with your schema objects
  **/
 
// state/index.js
import { mock } from 'mock-schema';

// If you create a Schema, you just use
mock('posts', 5); // -> [{id:1, title: 'Foo Bar', author: 'Jhon Doe'}, {id:2, title: 'Foo Bar', author: 'Jhon Doe'}, ...]

// Or, you can pass Objects instead
mock({ name: 'Jhon Doe', type: 'Person'}, 5); // -> [{id:1, name:'Jhon Doe', type: 'Person'}, {id:2, name:'Jhon Doe', type: 'Person'}, ...]

```
