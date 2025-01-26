<template>
    <div>
        <div class='calculator'>
            <div class='display'>{{limitedCurrent}}</div>
            <div @click="clear" class='btn clear'>C</div>
            <div @click="del" class="btn remove">Del</div>
            <div @click="sign" class='btn'>+/-</div>
            <div @click='percent' class='btn'>%</div>
            <div @click="square" class="btn">x<sup><small>2</small></sup></div>
            <div @click="divide" class='btn operator'>÷</div>
            <div @click="append('7')" class='btn'>7</div>
            <div @click="append('8')" class='btn'>8</div>
            <div @click="append('9')" class='btn'>9</div>
            <div @click="multiplication" class='btn operator'>×</div>
            <div @click="append('4')" class='btn'>4</div>
            <div @click="append('5')" class='btn'>5</div>
            <div @click="append('6')" class='btn'>6</div>
            <div @click="minus" class='btn operator'>-</div>
            <div @click="append('1')" class='btn'>1</div>
            <div @click="append('2')" class='btn'>2</div>
            <div @click="append('3')" class='btn'>3</div>
            <div @click="add" class='btn operator'>+</div>
            <div @click="append('0')" class='btn zero'>0</div>
            <div @click="dot" class='btn'>.</div>
            <div @click="eqal" class='btn operator'>=</div>
       </div>
    </div>
</template>

<script>
    export default {
        name:'calculatorZ',
        data(){
            return{
                current:'',
                provisNumber:null,
                operatorClicked:false,
                oprator:null ,
                resultCalculated:false
            }
        },
        computed: {
    limitedCurrent() {
      return this.current ? this.current.substring(0, 20) : '0';
    },
    },
        methods:{
             del(){
            this.current=this.current.slice(0,-1)
        },
            square(){
                if(this.current !== ''){
                this.current=`${parseFloat(this.current)*parseFloat(this.current)}`
                }


            },
            clear(){
                this.current='';
                this.provisNumber=null;
                this.operatorClicked=false;
                this.oprator= null;
                this.resultCalculated=false;
            },
            sign(){
                if(this.current !== ''){
                this.current = this.current.charAt(0) === '-' ?
                this.current.slice(1): `-${this.current}`
                }

            },
            percent(){
                if(this.current !== ''){
                this.current =`${parseFloat(this.current) / 100}`
                }

            },
           append(val) {
            if (this.operatorClicked) {
              this.current = '';
              this.operatorClicked = false;
              }if(this.resultCalculated){
                this.current= '';
                this.resultCalculated= false;
              }
            this.current = `${this.current}${val}`;
              },
            dot(){
                if(this.current.indexOf('.') === -1 && this.current.length>0){
                    this.append('.')
                }
            },
            setPrevious(){
                this.provisNumber = this.current
                this.operatorClicked=true
            },
            multiplication(){
                if(this.current !== ''){
                this.oprator = (a,b)=> a*b
                this.setPrevious()
                }
            },
            divide(){
                if(this.current !== ''){
                this.oprator = (a,b) => a/b
                this.setPrevious()
                }
            },
            add(){
                if(this.current !== ''){
                this.oprator = (a,b) => a+b
                this.setPrevious()
                }
            },
            minus(){
                if(this.current !== ''){
                this.oprator= (a,b) => a-b
                this.setPrevious()
                }
            }, 
            eqal(){
                if (this.oprator && this.provisNumber !== null){
                this.current= `${this.oprator(
                    parseFloat(this.provisNumber),
                    parseFloat(this.current),
                )}`
                }
                this.provisNumber=null;
                this.operatorClicked=false;
                this.oprator= null;
                this.resultCalculated=true
            }
        }    
    }
</script>

<style  scoped>
.calculator{
    display:grid;
    grid-template-columns: repeat(4 ,1fr);
    grid-template-rows: minmax(50 , auto);
    margin: 0 auto;
    width: 500px;
    font-weight: bold;
}
.display{
    grid-column: 1/5;
    background-color: #333;
    height: 50px;
    font-size: 40px;
    color: aliceblue;
}
.btn{
    border: 1px solid black;
   height: 50px;
    text-align: center;
    font-size: 40px;
    cursor: pointer;
    background-color: #09df74;
    color: beige;
    

}
.zero{
    grid-column: 1/3;

}
.operator{
    background-color: orange;
    color: white;
}
.btn:hover{
    background-color: aqua;
}
.clear{
    grid-column: 1/3;
    background-color: rgb(223, 3, 3);
    color: white;
}
.remove{
    grid-column: 3/5;
    background-color: blue;
    color: white;
}
</style>