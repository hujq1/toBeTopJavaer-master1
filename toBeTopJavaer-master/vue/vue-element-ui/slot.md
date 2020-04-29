vue中的插槽————slot
什么是插槽？
插槽（Slot）是Vue提出来的一个概念，正如名字一样，插槽用于决定将所携带的内容，插入到指定的某个位置，从而使模板分块，具有模块化的特质和更大的重用性。
插槽显不显示、怎样显示是由父组件来控制的，而插槽在哪里显示就由子组件来进行控制
怎么用插槽？
默认插槽
父组件

<template>
  <div>
    我是父组件
    <slotOne1>
      <p style="color:red">我是父组件插槽内容</p>
    </slotOne1>
  </div>
</template>
在父组件引用的子组件中写入想要显示的内容（可以使用标签，也可以不用）

子组件(slotOne1)

<template>
  <div class="slotOne1">
    <div>我是slotOne1组件</div>
    <slot></slot>
  </div>
</template>
在子组件中写入slot，slot所在的位置就是父组件要显示的内容



当然再父组件引用的子组件中也可以写入其他组件
父组件

<template>
  <div>
    我是父组件
    <slotOne1>
      <p style="color:red">我是父组件插槽内容</p>
      <slot-one2></slot-one2>
    </slotOne1>
  </div>
</template>
子组件(slotOne2)

<template>
  <div class="slotOne2">
    我是slotOne2组件
  </div>
</template>


具名插槽
子组件

<template>
  <div class="slottwo">
    <div>slottwo</div>
    <slot name="header"></slot>
    <slot></slot>
    <slot name="footer"></slot>
  </div>
</template>
在子组件中定义了三个slot标签，其中有两个分别添加了name属性header和footer

父组件

<template>
  <div>
    我是父组件
    <slot-two>
      <p>啦啦啦，啦啦啦，我是卖报的小行家</p>
      <template slot="header">
          <p>我是name为header的slot</p>
      </template>
      <p slot="footer">我是name为footer的slot</p>
    </slot-two>
  </div>
</template>
在父组件中使用template并写入对应的slot值来指定该内容在子组件中现实的位置（当然也不用必须写到template），没有对应值的其他内容会被放到子组件中没有添加name属性的slot中



插槽的默认内容
父组件

<template>
  <div>
    我是父组件
    <slot-two></slot-two>
  </div>
</template>
子组件

<template>
  <div class="slottwo">
    <slot>我不是卖报的小行家</slot>
  </div>
</template>
可以在子组件的slot标签中写入内容，当父组件没有写入内容时会显示子组件的默认内容，当父组件写入内容时，会替换子组件的默认内容



编译作用域
父组件

<template>
  <div>
    我是父组件
    <slot-two>
      <p>{{name}}</p>
    </slot-two>
  </div>
</template>
<script>
export default {
  data () {
    return {
      name： 'Jack'
    }
  }
}
</script>
子组件

<template>
  <div class="slottwo">
    <slot></slot>
  </div>
</template>


作用域插槽
子组件

<template>
  <div>
    我是作用域插槽的子组件
    <slot :data="user"></slot>
  </div>
</template>

<script>
export default {
  name: 'slotthree',
  data () {
    return {
      user: [
        {name: 'Jack', sex: 'boy'},
        {name: 'Jone', sex: 'girl'},
        {name: 'Tom', sex: 'boy'}
      ]
    }
  }
}
</script>
在子组件的slot标签上绑定需要的值

父组件

<template>
  <div>
    我是作用域插槽
    <slot-three>
      <template slot-scope="user">
        <div v-for="(item, index) in user.data" :key="index">
        {{item}}
        </div>
      </template>
    </slot-three>
  </div>
</template>
在父组件上使用slot-scope属性，user.data就是子组件传过来的值