<template>
  <div id = "app">
    <h1>Todo List</h1>
<input type="text" v-model="sendtext">
<button @click="addmethod">Add</button>

<ul>
  <li v-for="(list,index) in response" :key=index>
    <!--チェックボックスもつけれる listのisdoneをv-modelと結びつける -->
    <input type="checkbox" v-model="list.isdone">
    <!-- チェックが入ったら、取り消し線引くには、v-vindで動的にclassをつける 、isdoneがfalseだったら、doneというクラスは設定されない-->
    <span :class="{done:list.isdone}">
      {{list.info}}
      </span>
      <!-- どこのやつをけしたらいいかわからないから、引数に上で設定したindexを渡す。 -->
      <button @click="deleteitem(index)">Delete</button>
    </li>
</ul>

</div>
</template>

<script>
export default{
 data(){
   return{
     sendtext:"",
     response:[]
   };
 },
 methods:{
   addmethod(){
    // 空欄だったら追加しない、作業を終わらせる
     if(this.sendtext=="") return;
     let todo ={
       info:this.sendtext,
       isdone:false
     };
     this.response.push(todo);
     this.sendtext="";
   },
   deleteitem(index){
    //  削除の動作。index のとこ消して、第２引数はそこから何個削除するか
     this.response.splice(index,1)
   }
 }
};

</script>

<style scoped>
#app ul{
  list-style: none;
}
span .done{
text-decoration: line-through;
}
</style>