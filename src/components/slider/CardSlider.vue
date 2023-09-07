<template>
    <div class="slider-card">
        <div class="content">
            <img :src="image"/>
            
            <strong>{{ title }}</strong>

            <p>{{ description }}</p>
            
            <button v-if="link!=='undefined' || link!==''" class="button" :style="`color:${color};background-color:${backgroundcolor}`"
            @click.prevent="handleClick"
            >{{ buttontext }}</button>
        </div>
    
    </div>
</template>
<script>
export default {
    name:'CardSlider',
    setup(){

    },
    component:{

    },
    props:{
        image:{
            type:String,
            default:''
        },
        alt:{
            type:String,
            default:''
        },
        title:{
            type:String,
            default:''
        },
        description:{
            type:String,
            default:''
        },
        buttontext:{
            type:String,
            default:'',
        },
        color:{
            type:String,
            default:''
        },
        backgroundcolor:{
            type:String,
            default:''
        },
        link:{
            type:String,
            default:''
        }
    },
    emits:["buttonClick"],
    methods:{
        handleClick(){
            console.log(this.link);
            this.$emit("buttonClick",this.link)
        }
    }
}
</script>
<style lang="scss" scoped>
.content {

      min-height: 350px;

      img {
        border-radius: 3%;
        width:100%
      }

      strong {
        margin: 20px 0 0;
      }

      p {
        font-size: .8em;
        margin: 15px 0px;
      }

      .button {
        display: inherit;
        padding: 11px 13px;
        font-weight: 600;
        text-decoration: none;
        text-transform: uppercase;
        cursor: pointer;
      }
    }
</style>