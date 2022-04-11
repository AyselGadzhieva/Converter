<template>
    <Page>
        <ActionBar title="Вес" />
        <ScrollView>
            <StackLayout class="container">
                <Button class="return" text="< Назад" @tap="$navigateBack" />
                <GridLayout class="value" columns="2*, *"
                    rows="auto, auto, auto, auto, auto, auto">
                    <TextField class="bt1" v-model="textFieldValue"
                        @textChange="calculationValue(currentValue)"
                        keyboardType="number" hint="Введите значение..."
                        row="0" col="0" />
                    <Button class="bt1" :text="currentValue"
                        @tap="selectValue" row="0" col="1" />
                    <Label class="value" :text="gram" row="1" col="0" />
                    <Label class="value" text="г" row="1" col="1" />
                    <Label class="value" :text="kilogram" row="2" col="0" />
                    <Label class="value" text="кг" row="2" col="1" />
                    <Label class="value" :text="ton" row="3" col="0" />
                    <Label class="value" text="т" row="3" col="1" />
                    <Label class="value" :text="funt" row="4" col="0" />
                    <Label class="value" text="фунт" row="4" col="1" />
                </GridLayout>
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
    export default {
        data() {
            return {
                textFieldValue: "",
                currentValue: "г",
                gram: "",
                kilogram: "",
                ton: "",
                funt: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.gram = "";
                this.kilogram = "";
                this.ton = "";
                this.funt = ""
            },
            calculationValue(currentValue) {

                if (this.textFieldValue != "") {
                    if (this.textFieldValue == "-") {
                        alert({
                            title: "Ошибка!",
                            message: "Величина не может быть отрицательной.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear()
                        });
                    }
                    if (this.textFieldValue == "." || this.textFieldValue == "+") {
                        alert({
                            title: "Ошибка!",
                            message: "Некорректный ввод.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear()
                        });
                    }
                    switch (currentValue) {
                        case "г": {
                            this.gram = parseFloat(this.textFieldValue);
                            this.kilogram = parseFloat(this.textFieldValue) /
                                1000;
                            this.ton = parseFloat(this.textFieldValue) /
                                1000000;
                            this.funt = parseFloat(this.textFieldValue) / 454;
                            break;
                        }
                        case "кг": {
                            this.gram = parseFloat(this.textFieldValue) *
                            1000;
                            this.kilogram = parseFloat(this.textFieldValue);
                            this.ton = parseFloat(this.textFieldValue) / 1000;
                            this.funt = parseFloat(this.textFieldValue) / 2.205;
                            break;
                        }
                        case "т": {
                            this.gram = parseFloat(this.textFieldValue) *
                                1000000;
                            this.kilogram = parseFloat(this.textFieldValue) *
                                1000;
                            this.ton = parseFloat(this.textFieldValue);
                            this.funt = parseFloat(this.textFieldValue) / 2205;
                            break;
                        }
                        case "фунт": {
                            this.gram = parseFloat(this.textFieldValue) * 454;
                            this.kilogram = parseFloat(this.textFieldValue) /
                                2.205;
                            this.ton = parseFloat(this.textFieldValue) / 2205;
                            this.funt = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.gram = "";
                    this.kilogram = "";
                    this.ton = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "г",
                    "кг",
                    "т",
                    "фунт"
                ]).then(result => {
                    if (result != "Отменить") {
                        this.currentValue = result;
                        this.calculationValue(this.currentValue);
                    }
                });
            }
        }
    };
</script>

<style>

</style>