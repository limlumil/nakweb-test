<template>
    <div class="slider-card">
        <div class="content">
            <div class="image">

                <img :src="image" style="width:100%"/>
            </div>
            
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

      .image{
        width:100%;
        img{
            border-radius: 0.5rem !important;
            width:100% 
        }

    }
    

      strong {
        margin: 20px 0 0;
      }

      p {
        font-size: .8em;
        margin: 15px 0px;
        color:rgb(41, 134, 102);
      }

      .button {
        display: inherit;
        padding: 11px 13px;
        border:none;
        font-weight: 600;
        text-decoration: none;
        text-transform: uppercase;
        cursor: pointer;
      }
    }

</style>