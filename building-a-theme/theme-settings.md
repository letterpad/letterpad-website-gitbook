# Theme Settings

You can offer some level of customizations to the users using your theme. To do that, create `settings.json` file in the root of your theme folder. It should contain an array of objects, where each object represents a HTML element. So the basic structure should be like this:

```text
[ 
   { ... },
   { ... }
] 
```

> As these options will be availble publicly, dont provide options like passwords, api keys, or personal details.

These are the elements that you can provide.

### Input box

```javascript
{        
  "name": "first-name",
  "type": "text",       
  "tag": "input",        
  "placeholder": "Enter your name",        
  "defaultValue": "Foo Bar",        
  "label": "Enter your name",        
  "helpText": "..."    
 }
```

### Radio Button

```javascript
{        
  "name": "display-footer",
  "type": "radio",       
  "tag": "input",   
  "options": ["Yes", "No"],            
  "defaultValue": "No",        
  "label": "Would you like to display a footer ?",        
  "helpText": ".."    
 }
```

### Checkbox

```javascript
{        
  "name": "fruit-likes",
  "type": "checkbox",       
  "tag": "input",   
  "options": ["Orange", "Apple", "Banana"],         
  "defaultValue": ["Apple"], // <== This is an array
  "label": "Which fruits do you like ?",        
  "helpText": ".."    
 }
```

### Dropdown

```javascript
{        
  "name": "post-count",      
  "tag": "select",   
  "options": ["5", "10", "15", "20"],         
  "defaultValue": 25,
  "label": "How many posts would you like to display ?",        
  "helpText": ".."    
 }
```

This settings will be available to you automatically in the Layout Component as props as `props.themeConfig`



