

```dataviewjs
//get all md files in vault
const files = app.vault.getMarkdownFiles()

//create an array with the filename and lines that include the desired tag
let arr = files.map(async(file) => {
  const content = await app.vault.cachedRead(file)
//turn all the content into an arra
let lines = await content.split("\n").filter(line => line.includes("- [ ]"))
return ["[["+file.name.split(".")[0]+"]]", lines]
})

//resolve the promises and build the table
Promise.all(arr).then(values => {
console.log(values)
//filter out files without "ad-question" and the note with the dataview script
const exists = values.filter(value => value[1][0] && value[0] != "[[dataviewjs-testing]]")
dv.table(["file", "lines"], exists)
})
``` 
