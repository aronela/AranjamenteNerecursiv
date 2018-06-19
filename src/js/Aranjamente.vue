<template>
    <div>
        <div class="container">
            <h1>Aranjamente Nerecursiv</h1>
            <h3>Algoritmul afiseaza Aranjamente de n luate cate k</h3>
            <br>
            <h4>Introduceti n:</h4>
            <br>
            <input type="text" class="form-control" id="exampleFormControlInput1" v-model="n"
                   placeholder="Introduceti n">
            <br>
            <h4>Introduceti k:</h4>
            <br>
            <input type="text" class="form-control" id="exampleFormControlInput2" v-model="p"
                   placeholder="Introduceti k">
            <br>
            <button type="button" class="btn btn-secondary" v-on:click="apeleazaAranjamente()">
                Aranjamente!
            </button>
            <br><br>
            <div v-if="solutii.length">
                <h3>Solutii posibile:</h3>
                <div v-for="sol in solutii">
                    <span  class="box rounded" v-for="item in sol" :style="{ backgroundColor: colors[item-1]}">
                    {{ item }}
                    </span><br>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                n: null,
                p: null,
                solutii: [],
                colors: [],
            }
        },
        methods: {
            aranjamenteNerecursiv: function (n, p) {
                let k = 0;
                let valid = false;
                let s = [];
                for (let i = 0; i < p; i++) {
                    s[i] = 0;
                }
                while (k >= 0) {
                    s[k]++;
                    valid = false;

                    while (!valid && s[k] <= n) {
                        if (this.ver(s, k + 1)) {
                            valid = true;
                        } else {
                            s[k]++;
                        }
                    }

                    if (valid) {
                        if (k === p - 1) {
                            console.log(s);
                            this.solutii.push(s.slice(0));

                        } else {
                            k++;
                            s[k] = 0;
                        }

                    } else {
                        k--;
                    }
                }
            },
            ver: function (s, k) {
                for (let i = 0; i < k - 1; i++) {
                    for (let j = i + 1; j < k; j++) {
                        if (s[i] === s[j]) {
                            return false;
                        }
                    }
                }
                return true;
            },
            apeleazaAranjamente: function () {
                this.colors = [];
                this.solutii = [];
                this.colorGenerator(this.n);
                this.aranjamenteNerecursiv(this.n, this.p);
            },
            colorGenerator: function (n) {
                for (let i = 0; i < n; i++) {
                    this.colors.push('#' + Math.floor(Math.random() * 16777215).toString(16));
                }
                console.log(this.colors);
            }
        }
    }
</script>

<style lang="scss">
    .box{
        display: inline-block;
        padding: 30px;
        margin: 10px;
    }
</style>