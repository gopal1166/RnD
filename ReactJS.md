### Adding background color to entire react app: 13-07-2020:

in public/index.html:
```
<body style="background-color: red">
```


### Modify antd default theme (primary color) : 11-07-2020

[link](https://medium.com/@okoriechinedusunday/a-baby-guide-to-overriding-antdesign-theme-and-color-aa6df1f85e0)
```
npm install less -g
```

Create a new file 'my-theme.less' in node_modules/antd/dist , and paste below
```
@import "./antd.less";   // Import Ant Design styles by less entry

@primary-color: #d228e9;                         // primary color for all components
@link-color: #1890ff;                            // link color
@success-color: #52c41a;                         // success state color
@warning-color: #faad14;                         // warning state color
@error-color: #f5222d;                           // error state color
@font-size-base: 16px;                           // text font size
@heading-color: rgba(0, 0, 0, .85);              // heading text color
@text-color: rgba(0, 0, 0, .65);                 // major text color
@text-color-secondary : rgba(0, 0, 0, .45);      // secondary text color
@disabled-color : rgba(0, 0, 0, .25);            // disable state color
@border-radius-base: 4px;                        // major border radius
@border-color-base: #d9d9d9;                     // major border color
@box-shadow-base: 0 2px 8px rgba(0, 0, 0, .15);  // major shadow for layers

```
and can remove unnecessay item from the above list

cd to node_modules/antd/dist
```
lessc --js my-theme.less result.css
```

```
lessc --js my-theme.less ../../../src/style/custom-antd.css
```

Now style folder will be created in src folder. 

Replace the exisitng antd.css file path with the custom-antd.css path in App.css

Done----------------------------------


