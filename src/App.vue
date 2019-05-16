<template>
  <div id="app">
    <div class="window">
      <p class="header-text">введите координаты фигуры</p>
      <input type="text" class="form-control" v-model="coord">
      <div class="err" v-show="showErr">
        {{err}}
      </div>
      <div class="btn btn-primary" @click="check()">Check</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      err: "Здесь будет текст ошибки",
      coord: "D4" ,
      x: ["A", "B", "C", "D", "E", "F", "G", "H"],
      showErr: false,
      arr:[]
    }
  },
  methods:{
    check(){
      this.arr = []
      var coordFig = this.coord.split('');
      var a = coordFig[0].toUpperCase()
      coordFig[0] = a;
      if(coordFig.length < 3 & Number(coordFig[1]) != 9 & Number(coordFig[1]) != 0 ){
      for (var item=0; item < this.x.length; item++){
        if (coordFig[0] === this.x[item]){
          if(item-2 >= 0 & Number(coordFig[1])+1 < 9){
          this.arr.push(this.x[item-2]+(Number(coordFig[1])+1))
          }
          if(item-2 >= 0 & Number(coordFig[1])-1 > 0){
            this.arr.push(this.x[item-2]+(Number(coordFig[1])-1))
          }
          if(item+2 < 8 & Number(coordFig[1])+1 < 9){
            this.arr.push(this.x[item+2]+(Number(coordFig[1])+1))
          }
          if(item+2 < 8 & Number(coordFig[1])-1 > 0){
            this.arr.push(this.x[item+2]+(Number(coordFig[1])-1)) 
          }
          
          if(Number(coordFig[1])+2 < 9 & item+1<8) {
            
            this.arr.push(this.x[item+1]+(Number(coordFig[1])+2))
          }
          if(Number(coordFig[1])+2 < 9 & item-1>=0){
            this.arr.push(this.x[item-1]+(Number(coordFig[1])+2))
          }
          if (Number(coordFig[1]-2) > 0 & item-1 >= 0){
          this.arr.push(this.x[item-1]+(Number(coordFig[1])-2))
          
          }
          if (Number(coordFig[1]-2) > 0 & item+1 < 8){
            this.arr.push(this.x[item+1]+(Number(coordFig[1])-2))
          }
          
        }
      }
      } else {
        this.showErr= true;
        this.err = "Введите пожалуйста корректные координаты шахматной доски"
      }
      var msg = "Возможные варианты хода: "
      this.arr.forEach(el => {
        msg += el + ", "
      });
      alert(msg)
    }
  }
}
</script>

<style>
  html,body{
    width: 100%;
    height: 100%;
  }
  #app{
    position: absolute;
    width: 100%;
    height: 100%;
    background: #AD66D5;
  }
  .window{
    position: absolute;
    width: 300px;
    margin: 20px 0 0 -150px;
    left: 50%; 
    border: 1px solid black;
    border-radius: 10px;
    padding: 10px;
    background: #876ED7;
  }
  .header-text{
    text-transform: uppercase;
    font-weight: bold;

  }
  .btn{
    position: relative;
    width: 100px;
    margin: 20px 0 10px -50px;
    left: 50%;

  }
  .err{
    position: relative;
    margin: 10px 0 10px 0 ;
    background-color:#E667AF;
    border-radius: 5px;
    color: red
  }
</style>
 