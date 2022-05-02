<template>
    <div>
        <h1>글을 수정하는 곳입니다</h1>
        <input type="text" v-model="memo.title"> <br>
        <textarea cols="30" rows="10" v-model='memo.memo'></textarea> <br>
        <button @click="updateMemo">수정</button>
    </div>
</template>

<script>
export default {
    data () {
        return {
            memo : {
                title : '',
                memo : ''
            }
        }
    },
    created() {
        //memo id값
        this.$http.get(`/api/memo/${this.$route.params.id}`)
        .then((response) => {
            // data를 통해서 값 가져올 수 있다.
            console.log(response.data);
            this.memo = response.data
        })
    },
    methods : {
        // axios를 이용해 수정버튼을 눌렀을 때 수정된 값을 보내줌
        updateMemo() {
            this.$http.put('/api/memo/updateform',{
                data : {
                    title :this.title,
                    memo : this.memo
                }
            }).then((response)=>{
                console.log(response.data)
            });
            this.$router.push('/')
        }
    }
}
</script>