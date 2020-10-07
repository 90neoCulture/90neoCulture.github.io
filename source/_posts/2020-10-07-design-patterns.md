---
layout:     post
title:      "JavaScript设计模式初体验"
subtitle:   "JavaScript设计模式"
date:       2020-10-07
author:     "90neoculture"
catalog:    true
categories: 
    - 前端
    - js
    - 设计模式
tags:
    - 前端
    - js
    - 设计模式
---


### 设计模式

#### 设计模式的目的

设计模式是为了让程序（软件）具有更好的：

- 代码重用性
  - 即：相同的功能的代码，无需多次编写
- 可读性
  - 即：编程规范性，便于其他程序员的阅读和理解
- 可扩展性
  - 即：也称为可维护性，当需要新增功能时，非常方便
- 可靠性
  - 即：新增功能后，对原有功能没有影响
- 使程序实现高内聚、低耦合的特性

### 设计模式的七大原则

#### 单一职责原则

##### 1. 概念

基本介绍： 对类来说，即一个类应该只负责一项职责。如类A负责两个不同职责：职责1，职责2。当职责1需求变更而改变A时，可能造成职责2执行错误，所以需要将类A的粒度分解为A1，A2。 让我们来看以下交通工具的例子：

```javascript
class Transportation {
  constructor(name){
    this.name = name
  }

  run() {
    console.log(`${this.name}在地上跑`)
  }
}

const transportation = new Transportation('汽车')
transportation.run()
const transportation2 = new Transportation('轮船')
transportation2.run()
const transportation3 = new Transportation('飞机')
transportation3.run()
// 结果为：
// 汽车在地上跑
// 轮船在地上跑
// 飞机在地上跑
```

上述打印结果，轮船和飞机在地上跑是不合理的，于是我们遵循单一职责原则对上述代码进行改造：

```javascript
class GroundTransportation{
  constructor(name){
    this.name = name
  }

  run(){
    console.log(`${this.name}在地上跑`)
  }
}
class WaterTransportation{
  constructor(name){
    this.name = name
  }

  run(){
    console.log(`${this.name}在水上跑`)
  }
}
class AirTransportation{
  constructor(name){
    this.name = name
  }

  run(){
    console.log(`${this.name}在天上跑`)
  }
}
const transportation = new GroundTransportation('汽车')
transportation.run()
const transportation2 = new WaterTransportation('轮船')
transportation2.run()
const transportation3 = new AirTransportation('飞机')
transportation3.run()
// 结果为
// 汽车在地上跑
// 轮船在水上跑
// 飞机在天上跑
```

上述代码符合单一职责原则，但是重复过多，过于冗余，且类中的方法足够少，于是我们进行进一步改写：

```javascript
class Transportation {
  constructor(name){
    this.name = name
  }

  runGround() {
    console.log(`${this.name}在地上跑`)
  }
  runWater() {
    console.log(`${this.name}在水上跑`)
  }
  runAir() {
    console.log(`${this.name}在天上跑`)
  }
}

const transportation = new Transportation('汽车')
transportation.runGround()
const transportation2 = new Transportation('轮船')
transportation2.runWater()
const transportation3 = new Transportation('飞机')
transportation3.runAir()
// 结果为
// 汽车在地上跑
// 轮船在水上跑
// 飞机在天上跑
```

##### 2.tips:

- 降低类的复杂度，一个类只负责一项职责
- 提高类的可读性，可维护性
- 降低变更引起的风险
- 通常情况下，我们应当遵守单一职责原则，只有逻辑足够简单，才可以在代码级别违反单一职责原则；只有类中方法数量足够少，才可以在方法级别保持单一职责原则