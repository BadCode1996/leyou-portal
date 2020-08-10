# Leyou前台页面

## 运行
live-server --port=9002

## 细节扩展
1. 当搜索栏搜索条件为空时点击搜索按钮，搜索页面的搜索栏显示`null`

   修改top.js，90行处，把`null`改为空

   ~~~js
   return null;	// 修改前
   return "";		// 修改后
   ~~~

2. 不可以按回车键进行搜索，只能点击搜索按钮（待实现）



3. 在展示页面，商品标题显示不完整，添加鼠标悬停

   添加`:title`指令

   ~~~html
   <em :title="goods.selected.title">{{goods.selected.title.length > 20 ? goods.selected.title.substring(0,20) :
                                           goods.selected.title}}</em>
   ~~~

4. 当部分商品的sku超过6个时，格式不太美观（<span style="color: red">依然不够完美，第9点继续优化</span>）

   Vue控制v-for循环次数的方法

   1. 通过`v-if`对超出部分进行隐藏

      ~~~html
      <li v-for="(sku,i) in goods.skus" v-if="i < 6" :key = "sku.id"><img :src="sku.image"></li>
      ~~~

   2. 通过`slice`截取数组长度，控制循环的次数

        ~~~html
        <li v-for="sku in goods.skus.slice(0,6)" :key="sku.id"><img :src="sku.image"></li>
        ~~~

5. 搜索页中，输入页号进行跳转

   使用`ref`获取文本框的内容

   ~~~html
   <span>
       到第<input type="text" class="page-num" :value="search.page" ref="jumpPage">页
       <button class="page-confirm" @click="jumpTo">确定</button>
   </span>
   <script>
       var vm = new Vue({
           el: "#app",
           data:{
               jumpPage: ""
           },
           methods:{
               jumpTo(){
                   //使用$ref获取jumpPage的value值
                   this.search.page = this.$ref.jumpPage.value
               }
           }
       })
   </script>
   ~~~

6. 当页面为第一页/最后一页时，取消显示页码前/后的 `...`

   ~~~html
   <li class="dotted" v-show="totalPage > 5 && search.page > 3"><span>...</span></li>
   <li class="dotted" v-show="totalPage > 5 && search.page < totalPage - 2"><span>...</span>
   ~~~

7. 商品列表右上角的翻页按钮，当页面为第一页/最后一页时，前一页/后一页按钮失效（待实现）

   

8. 搜索过滤时，部分品牌logo查不到（待实现）

   

9. 商品列表中的sku小图，只展示前6个，当sku多的时候，就无法展示全部sku图，预想只展示每个sku的一张图（待实现）

   

10. 待发现