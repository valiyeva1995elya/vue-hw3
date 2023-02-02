<script>
export default {
    data() {
        return {
            posts: [],
            textTitle: '',
            textPost: '',
            textComment: '',
            post: [],
            edStyle: false,
            isEdit: false,
            disNone: true,
            editTitle: "",
            editPost: "",
            editComment: "",
            editId: "",

            styleObject: {
                color: "blueviolet",
                background: "#e5c9ff",
                fontFamily: "Arial",
                fontSize: "15px",
                fontStyle: "italic"
            }
        }
    },
    methods: {
        addPost() {
            if (this.textTitle == "" || this.textPost == "" || this.textComment == "") {
                return
            }
            let newPost = {
                id: this.posts.length + 1,
                title: this.textTitle,
                post: this.textPost,
                comment: this.textComment
            }
            this.posts.push(newPost)
            this.textTitle = ""
            this.textPost = ""
            this.textComment = ""
        },
        openWindPost(id) {
            this.editId = id
            this.isEdit = true
            this.disNone = false
        },
        savePost() {
            if (this.editTitle == "" || this.editPost == "" || this.editComment == "") {
                return
            }
            let editNewPost = {
                id: this.editId,
                title: this.editTitle,
                post: this.editPost,
                comment: this.editComment,
            }
            this.posts = this.posts.map(post => {
                if (post.id == editNewPost.id) {
                    return editNewPost
                }
                return post
            })
            this.editTitle = ""
            this.editPost = ""
            this.editComment = ""
            this.isEdit = false
            this.disNone = true
        },
        openWindStyle(id) {
            this.editId = id
            this.edStyle = true
            this.disNone = false
        },
        saveStyle() {

            if (this.activeColor == "" || this.activeBackgr == "" || this.fontFamily == "" || this.fontSize == "" || this.fontWeight == "") {
                return
            }
            let newStyle = {
                color: this.activeColor,
                background: this.activeBackgr,
                fontFamily: this.fontFamily,
                fontSize: this.fontSize + "px",
                fontStyle: this.fontStyle,
            }
            this.styleObject = newStyle

            this.edStyle = false
            this.disNone = true
        },
    }
}


</script>

<template>
    <div class="add-block" v-if="disNone">
        <input type="text" placeholder="Название" v-model="textTitle"><br>
        <textarea class="add-post-text" cols="30" rows="10" placeholder="Пост" v-model="textPost"></textarea>
        <input type="text" placeholder="Комментарий" v-model="textComment"><br>
        <button class="addBtn" @click="addPost">Добавить пост</button>
    </div>
    <div class="posts-block" v-if="disNone">
        <div class="post-block" v-for="post in posts">
            <div v-bind:style="styleObject">
                <p>Название: <b> {{ post.title }}</b></p>
                <p>Пост:<b>{{ post.post }}</b></p>
                <p>Комментарий:<b>{{ post.comment }}</b></p>
                <button class="addBtn mb-20" @click="openWindPost(post.id)">Изменить пост</button>
                <button class="addBtn" @click="openWindStyle(post.id)">Изменить стили</button>
            </div>
        </div>

    </div>
    <div class="add-block" v-if="isEdit">
        <h1>Изменить пост</h1>
        <input class="mb-20" type="text" placeholder="Название" v-model="editTitle">
        <textarea class="add-post-text" cols="30" rows="10" placeholder="Пост" v-model="editPost"></textarea>
        <input type="text" placeholder="Комментарий" v-model="editComment"><br>
        <button class="addBtn" @click="savePost">Сохранить</button>


    </div>
    <div class="add-block" v-if="edStyle">
        <h1>Изменить стили</h1>
        <p>Цвет текста</p>
        <input class="mb-20" type="text" placeholder="цвет текста" v-model="activeColor">
        <p>Цвет фона</p>
        <input class="mb-20" type="text" placeholder="цвет фона" v-model="activeBackgr">
        <p>Шрифт</p>
        <input class="mb-20" type="text" placeholder="шрифт" v-model="fontFamily">
        <p>Размер шрифта</p>
        <input class="mb-20" type="text" placeholder="размер шрифта" v-model="fontSize">
        <p>Начертание шрифта"</p>
        <input class="mb-20" type="text" placeholder="начертание шрифта" v-model="fontStyle">
        <button class="mb-20 addBtn" @click="saveStyle">Изменить</button>

    </div>

</template>

<style scoped>
h1{
    color: #8a2be2;
    
}
.add-block {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border: 2px solid rgb(179, 111, 242);
    padding: 10px;
    width: 250px;
    margin: 0 auto;
    border-radius: 10px;
    background-color: rgba(211, 171, 248, 0.411);
    color: #8a2be2;
}

input {
    text-align: center;
    color: blueviolet;
    border-radius: 7px;
    outline: none;
    border: 2px solid rgb(119, 0, 230);
    padding: 5px;
    width: 150px;
}

.addBtn {
    border-radius: 7px;
    outline: none;
    background-color: #8a2be2;
    padding: 5px;
    width: 160px;
    border: 2px solid rgb(125, 7, 236);
    color: white;
    margin-bottom: 10px;
}

.posts-block {
    display: flex;
    flex-wrap: wrap;
    margin-right: 15px;
    justify-content: center;
}

.post-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    justify-content: center;
    border: 1px solid blueviolet;
    width: 250px;
    height: 100%;
    margin: 20px 10px 20px 10px;
    border-radius: 10px;
    background-color: rgba(139, 14, 255, 0.497);
    padding: 10px;
    box-sizing: border-box;
}

.add-post-text {
    text-align: center;
    color: blueviolet;
    border-radius: 7px;
    outline: none;
    border: 2px solid rgb(119, 0, 230);
    padding: 5px;
    width: 150px;
    margin-bottom: 10px;

}

.mb-20 {
    margin-bottom: 20px;
    
}


</style>
