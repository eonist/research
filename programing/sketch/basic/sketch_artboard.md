## Get fartboard

```js
var firstPage = context.document.pages().firstObject()
var artboard = firstPage.artboards().firstObject()
log(artboard) // artboard
```

## Get artboard names

```javascript
var copyNames = []
var numBoards = 0
for (var i = 0; i < selection.length; i++) {
    var current = selection[i];
    if ([current className] == "MSArtboardGroup") {
        copyNames.push([current name] + '');
        numBoards +=1
     }
  }
  if (numBoards == 0) {
    doc.showMessage("At Least One Artboard Must Be Selected");
    return;
  }
}
```

## Get artboards:

```javascript
var getAllArtboardNames = function(context) {
    let pages = context.document.pages();
    var names = []
    // Filter layers using NSPredicate
    for(var i = 0; i < pages.length; i++) {
        var currentPage = pages[i]
        var scope =  [currentPage children],
        predicate = NSPredicate.predicateWithFormat("(className == %@)", "MSArtboardGroup"),
        layers = [scope filteredArrayUsingPredicate:predicate];
        var loop = [layers objectEnumerator], layer;

        while (layer = [loop nextObject]) {
	     var nameOfBoard = [layer name]
            if (nameOfBoard.indexOf("-synced") < 0) {
                names.push(nameOfBoard);
            }
        }
    }
    return names;
}
```

## Get artboards (alternative)

```javascript
let artboardsOnOtherPages = [];
let pages = Array.fromNSArray(document.pages());
pages = pages.filter(page => page != document.currentPage());
for (var i = 0; i < pages.length; i++) {
    var artboards = Array.fromNSArray(pages[i].artboards());
    artboardsOnOtherPages = artboardsOnOtherPages.concat(artboards);
}
```

## Create artboard

```js
let Artboard = sketch.Artboard
let myArtboard = new Artboard()
myArtboard.parent = page
myArtboard.frame = { x: 0, y: 0, width: 400, height: 400 }
```

## Remove artboard

```js
var firstPage = context.document.pages().firstObject()
var artboard = firstPage.artboards().firstObject()
log(artboard)
artboard.removeFromParent()
```

## Remove all artboards:
```js
var firstPage = context.document.pages().firstObject()
var artboards = firstPage.artboards()
artboards.forEach(artboard => {
    artboard.removeFromParent()
});
```
