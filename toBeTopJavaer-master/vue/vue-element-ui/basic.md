
**1 vue属性赋值:width**
2 **方式一** 传值到子页面 父页面 :xxx='100'  子页面 props:{ xxx:{type:类型,defalut:默认值,required: 必填} }
#
3 **props:** 
父类向子类传值 当向传递
{
            // 基础类型检测 （`null` 意思是任何类型都可以）
            propA: Number,
            // 多种类型
            propB: [String, Number],
            // 必传且是字符串
            propC: {
                type: String,
                required: true
            },
            // 数字，有默认值
            propD: {
                type: Number,
                default: 100
            },
            // 数组／对象的默认值应当由一个工厂函数返回
            propE: {
                type: Object,
                default: function () {
                    return { message: 'hello' }
                }
            },
            // 自定义验证函数
            propF: {
                validator: function (value) {
                    return value > 10
                }
            }
        },
		
# 
**4 slot插槽**   https://www.cnblogs.com/loveyt/p/9946450.html 用法
**5 回调**
父页面
@callBack='xxx'
methonds:{
 xxx(a){
 }
}

子页面
this.$emit('callBack','参数')
父页面调用子页面
6 :visible.sync="aduitVisible"  不可见   v-if=true



**7  CubeDialog** 弹出出框
     destroy-on-close 
      <Aduit v-if="aduitVisible" :props-data="propsData" :just-read="justRead" :visible.sync="aduitVisible" />
<CubeDialog
      destroy-on-close 
      :title="cubeDialogTitle"
      append-to-body
      fullscreen
      :visible.sync="personlistdialogVisible"
    >
      <!--      人员详情-->
      <personlist
        v-if="personlistdialogVisible"
        :props-data="propsData"
        @close="personlistdialogVisible = false"
      />
	  
    closeDialog(isFlush) {
      this.$emit('closeDialog', isFlush)
    },
    </CubeDialog>
