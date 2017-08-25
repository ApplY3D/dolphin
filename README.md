<p align="center"><a href="http://miloslav.website/dolphin" target="_blank"><img width="100"src="http://miloslav.website/dolphin/media/logo.svg"></a></p>
<p align="center"><h1 align="center">Dolphin</h1></p>

<br>

> _If what you're doing is unnecessary difficult, then you maybe doing it wrong._  

<br>

Dolphin is full-svg diagram editor. I made it in two weeks for my ITMO graduation.

It may be not the software engineering masterpiece, but I've done what needed to be done and got an 🅰 mark.
Consider Dolphin as pretty straightforward example of how [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) work: you either edit the text in the editor or move diagram, and by doing that you change the model, which is represented as the text at the text editor. After you make changes, the diagram updates itself.

Creating Dolphin was such an educational experience for me, and I've learned a lot.

## Core concepts and the process
[Functional programming](https://en.wikipedia.org/wiki/Functional_programming) in JavaScript [is maybe an antipattern](https://hackernoon.com/functional-programming-in-javascript-is-an-antipattern-58526819f21e), but functional _style_ is great. Since quick prototyping with completely new tools may produce loads of errors, pure functions may help you a lot on debugging. That's why I decided to make use of them.

Initially I thought this tool as something like typical React+Redux web app and was coding it accordingly. As the academic deadline came closer and closer, and I had absolutely no time to have a rest, so soon I threw designing away and went to raw coding. That was awful mistake that lead to huge overhead and complete loss of sleep. I was adding more and more tools that I had never used before, and very soon I had cool Webpack config, React+Grommet UI, co-op editing with Gun.js and much more, but the code was completely messed up. That wasn't great, so I decided to calm down and rewrite the UI and the data storage (the hardest parts because I couldn't use pure functions), and that latest version is the one you may see now.

I had several breaking changes during the development.

 - __Initial: “Functional appoach to SVG”__  
I just wanted this tool to use pure functions, but this ended up to be impossible because each and every method of SVG.js has direct side effects on DOM. It just wasn't _meant to be_. You can't just make an SVG element and render it when you want it to be rendered, like in React. The element renders instantly when you create it, and that kind of behavior made me to stop coding in functional style. Functional style and SVG.js are incompatible.

 - __Change 1: Moving to OOP__  
Since SVG.js is appeared to be object-oriented, it seemed nice to build the components (diagram element, connection) as SVG.js classes. I did it and it was good and easy. It wasn't functional, but it definetely was better than my old approach.

 - __Change 2: Moving to CSS__  
I've done terrible mistake using SVG.js styling, and the code was all messed up very quickly. After 500 lines of crappy code (oh my god) when things came to style merging, I realized that I was recreating browser CSS engine and then decided to just attach some classes to the elements and make everything else in CSS. That was like magic.

 - __Change 3: Redux falls into place__  
Tools without undo function are awful. That's why I used Redux: I had my undo and redo implemented easily. It was good at the beginning, but then...

 - __Change 4: Gun server and awful consequences__  
The server was needed. Since Logux wasn't released back then, I decided to use Gun.js.  
[_frantically codes all night long_]  
I got the situation when diagram was being loaded to Redux store, and Redux event updated Gun, and Gun event updated Redux, and this wasn't going to stop. That was awful. I was too tired to use Redux the right way, and that situation made me to learn Redux much better after the graduation. But back then, I had to replace Redux with Gun.

 - __Change 5: Trying to make UI with React and Grommet__  
I need an UI. React UI libraries big picture seems boring now: the UI libraries are just not ready for production yet. Some of them looks bad, some of them behaves bad. Except for one. Grommet looks amazing. The bad things started at the very beginning: [Grommet just doesn't seem to work](https://github.com/grommet/grommet-cli/issues/35). There was very little time left before the deadline, so I decided to dig Grommet on my own. Thanks Internet, it worked.  
I had my UI done very quickly.  
UI is ready, diagram editor is ready, so let's just put it together...  
...  
__Oh no! React doesn't allow side effects!__   
... 
After hours of messing around, I managed to put them together. Don't repeat this at home.

 - __Change 6: Gun authentication and why it's awful__  
_coming soon_

 - __Change 7: Major cleenup__  
_coming soon_

## Errors made
_coming soon_

## Lessons learned
_coming soon_

## Good parts
_coming soon_

## Tools used
 - [Redux](http://redux.js.org/)
 - [Gun.js](http://gun.js.org/)
 - [SVG.js](http://svgjs.com/) ([very good community](https://github.com/svgdotjs/svg.js/issues/684), thanks [@Fuzzyma](https://github.com/Fuzzyma) and others)
 - [React](https://facebook.github.io/react/)
 - [Grommet](https://grommet.github.io/)
 - [Webpack](https://webpack.github.io/)
 - [Ace](https://ace.c9.io/)