<template>
    <Page>
        <ActionBar title="Валюта" />
        <ScrollView>
            <StackLayout class="container">
                <Button class="return" text="< Назад" @tap="$navigateBack" />
                <GridLayout class="value" columns="2*, *"
                    rows="auto, auto, auto, auto">
                    <TextField class="bt1" v-model="textFieldValue"
                        @textChange="calculationValue(currentValue)"
                        keyboardType="number" hint="Введите значение..."
                        row="0" col="0" />
                    <Button class="bt1" :text="currentValue"
                        @tap="selectValue" row="0" col="1" />
                    <Label class="value" :text="usd" row="1" col="0" />
                    <Label class="value" text="USD" row="1" col="1" />
                    <Label class="value" :text="eur" row="2" col="0" />
                    <Label class="value" text="EUR" row="2" col="1" />
                    <Label class="value" :text="rub" row="3" col="0" />
                    <Label class="value" text="RUB" row="3" col="1" />
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
                currentValue: "USD",
                usd: "",
                eur: "",
                rub: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.usd = "";
                this.eur = "";
                this.rub = ""
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
                        case "USD": {
                            this.usd = parseFloat(this.textFieldValue);
                            this.eur= parseFloat(this.textFieldValue) * 0.92;
                            this.rub = parseFloat(this.textFieldValue) * 74.85;
                            break;
                        }
                        case "EUR": {
                            this.usd = parseFloat(this.textFieldValue) * 1.1;
                            this.eur= parseFloat(this.textFieldValue);
                            this.rub = parseFloat(this.textFieldValue) * 81.71;
                            break;
                        }
                        case "RUB": {
                            this.usd = parseFloat(this.textFieldValue) * 0.0134;
                            this.eur= parseFloat(this.textFieldValue) * 0.01224;
                            this.rub = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.usd = "";
                    this.eur = "";
                    this.rub = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "USD",
                    "EUR",
                    "RUB"
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
    .value {
        margin: 0px 40px 40px 40px;
        background-color: white;
        font-size: 20;
        text-align: center;
        padding: 20px 15px;
    }

    .bt1 {
        padding: 20px 10x;
        margin-bottom: 80px;
        margin-top: 40px;
        border-radius: 2;
        font-size: 18px;
        background-color: white;
    }

    .return {
        font-size: 18px;
        margin-bottom: 50px;
    }

    .container {
        padding: 40px 20px;
        background-color: #E6FFFF;
    }

</style>