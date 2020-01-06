### d2s

![](https://github.com/dschu012/d2s/workflows/.github/workflows/release.yml/badge.svg)

The goal of this project is to create an es6 compliant reader/writer of Diablo II save files. Additionally, the library should be able to consume files generated by nokka's Go implementation [d2s](https://github.com/nokka/d2s), therefore the output of reading a save will closely mirror the Go's output.

##### Examples
* https://dschu012.github.io/d2s/  [[Source](docs/index.html)]

Using [d2s-ui](https://github.com/dschu012/d2s-ui) for a frontend: 
* https://diablo.dannyschumacher.com/#/
* https://resurgence.dannyschumacher.com/#/

##### API/General Usage

```typescript
/**
* @see constants.bundle.min.js for an already parsed version of 1.13c data
* @param buffers: object of ALL txt files. example: {
*  "ItemStatCost.txt": "Stat\tIDt\Send...",
*  "string.txt": "WarrivAct1IntroGossip1\t45}Greetings,...",
*  ...
* }
* @return constants: constant data required for parsing built from the txt files.
**/
function readConstantData(buffers: any): types.IConstantData

/**
* @param buffer: Uint8Array representation of the file
* @param constants: constant data used for reading the files. @see readConstantData or constants.bundle.min.js
* @param userConfig: optional configuration. used for if there is a dll edit to allow larger stash sizes. example: {
*  extendedStash: true
* }
* @return d2s: the parsed save information
**/
function read(buffer: Uint8Array, constants: types.IConstantData, userConfig?: types.IConfig): Promise<types.ID2S>;

/**
* @param d2s: the parsed save information
* @param constants: constant data used for reading the files. @see readConstantData or constants.bundle.min.js
* @param userConfig: optional configuration. used for if there is a dll edit to allow larger stash sizes. example: {
*  extendedStash: true
* }
* @return buffer: Uint8Array representation of the file
**/
function write(data: types.ID2S, constants: types.IConstantData, userConfig?: types.IConfig): Promise<Uint8Array>;
```

##### Useful Links:
* https://github.com/nokka/d2s
* https://github.com/krisives/d2s-format
* http://paul.siramy.free.fr/d2ref/eng/
* http://user.xmission.com/~trevin/DiabloIIv1.09_File_Format.shtml
* https://github.com/nickshanks/Alkor
* https://github.com/HarpyWar/d2s-character-editor