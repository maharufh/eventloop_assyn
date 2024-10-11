# eventloop_assyn

Explanation of Output and the Event Loop:
"1. Program started" is logged immediately because it is the first synchronous operation. The function demonstrateEventLoop() starts executing from the top, and this message is logged before any asynchronous operation begins.
"2. Timeout message (after 1 second)" is logged after 1 second due to the setTimeout function. The setTimeout callback is placed in the task queue. After the synchronous part of the code completes (including awaiting the promise), the event loop allows this callback to be processed.
"3. Promise resolved (after 2 seconds)" is logged after 2 seconds. The promise is created and starts its timer for 2 seconds. Once the timer completes, the promise is resolved and the await keyword allows the function to "pause" and wait for this promise to resolve. Once resolved, the message is logged to the console.
"4. End of program" is logged immediately after the promise resolves because it follows the await statement. The function doesn't proceed to this line until the promise has been resolved.

Explanation of Why This Order Occurs:
Event Loop: The event loop handles the execution of both synchronous and asynchronous code. When the synchronous code runs, it gets executed line by line. Asynchronous tasks, such as setTimeout and Promise resolution, are handled in the background, and their callbacks are placed in the event loop's task queue to be processed once the synchronous code completes.
setTimeout: The setTimeout callback is scheduled to run after 1 second. However, it will only be executed once the synchronous code and any awaited asynchronous operations (such as promises) have completed. After the 1 second passes, the event loop processes the setTimeout callback, logging the second message.
Promise: The promise is set to resolve after 2 seconds. Using await tells the JavaScript engine to pause the execution of the function until the promise is resolved. Once the promise resolves (after 2 seconds), the next log message (the resolved value) is printed.
Order: The setTimeout (1 second) happens before the promise resolves (2 seconds). However, the await pauses the function until the promise resolves, so the program logs the promise resolution (after 2 seconds) and then proceeds to the final log statement ("End of program").
