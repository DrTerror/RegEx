# Reg-Ex-Hax

## Zeile mit String finden (z. B. zum Löschen)

!!! Wichtig !!!
    RegEx einschalten
    finden von \r \n abschalten!
    Ersetzen durch: <NIX>

```    
.+(TEXT).+[\r\n|\n\r|\n]
.+(TEXT|TEXT2|TEXT3).*[\r\n|\n\r|\n]
```    

Danach müssen noch Leerzeilen gelöscht werden.


### alte versuche

```    
^.+?\TEXT.+$\r\n
^.*#TEXT.*$\r\n
^(\s)*(TEXT).*(\r\n|\n\r|\r|\n)?
^.*(TEXT).*(\r\n|\n\r|\r|\n)?
```    

### This is also possible with Notepad++

Goto the search menu Ctrl+F and there to the "Mark" tab. Check "Bookmark line" (if there is no "Mark" tab update to the current version). Then just enter your search term and click "Mark All"
==> All line containing the search term are bookmarked.
Now go to the Menu "Search -> Bookmark -> Remove Bookmarked lines"

#### Remove duplicate lines    

```    
^(.*?)$\s+?^(?=.*^\1$)
```    
    

## MOD- und FUNC-Makros ersetzen:

Suchstring:
```
	<ALTER_NAME>\s*\(\s*(\w+)\s*\)
```
Ersetzenstring:
```
	<NEUER_NAME>_$1
```
Bsp.:
```
	(PARA)Func\s*\(\s*(\w+)\s*\)
->  fn$1_$2
```

Weitere Bespiele:
```
	(PARA_)(\w+\()
->  fn$1$2
```

```
	func\s*\(\s*(\w+)\s*\)
->  fn<MOD_TOKEN>_$1
```

```
	MOD\s*\(\s*(\w+)\s*\)
->  <MOD_TOKEN>_$1
```


## Umlaute :
```
//^s*[äöüß]
```
		
```
UTF8  <-->  Cp1252
ä           Ã¤
Ä           Ã„
ö           Ã¶
Ö           
ü           Ã¼
Ü           Ãœ
ß           ÃŸ
```


### Umlaute in Kommentaren:
```
\/\/.*[ÄäÖöÜüß]
```

---

## JAVA

```java
function umlaut(str) {
 return str
  .replace(/Â|À|Å|Ã/g, "A")
  .replace(/â|á|à|å|ã/g, "a")
  .replace(/Ä/g, "AE")
  .replace(/ä/g, "ae")
  .replace(/Ç/g, "C")
  .replace(/ç/g, "c")
  .replace(/É|Ê|È|Ë/g, "E")
  .replace(/é|ê|è|ë/g, "e")
  .replace(/Ó|Ô|Ò|Õ|Ø/g, "O")
  .replace(/ó|ô|ò|õ/g, "o")
  .replace(/Ö/g, "OE")
  .replace(/ö/g, "oe")
  .replace(/Š/g, "S")
  .replace(/š/g, "s")
  .replace(/ß/g, "ss")
  .replace(/Ú|Û|Ù/g, "U")
  .replace(/ú|û|ù/g, "u")
  .replace(/Ü/g, "UE")
  .replace(/ü/g, "ue")
  .replace(/Ý|Ÿ/g, "Y")
  .replace(/ý|ÿ/g, "y")
  .replace(/Ž/g, "Z")
  .replace(/ž/, "z"); 
}
```    


## Versuch C++-Kommentare in Ansi-C-Kommentare zu konvertieren

### C++-Line-Comments -> C-Block-Comments

Text:
```
    test"123"(456)#[78]9+0!_abc/{}@
```

```    
s#//\(.*\)#/*\1 */#
s#//(.*)#/*\1 */#
s!//\(.*\)!/*\1*/!g
```    


I think you should first replace the /* and */ after //, and then
replace //. Something like:

```    
s!//.*\zs/\*!{!
s!//.*\zs\*/!}!
s!//\(.*\)!/*\1 */!
```    


why not /\*(.(?!\*/))*\*/ ? first an /* then any character not followed by */ then */

Wouldn't it be simpler to use /\*.*?\*/

I like to add raw-string r"/[*]([^*]|([*][^/]))*[*]/" as it worked in python !

```    
((\s*)(\/\/)(\s*))+(.*)[\n|\n\r|\r\n\r]

^(.*)(\/\/)(.*)
```    


```    
(\s*)((\s*)(\/\/)(\s*))+(.*)([\n|\n\r|\r\n\r])
--> $1/*$5$6 */$7
```    

### test strings

```    
// test"123"(456)#[78]9+0!_abc/{}@ test"123"(456)#[78]9+0!_abc/{}@
//test"123"(456)#[78]9+0!_abc/{}@ test"123"(456)#[78]9+0!_abc/{}@
   // test"123"(456)#[78]9+0!_abc/{}@ test"123"(456)#[78]9+0!_abc/{}@
   //test"123"(456)#[78]9+0!_abc/{}@ test"123"(456)#[78]9+0!_abc/{}@
test"123"(456)#[78]9+0!_abc/{}@ // test"123"(456)#[78]9+0!_abc/{}@
 test"123"(456)#[78]9+0!_abc/{}@ // test"123"(456)#[78]9+0!_abc/{}@

///////test"123"(456)#[78]9+0!_abc/{}@ // test"123"(456)#[78]9+0!_abc/{}@
// // // /test"123"(456)#[78]9+0!_abc/{}@

// test"123"(456)#[78]9+0!_abc/{}@ /* test"123"(456)#[78]9+0!_abc/{}@ */

/*
// test"123"(456)#[78]9+0!_abc/{}@
*/
```    


### ???

```    
^([ \t]*(\.\w{2,}+\s+(\w*)\s+(\w*)\s+(.*)\R))
^([ \t]*(\.\w{2,}+[ \t]+(\w*)[ \t]+(\w*)[ \t]+(.*)))
(^.*\R*$)(?!([ \t]*(\.\w{2,}+[ \t]+(\w*)[ \t]+(\w*)[ \t]+(.*))))

^([ \t]*(\.\w{2,}+[ \t]+(\w*)[ \t]+(\w*)[ \t]+(.*)))$
```    

```    
(?:(?!([ \t]*(\.\w{2,}+[ \t]+(\w*)[ \t]+(\w*)[ \t]+(.*)))).)*
```    


## komplette zeile löschen

```    
([\S| ]*(__TEXT__)[\S| ]*)\r\n
([\S| ]*(__TEXT__)[\S| ]*)\n
```    
