## event loop

JavaScript 为了协调事件、用户交互、脚本、渲染、网络等，就搞出来一个 **事件循环（Event Loop）**。

#### Event Loop 执行过程

- 一开始整个脚本 `script` 作为一个宏任务执行
- 执行过程中，**同步代码** 直接执行，**宏任务** 进入宏任务队列，**微任务** 进入微任务队列。
- 当前宏任务执行完出队，检查微任务列表，有则依次执行，直到全部执行完毕。
- 执行浏览器 `UI` 线程的渲染工作。
- 检查是否有 `Web Worker` 任务，有则执行。
- 执行完本轮的宏任务，回到步骤 2，依次循环，直到宏任务和微任务队列为空。

事件循环中的异步队列有两种：宏任务队列（`MacroTask`）和 微任务队列（`MicroTask`）。

**宏任务队列可以有多个，微任务队列只有一个。**



**宏任务** 包括：(**DOM操作任务源、用户交互任务源、网络任务源、history traversal任务源**)

- `script`
- `setTimeout`
- `setInterval`
- `setImmediate`
- `I/O`     **(用户交互任务源)**
- `UI rendering`

**微任务** 包括：**event loop里只有一个microtask 队列**

- `MutationObserver`
- `Promise.then()/catch()`
- 以 `Promise` 为基础开发的其他技术，例如 `fetch API`
- V8 的垃圾回收过程
- Node 独有的 `process.nextTick`
  

### 浏览器渲染
- 在一轮event loop中多次修改同一dom，只有最后一次会进行绘制。
- 渲染更新（Update the rendering）会在event loop中的tasks和microtasks完成后进行，但并不是每轮event loop都会更新渲染，这取决于是否修改了dom和浏览器觉得是否有必要在此时立即将新状态呈现给用户。如果在一帧的时间内（时间并不确定，因为浏览器每秒的帧数总在波动，16.7ms只是估算并不准确）修改了多处dom，浏览器可能将变动积攒起来，只进行一次绘制，这是合理的。
- 如果希望在每轮event loop都即时呈现变动，可以使用requestAnimationFrame。