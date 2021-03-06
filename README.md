## input-listener

> * 鼠标触屏点击、拖拽、缩放、旋转手势监听，和任意普通按键与组合键监听
> * 兼容同时存在鼠标和触屏的设备，跟踪交互必须的每个触点（避免响应无关触点事件导致不必要的性能消耗，多触点过度时无抖动）
> * [测试链接](https://feff01.github.io/input-listener/dist/test.html)
> * [网址导航编辑器](http://www.holdhot.com/#/editor)


## 安装

```
    npm install input-listener
```
> * 免安装可直接保存 `https://feff01.github.io/input-listener/dist/js/input_listener.js` 文件，本地 script 引入后通过 `window.InputListener` 使用


## 应用

```javascript

    import InputListener from 'input-listener';
    //const InputListener = require('input-listener');
    //const InputListener = window.InputListener;

    /**
     * @description 
     * @param {HTMLElement} 被监听的目标元素
     * @param {Object} events 可指定任意 key 不相同的监听
     * @param {?Object} options 同原生 addEventListener 方法的第三个参数
     */
    let inputListener = new InputListener(element,{

        /**
         * @description 鼠标或第一个触点按下时触发
         * @param {Event}
         */
        dragStart:console.log.bind(console,"dragStart"),

        /**
         * @description 鼠标或第一个触点（只存在一个触点时）按下并拖动时触发
         * @param {Event} 
         * @param {Array[0]} 距离上次响应移动的x轴距离
         * @param {Array[1]} 距离上次响应移动的y轴距离
         */
        dragMove:console.log.bind(console,"dragMove"),

        /**
         * @description 鼠标或最后一个触点弹起时触发
         * @param {Event} 
         */
        dragEnd:console.log.bind(console,"dragEnd"),

        /**
         * @description 当存在两个或以上触点时，第一或第二个触点移动时触发
         * @param {Event} 
         * @param {Array[0]} 距离上次响应移动的x轴距离
         * @param {Array[1]} 距离上次响应移动的y轴距离
         */
        dragMove2:console.log.bind(console,"dragMove2"),

        /**
         * @description 响应点击动作
         * @param {Event} 
         */
        click:console.log.bind(console,"click"),

        /**
         * @description 响应双指缩放手势
         * @param {Event} 
         * @param {number} 缩放距离（px）
         * @param {?Array[0]} 缩放中心点x（一次缩放手势过程中的第一次回调才存在该参数）
         * @param {?Array[1]} 缩放中心点y（一次缩放手势过程中的第一次回调才存在该参数）
         */
        pinch:console.log.bind(console,"pinch"),

        /**
         * @description 响应双指旋转手势
         * @param {Event} 
         * @param {number} 旋转弧度
         * @param {?Array[0]} 旋转中心点x（一次旋转手势过程中的第一次回调才存在该参数）
         * @param {?Array[1]} 旋转中心点y（一次旋转手势过程中的第一次回调才存在该参数）
         */
        rotate:console.log.bind(console,"rotate"),

        /**
         * @description 可用于组合键监听或者按键按下的监听（每个组合键或按键用 "," 分隔，可用 "|" 代表监听链中的"或"光系）
         * @param {Event} 
         * @param {string} 按键路径（类似 "alt+a" "arrowup+q+s" "w" 的字符串）
         */
        "alt|ArrowUp+a,arrowup+a|q+s,w_keyDown":console.log.bind(console,"keyDown"),

        /**
         * @description 监听指定的按键弹起（每个按键用 "," 分隔）
         * @param {Event} 
         */
        "alt,a,s,d_keyUp":console.log.bind(console,"keyUp"),

        /**
         * @description 监听指定的按键输入（每个按键用 "," 分隔）
         * @param {Event} 
         */
        "arrowup,q,w,e_keyPress":console.log.bind(console,"keyPress"),
    });

    /**
     * @description 由于屏幕交互事件额外支持一些冒泡功能（用于做更细致的交互定制），现在一种屏幕交互事件只支持同时存在一个监听，可通过实例化多个InputListener来支持复数个相同监听
     */
    inputListener.off("dragStart");
    inputListener.on("dragStart",console.log.bind(console,"dragStart"));

    /**
     * @description 键盘监听同一按键可存在多个不同监听回调方法
     */
    let ctrl_z_listener=console.log.bind(console,"ctrl_z_listener");
    inputListener.on("ctrl+z_keyDown",ctrl_z_listener);
    inputListener.off("ctrl+z_keyDown",ctrl_z_listener);

```