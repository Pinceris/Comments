<template>
    <div class="comment"
         @mouseover="hover = true"
         @mouseleave="hover = false">
        <div class="avatar">
            <img :src="comment.avatar"  alt="">
        </div>
        <div class="text">
            <a class="username" href="#">@{{ comment.user }} </a> <span>{{ comment.text }}</span>
            {{comment.date}}
        </div>
        <div class="del">
            <button type="button" class="btn-outline-danger btn-sm"v-if="hover" v-on:click="my">delete</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'singleComment',
        props: {
            comment: {
                type: Object,
                default: function () {
                    return {
                        id: 0
                    }
                }
            }
        },

        methods: {
            my: function(){
                let comments = this.$parent.comments;
                for (let i = 0; i < comments.length; i++) {
                    if(comments[i].id === this.comment.id) {
                        comments.splice(i,1);
                        for(let j = i;j < comments.length ;j++){
                            if(j < comments[j].id) {
                                comments[j].id--;
                            }
                        }
                    }
                }
                localStorage.setItem('comments', JSON.stringify(this.$parent.comments));
            }


        },
        data() {
            return{
                hover: false
        }
    }
    }

</script>

<style scoped>
/* Single-comment component */
.comment {
    display: flex;
    padding: 10px;
    margin-bottom: 10px;
    align-items: center;
    color: #333;
    background-color: #F2F2F2;
    border-radius: 30px;
    box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
}

.comment .avatar {
    align-self: flex-start;
}

.comment .avatar > img {
    width: 40px;
    height: 40px;
    border-radius: 100%;
    align-self: start;
}

.comment .text {
    text-align: left;
    margin-left: 5px;
}

.comment .text span {
    margin-left: 5px;
}

.comment .text .username {
    font-weight: bold;
    color: #333;
}
.comment .del {
    text-align: right;
    margin-left: auto;
}
</style>
