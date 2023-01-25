<template>
  <div class="container">
    <nav>
        <h2>Monster Slayer</h2>
    </nav>
    <div class="healthcontainer" >
        <h3>Monsters Health</h3>
        <div class="healthdisplayer">
           {{ monsterHealth }}
        </div>
    </div>

    <div class="healthcontainer">
        <h3>Hero Health</h3>
        <div class="healthdisplayer">
            {{ playerHealth }}

        </div>
    </div>
    <div class="resultScreen" v-if="winner">
        <h2>Game Over</h2>
        <h3 v-if="winner === 'Monster'">You Lost!</h3>
        <h3 v-if="winner === 'Player'">You Won!</h3>
        <h3 v-if="winner === 'draw'">It's Draw!</h3>

        <button @click="newGame">New Game</button>
    </div>
    
    <div class="btncontainer">
        <button class="btn" @click="attackMonster">Attack</button>
        <button class="btn" :disabled="counter % 3 !== 0" @click="specialAttackMonster">Special Attack</button>   
        <button class="btn" @click="healer">Heal</button>   
    </div>
  </div>

     
</template>

<script>
export default{
    data(){
        return{
            monsterHealth: 100,
            playerHealth:100,
            healWeight: 3,
            counter: 0,
            winner: null,
        }
    },
    watch:{
        playerHealth(value){
            if(value <= 0 && this.monsterHealth <=0){
                this.winner = 'draw'
            } else if(value <= 0){
                this.winner = 'Monster'

            }
        },
        monsterHealth(value){
            if(value <= 0 && this.playerHealth <=0){
                this.winner = 'draw'
            } else if(value <= 0){
                this.winner = 'Player'

            }
        }

    },
    methods:{

       

        attackMonster(){
           const attackWeight= Math.floor(Math.random() * (12-5)) + 5;
           this.monsterHealth -= attackWeight;
           if(this.monsterHealth <0 ){
            this.monsterHealth = 0;
           }
           this.attackPlayer();
        },
        attackPlayer(){
           this.counter++;
           const attackWeight= Math.floor(Math.random() * (15-8)) + 8;
           this.playerHealth -= attackWeight;
           if(this.playerHealth <0 ){
            this.playerHealth = 0;
           }
        },
        specialAttackMonster(){
           
            const attackWeight= Math.floor(Math.random() * (25-12)) + 12;
            this.monsterHealth -= attackWeight;
            this.attackPlayer();


        },
        healer(){
            this.playerHealth += this.healWeight;

        },
        newGame(){
            this.monsterHealth= 100;
            this.playerHealth=100;
            this.healWeight= 3;
            this.counter= 0;
            this.winner= null;
        }
       
    }
}
</script>

<style>
body{
    margin: 0;
    padding: 0;
}

.container{
    width: 500px;
    height: 900px;
    margin: 50px auto;
    background-color: rgb(96, 94, 94);
}

nav{
    height: 80px;
    background: rgb(38, 37, 37);
    color: white;
    padding:auto;
    display: flex;
    align-items: center;
    justify-content: center;
}

.healthcontainer{
    background-color: rgb(125, 128, 127);
    width: 300px;
    margin: 10px auto;
    text-align: center;
    padding: 20px;
    border-radius: 10px;
    color:rgb(255, 254, 254);
    letter-spacing:   
}
.healthdisplayer{
    width: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 50px;
    background-color: #fff;
    margin: 0 auto;
    font-weight: 900;
    font-size:1.5rem;
   
}
.btncontainer{
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    margin-top: 30px;
   
}
.btn{
    width: 200px;
    padding: 20px;
    margin: 5px;
    text-transform: uppercase;
    font-weight: 600;
    border-radius: 50px;
    border: none;
    color: white;
    background-color: rgb(59, 18, 18);
    cursor: pointer;

    
}
</style>