
Hanzi Writer
=====================

[![CircleCI](https://img.shields.io/circleci/project/github/chanind/hanzi-writer/master.svg)](https://circleci.com/gh/chanind/hanzi-writer/tree/master)
[![Codecov](https://img.shields.io/codecov/c/github/chanind/hanzi-writer/master.svg)](https://codecov.io/gh/chanind/hanzi-writer)
[![npm](https://img.shields.io/npm/v/hanzi-writer.svg)](https://www.npmjs.com/package/hanzi-writer)

https://chanind.github.io/hanzi-writer

Hanzi Writer is a free and open-source javascript library for Chinese character stroke order animations and stroke order practice quizzes. Works with both simplified and traditional characters.

[Live demo](https://chanind.github.io/hanzi-writer/demo.html)

## Getting Started and Documentation

For more info and instructions on getting started check out https://chanind.github.io/hanzi-writer

## Data source

The chinese character svg and stroke order data used by Hanzi Writer is derived from the [Make me a Hanzi](https://github.com/skishore/makemeahanzi) project with some slight tweaks. The data can be found in the [Hanzi Writer Data](https://github.com/chanind/hanzi-writer-data) repo. There's a visualizer for this data [here](https://chanind.github.io/hanzi-writer-data).

## Contributing

Pull requests are welcome! If you would like to contribute code, you'll need to be able to build the project locally. After cloning the Hanzi Writer repo, you can get it set up by running:

```
yarn install
```

You can run tests with `yarn test` and you can build the project with `yarn build`.

## License

Hanzi Writer is released under an [MIT](https://raw.githubusercontent.com/chanind/hanzi-writer/master/LICENSE) license.

The Hanzi Writer data comes from the [Make Me A Hanzi](https://github.com/skishore/makemeahanzi) project, which extracted the data from fonts by [Arphic Technology](http://www.arphic.com/), a Taiwanese font forge that released their work under a permissive license in 1999. You can redistribute and/or modify this data under the terms of the Arphic Public License as published by Arphic Technology Co., Ltd. A copy of this license can be found in [ARPHICPL.TXT](https://raw.githubusercontent.com/chanind/hanzi-writer-data/master/ARPHICPL.TXT).

## Example code 

```
<!-- Container for Hanzi Writer characters with flex display -->
<div style="display: flex; gap: 20px;">
  <!-- Container for first Hanzi Writer character -->
  <div id="character-container1"
    style="width: 200px; height: 200px; border: 1px solid #000;"></div>
  <!-- Container for second Hanzi Writer character -->
  <div id="character-container2"
    style="width: 200px; height: 200px; border: 1px solid #000;"></div>
</div>
<p><button id="animate-button">Start</button></p>
<!-- Include Hanzi Writer library -->
<p>
  <script
    src="https://cdn.jsdelivr.net/npm/hanzi-writer@2.1.0/dist/hanzi-writer.min.js">
  </script>
  <script>
    document.addEventListener('DOMContentLoaded', function() {
      var writer1 = HanziWriter.create('character-container1', '你', {
        width: 200,
        height: 200,
        padding: 10,
        strokeColor: '#000000',
        radicalColor: '#FF0000',
        delayBetweenStrokes: 1000,
      });


      var writer2 = HanziWriter.create('character-container2', '好', {
        width: 200,
        height: 200,
        padding: 10,
        strokeColor: '#000000',
        radicalColor: '#FF0000',
        delayBetweenStrokes: 1000,
      });

      function chainAnimations() {
        var delayBetweenAnimations = 1000; // milliseconds
        writer1.hideCharacter();
        writer2.hideCharacter();

        writer1.animateCharacter({
          onComplete: function() {
            setTimeout(function() {
              writer2.animateCharacter();
            }, delayBetweenAnimations);
          }
        });
      }

      document.getElementById('animate-button').addEventListener('click',
        chainAnimations);

    });
  </script>
</p>
```
