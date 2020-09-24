# Node

## Usage
```
const Node = require('butterfly-dag').Node;
class ANode extends Node {
  draw(obj) {
    // here you can custom dom according to your needs.
  }
}

canvas.draw({
  nodes: [{
    id: 'xxxx',
    top: 100,
    left: 100,
    Class: ANode // after setting the base class, the canvas will render based on the custom class.
  }]
})
```

## attribute<a name='node-attr'></a>：

| key | describe | type | default 
| :------ | :------ | :------ | :------ 
| id | unique id| string (Require) | - 
| top | y coordinate | number (Require) | - 
| left | x coordinate | number (Require) | - 
| draggable | set whether the node can be dragged | boolean (Option) | overwrite global draggable attributes
| group | group unique id | string (Option) | - 
| endpoints | endpoint data | array (Option) | - 
| Class | extended class | Class (Option) | When the extended class is passed in, the node group will be rendered according to the draw method of the extended class, and the related methods of the extended class will also override the method of the parent class.
| scope | scope | boolean (Option) | When the scope of the node is consistent with the scope of the group, it can be added to the group. You can join as you like without setting it by default.

`* The returned dom of the node must be set to position: absolute;`

## API：

### <a name='node-custom'>custom node</a>：

```js
/**
  * node draw function
  * @param {obj} data - node data
  * @return {dom} - node dom
  */
draw = (obj) => {}

/**
  * callback after node mount
  */
mounted = () => {}

/**
  * callback after node updated
  */
updated = () => {}

/**
  * remove node myself
  */
remove = () => {}

/**
  * @return {number} - node width
  */
getWidth = () => {}

/**
  * @return {number} - node height
  */
getHeight = () => {}

/**
  * @param {boolean} draggable - set whether the node is draggable
  */
setDraggable = (boolean) => {}

/**
  * focus callback
  */
focus = () => {}

/**
  * unfocus callback
  */
unFocus = () => {}
```

### <a name='node-endpoint'>custom endpoint</a>：

```js
/**
  * @param {obj} data - endpoint data (this method must be executed after the node is mounted)
  * @param {string} param.id - endpoint id
  * @param {string} param.orientation - endpoint direction (it can control the direction of the edge linkin or linkout)
  * @param {string} param.scope - scope
  * @param {string} param.type - 'source' / 'target' / undefined，ednpoint is both source and target when undefined
  * @param {string} param.dom - any sub DOM in the node can be used as a custom endpoint
  */
addEndpoint = (obj) => {}

/**
  * @param {obj} data - endpoint data (this method must be executed after the node is mounted)
  * @return {Endpoint} - Endpoint object
  */
removeEndpoint = (obj) => {}

/**
  * @param {string} pointId - endpoint id
  * @param {string(Option)} type - endpoint type (Optional)
  * @return {Endpoint} - Endpoint object
  */
getEndpoint = (id, type) => {}
```

### <a name='node-move'>move</a>：

```js
/**
  * @param {number} x - move to x coordinate
  * @param {number} y - move to y coordinate
  */
moveTo = (obj) => {}
```

### <a name='node-event'>event</a>：

```js
/**
  * emit events
  */
emit = (string, obj) => {}

/**
   * accept events
  */
on = (string, callback) => {}
```

### <a name='node-collapse'>[tree layout] 收缩 & 展开子节点</a>：

```js
/**
  * [tree layout] collapse node
  * @param {string} nodeId - nodeId
  */
collapseNode = (string) => {}

/**
  * [tree layout] expand node
  * @param {string} nodeId - nodeId
  */
expandNode = (string) => {}
```