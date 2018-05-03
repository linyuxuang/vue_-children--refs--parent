# vue_-children--refs--parent
vue-$children--$refs-$parent




            <!DOCTYPE html>
              <html>
              <head lang="en">
                  <meta charset="UTF-8">
                  <title></title>
                  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
              </head>
              <body>
               <div id="app">
                   <parent-component></parent-component>
               </div>

               <template id="parentcomponent">
                <div>
                  <firstchild ref="f1"></firstchild>
                  <secondchild ref="f2"></secondchild>
                  <button @click="show_child_of_parents">btn</button>
                 </div>
               </template>

               <script type="text/x-template" id="childOne">
                   <div>
                       <p>this is first child</p>
                       <!--//使用stop阻止默认事件（vue的事件处理机制）-->
                       <button @click.stop='getParent'>get parent msg</button>
                   </div>
               </script>

               <template id="childSec">
                   <div>我是第二个子组件</div>
               </template>

               $children   获取所有子组件的值
               $refs        相当于dom绑定
               $parent    获取父组件的值

              <script>
                  new Vue({
                      el:"#app",
                      data:{},
                      components:{
                          "parent-component":{
                              template:'#parentcomponent',
                              data:function(){
                               return{msg:'这是父组件中的内容'}
                       },
                       methods:{
                           show_child_of_parents:function(){
                          //children方式访问自组件  （获取所有子组件的值）
                            for(let i=0;i<this.$children.length;i++){
                              console.log(this.$children[i].msg);
                            }
                           //通过$ref打标记，访问子组件 (在这里获取到dom有f1的-相当于dom绑定)　
                            console.log(this.$refs.f1.msg);
                             this.$refs.f1.getParent();
                        }
                     },
                    components:{
                      'firstchild':{
                          template:'#childOne',
                              data:function(){
                              return {msg:'这是第一个子组件'};
                          },
                          methods:{
                              getParent:function(){
                                // $parent获取父组件的值
                                 alert(this.$parent.msg);
                              }
                          }
                       },
                      'secondchild':{
                          template:'#childSec',
                          data:function(){
                          return {msg:"这是第二个组件"};
                          }
                        }
                     }
                    }
                  }

                  });
              </script>
              </body>
              </html>
