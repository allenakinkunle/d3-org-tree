[![GitHub stars](https://img.shields.io/github/stars/benyasin/d3-org-tree.svg?style=flat-square)](https://github.com/benyasin/d3-org-tree/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/benyasin/d3-org-tree.svg?style=flat-square)](https://github.com/benyasin/d3-org-tree/issues)
[![GitHub forks](https://img.shields.io/github/forks/benyasin/d3-org-tree.svg?style=flat-square)](https://github.com/benyasin/d3-org-tree/network)
[![GitHub last commit](https://img.shields.io/github/last-commit/benyasin/d3-org-tree.svg?style=flat-square)](https://github.com/benyasin/d3-org-tree)

<div style="width: 100%; height:150px; text-align:center; display:flex; flex-direction: row; justify-content: center; align-items: center;">
  <a href="javascript:void(0)" style="display:inline-block;">
    <img src="https://user-images.githubusercontent.com/1866848/112085779-165e5b00-8bc6-11eb-9fea-82498bb953d5.png" width="60%">
  </a>
</div>

## Futures

`d3-org-tree` is highly customizable tree built with d3.js v6 that can run in modern browser like `Chrome`, `Edge`, `Firefox` and `Safari`.
Except d3.js, it does not have any third-party dependencies.

Some d3-org-tree features:
*  custom node style, including svg and pure html dom through `template`
*  customize the node behavior, including `expand` child nodes, `add` child nodes, and `delete` it
*  customize the current node `highlight` style and can manually change the current node
*  pre-set or dynamically change the layout `orientation`, link style, and whether to `display arrows`
*  pre-set the `width/height` of the svg container and the margin offset of the content
*  pre-set transform animation `duration`
*  customize callback function on node `click`,`add` and `remove` event

## Demo

* <a target="_blank" href="https://github.com/benyasin/d3-org-tree-vue-demo">Vue integration demo</a>

![tree](https://user-images.githubusercontent.com/1866848/88409973-4b809680-ce08-11ea-99a7-ac49d47f7cf7.png)

## Installing

```
npm i d3-org-tree
```

## Usage

```javascript
import OrgTree from "d3-org-tree";

const orgTree = new OrgTree()
orgTree.container('body') //dom element
       .data(/**{}*/)     //data json array, example as below
       .svgWidth(800)
       .svgHeight(600)
       .highlight({
            "borderWidth": 1,
            "borderRadius": 15,
            "borderColor": {"red": 50,"green": 255,"blue": 30,"alpha": 1},
            "backgroundColor": {"red": 20,"green": 100,"blue": 40,"alpha": 1}
        })
       .initialZoom(.3)
       .onNodeClick(d => {
            console.log(d + " node clicked")
        })
        .onNodeAdd(d => {
            console.log(d + " node added")
            orgTree.addNode(/*added node json*/)
        })
        .onNodeRemove(d => {
            console.log(d + " node removed")
            orgTree.remove(/*removed nodeId*/)
        })
       .render()
```

**data example**:
```json
[  {
     "nodeId": "O-1",
     "parentNodeId": null,
     "width": 325,
     "height": 139,
     "borderWidth": 1,
     "borderRadius": 15,
     "borderColor": {
       "red": 15,
       "green": 140,
       "blue": 121,
       "alpha": 0.5
     },
     "backgroundColor": {
       "red": 0,
       "green": 81,
       "blue": 90,
       "alpha": 0.5
     },
     "template": "<div class=\"domStyle\">\n<span>Ben</span></div>",
     "expanded": true,
     "added": false,
     "removed": false
   },
   {
     "nodeId": "O-2",
     "parentNodeId": "O-1",
     "width": 319,
     "height": 134,
     "borderWidth": 1,
     "borderRadius": 15,
     "borderColor": {
       "red": 15,
       "green": 140,
       "blue": 121,
       "alpha": 0.5
     },
     "backgroundColor": {
       "red": 0,
       "green": 81,
       "blue": 90,
       "alpha": 0.5
     },
     "template": "<div class=\"domStyle\"><span>Honey</span></div>",
     "expanded": true,
     "added": true,
     "removed": false
   }]
```
## API
            
|  Properties  | Usage |
|  --- | --- |
|  svgWidth  | `number`, the svg width, and will be 100% of the container's width if not set|
|  svgHeight  | `number`, the svg height, and will be `600` if not set |
|  container  | `string`, the svg dom selector, can be a class name or dom tag name, the default value is `body`|
|  backgroundColor  | `string`, background color of the svg container, the default value is `#fafafa` |
|  data  | `array`, all nodes data definition, the data struct can be seen above |
|  highlight  | `object`, define highlight styles of the current node |
|  current  | `string`, mark the current chosen node |
|  duration  | `number`, the transition duration, the default value is `600` |
|  strokeWidth  | `number`, the stroke width of node, the default value is `3` |
|  linkColor  | `object`, the rgba color object of link, the default value is `3` |
|  linkWidth  | `number`, the stroke width of link, the default value is `5` |
|  initialZoom  | `number`, the initial zoom scale, the default value is `0.4` |
|  orientation  | `string`, the layout orientation, which value is one of `left-to-right`、`right-to-left`、`top-to-bottom`、`bottom-to-top`, and the default one is `right-to-left` |
|  collapsible  | `boolean`, show the expand/collapse button, the default value is `false`, if its value is `false`, all `expanded` property in each data object will not take in effect  |
|  displayArrow  | `boolean`, show the link arrow, the default value is `true` |
|  straightLink  | `boolean`, display the link with straight line, the default value is `false`, transform it to curve line when set the property to `true`|

|  Method  | Usage |
|  --- | --- |
|  onNodeClick(nodeId)  | `function`, callback after node clicked |
|  onNodeAdd(nodeId)  | `function`, callback after the add button clicked |
|  onNodeRemove(nodeId)  | `function`,callback after the remove button clicked |

|  Callback  | Usage |
|  --- | --- |
|  transformLayout(orientation)  | `function`, change the the layout orientation, the passed value can be `left-to-right`、`right-to-left`、`top-to-bottom`、`bottom-to-top` |
|  transformStraightLink(straightLink)  | `function`, change the the link style to straight line, the passed value can be `false`、`true` |
|  toggleArrow(display)  | `function`, toggle visibility of link arrow, default value is `false` |
|  addNode(nodeJson)  | `function`, add a children node under a parent node you clicked |
|  removeNode(nodeId)  | `function`, remove a node by the nodeId |

## Changelog

**0.0.8** Changes:

* Fixed bugs for svg element position

**0.0.7** Changes:

* Added an exported switch property for controls of the expand and collapse button

**0.0.6** Changes:

* Re-adjusted position of the add and remove buttons
* Add expand and collapse buttons to manually show and hide sub-nodes

**0.0.5** Changes:

* Added function for transform link line style
* Set default link style as curve line

**0.0.4** Changes:

* Added control for arrows visibility
* optimized link position

**0.0.3** Changes:

* Fixed node distance bug
* Added a vue integrated demo

**0.0.2** Changes:

* Added layout orientation support
* Completed documentation

**0.0.1** Changes:

* The initial version first publish to npm library

## Contributing

If the existing component doesn't meet your needs, fork the project, implement the future and an example using it, send us a pull request, for consideration for inclusion in the project.

If you'd like to contribute consistently, show me what you've got with some good pull requests!