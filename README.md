# Module 10 Reflection
## Malvin Muhammad Raqin - 2306275821

### 1. Print Task Outside Spawner
![alt text](image.png)

The output **"Malvin's Computer: hey hey"** appears first because it executes outside any asynchronous context and runs immediately as part of the regular synchronous flow within the `main()` function.

Meanwhile, the **"howdy!"** and **"done!"** outputs are contained within an async block that gets submitted to the task executor through the `spawner.spawn(...)` method. These asynchronous operations don't run immediately—instead, they get placed in a queue waiting for the executor to process them.

The execution order follows this pattern:
1. Synchronous code runs immediately, which includes `println!("Malvin's Computer: hey hey");`
2. The spawner gets dropped, indicating that no additional tasks will be submitted
3. `executor.run()` starts processing the queued asynchronous tasks, resulting in the delayed output of **"howdy!"**, followed by the timer wait, and finally **"done!"**

This demonstrates a fundamental principle in asynchronous Rust programming: async tasks are lazy by nature and only advance when actively polled by an executor. The spawned future remains dormant until `executor.run()` is invoked to drive it forward.