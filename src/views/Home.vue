<template>
  <div class="home">
    <h1>TODO LIST</h1>
    <p>할 일은 해야하지 않겠니?</p>
    <!-- <input type="text" value="오늘 할 일" v-model="newPlayer" v-on:keyup.enter="addPlayer" > -->
      <!--  v-on:keyup.enter  @keyup.enter  대체 가능 -->
    <!-- <input @keyup="whatodo" :value="text" type="text" id="inputText">     v-on:keyup.enter="addList"-->
    <input type="text" v-model="newPlan" >
    <button v-on:click="addList" class="test_btn1">Click me!!!! </button>
    <hr>
    {{newPlan}}<br>
    <ul>
      <li v-for="(list,index) in lists" v-bind:key="index">
          [ {{index+1}} ] - {{list.name}}   <button v-on:click="deleteList(index)" class="test_btn1">끝 ^_^</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data: function(){
    return{
      text : '',
      lists : [
        {name : '빨래'}
      ],
      newPlan : '',
      index : '',
    }
  },
  methods:{
    addList(event){
      event.preventDefault()
     // alert("이건 에러 안나냐")
      this.lists.push({name: this.newPlan})

      // Immutable 패턴!!

      // push는 v-model:lists 와 같이 lists 의 변경점을 캐치하고자 하는 경우 반응하지 않는 메서드 입니다.
      // 따라서, lists 자체를 초기화해주는 패턴을 이용하는 것이 좋습니다. 이런 패턴을 Immutable 패턴이라고 하는데,
      // 자세한 건 구글링을 해보시면 좋겠습니다. 조금의 팁을 드리면, lists = [...this.lists, {name: this.newPlan}]
      // 정도로 진행해주시면 Immutable 패턴으로 진행하실 수 있을거에요. push 메서드와 같이 기존 객체를 재활용하는 메서드는
      // 되도록이면 사용하지 않는 것이 좋습니다. v-model:text <= string, number ,, v-model:obj = obj.text = "dsda";
      // '...' 은 디스트럭쳐링 이라고 해서 '해체'라는 의미인데, lists = [1,2,3,4]; 
      // console.log(this.lists) ===> "[1,2,3,4]"
      // console.log(...this.lists) ===> "1,2,3,4";
      // console.log(...this.lists, 5) ===> "1,2,3,4    ,5"
      // obj = {id:2, text:1} ,, console.log(this.obj); ==> obj ==> id, text
      // console.log({...this.obj}) ===> { id:2, text:1}
      // this.lists = [{name:"asd"}] ,,, [...this.lists , {name: this.newPlan}] ==> [{name:"asd"},{name:this.newPlan}]
      this.newPlan=''
    },
    deleteList(index){
     // event.preventDefault()
      alert("끝이다")
      this.lists.pop(index)
      // this.lists.slice(1,2)  ,,, console.log(this.lists) 변화없음
      // this.lists = this.lists.slice(1,2);  // 기존 배열에 변화를 주지 않고, 결과값으로 새로운 배열을 반환함 (주소값 변경)
      
      // this.lists.splice(1,2) ,,, console.log(this.lists) 변화있음
    }
  }
}
</script>
<style scoped>
</style>
