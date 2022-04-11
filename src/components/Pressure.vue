<template>
    <Page>
        <ActionBar title="Давление" />
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
                    <Label class="value" :text="bar" row="1" col="0" />
                    <Label class="value" text="бар" row="1" col="1" />
                    <Label class="value" :text="kpascal" row="2" col="0" />
                    <Label class="value" text="кПа" row="2" col="1" />
                    <Label class="value" :text="nck" row="3" col="0" />
                    <Label class="value" text="Н/см²" row="3" col="1" />
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
                currentValue: "бар",
                bar: "",
                kpascal: "",
                nck: "",
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.bar = "";
                this.kpascal = "";
                this.nck = "";
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
                        case "бар": {
                            this.bar = parseFloat(this.textFieldValue);
                            this.kpascal= parseFloat(this.textFieldValue) * 100;
                            this.nck = parseFloat(this.textFieldValue) * 10;
                            break;
                        }
                        case "кПа": {
                            this.bar = parseFloat(this.textFieldValue) * 0.01;
                            this.kpascal= parseFloat(this.textFieldValue);
                            this.nck = parseFloat(this.textFieldValue) * 0.1;
                            break;
                        }
                        case "Н/см²": {
                            this.bar = parseFloat(this.textFieldValue) * 0.1;
                            this.kpascal= parseFloat(this.textFieldValue) * 10;
                            this.nck = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.bar = "";
                    this.kpascal = "";
                    this.nck = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "бар",
                    "кПа",
                    "Н/см²"
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