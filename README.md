# React Native SectionList getItemLayout

This package provides a function that helps you construct the `getItemLayout` function for your `SectionList`s. For an explanation of why this exists, see [this post](https://medium.com/@jsoendermann/sectionlist-and-getitemlayout-2293b0b916fb). It's meant to be used like this:

```javascript
import sectionListGetItemLayout from 'react-native-section-list-get-item-layout'

class MyComponent extends React.Component {
  constructor(props) {
    super(props)

    this.getItemLayout = sectionListGetItemLayout({
      // The height of the row with rowData at the given sectionIndex and rowIndex
      getItemHeight: (rowData, sectionIndex, rowIndex) => sectionIndex === 0 ? 100 : 50,

      // These four properties are optional
      getSeparatorHeight: () => 1 / PixelRatio.get(), // The height of your separators
      getSectionHeaderHeight: () => 20, // The height of your section headers
      getSectionFooterHeight: () => 10, // The height of your section footers
      listHeaderHeight: 40, // The height of your list header
    })
  }

  render() {
    return (
      <SectionList
        {...otherStuff}
        getItemLayout={this.getItemLayout}
      />
    )
  }
}
```


We modify this project to fit on our project we added this on `dist/index.js`


```javascript
"use strict";
exports.__esModule = true;
exports["default"] = (function (_a) {
    var getItemHeight = _a.getItemHeight, _b = _a.getSeparatorHeight, getSeparatorHeight = _b === void 0 ? function () { return 0; } : _b, _c = _a.getSectionHeaderHeight, getSectionHeaderHeight = _c === void 0 ? function () { return 0; } : _c, _d = _a.getSectionFooterHeight, getSectionFooterHeight = _d === void 0 ? function () { return 0; } : _d, _e = _a.listHeaderHeight, listHeaderHeight = _e === void 0 ? 0 : _e;
    return function (data, index) {
        var i = 0;
        var sectionIndex = 0;
        var elementPointer = { type: 'SECTION_HEADER' };
        var offset = typeof listHeaderHeight === 'function'
            ? listHeaderHeight()
            : listHeaderHeight;
        while (i < index) {
            switch (elementPointer.type) {
                case 'SECTION_HEADER': {
                    var sectionData = data[sectionIndex].data; 
                    const finalHeight = data?.[sectionIndex]?.headerHeight || getSectionHeaderHeight(sectionIndex) // << added line on line 15
                    offset += finalHeight; // << added line on line 16
```


```javascript
        var length;
        switch (elementPointer.type) {
            case 'SECTION_HEADER':
                const finalHeight = data?.[sectionIndex]?.headerHeight || getSectionHeaderHeight(sectionIndex) // << added line on line 53
                length = finalHeight; // << added line on line 54
                break;
            case 'ROW':
```