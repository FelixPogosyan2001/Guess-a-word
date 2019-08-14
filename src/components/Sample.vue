<template>
  <div>
    <p class = 'alert alert-danger' v-if = "warning">Empty fields</p>
    <div class = 'form-same'>
        <input ref = "user" v-model.trim = "name" class = 'form-control' type = 'text' placeholder = "Name" />
        <input ref = "rounds" maxlength = "2" v-model.number = "count" class = 'form-control' type = 'text' placeholder = "Count of the words" />
        <select ref = "level" v-model = "choice" class = 'form-control'> 
            <option>Easy</option>
            <option>Normal</option>
            <option>Hard</option>
        </select>
        <button @click = "go">Start game</button>
    </div>
    <div class = 'rules'>
        <h2>Rules of the game</h2>
    </div>
    <hr style = 'border:1.4px solid #80ffff'/>
    <div class = 'instruction'>
        <div>
            <p>
                Before you start the game, you should familiarize yourself with the rules of the game. 
                First of all, fill in the fields. 
                The maximum number of words, which can be 100, you can also choose the level that suits you
            </p>
        </div>
        <i class="fas fa-angle-right"></i>
        <div>
            <p> 
                When you start the game, words will appear that will not be displayed correctly, and you will need to pronounce the correct version of the word. 
                For each correct answer you get one point
            </p>
        </div>
         <i class="fas fa-angle-right"></i>
        <div>
            <p> 
                After completing all the words, the game will end. 
                And you will see your points and also a table where it is shown in which cases you will get gold
            </p>
        </div>
    </div>
  </div>
</template>
<script>
function valid () {
    if (!this.name || !this.count || !this.choice) {
        this.warning = true;
        return false;
    } 
    return true;
}
export default {
    props : ['begin'],
    data : function ()  {
        return {
            name : null,
            count : null,
            choice : null,
            warning : false
        }
    },
    methods: {
        go(){
            if (valid.apply(this)) {
                this.begin(this.name,this.choice,this.count)
            }
        }
    },
    watch : {
        name() {
            this.warning = false
        },
        count() {
            this.warning = false
        }
    }
}
</script>
<style>
.rules {
    color:#ffdb4d;
    text-align:center;
    font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
.rules > h2 {
    text-shadow:2px 1px 10px #ffdb4d;
}
.instruction {
    display:grid;
    grid-template-columns:1fr 10px 1fr 10px 1fr;
    margin:40px;
    justify-items:center;
}
.instruction > div:nth-child(1) {
    background:#d580ff;
    box-shadow : 3px 4px 20px #d580ff;
}
.instruction > div:nth-child(3) {
    background:  #ff6666;
    box-shadow : 3px 4px 20px #ff6666; 
}
.instruction > div:nth-child(5) {
    background:  #ff944d;
    box-shadow:  3px 4px 20px #ff944d; 
}
.instruction > div {
    min-height:200px;
    width:60%;
    border-radius:3px;
    padding:8px
}
.instruction > i {
    color : rgb(30, 236, 208);
    font-size:3em;
    align-self:center;
    animation: angle 2s infinite linear
}
.instruction > div p {
    color:white;
    font-weight: bold;
    font-family:sans-serif;
    opacity:0.7
}
.form-same {
    text-align:center;
    display:grid;
    grid-gap: 1.5em;
    width:40%;
    justify-items:center;
    margin:80px auto;
}
.form-same select {
    justify-self: left
}
.form-same input[placeholder = 'Name'] {
    grid-column:1/3
}
.form-same input[placeholder = "Count of the words"] {
    width:70%;
    grid-row-start: 2;
    justify-self:left
}
.form-same select {
    grid-row-start: 2;
    grid-column: 2;
    justify-self:right
}
.alert {
    width:20%;
    text-align:center;
    position:absolute;
    left : 40%;
    right: 40%;
    top:15%;
    font-weight:bold;
    font-size:20px;
    height:7vh;
    padding-top:5px
}
.form-same button {
    grid-row-start : 4;
    grid-column : 1/3;
    border : none;
    background: rgba(10, 235, 235, 0.952);
    color:white;
    font-size:1.3em;
    padding:5px 10px 5px 10px;
    border-radius:3px;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif
}
@keyframes angle {
    from {
        transform: translateX(0px)
    } to {
         transform: translateX(50px)
    }
}
@media (max-width:762px) {
    .form-same {
        width:80%;
    }
    .instruction {
        grid-template-columns: 1fr
    }
    .instruction > i {
        visibility:hidden
    }
}
</style>