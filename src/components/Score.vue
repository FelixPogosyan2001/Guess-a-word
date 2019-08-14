<template>
 <div>
    <div class = 'score col-8 offset-2'>
        <i :class = "[reward]" class="score__reward fas fa-trophy"></i>
        <div class = 'score__conclusion'>
            <strong><p id = 'congrats'>Congratulations,{{user}}</p></strong>
            <p id = 'text'>If you suddenly do not like the number of points earned, then do not lose heart and go through again</p>
        </div>
        <div class = 'score__display'>
            <p class = 'score__description'>{{count}}</p>
            <p class = 'score__points'>Points</p>
            <span class = 'score__sign'>Guess a word </span>
        </div>
    </div>
    <center><a href = '/' class = 'btn btn-outline-warning'>Go back</a></center>
 </div>
</template>
<script>
export default {
    data : () => {
        return {
            reward : ''
        }
    },
    props : {
        user : String,
        count : Number,
        allWords : Number
    },
    created:function() {
        var x = Math.round((100 * this.count) / this.allWords);
        if (x < 60) this.reward = 'bronze';
        else if (x <= 80 && x >= 60) this.reward = 'silver';
        else if (x <= 100 && x > 80) this.reward = 'gold';
    }
}
</script>
<style scoped>
#congrats {
    font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size:1.1em
}
.score {
    background: #1875f0;
    min-height:50vh;
    margin-top:60px;
    display:grid;
    grid-template-columns:repeat(3,1fr);
    grid-gap : 40px
}
.score__display {
    background-color:#00459f;
    width:90%;
    min-height:80%;
    align-self:center;
    text-align:center;
    padding:10px
}
#text {
    font-size:0.8em !important;
    opacity:0.8;
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif
}
.silver {
    color:rgb(190, 190, 190)
}
.gold {
    color:rgb(230, 230, 14)
}
.bronze {
    color:rgb(156, 87, 87)
}
.score__conclusion {
    color:white;
    position:relative;
    top:70px;
    font-size:20px;
    font-weight: bold
}
.score__points {
    color:yellow;
    opacity:0.9;
    font-size:1.2em;
    font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif
}
a{
    position:relative;
    top:80px
}
.score__description {
    color:yellow;
    font-size:4em;
    font-weight: bold;
}
.score__reward {
    font-size:8em;
    align-self: center;
    justify-self: center
}
.score__sign{
    position:relative;
    top:40px;
    color:white;
    font-family:monospace;
    font-size:1.2em
}
@media (max-width:762px) {
    .score {
        grid-template-columns:1fr;
    }
    .score__sign {
        top:0px;
    }
    .score__conclusion {
        top:10px
    }
    .score__reward {
        margin-top:20px
    }
}
</style>