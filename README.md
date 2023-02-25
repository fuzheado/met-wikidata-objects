# met-wikidata-objects
Python script to enhance Met Museum Wikidata objects

This Python script runs through all the Met Wikidata items with the generic:

    P31 -> item of collection or exhibition (Q18593264)
    P1932 -> <string Met supplied as objectName> such as "Brandy tumbler"

It starts with a SPARQL query such as this:
    
    SELECT ?item ?metid WHERE {
      ?item wdt:P31 wd:Q18593264 .
      ?item wdt:P3634 ?metid .
    }
    
To upgrade that general statement, the script takes that P1932 string and checks the exact matches on:
https://www.wikidata.org/wiki/Wikidata:GLAM/Metropolitan_Museum_of_Art/glamingest/objectName

Then uses the regex version for a wildcard match:
https://www.wikidata.org/wiki/Wikidata:GLAM/Metropolitan_Museum_of_Art/glamingest/objectName_regex

This SPARQL query identifies the most frequent "objectName" strings that we don't map to a specific P31 yet:
https://w.wiki/6Ndi
    
Here is a sample output of this script and the replacements:
https://gitlab.wikimedia.org/-/snippets/60

After one session, here's a sample output of what was replaced:

    Total examined: 23530
    Replaced: 8456