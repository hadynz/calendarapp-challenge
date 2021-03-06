# calendar-app-challenge

[![Build Status](https://travis-ci.org/hadynz/calendar-app-challenge.svg)](https://travis-ci.org/hadynz/calendar-app-challenge)

Calendar app coding challenge. Demo page is at http://hady.geek.nz/calendar-app-challenge.

## Introduction
I was approached by an organisation to do a very intriguing coding challenge as part of their recruitment process. The challenge had three basic rules (detailed in the following section) and a screenshot of the expected output's look and feel.

## The Code Challenge

Given a set of events, render the events on a single day calendar (similar to Outlook, Calendar.app, and 
Google Calendar). There are several properties of the layout:

1. No events may visually overlap.
2. If two events collide in time, they must have the same width.
3. An event should utilize the maximum width available, but constraint 2) takes precedence over this constraint.

Each event is represented by a JS object with a start and end attribute. The value of these attributes is the 
number of minutes since 9am. So `{start:30, end:90)` represents an event from 9:30am to 10:30am. The events should be 
rendered in a container that is 620px wide (600px + 10px padding on the left/right) and 720px (the day will end 
at 9pm). The styling of the events should match the attached screenshot.

You may structure your code however you like, but you must implement the following function in the global namespace. 
The function takes in an array of events and will lay out the events according to the above description.

```js
function layOutDay(events) {
  // ...
}
```

This function will be invoked from the browser’s JavaScript console for testing purposes. If it cannot be invoked, 
the submission will be rejected. In your submission, please implement the calendar with the following input and style 
the calendar accordingly.

```js
[{start: 30, end: 180}, {start: 540, end: 600}, {start: 560: 620}, {start: 610, end: 670}]
```

## Solution
Unknown to me initially, this problem turned out to be a very tricky algorithm challenge around the laying out of events whilst taken into account event clashes taking place in the day. Best way to see my solution is to walk through the code; it's heavily commented.

The front end was built using custom web components built on top of the [Polymer framework][polymer]. I used the awesome [Polymer Yeoman generator][generator-polymer] for scaffolding the project and getting up and running really quickly.

Other frameworks used in the solution are [MomentJS][momentjs] for date and time manipulation, and a [Mocha][mochajs] and [Chai][chaijs] combo for my unit tests.

The key learning from this coding challenge is coming up with valid test scenarios in an early stage, and using test-driven development, keep chipping at the problem in code. Writing small and modular modules was key in reducing the challenge's complexity into smaller pieces that were easy to think and solve individually.

## Test Scenarios

[Sample test scenarios][test-scenarios] with their expected visual layouts were created according to the 
coding challenge rules. The following are some compiled examples to use in a browser's console to have a squiz at 
how the application updates and renders different event layouts.

```js
// Scenario B1
layOutDay([
  {id: 'event1', start: 0, end: 180},
  {id: 'event2', start: 60, end: 300},
  {id: 'event3', start: 240, end: 360},
  {id: 'event4', start: 240, end: 360},
  {id: 'event5', start: 300, end: 360},
]);

// Scenario C4
layOutDay([
  {id: 'event1', start: 0, end: 240},
  {id: 'event2', start: 60, end: 300},
  {id: 'event3', start: 120, end: 360},
  {id: 'event4', start: 120, end: 360},
  {id: 'event5', start: 240, end: 300},
  {id: 'event6', start: 300, end: 360},
  {id: 'event7', start: 300, end: 420}
]);

// Scenario C5
layOutDay([
  {id: 'event1', start: 0, end: 240},
  {id: 'event2', start: 60, end: 240},
  {id: 'event3', start: 120, end: 300},
  {id: 'event4', start: 120, end: 360},
  {id: 'event5', start: 240, end: 300},
  {id: 'event6', start: 240, end: 360},
  {id: 'event7', start: 300, end: 360},
  {id: 'event8', start: 300, end: 360}
]);

// Scenario C6
layOutDay([
  {id: 'event1', start: 0, end: 180},
  {id: 'event2', start: 0, end: 180},
  {id: 'event3', start: 60, end: 240},
  {id: 'event4', start: 60, end: 300},
  {id: 'event5', start: 180, end: 300},
  {id: 'event6', start: 240, end: 300},
  {id: 'event7', start: 240, end: 360},
  {id: 'event8', start: 300, end: 360}
]);

```

## License

Copyright (c) 2014 Hady Osman  
Licensed under the [MIT][license] license.

[test-scenarios]: http://bit.ly/1vrptyB
[license]: https://github.com/hadynz/calendar-app-challenge/blob/master/LICENSE
[polymer]: https://www.polymer-project.org/
[generator-polymer]: https://github.com/yeoman/generator-polymer
[momentjs]: http://momentjs.com/
[mochajs]: http://mochajs.org/
[chaijs]: http://chaijs.com/
