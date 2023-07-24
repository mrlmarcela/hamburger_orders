<template>
    <div>
        <div>
            <Message :msg="msg" v-show="msg"/>
        </div>
        <div>
            <form id="burger-form" @submit="createBurger">
                <div class="mb-4 pt-3 col-lg-4 col-6 mx-auto">
                    <label for="name" class="form-label border-start border-4 border-warning ps-2">Name</label>
                    <input type="text" class="form-control" id="name" name="name" v-model="name" placeholder="Write here your name">
                </div>
                <div class="mb-4 col-lg-4 col-6 mx-auto">
                    <label for="bread" class="form-label border-start border-4 border-warning ps-2">Bread</label>
                    <select name="bread" class="form-select" aria-label="Choice the bread" v-model="bread">
                        <option value="">Choice the bread</option>
                        <option v-for="bread in breads" :value="bread.type">{{ bread.type }}</option>
                    </select>
                </div>
                <div class="mb-4 col-lg-4 col-6 mx-auto">
                    <label for="meat" class="form-label border-start border-4 border-warning ps-2">Meat</label>
                    <select name="meat" class="form-select" aria-label="Choice the meat" v-model="meat">
                        <option value="">Choice the meat</option>
                        <option v-for="meat in meats" :value="meat.type">{{ meat.type }}</option>
                    </select>
                </div>
                <div class="mb-5 col-lg-4 col-6 mx-auto">
                    <label for="optional" class="form-label border-start border-4 border-warning ps-2">Optionals:</label>
                        <div class="form-check" v-for="optionalData in optionals">
                            <input class="form-check-input" type="checkbox" :value="optionalData.type" id="flexCheckDefault" v-model="optional">
                            <label class="form-check-label" for="flexCheckDefault">
                                {{optionalData.type}}
                            </label>
                        </div>
                </div>
                <div class="d-grid col-lg-4 col-6 mx-auto mb-5">
                    <input class="btn btn-warning" type="submit">
                </div>
            </form>
        </div>
    </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Message from './Message.vue';

interface IngredientsData {
    id: number,
    type: string
}

@Options({
  components: {
   Message,
  },
})

export default class BurgerForm extends Vue {
    
    public name: string;
    public bread: string;
    public meat: string;
    public optional: Array<string>;
    public status: string;
    public msg: string;
    public statusMsg: boolean;
    public breads: Array<IngredientsData>;
    public meats: Array<IngredientsData>;
    public optionals: Array<IngredientsData>;

    data(){
        return{
            name: "",
            bread: "",
            meat: "",
            optional: [],
            status: "Solicitado",
            breads: [],
            meats: [],
            optionals: [],
            msg: ""
        }
    }

    async getIngredients() {
        const request = await fetch("http://localhost:3000/ingredients"); 
        const data = await request.json();

        this.optionals = data.optional;
        this.breads = data.breads;
        this.meats = data.meat;
        this.statusMsg = false;
    }

    async createBurger(e: any) {
        e.preventDefault();
        
        const data = {
            name: this.name,
            bread: this.bread,
            meat: this.meat,
            optional: Array.from(this.optional),
            status: "Requested"
        }

        const dataJson = JSON.stringify(data);

        const req = await fetch("http://localhost:3000/burgers", {
            method: "POST",
            headers: {"Content-type": "application/json"},
            body: dataJson
        });

        const response = await req.json();

        this.name = '';
        this.bread = '';
        this.meat = '';
        this.optional = [];
        this.msg = `Order Nº ${response.id} successfully completed!`;

        setTimeout(() => this.msg = "", 3000);
        this.statusMsg = true;
    }

    mounted(){
        this.getIngredients();
    }
}
</script>