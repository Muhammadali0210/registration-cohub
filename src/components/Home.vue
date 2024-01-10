<template>
    <div class="bg">
        <div class="registration-wrap">
            <div class="registration-content">
                <div class="logo">
                    <img src="../images/orange white.png" alt="CoHub">
                </div>
                <h1 v-if="form">Ro'yhatdan o'tish</h1>
                <br>
                <form @submit.prevent="submitForm()" v-if="form">
                    <label  class="profil-text" for="ism">Ism</label>
                    <input type="text " id="ism" v-model="data.Firstname" class="profile-input" text="Ism" placeholder="Ismingizni kiriting...">
                    <label  class="profil-text" for="familiya">Familiya</label>
                    <input type="text " id="familiya" v-model="data.Lastname" class="profile-input" text="Ism" placeholder="Familiyangizni kiriting...">
                    <label  class="profil-text" for="number">Telefon nomer</label>
                    <input type="number" id="number" v-model="data.phone" class="profile-input" text="Ism" value="+998" placeholder="Telefon nomeringizni kiriting...">
                    <button type="submit" class="btn">Yuborish</button>
                </form>
                <div class="telegram" v-if="!form">
                    <h3>Endi telegram kanalimizga qo'shilib olishingiz mumkin <img src="../images/Animation.gif" width="50px" height="50px" alt=""></h3>
                    <a href="https://t.me/sammi_community">
                        <button type="button" class="btn">
                        <img src="../images/telegram.png" alt="t" width="30px" height="30px">
                        Telegram
                        </button>
                    </a>
                </div>
            </div>
        </div>

    </div>
</template>
<script>
import axios from 'axios';
import Swal from 'sweetalert2'
export default {
    data() {
        return {
            data:{
                "Firstname": "",
                "Lastname": "",
                "phone": "",
            },
            form: true
        }
    },
    methods: {
        submitForm() {
            console.log(this.data)
            axios.post('https://ilkham.uz/api/coHub', this.data, {
                headers: {
                    'accept': 'application/json',
                    'Authorization': 'Bearer 2|OTufZWXaddSTG87K8KFk8XpsYsY5YcI1CxNpvjAq4b214811'
                }
            })
            .then(response => {
                if(response.status==200){
                    this.toast()
                    this.form = false
                }
            })
            .catch(error => {
                console.error('Formani yuborishda xato:', error);
            });
        },
        toast(icon = "success", title = "Muvaffaqiyatli ro'yhatdan o'tdingiz!") {
        const Toast = Swal.mixin({
        toast: true,
        position: "top-right",
        showConfirmButton: false,
        timer: 2000,
        timerProgressBar: true,
        didOpen: (toast) => {
            toast.addEventListener("mouseenter", Swal.stopTimer);
            toast.addEventListener("mouseleave", Swal.resumeTimer);
        },
        });
        return Toast.fire({
        icon: icon,
        title: title,
        });
  },
    },

};
</script>
<style>
a{
    text-decoration: none;
}
:root{
    --text: #005fad;
}
.telegram{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    flex-direction: column;
    transition: all 2s;
}
h1{
    text-align: center;
    color: var(--text);
    text-shadow: .5px .5px 0px #b4b4b4;
    font-weight: 900;
}
h3{
    text-align: center;
    color: #c6c6c6;
    font-weight: 600;
    display: flex;
    flex-direction: column;
    align-items: center;
}
.logo{
    width: 150px;
    height: 75px;
    margin: 0 auto;
    margin-bottom: 30px;
}
.logo img{
    width: 100%;
    height: 100%;
    object-fit: contain;
}
.registration-wrap{
    position: relative;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #00000089;
    backdrop-filter: blur(3px);
    /* background-color: #424242; */
}

.bg{
    background-image: url(../images/bg.jpg);
    background-position: center;
    background-repeat: no-repeat;
    width: 100%;
    height: 100%;
}
.registration-content{
    width: 600px;
    display: flex;
    justify-content: center;
    flex-direction: column;
    /* padding: 50px; */
    /* border-radius: 20px; */

}
.btn{
    padding: 12px 16px;
    width: 100%;
    background-color: #005FBE;
    color: #fff;
    border: none;
    font-size: 16px;
    font-weight: 600;
    border-radius: 5px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}
@media (max-width: 992px) {
    .registration-content{
        width: 90%;
    }
}

/* input  */
.profil-text{
    margin-bottom: 50px;
}
input{
    border: none;
    outline: none;
}
.profile-input{
    width: 100%;
    background-color: #F2F6F7;
    color: #1d1d1d;
    padding: 12px 20px;
    font-weight: 400;
    font-size: 14px;
    line-height: 20px;
    margin:10px 0 20px;
    border-radius: 6px;
    border: 1px solid #222;
}
.profil-text{
    color: #ededed;
    font-size: 16px;
    font-style: normal;
    font-weight: 600;
    line-height: normal;
}
</style>