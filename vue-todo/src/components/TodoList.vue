<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
        {{ todoItem }}
        <apan class="removeBtn" v-on:click="removeTodo(todoItem, index)">
        <i class="fas fa-trash-alt"></i>
        </apan>
      </li>
    </ul>
  </div> 
</template>

<script>
//ttjtjt 
export default {
  data: function() {
    return{
      todoItems: []
    }
  },
  methods: {
    removeTodo: function(todoItem, index) {
      console.log(todoItem, index);
      localStorage.removeItem(todoItem);
      //this.todoItems.splice(index, 1)
      //주어진 인덱스 의 값을 제외 한 나머지 항목만 추출하여
      //새로운 배열의 넣은뒤 그 배열로 Todo아이템스 를 갱신해준다

      // 새로운  임시배열을 만든다
      const newArray = [] ;
      // 기존 투두 아이템스 를 순회하며
      for(const idx in this.todoItems){
        console.log("idx",idx)
        // 넘겨준값과 현재 순회하는 값이 같으면 건너 띈다.
        if(index !== idx){
           // 새로운 임시 배열에 현재 순회 항목을 추가한다.
           newArray.push(this.todoItems[idx])
        }
      }
      // 같은 값이 빠진 배열로 기존 투두아이템스 베열을 업데이트한다
      this.todoItems = newArray
    }
  },

  created: function() {
   if (localStorage.length > 0) {
     for (var i = 0; i < localStorage.length ; i ++){
       this.todoItems.push(localStorage.key(i));

     }
   }
    
  }

}
</script>

<style>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #63adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}


</style>