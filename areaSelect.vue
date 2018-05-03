<template>
    <div class="hello">
        <div class="sub">
            <el-form>
                <el-row :gutter="20">
                    <el-col :span="8">
                        <el-form-item label="省">
                            <el-select v-model="province" @change="updateCity()">
                                <el-option
                                    v-for="(items,Proindex) in allArea"
                                    :label="items.name"
                                    :value="items.name"
                                    :key="Proindex"
                                ></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="8">
                        <el-form-item label="市">
                            <el-select v-model="city" @change="updateDistrict()">
                                <el-option
                                    v-for="(items,index) in allCity"
                                    :label="items.name"
                                    :value="items.name"
                                    :key="index"
                                ></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="8">
                        <el-form-item label="区">
                            <el-select v-model="district">
                                <el-option
                                    v-for="(items,index) in allDistrict"
                                    :label="items"
                                    :value="items"
                                    :key="index"
                                ></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                </el-row>

            </el-form>


        </div>


    </div>
</template>

<script>
    import area from './area'

    export default {
        data() {
            return {
                allArea: '',
                province: '',
                allProvice: [],
                allCity: [],
                allDistrict: [],
                city: '',
                district: '',

            }
        },
        created() {
            //初始化数据
            this.allArea = area
            this.updateCity()
            this.updateDistrict()
        },
        methods: {
            updateCity: function () {
                this.allArea.forEach(obj => {
                    if (obj.name == this.province) {
                        //循环找到所对应的省下的市 并保存
                        this.allCity = obj.cityList
                        this.city = obj.cityList[0].name
                    }

                    this.allCity.forEach(objs => {
                        //将市循环进行赋值
                        if (objs.name == this.city) {
                            this.allDistrict = objs.areaList
                            this.district = objs.areaList[0]
                        }
                    })


                })

            },
            updateDistrict: function () {
                this.allCity.forEach(obj => {
                    if (obj.name == this.city) {
                        this.allDistrict = obj.areaList
                        this.district = obj.areaList[0]
                    }
                })
            },


        },
        mounted() {
            // console.log( this.allArea)
        }

    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .sub {
        width: 1000px;
        margin: 0 auto
    }
</style>
