# Style guide

* La documentation est composée de fichiers markdown, nommés suivant le format `minuscules-avec-tirets.md`. 
  * Les underscores dans les noms de fichiers sont autorisés lorsqu'ils sont présents dans le sujet que le document va décrire (par exemple `child_process `).
  * Certains fichiers, tels que les fichiers markdown de premier niveau, sont a des exceptions.
* Les fichiers doivent être limité à 80 caractères par ligne.
* La mise en forme décrite dans `.editorconfig` est à préférer. 
  * Un [plugin](http://editorconfig.org/#download) est disponible pour certains éditeurs afin d'appliquer automatiquement ces règles.
* Changes to documentation should be checked with `make lint-md`.
* American English spelling is preferred. "Capitalize" vs. "Capitalise", "color" vs. "colour", etc.
* Use [serial commas](https://en.wikipedia.org/wiki/Serial_comma).
* Avoid personal pronouns in reference documentation ("I", "you", "we"). 
  * Personal pronouns are acceptable in colloquial documentation such as guides.
  * Use gender-neutral pronouns and gender-neutral plural nouns. 
    * OK: "they", "their", "them", "folks", "people", "developers"
    * NOT OK: "his", "hers", "him", "her", "guys", "dudes"
* When combining wrapping elements (parentheses and quotes), terminal punctuation should be placed: 
  * Inside the wrapping element if the wrapping element contains a complete clause — a subject, verb, and an object.
  * Outside of the wrapping element if the wrapping element contains only a fragment of a clause.
* Documents must start with a level-one heading.
* Prefer affixing links to inlining links — prefer `[a link][]` to `[a link](http://example.com)`.
* When documenting APIs, note the version the API was introduced in at the end of the section. If an API has been deprecated, also note the first version that the API appeared deprecated in.
* When using dashes, use [Em dashes](https://en.wikipedia.org/wiki/Dash#Em_dash) ("—" or `Option+Shift+"-"` on macOS) surrounded by spaces, as per [The New York Times Manual of Style and Usage](https://en.wikipedia.org/wiki/The_New_York_Times_Manual_of_Style_and_Usage).
* Including assets: 
  * If you wish to add an illustration or full program, add it to the appropriate sub-directory in the `assets/` dir.
  * Link to it like so: `[Asset](/assets/{subdir}/{filename})` for file-based assets, and `![Asset](/assets/{subdir}/{filename})` for image-based assets.
  * For illustrations, prefer SVG to other assets. When SVG is not feasible, please keep a close eye on the filesize of the asset you're introducing.
* For code blocks: 
  * Use language aware fences. ("```js")
  * Code need not be complete — treat code blocks as an illustration or aid to your point, not as complete running programs. If a complete running program is necessary, include it as an asset in `assets/code-examples` and link to it.
* When using underscores, asterisks, and backticks, please use proper escaping (`\_`, `\*` and `` \` `` instead of `_`, `*` and `` ` ``).
* References to constructor functions should use PascalCase.
* References to constructor instances should use camelCase.
* References to methods should be used with parentheses: for example, `socket.end()` instead of `socket.end`.
* Function arguments or object properties should use the following format:
  
  *     * `name` {type|type2} Optional description. **Default:** `value`.
    
    <!--lint disable maximum-line-length remark-lint-->
  
  * For example: `* <code>byteOffset` {integer} Index of first byte to expose. **Default:** `0`.</code> <!--lint enable maximum-line-length remark-lint-->
  
  * The `type` should refer to a Node.js type or a [JavaScript type](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Data_structures_and_types).

* Function returns should use the following format: 
  * `* Returns: {type|type2} Optional description.`
  * E.g. `* Returns: {AsyncHook} A reference to <code>asyncHook`.</code>

* Use official styling for capitalization in products and projects.
  
  * OK: JavaScript, Google's V8 <!--lint disable prohibited-strings remark-lint-->
  
  * NOT OK: Javascript, Google's v8 <!-- lint enable prohibited-strings remark-lint-->

* Use *Node.js* and not *Node*, *NodeJS*, or similar variants.
  
  * When referring to the executable, *`node`* is acceptable.

See also API documentation structure overview in [doctools README](../tools/doc/README.md).