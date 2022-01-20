# How to sort strings in foreign languages?

Sorting an array of strings in English language is prettry straightforward: use the Array's sort function.
But for non-English languages like German, Spanish, etc., it may produce incorrect results.  
  
Let us take an example of sorting strings in Spanish language.  

```
let spanishWords = ['único','árbol', 'cosas', 'fútbol'];
spanishWords.sort(); 
// ["cosas", "fútbol", "árbol", "único"] which is incorrect order
```

To correctly compare, here are two options:

**Option 1:**  
Using localeCompare function
```
spanishWords.sort((a,b) => {
  return a.localeCompare(b, 'es');
})
// ["árbol", "cosas", "fútbol", "único"]
```

[localeCompare in MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)

**Option 2:**  
The Intl.Collator object enables language-sensitive string comparison.  

```
spanishWords.sort(new Intl.Collator('es').compare);
// ["árbol", "cosas", "fútbol", "único"]
```
NOTE: The Intl object is the namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting. 

[Collator in MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Collator)

[back](../)
